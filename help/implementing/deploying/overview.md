---
title: 作为云服务部署到AEM
description: '作为云服务部署到AEM '
translation-type: tm+mt
source-git-commit: de23de0b79e6b897a69bd18035d2e7fcd07104c5

---


# 作为云服务部署到AEM {#deploying-to-aem-as-a-cloud-service}

## 简介 {#introduction}

与AEM内部部署和托管服务解决方案相比，AEM中代码开发的基础知识与云服务类似。 开发人员编写代码并在本地测试它，然后将其作为云服务环境推送到远程AEM。 Cloud manager是Managed services的可选内容交付工具，是必需的。 现在，这是将代码作为云服务环境部署到AEM的唯一机制。

AEM版本的更新始终是一个单独的部署事件，与推送自定义代码无关。 另一种方式是，自定义代码版本应针对生产上的AEM版本进行测试，因为它将部署在顶部。 随后发生的AEM版本更新（与当前的Managed services相比，该更新会很频繁）会自动应用。 它们旨在向后兼容已部署的客户代码。

本文档的其余部分将介绍开发人员如何调整其实践，以便将AEM作为云服务的版本更新和客户更新与之结合使用。

>[!NOTE]
>建议具有现有代码库的客户完成 [AEM文档中所述的存储库重组练习](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/authoring/restructure.html)。


## AEM版本更新 {#version-updates}

了解AEM将经常更新（可能像每天更新一次一样频繁），并将重点放在错误修复和性能增强上，这一点非常重要。 更新将透明地进行，不会造成停机。 更新旨在向后兼容，这意味着您不必修改自定义代码。 事实上，AEM更新是客户代码部署中的独立事件。 AEM更新部署在您上次成功的代码推送之上，这意味着自上次推送到生产后提交的任何更改都将不会被部署。

>[!NOTE]
>
> 如果将自定义代码推送到暂存，然后您拒绝，则下一次AEM更新将删除这些更改，以反映上次成功发布的客户的git标签到生产。

将定期推出功能版本，其重点是功能添加和增强功能，与每日版本相比，这些功能和增强功能将对用户体验产生更大影响。 功能发布不是通过部署大型更改集来触发的，而是通过触发发布切换，激活在日常更新中累积的数天或数周的代码。

运行状况检查用于监控应用程序的运行状况。 如果在AEM作为云服务的更新期间这些检查失败，则该版本将不会针对该环境继续执行，Adobe将调查更新为何导致此意外行为。

### 复合节点存储 {#composite-node-store}

如上所述，在大多数情况下，更新将导致零停机，包括作者（即节点群集）。 由于Oak中的“复合节点存储”功能，可以进行滚动更新。 此功能允许AEM同时引用多个存储库。 在滚动部署中，新的绿色AEM版本包含其自己的 `/libs` （基于TarMK的不可变存储库），这与旧的蓝色AEM版本不同，但两者都引用了一个基于共享DocumentMK的可变存储库，其中包含 `/content`、 `/conf``/etc` 和其他区域。 由于蓝色和绿色都有其自己的版本，因此在滚动更新期间，它们都可以处于活动状态，并且在蓝色被绿色完全替换之前都会保持流量。 `/libs`

## 客户发行 {#customer-releases}

### 针对正确的AEM版本进行编码 {#coding-against-the-right-aem-version}

对于以前的AEM解决方案，最新的AEM版本更改频繁（大约每年一次，每季度提供服务包），客户可以自行将生产实例更新到最新的快速启动，并引用API Jar。 但是，AEM作为云服务应用程序会更频繁地自动更新至AEM的最新版本，因此内部发行版的自定义代码应针对那些较新的AEM界面构建。

与现有非云AEM版本一样，将支持基于特定快速入门的本地脱机开发，并且在大多数情况下，预计该开发工具是进行调试的首选工具。

> [!注意}
>与Adobe cloud相比，应用程序在本地计算机上的行为方式与Adobe cloud有细微的操作差异。 在本地开发过程中，这些架构差异必须得到尊重，并可能导致在云基础架构上部署时出现不同的行为。 由于这些差异，在生产中推出新的自定义代码之前，必须对开发环境和舞台环境执行完全测试。

以下是开发人员访问AEM对象相关版本的过程，我们将其称为AEM（即云服务SDK），这是为内部版本开发自定义代码所需的过程。 有关调度程序的信息，请 [参阅此页](/help/implementing/dispatcher/overview.md)。

