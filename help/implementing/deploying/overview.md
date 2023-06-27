---
title: 部署到 AEM as a Cloud Service
description: 部署到 AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 48%

---

# 部署到 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 简介 {#introduction}

与 AEM 内部部署和 Managed Services 解决方案相比，AEM as a Cloud Service 中的代码开发基础是相似的。开发人员编写代码并在本地对其进行测试，然后将该代码推送到AEMas a Cloud Service上的远程环境。 需要使用 Cloud Manager，它是 Managed Services 的一个可选内容交付工具。此投放工具现在是将代码部署到AEMas a Cloud Service开发、暂存和生产环境的唯一机制。 为了在部署上述环境之前快速验证和调试功能，可以将代码从本地环境同步到 [快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md).

[AEM 版本](/help/implementing/deploying/aem-version-updates.md)的更新始终是独立于推送[自定义代码](#customer-releases)的部署事件。从另一个角度来看，自定义代码版本应针对生产中的 AEM 版本进行测试，因为这是它部署到其上的版本。之后将频繁进行 AEM 版本更新，并会自动应用这些更新。它们旨在与已部署的客户代码向后兼容。

本文档的其余部分描述了开发人员应如何调整其实践，以便他们能够与AEMas a Cloud Service的版本更新和客户更新一起使用。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客户发行版本 {#customer-releases}

### 针对正确的 AEM 版本进行编码 {#coding-against-the-right-aem-version}

对于以前的 AEM 解决方案，最新的 AEM 版本很少发生更改（约每年使用季度 Service Pack 更新一次），客户将根据自己的时间将生产实例更新到最新的快速入门，并参考 API Jar。但是，AEMas a Cloud Service上的应用程序会更频繁地自动更新到最新版本的AEM，因此内部版本的自定义代码应该针对最新AEM版本构建。

与现有的非云AEM版本一样，也支持基于特定快速入门的本地离线开发，并且通常希望将其作为调试的首选工具。

>[!NOTE]
>应用程序在本地计算机上的行为方式与在 Adobe Cloud 上的行为方式之间存在细小的操作差异。在本地开发过程中必须考虑这些架构差异，并且这些差异会导致在云基础架构上部署时发生不同的行为。由于存在这些差异，因此，在生产中推出新的自定义代码之前，务必要在开发和暂存环境中执行详尽的测试。

若要为内部版本开发自定义代码，应下载并安装相关版本的 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。有关使用 AEM as a Cloud Service Dispatcher 工具的其他信息，请参阅[此页面](/help/implementing/dispatcher/disp-overview.md)。

以下视频提供了有关如何将代码部署到AEMas a Cloud Service的高级概述：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 通过Cloud Manager和包管理器部署内容包 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 通过Cloud Manager部署 {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

客户通过 Cloud Manager 将自定义代码部署到云环境。Cloud Manager将本地组装的内容包转换为符合Sling功能模型的构件，这是在AEMas a Cloud Service中运行应用程序时的描述。 因此，在中查看包时 [包管理器](/help/implementing/developing/tools/package-manager.md) 在云环境中，名称包括“cp2fm”，转换后的包已删除所有元数据。 它们无法进行交互，这意味着无法下载、复制或打开它们。可以[在此处找到](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)有关转换器的详细文档。

为AEMas a Cloud Service上的应用程序编写的内容包必须在不可变和可变内容之间有一个干净的分隔，并且Cloud Manager仅安装可变内容，还会输出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本节的其余部分介绍不可变和可变包的构成和含义。

### 不可变内容包 {#immutabe-content-packages}

必须阿静存储在不可变存储库中的所有内容和代码签入 Git，并通过 Cloud Manager 部署它们。换句话说，与当前的 AEM 解决方案不同，代码绝不会直接部署到正在运行的 AEM 实例。此工作流可确保在任何云环境中为给定版本运行的代码都相同，从而消除在生产环境中无意中变异代码的风险。 例如，OSGI配置应提交到源代码管理，而不是在运行时通过AEM Web控制台的配置管理器进行管理。

由于部署模式导致的应用程序更改是由交换机启用的，因此除了服务用户、其ACL、节点类型和索引定义更改之外，它们不能依赖于可变存储库中的更改。

对于拥有现有代码库的客户，请务必完成 AEM 文档中描述的存储库重构实践，以确保将以前位于 /etc 下的内容移动到正确的位置。

一些附加限制适用于这些代码包，例如，[安装挂钩](https://jackrabbit.apache.org/filevault/installhooks.html)不受支持。

## OSGI 配置 {#osgi-configuration}

如上所述，OSGI 配置应提交给源代码管理，而不是通过 Web 控制台管理。用于执行此操作的方法包括：

* 使用 AEM Web 控制台的配置管理器对开发人员的本地 AEM 环境进行必要的更改，然后将结果导出到本地文件系统上的 AEM 项目
* 在本地文件系统上的 AEM 项目中手动创建 OSGI 配置，然后为属性名称引用 AEM 控制台的配置管理器。

参阅[为 AEM as a Cloud Service 配置 OSGi](/help/implementing/deploying/configuring-osgi.md)，了解有关 OSGI 配置的更多信息。

## 可变内容 {#mutable-content}

有时，在源代码管理中准备内容更改可能会有帮助，这样Cloud Manager可以在更新环境时部署这些更改。 例如，为某些根文件夹结构提供种子可能是合理的。 或者，排列可编辑模板中的更改，以启用由应用程序部署更新的策略组件。

有两种策略可描述Cloud Manager部署到可变存储库的内容：可变内容包和 `repoinit` 语句。

### 可变内容包 {#mutable-content-packages}

文件夹路径层次结构、服务用户和访问控制 (ACL) 等内容通常将提交到基于 Maven 原型的 AEM 项目。方法包括从 AEM 导出或以 XML 形式直接写入。在构建和部署过程中，Cloud Manager 将打包生成的可变内容包。可变内容在管道中的部署阶段会在三个不同的时间安装：

在启动新版本的应用程序之前：

* 索引定义（添加、修改、删除）

在启动新版本的应用程序期间，但在切换之前：

* 服务用户（添加）
* 服务用户 ACL（添加）
* 节点类型（添加）

切换到新版本的应用程序之后：

* 可通过Jackrabbit保险库定义的所有其他内容。 例如：
   * 文件夹（添加、修改、删除）
   * 可编辑模板（添加、修改、删除）
   * 上下文感知配置（`/conf` 下的任何内容）（添加、修改、删除）
   * 脚本（包可以在包安装的安装过程的各个阶段触发安装挂钩。参见 [Jackrabbit文件文档](https://jackrabbit.apache.org/filevault/installhooks.html) 关于安装挂钩。 AEM CS当前使用Filevault版本3.4.0，该版本限制管理员用户、系统用户和管理员组成员的安装挂接)。

可以通过在 `/apps` 下的 install.author 或 install.publish 文件夹中嵌入包，来仅允许创作或发布可变内容安装。在 AEM 6.5 中进行了重构以反映此分离，可以在 [AEM 6.5 文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中找到有关推荐的项目重构的详细信息。

>[!NOTE]
>内容包将部署到所有环境类型（开发、暂存、生产）。无法将部署限于特定环境。施加此限制以确保能够选择自动执行的测试运行。特定于环境的内容需要手动安装，方式为 [包管理器。](/help/implementing/developing/tools/package-manager.md)

此外，没有用于在应用可变内容包更改后回滚这些更改的机制。如果客户检测到问题，他们可以选择在下一个代码版本中修复它，或者在万不得已的情况下，将整个系统恢复到部署前的某个时间点。

必须验证任何包含的第三方软件包是否与AEMas a Cloud Service兼容，否则其包含会导致部署失败。

如上所述，拥有现有代码库的客户应遵循6.5版存储库更改所需的存储库重组练习，如中所述 [AEM 6.5文档。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## Repoinit {#repoinit}

对于以下情况，最好是采用在 OSGI 工厂配置中手动为显式内容创建 `repoinit` 语句编码的方法：

* 创建/删除/禁用服务用户
* 创建/删除组
* 创建/删除用户
* 添加 ACL

  >[!NOTE]
  >
  >ACL 的定义要求节点结构已存在。因此，前面的创建路径语句可能是必需的。

* 添加路径（例如，根文件夹结构）
* 添加 CND（节点类型定义）

由于 Repoinit 的以下好处，对于这些受支持的内容修改用例，Repoinit 更可取：

* `Repoinit` 在启动时创建资源，因此，逻辑可以将这些资源的存在视为理所当然。在可变内容包方法中，资源是在启动后创建的，因此依赖这些资源的应用程序代码可能会失败。
* `Repoinit` 是一个相对安全的指令集，因为您可以明确控制要执行的操作。此外，除了一些与安全相关的情况（允许删除用户、服务用户和组）之外，仅支持附加操作。 相比之下，在可变内容包方法中删除某些内容是明确的；在定义过滤器时，过滤器涵盖的任何内容都会被删除。不过，应谨慎行事，因为对于任何内容，在一些场景中，新内容的存在都会更改应用程序的行为。
* `Repoinit` 执行快速和原子操作。相比之下，可变内容包在性能方面可能在很大程度上取决于过滤器涵盖的结构。即使您更新单个节点，也可能创建大型树的快照。
* 可以验证 `repoinit` 运行时本地开发环境上的语句，因为它们在OSGi配置注册时运行。
* `Repoinit` 语句为原子且显式，如果状态已匹配，则跳过这些语句。

当 Cloud Manager 部署应用程序时，它会独立于任何内容包的安装来执行这些语句。

创建 `repoinit` 请遵循以下步骤：

1. 在项目的配置文件夹中，为工厂 PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` 添加 OSGi 配置。为配置使用描述性名称，例如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 添加 `repoinit` 语句添加到config的script属性。 [Sling 文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)中记录了语法和选项。应在其子文件夹之前显式创建父文件夹。 例如，在 `/content/myfolder` 和 `/content/myfolder/mysubfolder` 之前显式创建 `/content`。对于在低级结构上设置的ACL，建议将其设置为较高级别，然后使用 `rep:glob` 限制。 例如：`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在运行时在本地开发环境上进行验证。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>对于为下面的节点定义的ACL `/apps` 或 `/libs` 此 `repoinit`，将在空白存储库中开始执行。 之后将安装包 `repoinit` 因此，语句不能依赖包中定义的任何内容，但必须定义前提条件，如下的父结构。

>[!TIP]
>
>对于ACL，创建深层结构可能会很麻烦。 因此，更合理的做法是在更高层上定义ACL ，并限制它应通过 `rep:glob` 限制。

更多有关 `repoinit` 可在以下位置找到： [Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 包管理器的“一次性”可变内容包安装 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="包管理器 – 迁移可变内容包"
>abstract="探索包管理器的用法，以了解应将内容包安装为“一次性”的用例。 安装包括将特定内容从生产环境导入到暂存环境以调试生产问题，将小型内容包从内部部署环境传输到AEM云环境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en" text="内容传输工具"

在某些用例中，应“一次性”安装内容包。例如，将特定内容从生产环境导入到暂存环境以调试生产问题。 对于这些方案， [包管理器](/help/implementing/developing/tools/package-manager.md) 可以在AEMas a Cloud Service的环境中使用。

由于包管理器是一个运行时概念，无法将内容或代码安装到不可变存储库中，因此这些内容包应只包含可变内容（主要是 `/content` 或 `/conf`）。如果内容包包含混合内容（可变内容和不可变内容），则只会安装可变内容。

>[!IMPORTANT]
>
>包管理器用户界面可能返回 **未定义** 如果软件包的安装时间超过10分钟，则会出现错误消息。
>
>此时间不是由于安装出错，而是由于该Cloud Service对于所有请求超时。
>
>如果您看到此类错误，请不要重试安装。安装过程在后台正常进行。如果您确实重新启动了安装，则多个并发导入过程可能会引发一些冲突。

通过Cloud Manager安装的任何内容包（可变和不可变）都会在AEM Package Manager的用户界面中以冻结状态显示。 这些软件包无法重新安装、重新构建甚至下载，并且以 **&quot;cp2fm&quot;** 后缀，指示其安装由Cloud Manager管理。

### 包括第三方包 {#including-third-party}

客户通常包括来自第三方来源(如Adobe的翻译合作伙伴等软件供应商)的预建软件包。 建议在远程存储库中托管这些包，并在 `pom.xml` 中引用它们。此方法适用于公共存储库和具有密码保护的专用存储库，如中所述 [受密码保护的maven存储库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

如果无法将包存储在远程存储库中，客户可以将其放在基于文件系统的本地Maven存储库中，该存储库作为项目的一部分提交给SCM。 任何依靠它的东西都会引用它。 存储库在项目pom中声明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方软件包都必须遵守本文中所述的AEMas a Cloud Service编码和打包准则，否则其包含会导致部署失败。

以下Maven `POM.xml` 此代码段显示了如何将第三方包嵌入项目的“容器”包中，通常命名为 **&#39;全部&#39;**，通过 **filevault-package-maven-plugin** Maven插件配置。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          ...

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

## 滚动部署的工作原理 {#how-rolling-deployments-work}

与 AEM 更新一样，客户版本使用滚动部署策略进行部署，以便在适当的情况下消除创作群集停机时间。下面描述了事件的一般顺序，其中具有旧版本和新版本客户代码的节点运行相同版本的 AEM 代码。

* 具有旧版本的节点处于活动状态，新版本的候选发布版本已构建并可用。
* 如果存在任何新的或更新的索引定义，则处理相应的索引。旧版本的节点始终使用旧索引，而新版本的节点始终使用新索引。
* 新版本启动的节点，而旧版本仍会提供流量。
* 运行旧版本的节点并保持服务，同时通过运行状况检查检查新版本的节点是否已准备就绪。
* 具有新版本的节点已就绪，接受流量，然后使用已停止运行的旧版本替换节点。
* 随着时间的推移，旧版本的节点被新版本的节点替换，直到只剩下新版本的节点，从而完成部署。
* 然后部署任何新的或修改后的可变内容。

## 索引 {#indexes}

新索引或修改的索引会导致在新版本接收流量之前执行额外的索引或重新索引步骤。 有关 AEM as a Cloud Service 中的索引管理的详细信息，请参阅[本文](/help/operations/indexing.md)。您可以在Cloud Manager上检查构建页面的索引状态，并在新版本准备好接收流量时收到通知。

>[!NOTE]
>
>滚动部署所需的时间因索引大小而异。 原因在于，在生成新索引之前，新版本无法接受流量。

目前，AEMas a Cloud Service不能与ACS Commons Confirmate Oak Index工具等索引管理工具一起使用。

## 复制 {#replication}

发布机制向后兼容 [AEM复制Java™ API](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hans).

要使用AEM云就绪快速启动来开发和测试复制，经典复制功能必须与“创作/发布”设置一起使用。 如果为云删除了AEM Author上的用户界面入口点，则用户将转到 `http://localhost:4502/etc/replication` 进行配置。

## 用于滚动部署的向后兼容代码 {#backwards-compatible-code-for-rolling-deployments}

如上详述，AEM as a Cloud Service 的滚动部署策略意味着可以同时运行新版本和旧版本。因此，请注意无法与仍在运行的旧 AEM 版本向后兼容的代码更改。

此外，由于可变内容未删除，因此应该测试旧版本与新版本应用的任何新可变内容结构的兼容性（如果存在回滚）。

### 服务用户和 ACL 更改 {#service-users-and-acl-changes}

更改服务用户（或访问内容或代码的ACL）可能会导致旧版AEM中出现错误，从而导致使用过时的服务用户访问该内容或代码。 要解决此行为，建议在至少两个版本中进行更改，其中第一个版本在清除后续版本之前充当链接。

### 索引更改 {#index-changes}

如果对索引进行了更改，新版本必须继续使用其索引直至被终止，而旧版本使用自己的一组已修改的索引。开发人员应采用[本文](/help/operations/indexing.md)中描述的索引管理方法。

### 用于回滚的保守编码 {#conservative-coding-for-rollbacks}

如果部署后报告或检测到失败，则可能需要回滚到旧版本。确保新代码与该新版本创建的任何新结构兼容，因为新结构（任何可变内容）不会回滚。 如果旧代码不兼容，则必须在后续客户版本中应用修复。

## 快速开发环境 (RDE) {#rde}

[快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md) （简称RDE ）允许开发人员快速部署和查看更改，从而最大限度地减少测试已证明可在本地开发环境中工作的功能所需的时间。

与通过Cloud Manager管道部署代码的常规开发环境不同，开发人员使用命令行工具将代码从本地开发环境同步到RDE。 在RDE中成功测试更改后，通过Cloud Manager管道将它们部署到常规云开发环境，这将通过适当的质量关卡来放置代码。

## 运行模式 {#runmodes}

在现有的 AEM 解决方案中，客户可以选择在任意运行架构中运行实例，并应用 OSGI 配置或将 OSGI 捆绑包安装到这些特定实例。定义的运行架构通常包括&#x200B;*服务*（创作和发布）和环境（RDE、开发、暂存、生产）。

另一方面，AEM as a Cloud Service 会更武断地认定哪些运行架构可用以及如何将 OSGI 捆绑包和 OSGI 配置映射到这些架构：

* OSGI配置运行模式必须引用RDE、开发、暂存、环境生产，或服务创作、发布。 组合 `<service>.<environment_type>` 受支持，但这些环境必须以特定顺序使用(例如 `author.dev` 或 `publish.prod`)。 应直接从代码中引用OSGI令牌，而不是使用 `getRunModes` 方法，该方法不再包括 `environment_type` 在运行时。 有关更多信息，请参阅[为 AEM as a Cloud Service 配置 OSGi](/help/implementing/deploying/configuring-osgi.md)。
* OSGI 捆绑包运行架构仅适用于服务（创作、发布）。每运行架构 OSGI 捆绑包应安装在 `install.author` 或 `install.publish` 下的内容包中。

AEM as a Cloud Service 不允许使用运行模式为特定环境或服务安装内容。如果开发环境必须植入不在暂存或生产环境中的数据或HTML，则可以使用包管理器。

支持的运行模式配置包括：

* **config**（*默认值，适用于所有 AEM 服务*）
* **config.author**（*适用于所有 AEM 创作服务*）
* **config.author.dev**（*适用于 AEM 开发创作服务*）
* **config.author.rde**（*适用于 AEM RDE 创作服务*）
* **config.author.stage**（*适用于 AEM 暂存创作服务*）
* **config.author.prod**（*适用于 AEM 生产创作服务*）
* **config.publish**（*适用于 AEM 发布服务*）
* **config.publish.dev**（*适用于 AEM 开发发布服务*）
* **config.publish.rde**（*适用于 AEM RDE 发布服务*）
* **config.publish.stage**（*适用于 AEM 暂存发布服务*）
* **config.publish.prod**（*适用于 AEM 生产发布服务*）
* **config.dev**（*适用于 AEM 开发服务*）
* **config.rde**（*适用于 RDE 服务*）
* **config.stage**（*适用于 AEM 暂存服务*）
* **config.prod**（*适用于 AEM 生产服务*）

将使用具有最匹配运行模式的OSGI配置。

在本地开发时，运行模式启动参数 `-r`，用于指定运行模式OSGI配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 源代码管理中的维护任务配置 {#maintenance-tasks-configuration-in-source-control}

维护任务配置必须保留在源代码管理中，因为 **“工具”>“操作”** 屏幕在云环境中不可用。 此好处可确保更改被有意持久保留，而不是被反应性地应用和遗忘。 参见 [维护任务文章](/help/operations/maintenance.md) 以获取其他信息。
