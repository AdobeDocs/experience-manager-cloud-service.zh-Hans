---
title: AEM 项目结构
description: 了解如何定义部署到Adobe Experience ManagerCloud Service的包结构。
translation-type: tm+mt
source-git-commit: c2c6ee59849cbe041019e0a4395a499e81a671e0
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 17%

---


# AEM 项目结构

>[!TIP]
>
>熟悉基本的 [AEM Project Archetype使用](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，以及 [FileVault Content Maven插件，因为本文是在这些学习和概念的基础上构建的](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) 。

本文概述了将Maven项目Adobe Experience Manager为AEMCloud Service兼容所需的更改，具体方法是确保它们遵守可变内容和不可变内容的拆分； 建立必要的依赖关系以创建不冲突的确定性部署； 它们被装在一个可展开的结构里。

AEM应用程序部署必须由单个AEM包组成。 此包应包含子包，子包包含应用程序运行所需的一切，包括代码、配置和任何支持的基线内容。

AEM 要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离，这意味着单个内容包&#x200B;**不能****同时**&#x200B;部署到存储库的 `/apps` 和到运行时可写区域（例如，`/content`、`/conf`、`/home` 或 `/apps` 以外的任何区域)。相反，应用程序必须将代码和内容分离到离散包中，以部署到 AEM 中。

本文档中概述的包结构与本地开发部署&#x200B;**和** AEM 云服务部署兼容。

>[!TIP]
>
>本文档中概述的配置由AEM Project [Maven Archetype 21或更高版本提供](https://github.com/adobe/aem-project-archetype/releases)。

## 存储库的可变区与不可变区 {#mutable-vs-immutable}

`/apps` 和 `/libs` 被视为 AEM 中的&#x200B;**不可变**&#x200B;区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。运行时对不可改变区域所做的任何更改尝试都将失败。

存储库中的其 `/content`他 `/conf`所有内容 `/var`, `/etc`如 `/oak:index`、、 `/system`、 `/tmp`、、等等。 都是可 **变区** ，这意味着它们可以在运行时更改。

>[!WARNING]
>
> 与以前版本的AEM一样， `/libs` 不应进行修改。 只有AEM产品代码可部署到 `/libs`。

### Oak索引 {#oak-indexes}

Oak索引(`/oak:index`)由AEM Cloud服务部署流程进行专门管理。 这是因为Cloud Manager必须等到部署任何新索引并完全重新插入后才能切换到新代码映像。

因此，尽管Oak索引在运行时是可变的，但必须将其部署为代码，以便在安装任何可变包之前安装它们。 因 `/oak:index` 此，配置是代码包的一部分，而不是下面所述的内 [容包的一部分。](#recommended-package-structure)

>[!TIP]
>
>有关在AEM中作为Cloud Service建立索引的更多详细信息，请参阅 [文档内容搜索和索引。](/help/operations/indexing.md)

## 推荐的包结构 {#recommended-package-structure}

![Experience Manager项目包结构](assets/content-package-organization.png)

此图概述了建议的项目结构和包部署对象。

建议的应用程序部署结构如下：

+ 该 `ui.apps` 包或代码包包含要部署且仅部署到的所有代码 `/apps`。 软件包的常 `ui.apps` 见元素包括但不限于：
   + OSGi捆绑
      + `/apps/my-app/install`
   + [OSGi配置](/help/implementing/deploying/configuring-osgi.md)
      + `/apps/my-app/config`
   + [HTL脚本](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)
      + `/apps/my-app/components`
   + JavaScript和CSS（通过客户端库）
      + `/apps/my-app/clientlibs`
   + [/libs的](/help/implementing/developing/introduction/overlays.md) 叠加
      + `/apps/cq`, `/apps/dam/`, 等.
   + 回退上下文感知配置
      + `/apps/settings`
   + ACL（权限）
      + 任何 `rep:policy` 路径下的 `/apps`
   + 回购初始化OSGi配置指令（及随附的脚本）
      + [回购初始](#repo-init) (Repo Init)是部署（可变）内容（逻辑上属于AEM应用程序的一部分）的推荐方式。 回购初始化应用于定义：
         + 基线内容结构
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + 用户
         + 服务用户
         + 组
         + ACL（权限）
            + 任何 `rep:policy` 路径（可变或不可变）的任意
+ 该包 `ui.content` 或内容包包含所有内容和配置。 内容包包含包中不包含的 `ui.apps` 所有内容，换言之，不包含在或 `/apps` 中的任 `/oak:index`何 软件包的常 `ui.content` 见元素包括但不限于：
   + 上下文感知配置
      + `/conf`
   + 必需的、复杂的内容结构(即 在回购初始化中定义的基线内容结构的基础上构建并扩展的内容外部。
      + `/content`, `/content/dam`, 等.
   + 受管制的标记分类
      + `/content/cq:tags`
   + 等传统节点
      + `/etc`
+ `all` 包是一个“仅”包含 `ui.apps` 和 `ui.content` 包作为嵌入内容的容器包。`all` 包不得具有&#x200B;**任何自己的内容**，而是将所有部署委派到存储库的子包。

   现在，包是使用Maven FileVault包 [Maven插件的嵌入式配置](#embeddeds)，而不是使用配置 `<subPackages>` 提供的。

   对于复杂的Experience Manager部署，可能希望在AEM中创 `ui.apps` 建多 `ui.content` 个代表特定站点或租户的项目／包。 如果这样做，则确保可变内容和不可变内容之间的拆分得到遵守，并将所需的内容包添加为容器内容包 `all` 中的子包。

   例如，复杂的部署内容包结构可能如下：

   + `all` 内容包嵌入以下包，以创建单个部署对象
      + `ui.apps.common` 部署站点A **和站点** B所需的代码
      + `ui.apps.site-a` 部署站点A所需的代码
      + `ui.content.site-a` 部署站点A所需的内容和配置
      + `ui.apps.site-b` 部署站点B所需的代码
      + `ui.content.site-b` 部署站点B所需的内容和配置

## 包类型 {#package-types}

将用声明的包类型标记包。

+ 容器包不得具有 `packageType` 集。
+ 代码（不可变）包必须将其 `packageType` 设置为 `application`。
+ 内容（可变）包必须将其 `packageType` 设置为 `content`。

有关详细信息，请 [参阅Apache Jackrabbit FileVault - Package Maven Plugin文档](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) ，以 [及下面的FileVault Maven配置片段](#marking-packages-for-deployment-by-adoube-cloud-manager) 。

>[!TIP]
>
>有关完整 [的代码片断](#xml-package-types) ，请参见下面的POM XML代码片断部分。

## 标记要由Adobe Cloud Manager部署的包 {#marking-packages-for-deployment-by-adoube-cloud-manager}

默认情况下，Adobe Cloud Manager 会收集由 Maven 内部版本生成的所有包，但是，由于容器 (`all`) 包是包含所有代码和内容包的单个部署对象，因此我们必须确保&#x200B;**仅**&#x200B;部署容器 (`all`) 包。要确保这一点，Maven 内部版本生成的其他包必须使用 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` 的 FileVault Content Package Maven Plug-In 配置进行标记。

>[!TIP]
>
>有关完整 [的代码片断](#pom-xml-snippets) ，请参见下面的POM XML代码片断部分。

## 回购初始化{#repo-init}

回购初始化提供定义JCR结构的指令或脚本，这些结构从文件夹树等常见节点结构到用户、服务用户、组和ACL定义。

回购初始化的主要好处是它们具有执行其脚本定义的所有操作的隐式权限，并且在部署生命周期的早期被调用，确保执行时间代码时存在所有必需的JCR结构。

虽然回购初始化脚本本身作为 `ui.apps` 脚本存放在项目中，但它们可以而且应该用于定义以下可变结构：

+ 基线内容结构
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ 服务用户
+ 用户
+ 组
+ ACL

回购初始化脚本存储 `scripts` 为OSGi工厂 `RepositoryInitializer` 配置的条目，因此，可以通过运行模式隐式定位，允许AEM Author和AEM Publish服务的回购初始化脚本之间，甚至Env（开发、舞台和产品）之间的差异。

请注意，在定义“用户”和“组”时，只有组被视为应用程序的一部分，并且应在此处定义其功能的组成部分。 在AEM中，组织用户和用户组仍应在运行时进行定义； 例如，如果自定义工作流将工作分配给指定的组，则该组应通过AEM应用程序中的回购初始化进行定义，但是，如果分组只是组织形式（如“Wendy&#39;s Team”和“Sean&#39;s Team”），则这些工作流是在AEM中最佳定义并在运行时进行管理的。

>[!TIP]
>
>回购初始 *化脚本* 必须在内联字 `scripts` 段中定义，且 `references` 配置将无法工作。

Apache Sling Repo Init文档提供回购初始化脚本 [的完整词汇](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

>[!TIP]
>
>有关完整 [的代码片断](#snippet-repo-init) ，请参见下面的“回购初始化代码片断”部分。

## 存储库结构包 {#repository-structure-package}

代码包需要配置FileVault Maven插件的配置，以引 `<repositoryStructurePackage>` 用强制结构依赖关系正确性的配置（以确保一个代码包不安装在另一个代码包上）。 您可以 [为项目创建自己的存储库结构包](repository-structure-package.md)。

此操作&#x200B;**仅适用于**&#x200B;代码包，即任何标有 `<packageType>application</packageType>` 的包。

要了解如何为应用程序创建存储库结构包，请参 [阅开发存储库结构包](repository-structure-package.md)。

请注意，内容包(`<packageType>content</packageType>`) **不需要** 此存储库结构包。

>[!TIP]
>
>有关完整 [的代码片断](#xml-repository-structure-package) ，请参见下面的POM XML代码片断部分。

## 在容器包中嵌入子包{#embeddeds}

内容或代码包放在特殊的“侧车”文件夹中，并且可以定位为使用FileVault Maven插件配置在AEM作者或AEM发布上进行安 `<embeddeds>` 装。 请注意， `<subPackages>` 不应使用该配置。

常见用例包括：

+ AEM作者用户和AEM发布用户之间的ACL/权限不同
+ 仅用于支持AEM作者上的活动的配置
+ 代码（如与后台系统集成），仅在AEM作者上运行

![嵌入包](assets/embeddeds.png)

要目标AEM作者、AEM发布或两者，该包将嵌入到容器包中的一个特殊文件夹位置，格式如下： `all`

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

将此文件夹结构细分：

+ 第1级文件夹必 **须为**`/apps`。
+ 第2级文件夹表示文件夹名称 `-packages` 后缀为“后缀”的应用程序。 通常，只有一个2级文件夹所有子包都嵌入其中，但可以创建任意数量的2级文件夹以最好地表示应用程序的逻辑结构：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >按照惯例，子包嵌入式文件夹的名称带有后缀 `-packages`。这样可确保部署代码和内容包&#x200B;**不会**&#x200B;部署到任何子包 `/apps/<app-name>/...` 的目标文件夹，否则将会导致破坏性的循环安装行为。

+ 3级文件夹必须是
   `application` 或 `content`
   + 文件 `application` 夹包含代码包
   + 文件 `content` 夹包含内容包此文件夹名称必须与 [其包含](#package-types) 的包的包类型相对应。
+ 第 4 级文件夹包含子包，且必须是以下包之一：
   + `install`，以在 AEM 作者&#x200B;**和** AEM 发布上安装
   + `install.author`，以&#x200B;**仅**&#x200B;在 AEM 作者上安装
   + `install.publish` to **only** install on AEM publish注意 `install.author` , only and is supported `install.publish` 目标. 不支持其 **他运行模式** 。

例如，包含AEM作者和发布特定包的部署可能如下所示：

+ `all` 容器包嵌入以下包，以创建单一部署伪像
   + `ui.apps` 已嵌入 `/apps/my-app-packages/application/install` 到部署代码中，同时发布到AEM作者和AEM发布
   + `ui.apps.author` 嵌入到 `/apps/my-app-packages/application/install.author` 仅部署代码到AEM作者
   + `ui.content` 嵌入到 `/apps/my-app-packages/content/install` 将内容和配置同时部署到AEM作者和AEM发布
   + `ui.content.publish` 嵌入到 `/apps/my-app-packages/content/install.publish` 仅向AEM发布部署内容和配置

>[!TIP]
>
>有关完整 [的代码片断](#xml-embeddeds) ，请参见下面的POM XML代码片断部分。

### 容器包的过滤器定义 {#container-package-filter-definition}

由于容器包中嵌入了代码和内容子包，嵌入的目标路径必须添加到容器项目的包中，以 `filter.xml` 确保在构建时将嵌入的包包含在容器包中。

只需为包 `<filter root="/apps/<my-app>-packages"/>` 含要部署的子包的任何2级文件夹添加条目。

>[!TIP]
>
>有关完整 [的代码片断](#xml-container-package-filters) ，请参见下面的POM XML代码片断部分。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包都必须通过Adobe的 [公共Maven对象存储库或可访问的公共](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) 、可引用的第三方Maven对象存储库可用。

如果第三方包位于 **Adobe 的公共 Maven 对象存储库**，则 Adobe Cloud Manager 无需进一步配置即可解析对象。

如果第三方包位于&#x200B;**公共的第三方 Maven 对象存储库**，则必须在项目的 `pom.xml` 中注册此存储库，并将其嵌入到[以上所述](#embeddeds)的以下方法中。如果第三方应用程序/连接器同时需要代码和内容包，则必须将每个第三方应用程序/连接器嵌入到容器 (`all`) 包中的正确位置。

添加Maven依赖项遵循标准Maven惯例，并嵌入第三方对象（代码和内容包） [如上所述](#embedding-3rd-party-packages)。

>[!TIP]
>
>有关完整 [的代码片断](#xml-3rd-party-maven-repositories) ，请参见下面的POM XML代码片断部分。

## 来自包之间的 `ui.apps` 包依赖 `ui.content` 关系 {#package-dependencies}

为了确保正确安装软件包，建议建立软件包间依赖关系。

一般规则是包含可变内容(`ui.content`)的包，该可变内容()应取决于`ui.apps`支持可变内容的呈现和使用的不可变代码()。

此一般规则的一个显着例外是不可变的代码包(或`ui.apps` 任何其他代码包)仅 __包含__ OSGi包。 如果是，则任何AEM包都不应声明对它的依赖关系。 这是因为仅包含OSGi __包的不可__ 变代码包未在AEM包管理器中注册，因此，任何依赖于它的AEM包都将具有不满足的依赖关系，并且无法安装。

>[!TIP]
>
>有关完整 [的代码片断](#xml-package-dependencies) ，请参见下面的POM XML代码片断部分。

内容包依赖关系的常见模式有：

### 简单部署包依赖关系 {#simple-deployment-package-dependencies}

简单的案例将可变 `ui.content` 内容包设置为取决于不可变 `ui.apps` 的代码包。

+ `all` 没有依赖关系
   + `ui.apps` 没有依赖关系
   + `ui.content` 取决于 `ui.apps`

### 复杂部署包依赖关系 {#complex-deploxment-package-dependencies}

复杂的部署会根据简单情况进行扩展，并设置相应可变内容和不可变代码包之间的相关性。 根据需要，还可以在不可变的代码包之间建立依赖关系。

+ `all` 没有依赖关系
   + `ui.apps.common` 没有依赖关系
   + `ui.apps.site-a` 取决于 `ui.apps.common`
   + `ui.content.site-a` 取决于 `ui.apps.site-a`
   + `ui.apps.site-b` 取决于 `ui.apps.common`
   + `ui.content.site-b` 取决于 `ui.apps.site-b`

## 本地开发和部署 {#local-development-and-deployment}

本文中概述的项目结构和组织完全兼 **容本地** 开发AEM实例。

## POM XML片段 {#pom-xml-snippets}

以下是Maven配 `pom.xml` 置片段，可添加到Maven项目以符合上述建议。

### 包类型 {#xml-package-types}

作为子包部署的代码和内容包必须声明&#x200B;**应用程序**&#x200B;或&#x200B;**内容**&#x200B;包类型,具体取决于它们包含的内容。

#### 容器包类型 {#container-package-types}

容器 `all/pom.xml` 项 **目不声明** a `<packageType>`。

#### 代码（不可变）包类型 {#immutable-package-types}

代码包必须将其 `packageType` 设置为 `application`。

在中， `ui.apps/pom.xml`插件 `<packageType>application</packageType>` 声明的构建配置 `filevault-package-maven-plugin` 指令声明其包类型。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.apps}</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### 内容（可变）包类型 {#mutable-package-types}

内容包必须将其 `packageType` 设置为 `content`。

在中， `ui.content/pom.xml`插件声 `<packageType>content</packageType>` 明的构建配置指 `filevault-package-maven-plugin` 令声明其包类型。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.content}</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 标记Adobe Cloud Manager部署的包 {#cloud-manager-target}

在生成包的每个项目中，**除**&#x200B;容器 (`all`) 项目外，将 `<cloudManagerTarget>none</cloudManagerTarget>` 添加到 `filevault-package-maven-plugin` 插件声明的 `<properties>` 配置中，以确保 Adobe Cloud Manager **不**&#x200B;部署这些它们。The container (`all`) package should be the singular package deployed via Cloud Manager, which in turn embeds all required code and content packages.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 回购初始化{#snippet-repo-init}

包含回购初始化脚本的回购初始化脚本在OSGi工厂配 `RepositoryInitializer` 置中通过属性进行 `scripts` 定义。 请注意，由于这些脚本是在OSGi配置中定义的，因此运行模式可以使用通常的文件夹语义轻松 `../config.<runmode>` 地确定其范围。

请注意，由于脚本通常是多行声明，因此在文件中定义脚本比 `.config` 基于XML的格式更容 `sling:OsgiConfig` 易。

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

OSGi `scripts` 属性包含由Apache Sling的Repo [Init语言定义的指令](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)。

### 存储库结构包 {#xml-repository-structure-package}

在声明 `ui.apps/pom.xml` 代码包( `pom.xml` )的任何其他代码包中，将`<packageType>application</packageType>`以下存储库结构包配置添加到FileVault Maven插件。 您可以 [为项目创建自己的存储库结构包](repository-structure-package.md)。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### 在容器包中嵌入子包 {#xml-embeddeds}

在中， `all/pom.xml`将以下指令 `<embeddeds>` 添加到插件 `filevault-package-maven-plugin` 声明中。 请记 **住** ，不 `<subPackages>` 要使用配置，因为这将包括子包 `/etc/packages` 而不是 `/apps/my-app-packages/<application|content>/install(.author|.publish)?`。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### 容器包的过滤器定义 {#xml-container-package-filters}

在 `all` 项目的 `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) 中，**包括**&#x200B;要部署的任何包含子包的 `-packages` 文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

如果在嵌 `/apps/*-packages` 入目标中使用多个，则必须在此处枚举所有这些数据。

### 第三方Maven存储库 {#xml-3rd-party-maven-repositories}

>[!WARNING]
> 添加更多Maven存储库可能会延长大量构建时间，因为将检查其他Maven存储库是否具有相关性。

在反应堆项目中，添 `pom.xml`加任何必要的第三方公共Maven存储库指令。 完整配 `<repository>` 置应可从第三方存储库提供程序中使用。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### 来自包之间的 `ui.apps` 包依赖 `ui.content` 关系 {#xml-package-dependencies}

在中， `ui.content/pom.xml`将以下指令 `<dependencies>` 添加到插件 `filevault-package-maven-plugin` 声明中。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### 清除容器项目的目标文件夹 {#xml-clean-container-package}

在中 `all/pom.xml` 添加 `maven-clean-plugin` 将在Maven构建之前清除目标目录的插件。

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## 其他资源 {#additional-resources}

+ [使用Maven管理包](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [FileVault内容包Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)