## AEM作为云服务SDK {#aem-as-a-cloud-service-sdk}

AEM作为云服务SDK由以下对象组成：

* **快速入门Jar** —— 用于本地开发的AEM运行时
* **Java API Jar** - Java Jar/Maven依赖关系，它显示所有允许的Java API，这些API可用作云服务针对AEM进行开发。 以前称为Uberjar
* **Javadoc Jar** - Java API Jar的javadoc
* **Dispatcher Tools** —— 用于针对本地Dispatcher进行开发的工具集。 针对UNIX和Windows的单独对象

此外，某些先前已与AEM 6.5或更早版本一起部署的客户将使用以下对象。 如果本地编译不能与Quickstartjar一起使用，并且您怀疑是由于从作为云服务部署的AEM中删除的接口造成的，请联系客户支持以确定您是否需要访问。 这需要在后端进行更改。

* **6.5已弃用的Java API Jar** —— 自AEM 6.5以来已删除的另一组接口
* **6.5已弃用的Javadoc Jar** —— 用于附加的一组已接口的Javadoc

## 以云服务SDK形式访问AEM {#accessing-the-aem-as-a-cloud-service-sdk}

* 您可以检查AEM Admin Console的“关于 **Adobe Experience Manager** ”图标，以了解您正在生产中运行的AEM版本。
* 快速启动jar和调度程序工具可从软件分发门户下载为 [zip文件](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)。 请注意，对SDK列表的访问权限仅限于将AEM Managed services或AEM作为云服务环境的用户。
* Java API jar和Javadoc Jar可以通过各种工具（命令行或首选IDE）进行下载。
* 主项目窗格应引用以下API Jar包。 此依赖关系也应在任何子包中引用。

```
<dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>aem-sdk-api</artifactId>
  <version>2019.11.3006.20191108T223635Z-191201</version> 
  <scope>provided</scope>
</dependency>
```

> [!NOTE] SDK的版本条目应与AEM作为云服务的版本匹配。 登录AEM后，转到屏幕右上角的问号，然后选择“关于Adobe Experience Manager”，即可查看您使用的 **[!UICONTROL 版本。]**

* 托管包的主存储库的远程坐标应包含在pom文件中。

