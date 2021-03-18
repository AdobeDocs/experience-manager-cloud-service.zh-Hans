---
title: 部署到 AEM as a Cloud Service
description: '部署到 AEM as a Cloud Service '
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 部署到 AEM as a Cloud Service {#deploying-to-aem-as-a-cloud-service}

## 简介 {#introduction}

与AEM内部部署和Managed Services解决方案相比，AEM中代码开发的基础知识与Cloud Service相似。 开发人员编写代码并在本地测试它，然后将它作为Cloud Service环境推送到远程AEM。 Cloud Manager是Managed Services的可选内容投放工具，是必需的。 现在，这是将代码作为Cloud Service环境部署到AEM的唯一机制。

[AEM版本](/help/implementing/deploying/aem-version-updates.md)的更新始终是推送[自定义代码](#customer-releases)的单独部署事件。 换种方式来看，应针对生产上的AEM版本测试自定义代码发行版，因为它将部署在顶部。 AEM版本更新后发生，将会频繁进行并自动应用。 它们旨在向后兼容已部署的客户代码。

本文档的其余部分将介绍开发人员如何调整其做法，以便将AEM作为Cloud Service的版本更新和客户更新结合使用。

>[!NOTE]
>建议具有现有代码库的客户完成[ AEM文档](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中描述的存储库重构练习。

## 客户版本{#customer-releases}

### 针对正确的AEM版本{#coding-against-the-right-aem-version}进行编码

对于以前的AEM解决方案，最新的AEM版本更改不频繁（大约每年每季度提供一次Service Pack），客户会自行将生产实例更新到最新的快速启动程序（引用API Jar）。 但是，AEM作为Cloud Service应用程序会更频繁地自动更新到最新版AEM，因此内部发行版的自定义代码应根据最新AEM版本构建。

与现有非云AEM版本一样，将支持基于特定快速入门的本地脱机开发，并且在大多数情况下，预计该开发工具将成为调试的首选工具。

>[!NOTE]
>与Adobe Cloud相比，应用程序在本地计算机上的行为方式之间存在微妙的操作差异。 在本地开发过程中，必须尊重这些体系结构上的差异，并可能导致在云基础架构上部署时出现不同的行为。 由于这些差异，在生产中推出新的自定义代码之前，必须对开发和阶段环境执行详尽的测试。

为了为内部版本开发自定义代码，应下载并安装作为Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)的[AEM的相关版本。 有关将AEM用作Cloud Service调度程序工具的其他信息，请参阅[此页](/help/implementing/dispatcher/disp-overview.md)。

以下视频概括介绍了如何将代码作为Cloud Service部署到AEM:

>[!VIDEO](https://video.tv.adobe.com/v/30191?quality=9)

>[!NOTE]
>建议具有现有代码库的客户完成[ AEM文档](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)中描述的存储库重构练习。

## 通过Cloud Manager和Package Manager {#deploying-content-packages-via-cloud-manager-and-package-manager}部署内容包

### 通过Cloud Manager {#deployments-via-cloud-manager}进行部署

客户通过Cloud Manager将自定义代码部署到云环境。 应当注意的是，Cloud Manager会将本地组合的内容包转换为符合Sling特征模型的伪像，即在云环境中运行时，AEM应用程序是如何描述为Cloud Service应用程序的。 因此，在查看云环境上的包管理器中的包时，名称将包括“cp2fm”，转换的包将删除所有元数据。 它们无法与之交互，这意味着它们无法下载、复制或打开。 有关转换器的详细文档可在此](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)找到。[

作为Cloud Service应用程序写入的AEM内容包必须在不可变内容和可变内容之间保持清晰的隔离，Cloud Manager将通过失败生成来强制执行，并输出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本节的其余部分将描述不可改变和可变包的组成和含义。

### 不可变的内容包{#immutabe-content-packages}

必须在不可变存储库中保留的所有内容和代码都必须签入git并通过Cloud Manager进行部署。 换句话说，与当前的AEM解决方案不同，代码从未直接部署到正在运行的AEM实例。 这可确保在任何云环境中为给定版本运行的代码相同，从而消除在生产过程中无意发生代码变化的风险。 例如，OSGI配置应提交到源代码控制，而不是在运行时通过AEM Web控制台的配置管理器进行管理。

由于交换机启用了蓝绿色部署模式导致的应用程序更改，因此，除服务用户、其ACL、节点类型和索引定义更改外，这些更改不能取决于可变存储库中的更改。

对于具有现有代码库的客户，请仔细研究AEM文档中描述的存储库重组练习，以确保将以前位于/etc下的内容移动到正确的位置。

不支持对这些代码包应用一些附加限制，例如[安装挂接](http://jackrabbit.apache.org/filevault/installhooks.html)。

## OSGI配置{#osgi-configuration}

如上所述，应将OSGI配置提交到源代码控制，而不是通过Web控制台。 这样做的技术包括：

* 使用AEM web控制台的配置管理器对开发人员的本地AEM环境进行必要的更改，然后将结果导出到本地文件系统上的AEM项目
* 在本地文件系统上的AEM项目中手动创建OSGI配置，该配置将引用AEM控制台的配置管理器以获取属性名称。

有关OSGI配置的更多信息，请访问[将AEM的OSGi配置为Cloud Service](/help/implementing/deploying/configuring-osgi.md)。

## 可变内容{#mutable-content}

在某些情况下，在源代码管理中准备内容更改可能会很有用，以便在更新环境时，Cloud Manager可以部署它。 例如，为某些根文件夹结构植入种子或在可编辑模板中排列更改，以便在那些由应用程序部署更新的组件中启用策略，这可能是合理的。

有两种策略可描述Cloud Manager将部署到可变存储库的内容、可变内容包和重新指向语句。

### 可变内容包{#mutable-content-packages}

诸如文件夹路径层次结构、服务用户和访问控制(ACL)等内容通常会提交到基于主原型的AEM项目中。 技术包括从AEM导出或直接编写为XML。 在构建和部署过程中，Cloud Manager将生成的可变内容包打包。 可变内容在管道的部署阶段安装在3个不同的时间：

在启动新版本的应用程序之前：

* 索引定义（添加、修改、删除）

在启动新版本的应用程序时，但切换之前：

* 服务用户（添加）
* 服务用户ACL（添加）
* 节点类型（添加）

切换到新版应用程序后：

* 所有其他内容可通过jackrabbitvault定义。 例如：
   * 文件夹（添加、修改、删除）
   * 可编辑的模板（添加、修改、删除）
   * 上下文感知配置（`/conf`下的任何内容）（添加、修改、删除）
   * 脚本(软件包可以在软件包安装过程的各个阶段触发安装挂钩

通过将包嵌入install.author或install.publish文件夹（位于`/apps`下），可以将可变内容安装限制为创作或发布。 在AEM 6.5中进行了重组，以反映此分离，有关建议项目重组的详细信息，请参阅[AEM 6.5文档。](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html)

>[!NOTE]
>内容包将部署到所有环境类型(dev、stage、prod)。 无法将部署限制为特定环境。 此限制旨在确保自动执行的测试运行选项。 特定于环境的内容需要通过包管理器手动安装。

此外，在应用可变内容包更改后，没有回滚这些更改的机制。 如果客户检测到问题，他们可以选择在下一个代码版本中修复它，或作为最后手段，将整个系统恢复到部署前的某个时间点。

必须验证包含的任何第三方包是否与AEM兼容，否则其包含将导致部署失败。

如上所述，拥有现有代码库的客户应符合[AEM 6.5文档中描述的6.5存储库更改所需的存储库重构操作。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/repository-restructuring.html)

## 重新指向{#repoinit}

对于以下情况，最好在OSGI工厂配置中采用手工编码显式内容创建`repoinit`语句的方法：

* 创建/删除/禁用服务用户
* 创建/删除组
* 创建/删除用户
* 添加ACL

   >[!NOTE]
   >
   >定义ACL要求节点结构已存在。 因此，可能需要在创建路径语句之前执行。

* 添加路径（例如根文件夹结构）
* 添加CND（nodetype定义）

由于以下优点，对于这些受支持的内容修改用例，最好重新指明：

* Repoinit在启动时创建资源，这样逻辑就可以认为这些资源的存在是理所当然的。 在可变内容包方法中，资源是在启动后创建的，因此依赖它们的应用程序代码可能会失败。
* 重新指示是相对安全的指令集，因为您显式控制要执行的操作。 此外，除了允许删除用户、服务用户和组的一些与安全相关的情况外，唯一支持的操作是附加的。 相反，删除可变内容包方法中的某些内容是明确的； 在您定义过滤器时，过滤器所涵盖的任何内容都将被删除。 但是，应当小心谨慎，因为对于任何内容，新内容的存在可能会改变应用程序的行为。
* 重新指向可执行快速和原子操作。 相比之下，可变内容包可以高度依赖于滤镜所覆盖的结构的性能。 即使更新单个节点，也可能会创建大树的快照。
* 可以在运行时验证本地开发环境上的重新指向语句，因为在注册OSGi配置时将执行它们。
* 重新指向语句是原子和显式的，如果状态已匹配，则将跳过。

当Cloud Manager部署应用程序时，它将执行这些语句，而与任何内容包的安装无关。

要创建重新指向语句，请按照以下步骤操作：

1. 在项目的配置文件夹中添加工厂PID `org.apache.sling.jcr.repoinit.RepositoryInitializer`的OSGi配置。 对配置使用描述性名称，如&#x200B;**org.apache.sling.jcr.repoinit.RepositoryInitializer~initstructure**。
1. 将重新指向语句添加到配置的脚本属性。 语法和选项在[Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)中有说明。 请注意，应在父文件夹的子文件夹之前显式创建父文件夹。 例如，在`/content/myfolder`之前、在`/content/myfolder/mysubfolder`之前显式创建`/content`。 对于在低级结构上设置的ACL，建议在较高级别上设置ACL，并使用`rep:glob`限制。  例如`(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`。
1. 在运行时在本地开发环境上验证。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>对于为`/apps`或`/libs`下的节点定义的ACL，重新指向执行将开始空的存储库。 软件包安装在重新指向之后，因此语句不能依赖包中定义的任何内容，而必须定义先决条件，如下面的父结构。

>[!TIP]
>
>对于ACL，创建深层结构可能比较繁琐，因此更合理地在更高级别定义ACL，并通过rep:glob限制约束其应在何处操作。

有关重新指向的详细信息，请参阅[Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可变内容包{#package-manager-oneoffs-for-mutable-content-packages}的包管理器“one offs”

在某些情况下，内容包应作为“一次性”安装。 例如，将特定内容从生产导入到暂存，以调试生产问题。 对于这些情况，包管理器可以在AEM中用作Cloud Service环境。

由于包管理器是一个运行时概念，因此无法将内容或代码安装到不可变的存储库中，因此这些内容包只应由可变内容（主要是`/content`或`/conf`）组成。 如果内容包包含混合的内容（可变内容和不可变内容），则将仅安装可变内容。

通过Cloud Manager安装的任何内容包（可变和不可变）都将在AEM Package Manager的用户界面中显示为冻结状态。 无法重新安装、重新构建或甚至下载这些包，并将以&#x200B;**&quot;cp2fm&quot;**&#x200B;后缀列出，表明其安装由Cloud Manager管理。

### 包括第三方包{#including-third-party}

客户通常会包括来自第三方来源(如Adobe翻译合作伙伴等软件供应商)的预建包。 建议将这些包托管在远程存储库中，并在`pom.xml`中引用它们。 这适用于公共存储库，也适用于具有密码保护的专用存储库，如[受密码保护的主存储库](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories)中所述。

如果无法将包存储在远程存储库中，客户可以将包放置在基于本地文件系统的Maven存储库中，该存储库作为项目的一部分提交到SCM，并由依赖它的任何对象引用。 储存库将在以下项目展示中宣布：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方包都必须遵守AEM作为本文所述的Cloud Service服务编码和打包指南，否则，其包含将导致部署失败。

以下Maven POM XML代码片断展示了如何通过 **filevault-package-maven-plugin** Maven插件配置将第三方包嵌入项目的“容器”包中(通常名为 **** &#39;all&#39;)。

```
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <subPackages>
           
          <!-- Include the application's ui.apps and ui.content packages -->
          ...
 
          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <!-- Set the version for all dependencies, including 3rd party packages, in the project's Reactor POM -->
          <subPackage>
              <groupId>com.adobe.cq</groupId>
              <artifactId>core.wcm.components.all</artifactId>
              <filter>true</filter>
          </subPackage>
 
 
          <subPackage>
              <groupId>com.3rdparty.groupId</groupId>
              <artifactId>core.3rdparty.artifactId</artifactId>
              <filter>true</filter>
          </subPackage>
      <subPackages>
  </configuration>
</plugin>
...
```

## 滚动部署的工作方式{#how-rolling-deployments-work}

与AEM更新一样，客户版本使用滚动部署策略进行部署，以便在适当的情况下消除作者群集停机时间。 事件的常规序列如下所述，其中&#x200B;**Blue**&#x200B;是旧版客户代码，**Green**&#x200B;是新版本。 蓝色和绿色运行的AEM代码版本相同。

* 蓝色版本处于活动状态，并且已构建并提供绿色版的候选发行版
* 如果存在任何新的或更新的索引定义，则处理相应的索引。 请注意，蓝色部署将始终使用旧索引，而绿色部署将始终使用新索引。
* “蓝色”仍在服务时，“绿色”正在启动
* 蓝色正在运行，并且正在通过运行状况检查检查检查绿色是否准备就绪
* 准备就绪的绿色节点接受通信并替换已关闭的蓝色节点
* 随着时间的推移，蓝色节点被绿色节点替换，直到仅绿色节点保留，从而完成部署
* 已部署任何新的或修改的可变内容

## 索引{#indexes}

新的或修改的索引将导致在新（绿色）版本开始流量之前执行额外的索引或重新索引步骤。 有关AEM作为Cloud Service的索引管理的详细信息，请参阅本文[](/help/operations/indexing.md)。 您可以在Cloud Manager构建页上检查索引作业的状态，并在新版本准备就绪后收到通知。

>[!NOTE]
>
>滚动部署所需的时间会因索引的大小而异，因为生成新索引之前，绿色版本不能接受通信。

目前，AEM作为Cloud Service无法使用索引管理工具，如ACS Commons Ensure Oak Index工具。

## 复制 {#replication}

发布机制与[AEM Replication Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)向后兼容。

要使用云就绪型AEM快速启动开发和测试复制功能，需要将经典复制功能与作者/发布设置结合使用。 如果已为云删除AEM作者上的UI入口点，则用户将转至`http://localhost:4502/etc/replication`进行配置。

## 滚动部署的向后兼容代码{#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM作为Cloud Service的滚动部署策略意味着旧版本和新版本可能同时运行。 因此，请注意代码更改与仍在运行的旧AEM版本不向后兼容。

此外，应测试旧版本与回滚事件中新版本应用的任何新可变内容结构的兼容性，因为不会删除可变内容。

### 服务用户和ACL更改{#service-users-and-acl-changes}

更改访问内容或代码所需的服务用户或ACL可能会导致较早的AEM版本中出现错误，从而导致对过时服务用户访问该内容或代码。 要解决此行为，建议在至少2个版本之间传播更改，第一个版本在后续版本中清理之前充当桥。

### 索引更改{#index-changes}

如果对索引进行了更改，则Blue版本应继续使用其索引，直到其终止，而Green版本应使用其自己修改过的索引集。 开发人员应遵循本文](/help/operations/indexing.md)中描述的索引管理技术。[

### 回滚的保守编码{#conservative-coding-for-rollbacks}

如果在部署后报告或检测到故障，则可能需要回滚到蓝色版本。 最好确保蓝色代码与由绿色版本创建的任何新结构兼容，因为新结构（任何可变内容内容）不会回滚。 如果旧代码不兼容，则需要在后续客户版本中应用修复。

## 运行模式{#runmodes}

在现有的AEM解决方案中，客户可以选择以任意运行模式运行实例，并将OSGI配置或将OSGI捆绑包安装到这些特定实例。 通常定义的运行模式包括&#x200B;*service*（作者和发布）和环境(dev、stage、prod)。

而AEM作为Cloud Service，则对哪些运行模式可用以及如何将OSGI捆绑包和OSGI配置映射到这些模式更加确信：

* OSGI配置运行模式必须引用dev、stage、prod for the 环境或author， publish for the service。 支持`<service>.<environment_type>`的组合，但必须按此特定顺序使用它们（例如`author.dev`或`publish.prod`）。 OSGI令牌应直接从代码中引用，而不是使用`getRunModes`方法，该方法在运行时将不再包括`environment_type`。 有关详细信息，请参阅[将AEM的OSGi配置为Cloud Service](/help/implementing/deploying/configuring-osgi.md)。
* OSGI捆绑包运行模式仅限于服务（作者、发布）。 每运行模式OSGI包应安装在`install/author`或`install/publish`下的内容包中。

与现有的AEM解决方案一样，无法使用运行模式仅为特定环境或服务安装内容。 如果希望用未在舞台或生产中的数据或HTML为开发环境植入种子，则可以使用包管理器。

支持的运行模式配置有：

* **config** (*默认值，适用于所有AEM服务*)
* **config.author** (*适用于所有AEM作者服务*)
* **config.author.dev** (*适用于AEM Dev Author服务*)
* **config.author.stage** (*适用于AEM Staging Author服务*)
* **config.author.prod** (*适用于AEM Production Author服务*)
* **config.publish** (*适用于AEM发布服务*)
* **config.publish.dev** (*适用于AEM Dev Publish服务*)
* **config.publish.stage** (*适用于AEM Staging Publish服务*)
* **config.publish.prod** (*适用于AEM Production Publish服务*)
* **config.dev** (*适用于AEM Dev服务)
* **config.stage** (*适用于AEM Staging服务)
* **config.prod** (*适用于AEM Production Services)

使用具有最匹配运行模式的OSGI配置。

在本地开发时，可以传入运行模式启动参数，以指示将使用哪种运行模式OSGI配置。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## Source Control {#maintenance-tasks-configuration-in-source-control}中的维护任务配置

维护任务配置必须在源代码控制中保留，因为云环境中将不再提供&#x200B;**工具>操作**&#x200B;屏幕。 这样做的好处是，确保有意地坚持改变，而不是反复适用，或许会被遗忘。 请参考[维护任务文章](/help/operations/maintenance.md)以了解详细信息。
