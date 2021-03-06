---
title: 部署到 AEM as a Cloud Service
description: '部署到 AEM as a Cloud Service '
feature: Deploying
exl-id: 7fafd417-a53f-4909-8fa4-07bdb421484e
source-git-commit: 4fcb2ff39f0634cfcdab5500b03441f6db0b474d
workflow-type: tm+mt
source-wordcount: '3358'
ht-degree: 1%

---

# 部署到 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 简介 {#introduction}

与AEM On Premise和Managed Services解决方案相比，AEM as a Cloud Service中代码开发的基础知识相似。 开发人员编写代码并在本地进行测试，然后将代码推送到远程AEMas a Cloud Service环境。 Cloud Manager是Managed Services的可选内容交付工具，它是必需的。 现在，这是将代码部署到AEMas a Cloud Service环境的唯一机制。

更新 [AEM版本](/help/implementing/deploying/aem-version-updates.md) 始终是与推送分开的部署事件 [自定义代码](#customer-releases). 换种方式看，应针对生产上的AEM版本测试自定义代码版本，因为这是将在顶部部署的版本。 AEM版本更新之后发生的事件，该版本将会频繁进行并自动应用。 它们旨在向后兼容已部署的客户代码。

本文档的其余部分将介绍开发人员如何调整其实践，以便与AEM as a Cloud Service的版本更新和客户更新结合使用。

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html).
-->

## 客户版本 {#customer-releases}

### 使用正确的AEM版本进行编码 {#coding-against-the-right-aem-version}

对于以前的AEM解决方案，最新的AEM版本很少更改（大约每年一次，每季度提供Service Pack），客户将自行将生产实例更新为最新的快速启动，并引用API Jar。 但是，AEMas a Cloud Service应用程序会更频繁地自动更新到AEM的最新版本，因此内部版本的自定义代码应该针对最新版本的AEM构建。

与现有非云AEM版本一样，将支持基于特定快速入门的本地离线开发，在大多数情况下，该开发工具有望成为调试的首选工具。

>[!NOTE]
>与Adobe云相比，应用程序在本地计算机上的行为方式存在细微的操作差异。 在本地开发过程中，必须遵守这些架构差异，并且在云基础架构上部署时，可能会导致不同的行为。 由于这些差异，在生产中推出新的自定义代码之前，必须对开发环境和暂存环境执行详尽的测试。