```
<repository>
    <id>adobe-aem-releases</id>
    <name>Adobe AEM Repository</name>
    <url>https://downloads.experiencecloud.adobe.com/content/maven/public</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

## 使用新的SDK版本刷新本地项目 {#refreshing-a-local-prokect-with-a-new-skd-version}

何时建议使用新SDK刷新本地项目？

建议至 *少在月度维护版* 本发布后对其进行刷新。

在任何日 *常维护版本发布* 后，都可以对其进行刷新。 客户的生产实例成功升级到新AEM版本后，将通知他们。 对于日常维护版本，新SDK预计不会发生重大更改（如果有）。 但是，建议偶尔使用最新的SDK刷新本地AEM开发人员环境，然后重新构建并测试自定义应用程序。 月度维护版本通常包含更多有影响的更改，因此开发人员应立即刷新、重建和测试。

下面是刷新本地环境的建议过程：

1. 确保任何有用的内容已提交到源控件中的项目，或在可变内容包中提供以供以后导入
1. 本地开发测试内容需要单独存储，以便不作为Cloud manager管道构建的一部分进行部署。 因为只要用于地方开发
1. 停止当前正在运行的快速启动
1. 将文件夹移 `crx-quickstart` 至其他文件夹以保持安全
1. 请注意Cloud manager中介绍的新AEM版本（此版本将用于标识要进一步下载的新QuickStart Jar版本）
1. 从软件分发门户下载其版本与生产AEM版本匹配的QuickStart JAR
1. 创建全新文件夹并放入新的QuickStart Jar
1. 使用所需的运行模式（重命名文件或通过在运行模式中传递）启动新的快速 `-r`启动。
   * 确保文件夹中没有旧快速入门的其余部分。
1. 构建AEM应用程序
1. 通过PackageManager将AEM应用程序部署到本地AEM
1. 通过PackageManager安装本地环境测试所需的任何可变内容包
1. 继续开发并根据需要部署更改

如果每个新AEM快速入门版本都应安装内容，请将其包含在内容包中，并包含在项目的源控件中。 然后，每次安装。

建议经常更新SDK（例如，每周两次），并每天处理完整的本地状态，以免意外依赖于应用程序中的状态数据。

如果您依赖CryptoSupport(通过[在AEM中配置Cloudservices的凭据或SMTP邮件服务，或通过在应用程序中使用CryptoSupport API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/crypto/CryptoSupport.html))，加密的属性将由在AEM环境的第一次启动时自动生成的密钥进行加密。 虽然云设置负责自动重用特定于环境的CryptoKey，但是必须将密钥注入到本地开发环境中。

默认情况下，AEM配置为将关键数据存储在文件夹的数据文件夹中，但为了便于在开发中重用，AEM进程可在首次启动时使用“`-Dcom.adobe.granite.crypto.file.disable=true`”初始化。 这将在“”处生成加密数`/etc/key`据。

要能够重复使用包含加密值的内容包，您需要执行以下步骤：

* 最初启动本地quickstart.jar时，请确保添加以下参数：“`-Dcom.adobe.granite.crypto.file.disable=true`”。 建议始终添加它（但是可选）。
* 第一次启动实例时，会创建一个包，其中包含根“”的过滤`/etc/key`器。 这将保留机密，以便在您希望重复使用它们的所有环境中重复使用
* 导出包含机密的任何可变内容，或通过查找加密值，将 `/crx/de` 其添加到将在安装过程中重用的包中
* 每当您启动新实例（要替换为新版本或多个开发环境应共享用于测试的凭据）时，请安装在步骤2和3中生成的包，以便无需手动重新配置即可重复使用内容。 这是因为，现在密钥保持同步。

## 通过Cloud manager和Package Manager部署内容包 {#deploying-content-packages-via-cloud-manager-and-package-manager}

### 通过Cloud manager进行部署 {#deployments-via-cloud-manager}

客户通过Cloud manager将自定义代码部署到云环境。 应该注意的是，Cloud manager将本地组合的内容包转换为符合Sling特征模型的伪像，即在云环境中运行时对AEM作为云服务应用程序的描述。 因此，在云环境中查看包管理器中的包时，名称将包括“cp2fm”，转换后的包将删除所有元数据。 它们不能与之交互，这意味着它们无法下载、复制或打开。 有关转换器的详细文档，请 [单击此处](https://github.com/apache/sling-org-apache-sling-feature-cpconverter)。

为AEM编写为云服务应用程序的内容包必须在不可变内容和可变内容之间有清晰的分隔，云管理器将通过失败构建来强制执行该内容，从而输出如下消息：

`Generated content-package <PACKAGE_ID> located in file <PATH> is of MIXED type`

本节的其余部分将描述不可变和可变包的组成和含义。

### 不可变的内容包 {#immutabe-content-packages}

必须将保留在不可变存储库中的所有内容和代码签入git并通过Cloud manager进行部署。 换句话说，与当前AEM解决方案不同，代码从不直接部署到正在运行的AEM实例。 这可确保在任何云环境中为给定版本运行的代码都相同，从而消除生产过程中无意发生代码变化的风险。 例如，OSGI配置应提交到源控件，而不是通过AEM web控制台的配置管理器在运行时进行管理。

由于交换机启用了蓝绿色部署模式导致的应用程序更改，因此这些更改不能取决于可变存储库中的更改，服务用户、其ACL、节点类型和索引定义更改除外。

对于具有现有代码库的客户，请务必完成AEM文档中所述的存储库重组练习，以确保将以前位于/etc下的内容移到正确的位置。

## OSGI配置 {#osgi-configuration}

如上所述，OSGI配置应提交到源控件，而不是通过Web控制台。 这样做的技术包括：

* 使用AEM web控制台的配置管理器对开发人员的本地AEM环境进行必要的更改，然后将结果导出到本地文件系统上的AEM项目
* 在本地文件系统上的AEM项目中手动创建OSGI配置，将引用AEM控制台的配置管理器以获取属性名称。

## 可变内容 {#mutable-content}

在某些情况下，在源控件中准备内容更改可能很有用，这样，只要更新了环境，Cloud Manager就可以部署它。 例如，为应用程序部署更新的组件植入某些根文件夹结构或在可编辑模板中排列更改可能是合理的。

有两种策略可描述Cloud manager将部署到可变存储库、可变内容包和重新指向语句的内容。

### 可变内容包 {#mutable-content-packages}

诸如文件夹路径层次结构、服务用户和访问控制(ACL)等内容通常会提交到基于主原型的AEM项目中。 技术包括从AEM导出或直接编写为XML。 在构建和部署过程中，Cloud manager会打包生成的可变内容包。 可变内容在管道的部署阶段以3个不同的时间安装：

在启动新版本的应用程序之前：

* 索引定义（添加、修改、删除）

在启动新版本的应用程序期间但在切换之前：

* 服务用户（添加）
* 服务用户ACL（添加）
* 节点类型（添加）

切换到新版本的应用程序后：

* 可通过jackrabbit保险库定义的所有其他内容。 例如：
   * 文件夹（添加、修改、删除）
   * 可编辑的模板（添加、修改、删除）
   * 上下文感知配置(下面的任 `/conf`何内容)（添加、修改、删除）
   * 脚本(包可以在包安装过程的各个阶段触发安装钩子

通过将包嵌入install.author或install.publish文件夹，可以将可变内容安装限制为创作或发布 `/apps`。 有关建议的项目重组的 [AEM文档](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/restructuring/repository-restructuring.html) ，请参阅详细信息。

>[!NOTE] 内容包部署到所有环境类型(dev、stage、prod)。 无法将部署限制到特定环境。 此限制旨在确保自动执行测试运行的选项。 特定于环境的内容需要通过包管理器手动安装。

此外，在应用可变内容包更改后，也没有回滚这些更改的机制。 如果客户检测到问题，他们可以选择在下一个代码版本中修复它，或者作为最后手段，在部署之前将整个系统恢复到某个时间点。

必须验证包含的任何第三方包是否与AEM兼容，否则其包含将导致部署失败。

如上所述，拥有现有代码库的客户应符合 [AEM文档中所述的存储库重组练习](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/repository-restructuring.html)。

## 重新指示 {#repoinit}

对于以下情况，最好在OSGI工厂配置中采用手工编码显式内容创建 `repoinit` 语句的方法：

* 创建／删除／禁用服务用户
* 创建／删除用户组
* 创建／删除用户
* 添加ACL
   > [!NOTE] 定义ACL要求节点结构已存在。 因此，可能需要在创建路径语句之前执行。
* 添加路径（例如，根文件夹结构）
* 添加CND（nodetype定义）

由于以下优点，对于这些支持的内容修改用例，重点说明是最好的：

* Repoinit在启动时创建资源，这样逻辑就可以认为这些资源的存在是理所当然的。 在可变内容包方法中，资源是在启动后创建的，因此依赖它们的应用程序代码可能会失败。
* 重新指示是相对安全的指令集，因为您显式控制要执行的操作。 此外，除了允许删除用户、服务用户和用户组的一些与安全相关的情况外，唯一支持的操作是附加的。 相反，删除可变内容包方法中的某些内容是明确的； 当您定义过滤器时，过滤器所涵盖的任何内容都将被删除。 但是，应当小心，因为任何内容都会出现新内容可能改变应用程序行为的情况。
* 重新指示可执行快速且原子化的操作。 相反，可变内容包可以高度取决于过滤器所覆盖的结构的性能。 即使更新单个节点，也可能会创建大树的快照。
* 可以在运行时在本地开发环境上验证重定向语句，因为这些语句将在注册OSGi配置时执行。
* 重新指示语句是原子和显式的，如果状态已匹配，则将跳过。

当Cloud manager部署应用程序时，它将执行这些语句，与任何内容包的安装无关。

要创建重新指示语句，请按照以下步骤操作：

1. 将OSGi配置添加到项 `org.apache.sling.jcr.repoinit.RepositoryInitializer` 目的配置文件夹中的PID
1. 将重新指向语句添加到配置的script属性。 语法和选项在 [Sling文档中有说明](https://sling.apache.org/documentation/bundles/repository-initialization.html)。 请注意，应在父级文件夹的子文件夹之前显式创建父级文件夹。 例如，在之前、之 `/content` 前显式 `/content/myfolder`创建 `/content/myfolder/mysubfolder`。 对于在低级结构上设置的ACL，建议将其设置在更高级别上并使用限 `rep:glob` 制。  For example `(allow jcr:read on /apps restriction(rep:glob,/msm/wcm/rolloutconfigs))`.
1. 在运行时在本地开发环境上验证。

<!-- last statement in step 2 to be clarified with Brian -->

>[!WARNING]
>
>对于为位于下方的节点定义的ACL `/apps` , `/libs` 或重新指示执行将在空白存储库上启动。 这些包在重新指向后安装，因此语句不能依赖于包中定义的任何内容，但必须定义先决条件，如下面的父结构。

>[!TIP]
>
>对于ACL，创建深层结构可能很麻烦，因此更合理地在更高级别上定义ACL并通过rep:glob限制限制其应采取的操作位置。

有关重点说明的更多详细信息，请参阅 [Sling文档](https://sling.apache.org/documentation/bundles/repository-initialization.html)

<!-- ### Packaging of Immutable and Mutable Packages {#packaging-of-immutable-and-mutable-packages}

above appears to be internal, to confirm with Brian -->

### 可移动内容包的包管理器“一次性” {#package-manager-oneoffs-for-mutable-content-packages}

在某些情况下，内容包应作为“一次性”安装。 例如，将特定内容从生产导入到暂存，以调试生产问题。 对于这些情况，包管理器可以在AEM中用作云服务环境。

由于包管理器是运行时的概念，因此无法将内容或代码安装到不可改变的存储库中，因此这些内容包只应由可变内容(主要或 `/content` 者 `/conf`)组成。 如果内容包中包含混合的内容（可变内容和不可变内容），则只会安装可变内容。

通过Cloud manager安装的任何内容包（可变和不可变）都将显示在AEM Package manager的用户界面中处于冻结状态。 无法重新安装、重新构建或甚至下载这些包，并将以“ **cp2fm”后缀列出** ，表明其安装由Cloud manager管理。

### 包括第三方包 {#including-third-party}

客户通常会包括来自第三方来源的预建包，如Adobe翻译合作伙伴等软件供应商。 建议将这些包托管在远程存储库中，并在中引用它们 `pom.xml`。 这仅适用于公共存储库。

如果无法将包存储在远程存储库中，客户可以将包放入基于本地文件系统的Maven存储库中，该存储库作为项目的一部分提交到SCM，并由依赖它的任何对象引用。 将在以下项目提示中声明存储库：


```
<repository>
    <id>project.local</id>
    <name>project</name>
    <url>file:${maven.multiModuleProjectDirectory}/repository</url>
