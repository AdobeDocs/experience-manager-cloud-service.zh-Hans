---
title: 部署到 AEM as a Cloud Service
description: 部署到 AEM as a Cloud Service
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: a70bd2ffddcfb729812620743ead7f57860457f3
workflow-type: tm+mt
source-wordcount: '3541'
ht-degree: 89%

---

# 部署到 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 简介 {#introduction}

与 AEM 内部部署和 Managed Services 解决方案相比，AEM as a Cloud Service 中的代码开发基础是相似的。开发人员编写代码并在本地进行测试，然后将代码推送到远程 AEM as a Cloud Service 环境。需要使用 Cloud Manager，它是 Managed Services 的一个可选内容交付工具。现在，这是用于将代码部署到 AEM as a Cloud Service 开发、暂存和生产环境的唯一机制。要在部署上述环境之前进行快速功能验证和调试，可以将代码从本地环境同步到[快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md)。

[AEM 版本](/help/implementing/deploying/aem-version-updates.md)的更新始终是独立于推送[自定义代码](#customer-releases)的部署事件。从另一个角度来看，自定义代码版本应针对生产中的 AEM 版本进行测试，因为这是它将部署到其上的版本。之后将频繁进行 AEM 版本更新，并将自动应用这些更新。它们旨在与已部署的客户代码向后兼容。

本文档的其余部分将描述开发人员应如何调整他们的实践，以便他们同时使用 AEM as a Cloud Service 的版本更新和客户更新。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客户发行版本 {#customer-releases}

### 针对正确的 AEM 版本进行编码 {#coding-against-the-right-aem-version}

对于以前的 AEM 解决方案，最新的 AEM 版本很少发生更改（约每年使用季度 Service Pack 更新一次），客户将根据自己的时间将生产实例更新到最新的快速入门，并参考 API Jar。但是，AEM as a Cloud Service 应用程序将更频繁地自动更新到最新版本的 AEM，因此，应针对最新的 AEM 版本构建内部版本的自定义代码。

与现有的非云 AEM 版本一样，将支持基于特定快速入门的本地离线开发，在大多数情况下，它有望成为用于调试的首选工具。

>[!NOTE]
>应用程序在本地计算机上的行为方式与在 Adobe Cloud 上的行为方式之间存在细小的操作差异。在本地开发过程中必须考虑这些架构差异，并且这些差异会导致在云基础架构上部署时发生不同的行为。由于存在这些差异，在生产中推出新的自定义代码之前，在开发和暂存环境中执行详尽的测试非常重要。

要为内部版本开发自定义代码，应下载并安装相关版本的 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)。有关使用 AEM as a Cloud Service Dispatcher 工具的其他信息，请参阅[此页面](/help/implementing/dispatcher/disp-overview.md)。

以下视频高度概述了如何将代码部署到 AEM as a Cloud Service：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 通过 Cloud Manager 和包管理器部署内容包 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 通过 Cloud Manager 部署 {#deployments-via-cloud-manager}

<!-- Alexandru: temporarily commenting this out, until I get some clarification from Brian 

![image](https://git.corp.adobe.com/storage/user/9001/files/e91b880e-226c-4d5a-93e0-ae5c3d6685c8) -->

客户通过 Cloud Manager 将自定义代码部署到云环境。请注意，Cloud Manager 将本地汇编的内容包转换为符合 Sling 功能模型的构件，这就是在云环境中运行时描述 AEM as a Cloud Service 应用程序的方式。因此，在云环境中的[包管理器](/help/implementing/developing/tools/package-manager.md)中查看包时，名称将包含“cp2fm”，并且转换后的包中的所有元数据已被删除。它们无法进行交互，这意味着无法下载、复制或打开它们。可以[在此处找到](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)有关转换器的详细文档。

为 AEM as a Cloud Service 应用程序编写的内容包必须明确区分不可变内容和可变内容，并且 Cloud Manager 将仅安装可变内容，并输出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

此部分的其余内容将描述不可变包和可变包的构成和含义。

### 不可变内容包 {#immutabe-content-packages}

必须阿静存储在不可变存储库中的所有内容和代码签入 Git，并通过 Cloud Manager 部署它们。换句话说，与当前的 AEM 解决方案不同，代码绝不会直接部署到正在运行的 AEM 实例。这可确保在任意云环境中为给定版本运行的代码是相同的，从而消除生产中发生意外代码变化的风险。例如，OSGI 配置应提交给源代码管理，而不是在运行时通过 AEM Web 控制台的配置管理器进行管理。

由于部署模式导致的应用程序更改是由交换机启用的，因此除了服务用户、其ACL、节点类型和索引定义更改之外，它们不能依赖于可变存储库中的更改。

对于拥有现有代码库的客户，请务必完成 AEM 文档中描述的存储库重构实践，以确保将以前位于 /etc 下的内容移动到正确的位置。

一些附加限制适用于这些代码包，例如，[安装挂钩](https://jackrabbit.apache.org/filevault/installhooks.html)不受支持。

## OSGI 配置 {#osgi-configuration}

如上所述，OSGI 配置应提交给源代码管理，而不是通过 Web 控制台管理。用于执行此操作的方法包括：

* 使用 AEM Web 控制台的配置管理器对开发人员的本地 AEM 环境进行必要的更改，然后将结果导出到本地文件系统上的 AEM 项目
* 在本地文件系统上的 AEM 项目中手动创建 OSGI 配置，然后为属性名称引用 AEM 控制台的配置管理器。

参阅[为 AEM as a Cloud Service 配置 OSGi](/help/implementing/deploying/configuring-osgi.md)，了解有关 OSGI 配置的更多信息。

## 可变内容 {#mutable-content}

在某些情况下，在源代码管理中准备内容更改可能会很有用，这样它就能在更新环境时由 Cloud Manager 进行部署。例如，为某些根文件夹结构投放种子或在可编辑模板中排列更改，以便在其中为应用程序部署更新的组件启用策略可能是合理的。

可通过两种策略来描述将由 Cloud Manager 部署到可变存储库的内容、可变内容包和 repoinit 语句。

### 可变内容包 {#mutable-content-packages}

文件夹路径层次结构、服务用户和访问控制 (ACL) 等内容通常将提交到基于 Maven 原型的 AEM 项目。方法包括从 AEM 导出或以 XML 形式直接写入。在构建和部署过程中，Cloud Manager 将打包生成的可变内容包。将在管道的部署阶段的 3 个不同时间安装可变内容：

在启动新版本的应用程序之前：

* 索引定义（添加、修改、删除）

在启动新版本的应用程序期间，但在切换之前：

* 服务用户（添加）
* 服务用户 ACL（添加）
* 节点类型（添加）

切换到新版本的应用程序之后：

* 可通过 jackrabbit 库定义的所有其他内容。例如：
   * 文件夹（添加、修改、删除）
   * 可编辑模板（添加、修改、删除）
   * 上下文感知配置（`/conf` 下的任何内容）（添加、修改、删除）
   * 脚本（包可以在包安装的安装过程的各个阶段触发安装挂钩。有关安装挂钩的信息，请参阅 [Jackrabbit filevault 文档](https://jackrabbit.apache.org/filevault/installhooks.html)。请注意，AEM CS 目前使用 Filevault 版本 3.4.0，它仅允许管理员用户、系统用户和管理员组的成员安装挂钩）。

可以通过在 `/apps` 下的 install.author 或 install.publish 文件夹中嵌入包，来仅允许创作或发布可变内容安装。在 AEM 6.5 中进行了重构以反映此分离，可以在 [AEM 6.5 文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中找到有关推荐的项目重构的详细信息。

>[!NOTE]
>内容包将部署到所有环境类型（开发、暂存、生产）。无法将部署限于特定环境。施加此限制以确保能够选择自动执行的测试运行。特定于环境的内容需要通过[包管理器](/help/implementing/developing/tools/package-manager.md)手动安装。

此外，没有用于在应用可变内容包更改后回滚这些更改的机制。如果客户检测到问题，他们可以选择在下一个代码版本中修复它，或者在万不得已的情况下，将整个系统恢复到部署前的某个时间点。

必须确认任何包含的第三方包与 AEM as a Cloud Service 兼容，否则包含此包会导致部署失败。

如上所述，拥有现有代码库的客户应遵守 [AEM 6.5 文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)中所述的 6.5 存储库更改所需的存储库重构实践。

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

* Repoinit 在启动时创建资源，因此，逻辑可以将这些资源的存在视为理所当然。在可变内容包方法中，资源是在启动后创建的，因此依赖这些资源的应用程序代码可能会失败。
* Repoinit 是一个相对安全的指令集，因为您可以明确控制要执行的操作。此外，唯一支持的操作是累加的，但几种与安全相关的情况除外，这些情况允许删除用户、服务用户和组。相比之下，在可变内容包方法中删除某些内容是明确的；在定义过滤器时，过滤器涵盖的任何内容都将被删除。不过，应谨慎行事，因为对于任何内容，在一些场景中，新内容的存在都会更改应用程序的行为。
* Repoinit 执行快速和原子操作。相比之下，可变内容包在性能方面可能在很大程度上取决于过滤器涵盖的结构。即使您更新单个节点，也可能创建大型树的快照。
* 可以在运行时在本地开发环境中验证 repoinit 语句，因为在注册 OSGi 配置时将执行这些语句。
* Repoinit 语句是原子和显式的，如果状态已匹配，则会将其跳过。

当 Cloud Manager 部署应用程序时，它会独立于任何内容包的安装来执行这些语句。

要创建 repoinit 语句，请遵循以下过程：

1. 在项目的配置文件夹中，为工厂 PID `org.apache.sling.jcr.repoinit.RepositoryInitializer` 添加 OSGi 配置。为配置使用描述性名称，例如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 将 repoinit 语句添加到配置的脚本属性中。[Sling 文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)中记录了语法和选项。请注意，应该在其子文件夹之前显式创建父文件夹。例如，在 `/content/myfolder` 和 `/content/myfolder/mysubfolder` 之前显式创建 `/content`。对于在低层次结构上设置的 ACL，建议在更高层次设置它们并使用 `rep:glob` 限制。例如 `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在运行时在本地开发环境上进行验证。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>对于为 `/apps` 或 `/libs` 下的节点定义的 ACL，repoinit 执行将在空白存储库上开始。这些包是在 repoinit 之后安装的，因此，语句无法依赖包中定义的任何内容，但必须定义先决条件，例如下面的父结构。

>[!TIP]
>
>对于 ACL，创建深层结构可能会很麻烦，因此，在更高层次上定义 ACL 并通过 rep:glob 限制来限定它执行操作的位置会更合理。

有关 repoinit 的更多详细信息，请参阅 [Sling 文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 包管理器的“一次性”可变内容包安装 {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="包管理器 – 迁移可变内容包"
>abstract="探究包管理器在应“一次性”安装内容包的用例中的用法，其中包括将特定内容从生产导入到暂存来调试生产问题，将小型内容包从内部部署环境传输到 AEM 云环境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=zh-Hans#cloud-migration" text="内容传输工具"

在某些用例中，应“一次性”安装内容包。例如，将特定内容从生产环境导入到暂存环境来调试生产问题。在这些场景中，可以在 AEM as a Cloud Service 环境中使用[包管理器](/help/implementing/developing/tools/package-manager.md)。

由于包管理器是一个运行时概念，无法将内容或代码安装到不可变存储库中，因此这些内容包应只包含可变内容（主要是 `/content` 或 `/conf`）。如果内容包包含混合内容（可变内容和不可变内容），则只安装可变内容。

>[!IMPORTANT]
>
>如果用于安装包的时间超过 10 分钟，包管理器 UI 可能会返回&#x200B;**未定义**&#x200B;错误消息。
>
>这不是因安装错误导致的，而是因 Cloud Service 对所有请求的超时导致的。
>
>如果您看到此类错误，请不要重试安装。安装过程在后台正常进行。如果您重新启动安装，则多个并发导入进程可能会引入一些冲突。

通过 Cloud Manager 安装的任何内容包（可变内容包和不可变内容包）都将在 AEM 包管理器的用户界面中显示为冻结状态。这些包无法重新安装、重新构建甚至下载，并且将以&#x200B;**“cp2fm”**&#x200B;后缀列出，表明它们的安装由 Cloud Manager 管理。

### 包括第三方包 {#including-third-party}

客户通常将包含来自第三方来源（例如，Adobe 的翻译合作伙伴等软件供应商）的预建包。建议在远程存储库中托管这些包，并在 `pom.xml` 中引用它们。可以在公共存储库以及受密码保护的私有存储库中做到这一点，如[受密码保护的 maven 存储库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)中所述。

如果无法将包存储在远程存储库中，客户可以将包放置在基于文件系统的本地 Maven 存储库中，该存储库作为项目的一部分提交到 SCM，并由依赖它的任何项目引用。存储库将在项目 pom 中声明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方包都必须遵守本文中所述的 AEM as a Cloud Service 编码和打包准则，否则，包含该包将导致部署失败。

以下 Maven `POM.xml` 代码片段展示了如何通过 **filevault-package-maven-plugin** Maven 插件配置将第三方包嵌入项目的“容器”包（通常名为 **&#39;all&#39;**）中。

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

与 AEM 更新一样，客户版本使用滚动部署策略进行部署，以便在适当的情况下消除创作群集停机时间。下面介绍了事件的常规序列，其中具有旧版本和新版本客户代码的节点运行的是相同版本的AEM代码。

* 具有旧版本的节点处于活动状态，并且已构建新版本的发行候选版本，该版本将变得可用。
* 如果存在任何新的或更新的索引定义，则处理相应的索引。请注意，旧版本的节点将始终使用旧索引，而新版本的节点将始终使用新索引。
* 具有新版本的节点在旧版本仍提供流量时启动。
* 运行旧版本的节点并保持服务，同时通过运行状况检查检查新版本的节点是否已准备就绪。
* 新版本已就绪的节点将接受通信量并使用已停止运行的旧版本替换节点。
* 随着时间的推移，具有旧版本的节点将由具有新版本的节点替换，直到仅具有新版本的节点保留，从而完成部署。
* 然后部署任何新的或修改后的可变内容。

## 索引 {#indexes}

新索引或修改的索引将导致在新版本能够接收流量之前执行额外的索引或重新索引步骤。 有关 AEM as a Cloud Service 中的索引管理的详细信息，请参阅[本文](/help/operations/indexing.md)。您可以在 Cloud Manager 生成页面上查看索引工作的状态，并将在新版本准备好接收流量时收到通知。

>[!NOTE]
>
>滚动部署所需的时间因索引的大小而异，因为新版本在生成新索引之前无法接受流量。

目前，AEM as a Cloud Service 无法与 ACS Commons Ensure Oak Index 工具等索引管理工具配合使用。

## 复制 {#replication}

发布机制与 [AEM Replication Java API](https://helpx.adobe.com/cn/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html) 向后兼容。

为了使用云就绪 AEM 快速入门来开发和测试复制，需要将经典的复制功能与创作/发布设置结合使用。如果已为云删除 AEM 创作上的 UI 入口点，用户将转到 `http://localhost:4502/etc/replication` 以进行配置。

## 用于滚动部署的向后兼容代码 {#backwards-compatible-code-for-rolling-deployments}

如上详述，AEM as a Cloud Service 的滚动部署策略意味着可以同时运行新版本和旧版本。因此，请注意无法与仍在运行的旧 AEM 版本向后兼容的代码更改。

此外，应测试旧版本与新版本在回滚时应用的任何新的可变内容结构的兼容性，因为不会删除可变内容。

### 服务用户和 ACL 更改 {#service-users-and-acl-changes}

更改访问内容或代码所需的服务用户或 ACL 可能会导致旧 AEM 版本出错，从而导致使用过期的服务用户访问该内容或代码。要解决此行为，建议在至少两个版本中进行更改，其中第一个版本在后续版本中进行清理之前充当桥接器。

### 索引更改 {#index-changes}

如果对索引进行了更改，则新版本应继续使用其索引，直到被终止，而旧版本则使用自己的修改后的索引集，这一点非常重要。 开发人员应采用[本文](/help/operations/indexing.md)中描述的索引管理方法。

### 用于回滚的保守编码 {#conservative-coding-for-rollbacks}

如果在部署后报告或检测到故障，则可能需要回滚到旧版本。 建议确保新代码与该新版本创建的任何新结构兼容，因为不会回退新结构（任何可变内容内容）。 如果旧代码不兼容，则需要在后续的客户版本中应用修复。

## 快速开发环境 (RDE) {#rde}

[快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md)（简称为 RDE）允许开发人员快速部署和审查更改，最大程度地减少测试已证明适用于本地开发环境的功能所需的时间。

与通过 Cloud Manager 管道部署代码的常规开发环境不同，开发人员使用命令行工具将代码从本地开发环境同步到 RDE。在 RDE 中成功测试更改后，应通过 Cloud Manager 管道将更改部署到常规云开发环境，这可让代码通过相应的质量关卡。

## 运行模式 {#runmodes}

在现有的 AEM 解决方案中，客户可以选择在任意运行架构中运行实例，并应用 OSGI 配置或将 OSGI 捆绑包安装到这些特定实例。定义的运行架构通常包括&#x200B;*服务*（创作和发布）和环境（RDE、开发、暂存、生产）。

另一方面，AEM as a Cloud Service 会更武断地认定哪些运行架构可用以及如何将 OSGI 捆绑包和 OSGI 配置映射到这些架构：

* OSGI 配置运行架构必须引用 RDE、开发、暂存或生产作为环境，或引用创作和发布作为服务。支持组合使用 `<service>.<environment_type>`，但必须按此特定顺序使用它们（例如 `author.dev` 或 `publish.prod`）。应直接从代码中引用 OSGI 令牌，而不是使用 `getRunModes` 方法（该方法在运行时将不再包含 `environment_type`）引用它。有关更多信息，请参阅[为 AEM as a Cloud Service 配置 OSGi](/help/implementing/deploying/configuring-osgi.md)。
* OSGI 捆绑包运行架构仅适用于服务（创作、发布）。每运行架构 OSGI 捆绑包应安装在 `install.author` 或 `install.publish` 下的内容包中。

AEM as a Cloud Service 不允许使用运行模式为特定环境或服务安装内容。如果开发环境需要使用暂存或生产环境中不存在的数据或 HTML 进行播种，则可以使用包管理器。

不受支持的运行架构配置包括：

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

使用具有最匹配的运行架构的 OSGI 配置。

在进行本地开发时，运行架构启动参数 `-r` 用于指定运行架构 OSGI 配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 源代码管理中的维护任务配置 {#maintenance-tasks-configuration-in-source-control}

维护任务配置必须保留在源代码管理中，因为&#x200B;**工具 > 操作**&#x200B;屏幕在云环境中将不再可用。这样做的好处是确保有意保留更改，而不是被动应用并可能忘记更改。请参考[“维护任务”一文](/help/operations/maintenance.md)以了解更多信息。
