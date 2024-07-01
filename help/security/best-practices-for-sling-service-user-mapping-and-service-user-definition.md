---
title: Sling Service 用户映射和服务用户定义的最佳实践
description: 了解 Sling 服务用户映射和服务用户定义的最佳实践
exl-id: 72f0dcbf-b4e6-4a73-8232-3574a212ac19
feature: Security
role: Admin
source-git-commit: f28f212574dda0ece2cedb56a714d381e5bd7d3c
workflow-type: ht
source-wordcount: '1884'
ht-degree: 100%

---

# Sling Service 用户映射和服务用户定义的最佳实践 {#best-practices-for-sling-service-user-mapping-and-service-user-definition}

## 服务用户映射 {#service-user-mapping}

若要添加从您的服务到相应系统用户的映射，您需要为 `ServiceUserMapper` 服务创建出厂配置。为了保持这种模块化，可以使用 Sling“修改”机制提供此类配置（有关更多详细信息，请参阅 [SLING-3578](https://issues.apache.org/jira/browse/SLING-3578) ）。建议使用捆绑包安装此类配置的方法是将其添加到 Quickstart 设置模型中，如以下示例所述：

```
org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-my-mapping
    user.default=""
    user.mapping=[
        "com.adobe.cq.my-bundle:my-subservice\=[content-writer-service]",
        "com.adobe.cq.my-bundle:my-subservice-different-task\="[myfeature-configuration-writer-service,content-reader-service]"
    ]
```

### 映射格式 {#mapping-format}

自 AEM 6.4 起，映射格式定义如下：

>[!NOTE]
>
>`userName` 已弃用，因此不应再继续使用。

```
bundleId [:subserviceName] = userName | [principalNames]   
```

`bundleId` 和 `subserviceName` 识别服务，`userName/principalNames` 识别服务用户，而 `principalNames` 则是以逗号分隔的列表。

另请注意，`principalNames` 是服务用户主体名称列表，这些名称开箱即用，与 id 相同。


**最佳实践**

* 不同任务的子服务名称：如果您的捆绑包中的服务会执行不同的任务，则建议识别 `subserviceNames` 以按任务分组
* 如果给定服务会执行不同的操作（例如，读取资产内容并更新 `/var` 子树下的信息），则建议通过聚合反映单个操作的不同服务主体来反映这一点，例如将通用 `dam-reader-service` 与特定功能 `assetreport-writer-service` 聚合
* 理想情况下，每项服务都会绑定到一组非常具体且有限的操作
* 从 AEM 6.4 开始，`[one,or,multiple,principalNames]` 的新格式是定义服务用户映射的推荐方式。

以下是更改格式的原因列表，以及 Adobe 建议您使用该格式而不是仅针对单个用户 ID 的版本映射的原因：

* 通过将客户的特殊需求与常见任务相结合来重用服务用户的能力
* 避免重复设置权限
* 更好地理解给定服务实际执行的有效权限（和任务）
* 不需要服务用户明确的组成员身份。随着组权限的改变，这可能会造成麻烦
* 性能改进和可扩展性

## 映射解析与服务登录 {#mapping-resolution-and-service-login}

### 服务映射解析 {#service-mapping-resolution}

解析服务映射的调用顺序如下所述：

1. 搜索给定的 `principalNames` 和 `subserviceName` 的有效 `bundleId` 映射
1. `bundleId` 和空 `subserviceName` 的 `principalNames` 映射
1. `bundleId` 和 `subserviceName` 的 `userName` 映射
1. `bundleId` 和空 `subserviceName` 的 `userName` 映射
1. 默认映射
1. 默认用户

### SlingRepository - 服务登录 {#slingrepository-servicelogin}

获取服务 `Session/ResourceResolver` 的顺序如下：

1. 从  `ServiceUserMapper` => 预授权存储库登录中获取主体名称，如下所述
1. 从 `ServiceUserMapper` 中检索用户 id
1. 检查当前用户 id 是否已弃用 1ServiceUserConfiguration`
1. 默认 Sling 服务使用用户 id 登录（例如，序列为 `createAdministrativeSession` 并模拟服务用户 id）

具有主体名称的新映射使存储库登录得到简化：

* 主体名称集被视为用于填充 `Subject` 的有效主体
* 因此可以预先验证存储库登录
* 无组成员身份解析

  >[!NOTE]
  >
  >需要为服务用户声明所有必需的权限。“所有人”和其他组权限将无法再继承。

* 无需额外的管理员登录便可创建服务 - `Session/ResourceResolver`。

### 已弃用的 ServiceUserConfiguration {#deprecated-serviceUserConfiguration}

请注意，在映射中指定单个用户名等同于现有的 `ServiceUserConfiguration.simpleSubjectPopulation`。`ServiceUserConfiguration` 提供的解决方法的新格式可以直接反映在服务用户映射中。因此，`ServiceUserConfiguration` 在 AEM 中已被弃用，所有现有用法均已被替换。

## 服务用户 {#service-users}

### 重用现有的服务用户 {#reusing-existing-service-users}

如果满足以下条件，建议重新使用现有的服务用户：

* 您的需求与现有服务用户的意图相符
* 您的服务需要执行现有常见服务用户所涵盖的常见任务。在这种情况下，建议重新使用服务用户，而不是引入重复项
* 您的服务需要现有服务用户承担的特定任务。如果您对此不确定，请询问负责该功能的功能团队。

如果出现以下情况，请不要重复使用现有的服务用户：

* 您需要以不相关的方式修改其权限才能使其正常工作
* 如果您只需要它提供的权限的一小部分，并且您会重用它，因为它可以使您的功能发挥作用，而不是因为它是真正的匹配项
* 如果它的名字表明了与您需要的完全不同的意图。因为它有效而选择它可能会在以后导致问题，因为拥有特定服务的功能团队可能会更改权限并破坏您的功能。

### 创建服务用户 {#creating-a-service-user}

在您验证 AEM 中没有现有服务用户适用于您的用例并且相应的 RTC 问题已获批准后，您可以继续在默认内容中添加新用户。理想情况下，扩展安全团队的一名成员会参与 RTC 投票，因此请确保您也让适当的利益相关者参与进来。

**命名惯例**

AEM 安全团队为服务用户定义了以下命名惯例，以便为新服务用户增加一致性并提高其可读性和可维护性。

服务用户名由 3 个元素组成，并用破折号“**-**”分隔：

1. 服务操作所针对的逻辑实体/功能（避免可能改变的路径元素）
1. 服务将要执行的任务
1. 尾随&#x200B;**“服务”**，以便能够从 id 和主体名称中轻松识别出用户是服务用户

**最佳实践**

* 不要混合不同的实体/特征。如果您的服务有不同的需求，请拆分为单个服务用户，并在映射中聚合它们
* 每个服务用户只能执行一个定义明确的任务。如果最终授予过多或不相关的权限，则要进行拆分
* 花时间确定您的服务的真正需求
* 花时间寻找一个好的、有意义的、不言自明的服务用户名
* 征求反馈和评论：不熟悉您的功能的开发人员应该能够阅读并理解您的意图。他们将来可能会负责修复或维护该功能。

最后，服务用户名应该显示：

* 其预期用途是什么，以及是否可以重复使用：

   * 非常通用：`content-writer-service`。如果您的服务也需要能够读取所有内容，则可以安全地在聚合中重复使用
   * 非常具体：`asset-linkshare-service`。除非您的服务确实也进行资产链接共享，否则重复使用不太安全。

* 功能集和权限设置的预期外观：

   * 逻辑实体需要匹配权限设置：

      * `content-foo-service` 应该只与内容操作相关。授予其对配置或用户等其他实体进行操作的权限是错误的做法
      * 特定服务还应具备特定权限，例如 `personalization-foo-service`。如果您最终授予了所有内容的权限，则它就不再是特定的了。在名称中反映这一点或在聚合中重新使用通用用户
      * 特定功能服务只应具有与 msm 相关的权限，例如 `msm-xyz-service`。请不要将权限扩展到不相关的功能中，例如管理社区配置或筛选用户。

   * 该任务需要匹配权限：

      * `foo-reader-service` 应该只能读取常规项目。切勿授予写入权限
      * `foo-writer-service` 可以执行写入操作。但是，不应授予它读取/修改访问控制内容的权限
      * `foo-replicator-service` 可被授予 `crx:replicate`。

**示例**

`configuration-reader-service` 的例子：

* 该名称表示它指的是一般的配置，而不是特定功能的配置，如 DM 集成的配置。专门用于读取此类集成配置的服务用户更愿意被命名为 `dmconfig-reader-service` 或者 `s7config-reader-service`

  >[!NOTE]
  >
  >命名中不包含路径信息。配置已从 `/etc` 移至 `/conf`。

* 任务元素表示与该用户绑定的服务将只执行读取操作。

`userproperties-copy-service` 的例子：

* 与此服务用户绑定的服务将会根据用户/组属性（如配置文件或偏好设置）进行操作
* 它专门用于复制这些信息，而不是像 `userproperties-writer-service` 中包括任何类型的写入操作。因此，这些复制任务的权限设置可能只允许在一个位置添加项目并在另一个位置删除项目。

**权限设置的最佳实践**

* 始终对服务用户使用基于主体的访问控制设置。有关更多详细信息，请参阅下面的示例：

   * 允许在 Skyline 中将服务用户及其权限标记为不可变的应用程序内容
   * 无需创建路径和树结构

* 仅授予权限，从不拒绝
* 限制权限

   * 仅授予所需的最少权限
   * 如需了解更多信息，请咨询[将权限映射到项目](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoitems.html)和[将 API 调用映射到权限](https://jackrabbit.apache.org/oak/docs/security/privilege/mappingtoprivileges.html)文档
   * 不授予许可 `jcr:all`。这很可能不是最小集合。

* 缩小范围

   * 将访问控制策略置于特定功能的子树上
   * 对于分布式项目：使用限制内容来限制范围（请参阅[文档](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)阅内置限制列表）。

* 确保一致性

   * 使权限与您在服务用户名中使用的实体和任务保持一致
   * 避免添加不相关的权限。例如，有一个 `workflow-administration-service` 并授予其在 `/home/users/screens` 执行用户管理操作的权限或让其读取 s7-config 是很奇怪的。

* 完整性

   * 确保您的服务具有执行任务所需的所有权限。您的服务也需要在客户环境中能够立即发挥作用。
   * 请不要期望/要求客户扩展权限设置（例如，下面的 `/apps`）

* 避免重复设置权限

   * 重复使用公共服务用户
   * 将它们与提供您所需的特定权限的特定功能服务用户聚合在一起

* 请不要在不同功能之间分割权限设置。需要这样做表明您的服务用户定义不明确，或者做了太多不同的事项
* 请不要将服务用户分成几组，因为：

   * 它将服务用户的实施细节与“公共”群体混合在一起
   * 您缺乏对权限变化的控制（容易出现倒退和权限升级）
   * 登录与评估表现
   * 不适用于基于主体的 ac-setup

* 对没有可预测路径的用户主节点（或其中包含的任何子树）的访问是通过使用主页 (`userId`) 在 repo-init 中实现的。有关详细信息，请参阅 sling repo init [文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)。
* RTC：如果您更改现有服务用户的权限，请创建一个专用 RTC 问题，并确保安全团队对其进行审查。

**使用存储库初始化功能进行创建**

始终使用 `repo-init` 来定义服务用户及其权限设置，并将其放在 Quickstart 功能模型的恰当部分：

**最佳实践**

* 始终使用 `repo-init` 来创建服务用户
* 始终为服务用户的创建指定中间路径
* AEM 的所有内置服务用户必须位于 `system/cq:services/internal` 下方
* 另外附加到中间相对路径以按功能对服务用户进行分组：`system/cq:services/internal/<your-feature>`
* 客户定义的服务用户必须位于 `system/cq:services/<customer-intermediate-rel-path>` 下方，并且一定不能位于内部树下方
* 如果用户已经存在且需要移动到支持基于主体的授权的新位置，则搭配使用&#x200B;**强制路径**&#x200B;而非&#x200B;**路径**。

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

下面的 repo init 命令可用于清理未使用的服务用户及其权限：

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

为服务用户及其权限设置编写服务器端测试至关重要。这不仅可以验证您的设置是否真的有效，还可以帮助您在更改访问控制内容或服务用户时发现倒退和意外错误。

`com.adobe.granite.testing.clients` 库提供了许多实用程序，使服务用户可以轻松编写 SST。
