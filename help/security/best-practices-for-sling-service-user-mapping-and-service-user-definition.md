---
title: Sling服务用户映射和服务用户定义的最佳实践
description: 了解Sling服务用户映射和服务用户定义的最佳实践
source-git-commit: b6f7b6996b377ecfa372742ce1ad22139547ebdd
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---


# Sling服务用户映射和服务用户定义的最佳实践 {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## 服务用户映射 {#service-user-mapping}

要添加服务到相应系统用户的映射，您需要为创建工厂配置 `ServiceUserMapper` 服务。 要保持此模块化，可以使用Sling“修改”机制提供此类配置(请参阅 [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) 以了解更多详细信息)。 将此类配置与捆绑包一起安装的推荐方法是将其添加到快速启动配置模型，如以下示例中所述：

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### 映射格式 {#mapping-format}

自AEM 6.4起，映射格式定义如下：

>[!NOTE]
>
>此 `userName` 已弃用，不应再使用。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` 和 `subserviceName` 识别服务， `userName/principalNames` 识别服务用户并 `principalNames` 是以逗号分隔的列表。

此外，请注意 `principalNames` 是与id相同的开箱即用的服务用户主体名称列表。


**最佳实践**

* 不同任务的子服务名称 — 如果捆绑包的服务执行不同的任务，则建议识别 `subserviceNames` 按任务对这些用户进行分组
* 如果给定服务执行不同的操作(例如，读取资源内容并更新子树下的信息 `/var`)，建议通过聚合反映单独操作的不同服务主体(如聚合公共 `dam-reader-service` 具有您的特定功能 `assetreport-writer-service`
* 理想情况下，每项服务都绑定到一组非常特定且有限的操作
* 使用的新格式 `[one,or,multiple,principalNames]` 是从AEM 6.4开始定义服务用户映射的推荐方法。

下面列出了更改格式的原因以及Adobe建议您将它用于单个用户ID而非版本映射的原因：

* 通过将客户的特殊需求与常见任务结合起来重新使用服务用户的能力
* 避免权限设置的重复
* 更好地了解给定服务实际执行的有效权限（和任务）
* 不需要服务用户的显式组成员资格。 随着组权限更改，这可能会产生令人烦恼的副作用
* 性能改进和可扩展性

## 映射解析和服务登录 {#mapping-resolution-and-service-login}

### 服务映射解析 {#service-mapping-resolution}

用于解析服务映射的调用序列，如下所述：

1. 搜索活动 `principalNames` 给定对象的映射 `bundleId` 和 `subserviceName`
1. `principalNames` 映射 `bundleId` 和空 `subserviceName`
1. `userName` 映射 `bundleId` 和 `subserviceName`
1. `userName` 映射 `bundleId` 和空 `subserviceName`
1. 默认映射
1. 默认用户

### SlingRepository — 服务登录 {#slingrepository-servicelogin}

获取服务的顺序 `Session/ResourceResolver` 的工作方式如下：

1. 从获取主体名称 `ServiceUserMapper` =>预身份验证存储库登录，如下所述
1. 从检索用户ID `ServiceUserMapper`
1. 检查当前用户ID中是否存在已弃用的1ServiceUserConfiguration
1. 使用用户ID进行默认Sling服务登录(例如，序列 `createAdministrativeSession` 和模拟服务用户id)

带有主体名称的新映射可简化以下存储库登录：

* 主体名称集被视为用于填充 `Subject`
* 因此，存储库登录可以进行预验证
* 无组成员资格解析

  >[!NOTE]
  >
  >需要为服务用户声明所有必需的权限。 “everyone”和其他组权限将不再被继承。

* 无需额外的管理员登录即可使用该服务 — `Session/ResourceResolver` 创建。

### 已弃用的ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

请注意，在映射中指定单个用户名等同于现有 `ServiceUserConfiguration.simpleSubjectPopulation`. 对于新格式，提供的解决方法由 `ServiceUserConfiguration` 可以直接反映在服务用户映射中。 此 `ServiceUserConfiguration` 因此，AEM已弃用，所有现有用法均已替换。

## 服务用户 {#service-users}

### 重用现有的服务用户 {#reusing-existing-service-users}

如果满足以下条件，建议重用现有的服务用户：

* 您的需求与现有服务用户的意图相匹配
* 您的服务需要执行由现有公用服务用户覆盖的公用任务。 在这种情况下，建议重用服务用户，而不是引入重复
* 您的服务需要由现有服务用户负责的特定任务。 如果您不确定这一点，请咨询拥有该资产的功能团队。

如果符合以下条件，请勿重复使用现有服务用户：

* 您需要以不相关的方式修改其权限才能使其正常工作
* 如果您只需要它提供的权限的一小部分，并且您只需重复使用它，因为它使您的功能正常工作，而不是因为它真的匹配
* 如果其名称表示您需要的完全不同的目的。 选择因为它有效可能会导致以后出现问题，因为拥有特定服务的功能团队可能会更改权限并破坏您的功能。

### 创建服务用户 {#creating-a-service-user}

在您验证AEM中没有任何现有服务用户适用于您的用例并且相应的RTC问题已被批准后，您可以继续并将新用户添加到默认内容。 理想情况下，扩展安全团队的成员应参与RTC投票，因此请确保您也吸收适当的利益相关方参与。

**命名约定**

AEM安全团队为服务用户定义了以下命名约定，以便添加新服务用户的一致性并提高其可读性和可维护性。

服务用户名由3个元素组成，这些元素用短划线分隔 **&#39;-&#39;**：

1. 服务操作所针对的逻辑实体/功能（避免可能会更改的路径元素）
1. 服务将执行的任务
1. Trailing **&#39;服务&#39;** 能够轻松地从用户是服务用户的id和主体名称中识别出来

**最佳实践**

* 请勿混合不同的图元/特征。 如果服务具有不同的需求，则拆分到各个服务用户并在映射中聚合这些用户
* 将您自己限制为每个服务用户一个明确定义的任务。 如果您最终授予的权限过多或不相关，则进行拆分
* 花些时间确定您服务的真正需求
* 花时间寻找一个良好、有意义且易于解释的服务用户名
* 请求反馈和审查：不熟悉您的功能的开发人员应该能够阅读并了解您的意图。 将来可能会责成他们修复或维护此功能。

最后，服务用户名应显示：

* 其使用方式以及是否可以重复使用：

   * 非常宽泛： `content-writer-service`. 如果您的服务还需要能够读取所有内容，可在聚合中安全重复使用
   * 非常具体： `asset-linkshare-service`. 除非您的服务确实实现了资产链接共享，否则重复使用不会太安全。

* 功能集和权限设置应该如下所示：

   * 逻辑实体需要与权限设置匹配：

      * A `content-foo-service` 应仅与对内容的操作相关联。 向其授予对其他实体（如配置或用户）进行操作的权限是错误的
      * 特定服务，例如 `personalization-foo-service` 还应该随附特定的权限。 如果您最终授予了所有内容的权限，则它不再是特定的。 反映在名称中或在聚合中重复使用普通用户
      * 特定于功能的服务，例如 `msm-xyz-service` 应仅具有与msm相关的权限。 请勿将权限扩展到不相关的功能，如管理社区配置或Screens用户。

   * 该任务需要匹配以下权限：

      * A `foo-reader-service` 应该只能读取常规项目。 从不授予写入权限
      * A `foo-writer-service` 可以预期执行写入操作。 但是，不应向其授予读取/修改访问控制内容的权限
      * A `foo-replicator-service` 可以预期具有 `crx:replicate` 当然。

**示例**

示例 `configuration-reader-service`：

* 该名称表示它是指常规配置，而不是特定功能的配置，如DM集成的配置。 对于专门针对读取此类集成的配置的服务用户，应将其命名为 `dmconfig-reader-service` 或 `s7config-reader-service`

  >[!NOTE]
  >
  >命名中不包含路径信息。 配置已移出 `/etc` 到 `/conf`.

* task-element指示绑定到该用户的服务将只执行读取操作。

示例 `userproperties-copy-service`：

* 绑定到此服务用户的服务将对用户/组属性（如配置文件或首选项）进行操作
* 它专门用于复制该信息，而不是像这样的名称 `userproperties-writer-service` 包括任何类型的写操作。 因此，这些复制任务的权限设置可能仅允许在一个位置添加项目和在另一个位置删除项目。

**权限设置的最佳实践**

* 始终为服务用户使用基于承担者的访问控制设置。 有关更多详细信息，请参阅以下示例：

   * 允许将服务用户及其权限标记为Skyline中的不可变应用程序内容
   * 无需创建路径和树结构

* 仅授予权限，从不拒绝
* 限制权限

   * 仅授予所需的最小权限集
   * 欲知更多信息，请参见 [将权限映射到项目](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html) 和 [将API调用映射到权限](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html) 文档
   * 不授予权限 `jcr:all`. 这很可能不是最小集合。

* 缩小范围

   * 将访问控制策略放在特定于功能的子树中
   * 对于分布式项目：使用限制来限制范围(请参阅 [文档](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html) （了解内置限制的列表）。

* 确保一致性

   * 使权限与您在服务用户名中使用的实体和任务一致
   * 避免添加不相关的权限。 例如，如果有 `workflow-administration-service` 并授予it执行用户管理操作的权限 `/home/users/screens` 或者让它读取s7-config。

* 完整性

   * 确保您的服务具有执行设计任务所需的所有权限。 您的服务还需要在客户环境中开箱即用。
   * 切勿期望/要求客户扩展权限设置(例如，下面的 `/apps`)

* 避免权限设置的重复

   * 重用公用服务用户
   * 将它们与可提供您另外所需的特定权限的特定功能服务用户聚合在一起

* 请勿将权限设置拆分为不同功能。 执行此操作表明您的服务用户定义不明确或执行了太多不同的操作
* 请勿将服务用户置于组中，因为：

   * 它混合了来自服务用户和“公共”组的实施详细信息
   * 您对权限更改缺乏控制（容易出现回退和权限提升）
   * 登录和评估性能
   * 无法使用基于主体的交流设置

* 在repo init中通过使用home(`userId`)。 查看sling repo init [文档](https://sling.apache.org/documentation/bundles/repository-initialization.html) 以了解详细信息。
* RTC：如果更改现有服务用户的权限，请创建一个专用的RTC问题，并确保该问题由安全团队审核。

**通过存储库初始化创建**

始终使用 `repo-init` 要定义服务用户及其权限设置，并将两者都置于“快速入门”功能模型的正确部分，请执行以下操作：

**最佳实践**

* 始终使用 `repo-init` 创建服务用户
* 始终为服务用户创建指定中间路径
* AEM的所有内置服务用户必须位于下方 `system/cq:services/internal`
* 此外，将附加到中间相对路径，以按功能将服务用户分组： `system/cq:services/internal/<your-feature>`
* 客户定义的服务用户必须位于下方 `system/cq:services/<customer-intermediate-rel-path>` 而且绝不低于内部树
* 使用 **强制路径** 而不是 **带有路径** 如果用户已经存在，需要将其移动到支持基于主体的授权的新位置。

**示例**

```
create service user my-new-feature-readcomment-service with path system/cq:services/internal/myfeature
set principal ACL for my-new-feature-readcomment-service
    allow rep:readProperties on /content/myFeature restriction(rep:itemNames,commentTitle,commentDate,commentTxt)