</repository>
```

<!-- formatting appears broken in the code sample above, check how it appears on AEM -->

任何包含的第三方包都必须作为本文所述的云服务编码和打包准则遵守AEM，否则其包含将导致部署失败。

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

## 滚动部署的工作方式 {#how-rolling-deployments-work}

与AEM更新一样，客户版本也使用滚动部署策略进行部署，以便在适当的情况下消除作者群集停机。 事件的一般顺序如下所述，其中 **Blue** 是旧版本的客户代码， **Green** 是新版本。 蓝色和绿色都运行相同版本的AEM代码。

* 蓝色版本处于活动状态，并且已构建并提供绿色版的候选发行版
* 如果存在任何新的或更新的索引定义，则处理相应的索引。 请注意，蓝色部署将始终使用旧索引，而绿色部署将始终使用新索引。
* Green在启动，而Blue仍在使用
* 蓝色正在运行，并且正在通过运行状况检查检查绿色是否处于就绪状态
* 已准备好的绿色节点接受通信并替换已关闭的蓝色节点
* 随着时间的推移，蓝色节点被绿色节点替换，直到仅绿色节点保留，从而完成部署
* 已部署任何新的或修改的可变内容

## 索引 {#indexes}

新的或修改的索引将导致在新的（绿色）版本开始流量之前再执行一个索引或重新索引步骤。 有关Skyline中索引管理的详细信息，请参 [阅本文](/help/operations/indexing.md)。 您可以在Cloud manager构建页面上检查索引编制作业的状态，并在新版本可接收流量时收到通知。

>[!NOTE]
>
>滚动部署所需的时间因索引的大小而异，因为生成新索引之前，绿色版本不能接受流量。

目前，Skyline不使用索引管理工具，如ACS Commons Ensure Oak Index工具。

## 复制 {#replication}

发布机制向后兼容 [AEM Replication Java API](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/reference-materials/diff-previous/changes/com.day.cq.replication.Replicator.html)。

要使用云就绪型AEM快速启动开发和测试复制，需要将经典复制功能与作者／发布设置结合使用。 如果已为云删除AEM作者上的UI入口点，则用户将转到进行 `http://localhost:4502/etc/replication` 配置。