为了为内部版本开发自定义代码，请使用 [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 应下载并安装。 有关使用AEMas a Cloud ServiceDispatcher工具的其他信息，请参阅 [本页](/help/implementing/dispatcher/disp-overview.md).

以下视频提供了有关如何将代码部署到AEMas a Cloud Service的高级概述：

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

<!--
>[!NOTE]
>It is recommended for customers with existing code bases, to go through the repository restructuring exercise described in the [AEM documentation](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html). 
-->

## 通过Cloud Manager和包管理器部署内容包 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 通过Cloud Manager进行部署 {#deployments-via-cloud-manager}

客户可通过Cloud Manager将自定义代码部署到云环境。 应该注意的是，Cloud Manager会将本地装配的内容包转换为符合Sling特征模型的对象，该模型是在云环境中运行AEMas a Cloud Service应用程序时对该应用程序的描述方式。 因此，在查看 [包管理器](/help/implementing/developing/tools/package-manager.md) 在云环境中，名称将包含“cp2fm”，且转换的包已删除所有元数据。 它们不能进行交互，这意味着无法下载、复制或打开它们。 有关转换器的详细文档可以是 [此处](https://github.com/apache/sling-org-apache-sling-feature-cpconverter).

为AEMas a Cloud Service应用程序编写的内容包必须在不可变内容和可变内容之间保持清晰的隔离，Cloud Manager将只安装可变内容，并输出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本节的其余部分将介绍不可改变和可变包的组成和含义。

### 不可变内容包 {#immutabe-content-packages}

必须将不可变存储库中保留的所有内容和代码签入到git中，并通过Cloud Manager进行部署。 换言之，与当前的AEM解决方案不同，代码永远不会直接部署到正在运行的AEM实例。 这可确保在任何云环境中为给定版本运行的代码都相同，从而消除生产中无意更改代码的风险。 例如，OSGi配置应提交给源代码控制，而不是在运行时通过AEM Web控制台的配置管理器进行管理。

由于交换机启用了蓝绿色部署模式，因此应用程序发生更改时，除服务用户、其ACL、节点类型和索引定义更改外，它们不能依赖可变存储库中的更改。

对于具有现有代码库的客户，务必要完成AEM文档中描述的存储库重组练习，以确保将以前位于/etc下的内容移动到正确的位置。

例如，对这些代码包还存在一些其他限制 [安装挂钩](http://jackrabbit.apache.org/filevault/installhooks.html) 不受支持。

## OSGI 配置 {#osgi-configuration}

如上所述，OSGI配置应提交给源代码控制，而不是通过Web控制台。 实现此目的的技术包括：

* 使用AEM Web控制台的配置管理器在开发人员的本地AEM环境中进行必要的更改，然后将结果导出到本地文件系统上的AEM项目
* 在本地文件系统的AEM项目中手动创建OSGi配置，该配置将引用AEM控制台的配置管理器来获取属性名称。

有关OSGI配置的更多信息，请访问 [为AEMas a Cloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md).

## 可变内容 {#mutable-content}

在某些情况下，在源代码控制中准备内容更改可能会有所帮助，以便每当更新环境时，Cloud Manager都可以部署该内容。 例如，为某些根文件夹结构种子或在可编辑模板中排列更改，以便为应用程序部署所更新的组件启用策略，这可能是合理的。

有两种策略可描述Cloud Manager将部署到可变存储库、可变内容包和重新指向语句的内容。

### 可变内容包 {#mutable-content-packages}

文件夹路径层次结构、服务用户和访问控制(ACL)等内容通常会提交到基于Maven原型的AEM项目中。 技术包括从AEM导出或直接编写为XML。 在构建和部署过程中，Cloud Manager会打包生成的可变内容包。 在管道的部署阶段，可变内容会在3个不同的时间安装：

在启动新版应用程序之前：

* 索引定义（添加、修改、删除）

在应用程序新版本启动期间，但在切换之前：

* 服务用户（添加）
* 服务用户ACL（添加）
* 节点类型（添加）

切换到新版应用程序后：

* 可通过jackrabbit保管库定义的所有其他内容。 例如：
   * 文件夹（添加、修改、删除）
   * 可编辑的模板（添加、修改、删除）
   * 上下文感知配置( `/conf`)（添加、修改、删除）
   * 脚本(软件包可以在软件包安装过程的各个阶段触发安装挂接。 请参阅 [Jackrabbit filevault文档](http://jackrabbit.incubator.apache.org/filevault/installhooks.html) 关于安装挂钩。 请注意，AEM CS当前使用的是Filevault 3.4.0版，该版本限制管理员用户、系统用户和管理员组的成员安装挂接)。

可以通过将包嵌入install.author或install.publish文件夹(位于 `/apps`. 为了反映这一分离，已在AEM 6.5中完成了重组，有关推荐项目重组的详细信息，请参阅 [AEM 6.5文档。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>内容包将部署到所有环境类型（开发、暂存、生产）。 无法将部署限制到特定环境。 此限制旨在确保自动执行的测试运行选项。 特定于环境的内容需要通过手动安装 [包管理器。](/help/implementing/developing/tools/package-manager.md)

此外，在应用可变内容包更改后，没有回滚这些更改的机制。 如果客户检测到问题，他们可以选择在下一个代码版本中解决该问题，或者作为最后手段，在部署之前将整个系统恢复到某个时间点。

任何包含的第三方包都必须验证为与AEMas a Cloud Service服务兼容，否则，其包含将导致部署失败。

如上所述，具有现有代码库的客户应符合 [AEM 6.5文档。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## 重新指向 {#repoinit}

对于以下情况，最好采用手工编码显式内容创建的方法 `repoinit` OSGi工厂配置中的语句：

* 创建/删除/禁用服务用户
* 创建/删除群组
* 创建/删除用户
* 添加ACL

   >[!NOTE]
   >
   >ACL的定义要求节点结构已存在。 因此，可能需要在创建路径语句之前执行。

* 添加路径（例如根文件夹结构）
* 添加CND（节点类型定义）

由于具有以下优势，因此在这些受支持的内容修改用例中，请重新指出：

* 重新指向会在启动时创建资源，以便逻辑可以认为这些资源的存在是理所当然的。 在可变内容包方法中，资源在启动后创建，因此依赖这些资源的应用程序代码可能会失败。
* 由于您明确控制要执行的操作，因此重新指示是一个相对安全的指令集。 此外，除了允许删除用户、服务用户和组的一些与安全相关的案例外，唯一受支持的操作是附加的。 相反，在可变内容包方法中删除某些内容是明确的；在定义过滤器时，过滤器所涵盖的任何内容都将被删除。 但是，仍应谨慎行事，因为对于任何内容，存在新内容可能会改变应用程序的行为。
* 重新定位执行快速和原子操作。 相比之下，可变内容包的性能取决于过滤器所覆盖的结构。 即使您更新单个节点，也可能会创建大树的快照。
* 可以在运行时在本地开发环境中验证repoinit语句，因为这些语句将在注册OSGi配置时执行。
* 重新指向语句是原子和显式语句，如果状态已匹配，则将跳过。

当Cloud Manager部署应用程序时，它会执行这些语句，而不依赖于任何内容包的安装。

要创建重新指向语句，请按照以下步骤操作：

1. 为工厂PID添加OSGi配置 `org.apache.sling.jcr.repoinit.RepositoryInitializer` 在项目的配置文件夹中。 为配置使用描述性名称，如 **org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**.
1. 将重新指向语句添加到配置的script属性中。 语法和选项在 [Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html). 请注意，应在父文件夹的子文件夹之前明确创建父文件夹。 例如， `/content` 之前 `/content/myfolder`之前 `/content/myfolder/mysubfolder`. 对于在低级别结构上设置的ACL，建议在更高级别上设置ACL，并使用 `rep:glob` 限制。  例如 `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. 在运行时在本地开发环境中验证。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>为下面的节点定义的ACL `/apps` 或 `/libs` 将在空白存储库上开始重新指示执行。 资源包在重新指向后安装，因此语句不能依赖资源包中定义的任何内容，但必须定义先决条件，如下面的父结构。

>[!TIP]
>
>对于ACL，创建深层结构可能会很麻烦，因此在更高级别上定义ACL并通过rep:glob限制约束其应执行的位置更合理。

有关重新点击的更多详细信息，请参阅 [Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可变内容包的包管理器“一次性” {#package-manager-oneoffs-for-mutable-content-packages}

>[!CONTEXTUALHELP]
>id="aemcloud_packagemanager"
>title="包管理器 — 迁移可变内容包"
>abstract="探索包管理器的用例，了解应将内容包作为“一次性”安装的用例，其中包括将特定内容从生产导入到暂存，以调试生产问题、将小内容包从内部部署环境传输到AEM云环境等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#cloud-migration" text="内容传输工具"

在某些用例中，应将内容包安装为“一次性”。 例如，将特定内容从生产导入到暂存，以调试生产问题。 对于这些情况， [包管理器](/help/implementing/developing/tools/package-manager.md) 可在AEMas a Cloud Service环境中使用。

由于包管理器是一个运行时概念，因此无法将内容或代码安装到不可变存储库中，因此这些内容包应该只包含可变内容(主要是 `/content` 或 `/conf`)。 如果内容包包含混合内容（可变内容和不可变内容），则只会安装可变内容。

>[!IMPORTANT]
>
>包管理器UI可能会返回 **未定义** 安装包需要超过10分钟时出现错误消息。
>
>这不是由于安装错误，而是由于Cloud Service对所有请求具有的超时。
>
>如果看到此类错误，请不要重试安装。 安装在后台正常进行。 如果重新启动安装，则多个并发导入进程可能会引发一些冲突。

通过Cloud Manager安装的任何内容包（可变和不可变）都将在AEM Package Manager的用户界面中显示为冻结状态。 无法重新安装、重新构建或甚至下载这些包，这些包将随 **&quot;cp2fm&quot;** 后缀，表示其安装由Cloud Manager管理。

### 包括第三方包 {#including-third-party}

客户通常会包含来自第三方源(如Adobe的翻译合作伙伴等软件供应商)的预建包。 建议将这些包托管在远程存储库中，并在 `pom.xml`. 这对于公共存储库以及具有密码保护的专用存储库是可能的，如 [受密码保护的maven存储库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).

如果无法在远程存储库中存储包，则客户可以将包放置在基于本地文件系统的Maven存储库中，该存储库将作为项目的一部分提交到SCM，并由依赖于它的任何内容引用。 存储库将在项目pom中声明，如下所示：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方包都必须遵循本文中所述的AEMas a Cloud Service服务编码和打包准则，否则，其包含将导致部署失败。

以下马文 `POM.xml` 此代码片段显示了如何将第三方包嵌入项目的“容器”包中，通常名为 **“all”**，通过 **filevault-package-maven-plugin** Maven插件配置。

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

与AEM更新一样，客户版本使用滚动部署策略进行部署，以便在正确的情况下消除创作群集停机时间。 事件的一般顺序如下所述，其中 **蓝色** 是旧版本的客户代码和 **绿色** 是新版本。 蓝色和绿色运行的AEM代码版本相同。

* 蓝色版本处于活动状态，并且已构建并提供绿色的发布候选项
* 如果存在任何新的或更新的索引定义，则会处理相应的索引。 请注意，蓝色部署将始终使用旧索引，而绿色部署将始终使用新索引。
* Blue仍在服务时， Green即已启动
* 蓝色正在运行和提供服务，同时正在通过运行状况检查检查绿色是否已准备就绪
* 已准备就绪的绿色节点接受流量并替换蓝色节点，蓝色节点将被下拉
* 随着时间的推移，蓝色节点将被绿色节点替换，直到仅保留绿色节点，从而完成部署
* 部署了任何新的或修改的可变内容

## 索引 {#indexes}

新的或修改的索引将导致在新（绿色）版本的流量上执行额外的索引或重新索引步骤。 有关AEMas a Cloud Service中索引管理的详细信息，请参阅 [本文](/help/operations/indexing.md). 您可以在Cloud Manager内部版本页面上检查索引作业的状态，并在新版本准备好接收流量时收到通知。

>[!NOTE]
>
>滚动部署所需的时间将因索引的大小而异，因为绿色版本在生成新索引之前无法接受流量。

目前，AEM as a Cloud Service Index工具（如ACS Commons Ensure Oak Index工具）无法使用索引管理工具。

## 复制 {#replication}

发布机制向后兼容 [AEM复制Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html).

要使用云就绪型AEM快速启动开发和测试复制功能，需要将经典复制功能与创作/发布设置结合使用。 如果已为云删除AEM作者上的UI入口点，则用户将转到 `http://localhost:4502/etc/replication` ，以进行配置。

## 用于滚动部署的向后兼容代码 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM  as a Cloud Service的滚动部署策略意味着旧版本和新版本可能同时运行。 因此，请谨慎处理代码更改，这些更改不向后兼容仍在运行的旧AEM版本。

此外，应该对旧版本进行测试，以验证在回滚事件中新版本应用的任何新可变内容结构的兼容性，因为不会删除可变内容。

### 服务用户和ACL更改 {#service-users-and-acl-changes}

更改访问内容或代码所需的服务用户或ACL可能会导致旧版AEM中出现错误，从而导致服务用户对该内容或代码的访问权限过时。 要解决此问题，建议在至少2个版本之间进行更改，其中第一个版本在后续版本中清理之前充当桥梁。

### 索引更改 {#index-changes}

如果对索引进行了更改，则务必要让蓝色版本继续使用其索引，直到其终止，而绿色版本使用其自己修改过的索引集。 开发人员应遵循描述的索引管理技术 [在本文中](/help/operations/indexing.md).

### 回滚的保守编码 {#conservative-coding-for-rollbacks}

如果在部署后报告或检测到故障，则可能需要回滚到蓝色版本。 最好确保蓝色代码与绿色版本创建的任何新结构兼容，因为新结构（任何可变内容内容）将不会回滚。 如果旧代码不兼容，则需要在后续客户版本中应用修复。

## 运行模式 {#runmodes}

在现有AEM解决方案中，客户可以选择以任意运行模式运行实例，并将OSGi配置或安装OSGi包到这些特定实例。 通常定义的运行模式包括 *服务* （创作和发布）和环境(dev、stage、prod)。

AEMas a Cloud Service则对哪些运行模式可用以及如何将OSGi包和OSGi配置映射到这些模式有更多看法：

* OSGi配置运行模式必须引用dev、stage、prod for the environment或author、publish for the service。 组合 `<service>.<environment_type>` 受支持，但必须按此特定顺序使用(例如 `author.dev` 或 `publish.prod`)。 OSGi令牌应直接从代码中引用，而不应使用 `getRunModes` 方法，该方法将不再包含 `environment_type` 运行时。 有关更多信息，请参阅 [为AEMas a Cloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md).
* OSGi包运行模式仅限于服务（创作、发布）。 每次运行模式OSGi包应安装在以下任一模式下的内容包中 `install/author` 或 `install/publish`.

与现有的AEM解决方案一样，无法使用运行模式仅为特定环境或服务安装内容。 如果需要为开发环境种种不在暂存或生产环境中的数据或HTML，则可以使用包管理器。

支持的运行模式配置包括：

* **配置** (*默认值适用于所有AEM服务*)
* **config.author** (*适用于所有AEM创作服务*)
* **config.author.dev** (*适用于AEM Dev Author服务*)
* **config.author.stage** (*适用于AEM Staging Author服务*)
* **config.author.prod** (*适用于AEM Production Author服务*)
* **config.publish** (*适用于AEM发布服务*)
* **config.publish.dev** (*适用于AEM开发发布服务*)
* **config.publish.stage** (*适用于AEM Staging Publish服务*)
* **config.publish.prod** (*适用于AEM Production Publish服务*)
* **config.dev** (*适用于AEM开发服务*)
* **config.stage** (*适用于AEM Staging Services*)
* **config.prod** (*适用于AEM Production Services*)

使用的OSGi配置具有最匹配的运行模式。

在本地开发时，运行模式启动参数 `-r`，用于指定运行模式OSGI配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 源代码管理中的维护任务配置 {#maintenance-tasks-configuration-in-source-control}

维护任务配置必须保留在源代码控制中，因为 **工具>操作** 屏幕在云环境中将不再可用。 这有利于确保有意保留更改，而不是反向应用更改，或许会被遗忘。 请参考 [维护任务文章](/help/operations/maintenance.md) 以了解其他信息。