end
```

```
create service user my-existing-feature-addcomment-service with forced path system/cq:services/internal/myfeature
set principal ACL for my-existing-feature-addcomment-service
    allow jcr:addChildNodes,rep:addProperties on /content/myfeature restrictions(rep:glob,*/comments/*)
end
```

```
create service user myfeature-ims-service with path system/cq:services/internal/myfeature
set principal ACL for myfeature-ims-service
    allow jcr:read on home(myfeature-ims-service)
end
```

### 清理服务用户和权限 {#cleanup-service-users-and-permissions}

以下repo init命令可用于清除未使用的服务用户及其权限：

```
# Remove the principal-based access control policy for principal my-feature-service
delete principal ACL for my-feature-service

# Remove all resource-based access control entries (ACEs) for principal my-feature-service
delete ACL for my-feature-service

# Disable the service user
disable service user my-feature-service : "My feature is no longer used"

# Remove the service user
delete service my-feature-service 
```

### 测试服务用户 {#testing-service-users}

为服务用户及其权限设置编写服务器端测试至关重要。 这不仅可以验证您的设置是否真的有效，而且还可以帮助您在更改访问控制内容或服务用户时发现回退和意外错误。

此 `com.adobe.granite.testing.clients` 库提供了许多实用程序，使服务用户轻松编写SST。