## 滚动部署的向后兼容代码 {#backwards-compatible-code-for-rolling-deployments}

如上所述，AEM作为云服务的滚动部署策略意味着旧版和新版本可能同时运行。 因此，请小心代码更改，它们不向后兼容仍在运行的旧AEM版本。

此外，应测试旧版本是否与新版本在回滚时应用的任何新的可变内容结构兼容，因为不会删除可变内容。

### 服务用户和ACL更改 {#service-users-and-acl-changes}

更改访问内容或代码所需的服务用户或ACL可能导致旧版AEM中的错误，从而导致使用过时的服务用户访问该内容或代码。 为了解决这一行为，建议在至少2个版本之间进行更改，第一个版本在后续版本中清理之前充当桥接器。

### 索引更改 {#index-changes}

如果对索引进行了更改，则Blue版本应继续使用其索引，直到它终止，而Green版本应使用其自己修改过的索引集。 开发人员应遵循本文所述的索引 [管理技术](/help/operations/indexing.md)。

### 回退的保守编码 {#conservative-coding-for-rollbacks}

如果在部署后报告或检测到故障，则可能需要回滚到Blue版本。 最好确保蓝色代码与绿色版本创建的任何新结构兼容，因为新结构（任何可变内容内容内容）不会回滚。 如果旧代码不兼容，则需要在后续客户版本中应用修复。

## 运行模式 {#runmodes}

在现有AEM解决方案中，客户可以选择以任意运行模式运行实例，并将OSGI配置或将OSGI捆绑包安装到这些特定实例。 通常定义的运行模式包括服 *务* （创作和发布）和环境(dev、stage、prod)。

另一方面，AEM作为云服务，对于哪些运行模式可用以及如何将OSGI捆绑包和OSGI配置映射到这些模式，则更加明确：

* OSGI配置运行模式必须引用dev、stage、prod for the environment或author, publish for the service。 支持组合 `<service>.<environment_type>` ，但必须按此特定顺序（例如author.dev或publish.prod）使用组合。 OSGI令牌应直接从代码中引用，而不是使用方 `getRunModes` 法，该方法将在运行时不再包 `environment_type` 含该令牌。
* OSGI捆绑包的运行模式仅限于服务（作者、发布）。 每运行模式OSGI包应安装在内容包中，位于或 `install/author` 下方 `install/publish`。

与现有AEM解决方案一样，无法使用运行模式仅为特定环境或服务安装内容。 如果希望为开发环境注入数据或不在舞台或生产上的HTML，则可以使用包管理器。

支持的运行模式配置有：

* **config** (*默认值，适用于所有AEM服务*)
* **config.author** (适&#x200B;*用于所有AEM作者服务*)
* **config.author.dev** (适&#x200B;*用于AEM dev作者服务*)
* **config.author.stage** (适&#x200B;*用于AEM Staging Author服务*)
* **config.author.prod** (*适用于AEM Production author服务*)
* **config.publish** (*适用于AEM发布服务*)
* **config.publish.dev** (适&#x200B;*用于AEM dev发布服务*)
* **config.publish.stage** (适&#x200B;*用于AEM Staging Publish服务*)
* **config.publish.prod** (*适用于AEM Production Publish服务*)
* **config.dev** （*适用于AEM dev服务）
* **config.stage** （*适用于AEM Staging服务）
* **config.prod** （*适用于AEM Production服务）

使用最匹配运行模式的OSGI配置。

在本地开发时，可以传递运行模式启动参数以指定将使用哪个运行模式OSGI配置。

<!-- ### Performance Monitoring {#performance-monitoring}

Developers want to ensure that their custom code is performing well. For Cloud environments, performance reports can be viewed on Cloud Manager. -->

## 源控制中的维护任务配置 {#maintenance-tasks-configuration-in-source-control}

维护任务配置必须在源控制中保留，因 **为“工具”** >“操作”屏幕在云环境中将不再可用。 这有利于确保有意持续而不是重新应用或遗忘更改。 请参阅维护 [任务文章](/help/operations/maintenance.md) ，以了解更多信息。
