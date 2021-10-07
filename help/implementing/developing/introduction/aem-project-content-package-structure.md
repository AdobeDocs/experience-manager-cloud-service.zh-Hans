---
title: AEM 项目结构
description: 了解如何定义部署到Adobe Experience ManagerCloud Service的包结构。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '2880'
ht-degree: 12%

---

# AEM 项目结构

>[!TIP]
>
>熟悉基本的[AEM项目原型use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven插件](/help/implementing/developing/tools/maven-plugin.md)，因为本文基于这些学习和概念。

本文概述了Adobe Experience Manager Maven项目需要进行的更改，这些更改将通过确保AEM与可变和不可变内容的拆分保持一致，建立依赖关系以创建无冲突的确定性部署，并将它们打包为可部署的结构，从而实现as a Cloud Service兼容。

AEM应用程序部署必须由单个AEM包组成。 此包又应包含子包，子包包含应用程序正常运行所需的所有内容，包括代码、配置和任何支持的基线内容。

AEM 要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离，这意味着单个内容包&#x200B;**不能****同时**&#x200B;部署到存储库的 `/apps` 和到运行时可写区域（例如，`/content`、`/conf`、`/home` 或 `/apps` 以外的任何区域)。相反，应用程序必须将代码和内容分离到离散包中，以部署到 AEM 中。

本文档中概述的包结构与本地开发部署&#x200B;**和** AEM 云服务部署兼容。

>[!TIP]
>
>本文档中概述的配置由[AEM Project Maven Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 存储库的可变区域与不可变区域 {#mutable-vs-immutable}

`/apps` 和 `/libs`**被视为 AEM 中的不可变区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。**&#x200B;运行时对不可改变区域所做的任何更改尝试都将失败。

存储库中的其他所有内容：`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等。 是所有&#x200B;**可变**&#x200B;区域，这意味着可在运行时更改这些区域。

>[!WARNING]
>
>与以前版本的AEM一样，不应修改`/libs`。 只有AEM产品代码才能部署到`/libs`。

### Oak索引 {#oak-indexes}

Oak索引(`/oak:index`)由AEMas a Cloud Service部署过程专门管理。 这是因为Cloud Manager必须等待任何新索引部署完毕并完全重新编入索引后，才能切换到新代码图像。

因此，尽管Oak索引在运行时是可变的，但必须将其部署为代码，以便在安装任何可变包之前能够安装它们。 因此，`/oak:index`配置是代码包的一部分，而不是内容包[的一部分，如下文](#recommended-package-structure)所述。

>[!TIP]
>
>有关在AEMas a Cloud Service中索引的更多详细信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md)。

## 推荐的包结构 {#recommended-package-structure}

![Experience Manager项目包结构](assets/content-package-organization.png)

此图表概述了建议的项目结构和包部署工件。

推荐的应用程序部署结构如下：

### 代码包/ OSGi包

+ 将生成OSGi包Jar文件，并直接嵌入到所有项目中。

+ `ui.apps`包包含要部署的所有代码，并且仅部署到`/apps`。 `ui.apps`包的常见元素包括，但不限于：
   + [组件定义和](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hans) HTLscript
      + `/apps/my-app/components`
   + JavaScript和CSS（通过[客户端库](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) 覆盖  `/libs`
      + `/apps/cq`, `/apps/dam/`, 等.
   + 回退上下文感知配置
      + `/apps/settings`
   + ACL（权限）
      + `/apps`下任何路径的任何`rep:policy`
   + [预编译的捆绑脚本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

+ `ui.config`包包含所有[OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 包含特定于运行模式的OSGi配置定义的组织文件夹
      + `/apps/my-app/osgiconfig`
   + 通用OSGi配置文件夹，其中包含适用于所有目标AEMas a Cloud Service部署目标的默认OSGi配置
      + `/apps/my-app/osgiconfig/config`
   + 运行特定于模式的OSGi配置文件夹，其中包含应用于所有目标AEMas a Cloud Service部署目标的默认OSGi配置
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi配置脚本
      + [存储](#repo-init) 库炎是部署（可变）内容的推荐方法，从逻辑上讲，这些内容是AEM应用程序的一部分。Repo Init OSGi配置应位于如上所述的相应`config.<runmode>`文件夹中，并用于定义：
         + 基线内容结构
         + 用户
         + 服务用户
         + 组
         + ACL（权限）

>[!NOTE]
>
>必须将相同的代码部署到所有环境。 为确保在生产环境中也进行置信度验证，需要此功能。 有关更多信息，请参阅[Runmodes](/help/implementing/deploying/overview.md#runmodes)中的部分。


### 内容包

+ `ui.content`包包含所有内容和配置。 内容包包含`ui.apps`或`ui.config`包中未包含的所有节点定义，换言之，包含`/apps`或`/oak:index`中未包含的任何内容。 `ui.content`包的常见元素包括，但不限于：
   + 上下文感知配置
      + `/conf`
   + 必需且复杂的内容结构(即 内容构建基于并扩展到在存储库初始化中定义的基准内容结构之后。)
      + `/content`, `/content/dam`, 等.
   + 受管制的标记分类
      + `/content/cq:tags`
   + 旧版等节点（理想情况下，将这些节点迁移到非/等位置）
      + `/etc`

### 容器包

+ `all`包是一个容器包，它仅包含可部署的工件、OSGI包Jar文件、`ui.apps`、`ui.config`和`ui.content`包作为嵌入。 `all`包不得具有其自身的&#x200B;**任何内容或代码**，而是将所有部署委派到存储库的子包或OSGi包Jar文件。

   现在，使用Maven [FileVault Package Maven插件的嵌入式配置](#embeddeds)而不是`<subPackages>`配置来包含包。

   对于复杂的Experience Manager部署，可能需要在AEM中创建多个`ui.apps`、`ui.config`和`ui.content`项目/包，这些项目/包表示特定的站点或租户。 如果完成此操作，请确保在可变内容和不可变内容之间进行拆分，并且所需的内容包和OSGi包Jar文件将作为子包嵌入到`all`容器内容包中。

   例如，复杂的部署内容包结构可能如下所示：

   + `all` 内容包嵌入了以下包，以创建单个部署对象
      + `common.ui.apps` 部署站点A和 **** 站点B所需的代码
      + `site-a.core` 站点A所需的OSGi包Jar
      + `site-a.ui.apps` 部署站点A所需的代码
      + `site-a.ui.config` 部署站点A所需的OSGi配置
      + `site-a.ui.content` 部署站点A所需的内容和配置
      + `site-b.core` 站点B所需的OSGi包Jar
      + `site-b.ui.apps` 部署站点B所需的代码
      + `site-b.ui.config` 部署站点B所需的OSGi配置
      + `site-b.ui.content` 部署站点B所需的内容和配置

### 其他应用程序包{#extra-application-packages}

如果AEM部署使用了其他AEM项目（这些项目本身由其自己的代码和内容包组成），则应将其容器包嵌入项目的`all`包中。

例如，包含2个供应商AEM应用程序的AEM项目可能如下所示：

+ `all` 内容包嵌入了以下包，以创建单个部署对象
   + `core` AEM应用程序所需的OSGi包Jar
   + `ui.apps` 部署AEM应用程序所需的代码
   + `ui.config` 部署AEM应用程序所需的OSGi配置
   + `ui.content` 部署AEM应用程序所需的内容和配置
   + `vendor-x.all` 部署供应商X应用程序所需的所有内容（代码和内容）
   + `vendor-y.all` 部署供应商Y应用程序所需的所有内容（代码和内容）

## 包类型 {#package-types}

将使用其声明的包类型标记包。

+ 容器包必须将其`packageType`设置为`container`。 容器包不得直接包含OSGi包和OSGi配置，并且不允许使用[安装挂接](http://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代码（不可变）包必须将其`packageType`设置为`application`。
+ 内容（可变）包必须将其`packageType`设置为`content`。


有关更多信息，请参阅下面的[Apache Jackrabbit FileVault - Package Maven Plugin文档](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)和[FileVault Maven配置代码片段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-package-types)部分。

## 标记要由Adobe Cloud Manager部署的Adobe包 {#marking-packages-for-deployment-by-adoube-cloud-manager}

默认情况下，Adobe Cloud Manager 会收集由 Maven 内部版本生成的所有包，但是，由于容器 (`all`) 包是包含所有代码和内容包的单个部署对象，因此我们必须确保&#x200B;**仅**&#x200B;部署容器 (`all`) 包。要确保这一点，Maven 内部版本生成的其他包必须使用 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` 的 FileVault Content Package Maven Plug-In 配置进行标记。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#pom-xml-snippets)部分。

## Repo Init{#repo-init}

Repo Init提供了定义JCR结构的说明或脚本，这些结构从常见的节点结构（如文件夹树）到用户、服务用户、组和ACL定义。

Repo Init的主要优势在于它们具有执行其脚本定义的所有操作的隐式权限，并且可在部署生命周期的早期调用，以确保执行时间代码时存在所有必需的JCR结构。

虽然Repo Init脚本本身作为脚本在`ui.config`项目中存在，但它们可以而且应该用于定义以下可变结构：

+ 基线内容结构
+ 服务用户
+ 用户
+ 组
+ ACL

存储库初始化脚本存储为`RepositoryInitializer` OSGi工厂配置的`scripts`条目，因此可以通过运行模式隐式定位，从而允许AEM创作和AEM发布服务的存储库初始化脚本之间，甚至是环境（开发、暂存和生产）之间的差异。

存储库初始化OSGi配置最好以[`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)编写，因为它们支持多行，这对使用[`.cfg.json`定义OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)的最佳实践是一个例外。

请注意，在定义“用户”和“组”时，只有组被视为应用程序的一部分，并且应在此处定义其功能的组成部分。 组织用户和组仍应在AEM中在运行时进行定义；例如，如果自定义工作流将工作分配给指定的组，则应通过AEM应用程序中的Repo Init在中定义该组，但如果该组只是组织性的，如“Wendy&#39;s Team”和“Sean&#39;s Team”，则最好定义这些工作，并在AEM中运行时进行管理。

>[!TIP]
>
>在内联`scripts`字段中必须定义Repo Init脚本&#x200B;*，并且`references`配置将不起作用。*

[Apache Sling Repo Init文档](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)中提供了Repo Init脚本的完整词汇。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[Repo Init代码片段](#snippet-repo-init)部分。

## 存储库结构包 {#repository-structure-package}

代码包需要配置FileVault Maven插件的配置，以引用强制实施结构依赖关系正确性的`<repositoryStructurePackage>`（以确保一个代码包不会安装在另一个代码包上）。 您可以[为项目创建自己的存储库结构包](repository-structure-package.md)。

此操作&#x200B;**仅适用于**&#x200B;代码包，即任何标有 `<packageType>application</packageType>` 的包。

要了解如何为应用程序创建存储库结构包，请参阅[开发存储库结构包](repository-structure-package.md)。

请注意，内容包(`<packageType>content</packageType>`)**不**&#x200B;需要此存储库结构包。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-repository-structure-package)部分。

## 在容器包中嵌入子包{#embeddeds}

内容或代码包放置在特殊的“side-car”文件夹中，并且可以使用FileVault Maven插件的`<embeddeds>`配置，定位在AEM作者、AEM发布或两者上进行安装。 请注意，不应使用`<subPackages>`配置。

常见用例包括：

+ AEM创作用户和AEM发布用户之间的ACL/权限不同
+ 仅用于在AEM作者上支持活动的配置
+ 代码（如与后台系统的集成），仅在AEM作者上运行时才需要

![嵌入包](assets/embeddeds.png)

要定位AEM作者、AEM发布或两者兼有，请将以下格式将包嵌入到`all`容器包中的特殊文件夹位置：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

划分此文件夹结构：

+ 第1级文件夹&#x200B;**必须是** `/apps`。
+ 第2级文件夹表示文件夹名称后带有`-packages`的应用程序。 通常，所有子包都只嵌入一个第2级文件夹，但可以创建任意数量的第2级文件夹以最好地表示应用程序的逻辑结构：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >按照惯例，子包嵌入式文件夹的名称带有后缀 `-packages`。这样可确保部署代码和内容包&#x200B;**不会**&#x200B;部署到任何子包 `/apps/<app-name>/...` 的目标文件夹，否则将会导致破坏性的循环安装行为。

+ 第3级文件夹必须是
   `application`, `content` 或 `container`
   + `application`文件夹包含代码包
   + `content`文件夹包含内容包
   + `container`文件夹包含AEM应用程序可能包含的任何[额外应用程序包](#extra-application-packages)。
此文件夹名称对应于其包含的包的[包类型](#package-types)。
+ 第 4 级文件夹包含子包，且必须是以下包之一：
   + `install`，以在 AEM 作者&#x200B;**和** AEM 发布上安装
   + `install.author`，以&#x200B;**仅**&#x200B;在 AEM 作者上安装
   + `install.publish` 仅 **** 在AEM发布时安装请注意，仅和 `install.author` 受 `install.publish` 支持的目标。不支持其 **他运行模式** 。

例如，包含AEM作者和发布特定包的部署可能如下所示：

+ `all` 容器包嵌入以下包，以创建单个部署对象
   + `ui.apps` 嵌入到 `/apps/my-app-packages/application/install` 部署代码以同时将代码发布到AEM作者和AEM发布
   + `ui.apps.author` 嵌入到部 `/apps/my-app-packages/application/install.author` 署代码中，以仅将代码发布到AEM作者
   + `ui.content` 内嵌于 `/apps/my-app-packages/content/install` 将内容和配置部署到AEM作者和AEM发布
   + `ui.content.publish` 嵌入到中 `/apps/my-app-packages/content/install.publish` 部署内容和配置以仅发布AEM

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-embeddeds)部分。

### 容器包的过滤器定义 {#container-package-filter-definition}

由于在容器包中嵌入了代码和内容子包，因此必须将嵌入的目标路径添加到容器项目的`filter.xml`中，以确保在构建时将嵌入的包包含在容器包中。

只需为要部署的包含子包的任何2级文件夹添加`<filter root="/apps/<my-app>-packages"/>`条目。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-container-package-filters)部分。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包都必须通过[Adobe的公共Maven对象存储库](https://repo.adobe.com/nexus/content/groups/public/com/adobe/)或可访问的可引用的第三方Maven对象存储库来提供。

如果第三方包位于 **Adobe 的公共 Maven 对象存储库**，则 Adobe Cloud Manager 无需进一步配置即可解析对象。

如果第三方包位于&#x200B;**公共的第三方 Maven 对象存储库**，则必须在项目的 `pom.xml` 中注册此存储库，并将其嵌入到[以上所述](#embeddeds)的以下方法中。

应使用其`all`包作为项目容器(`all`)包中的容器来嵌入第三方应用程序/连接器。

添加Maven依赖项遵循标准的Maven实践，并且嵌入第三方工件（代码和内容包）如下所述：[以上](#embedding-3rd-party-packages)。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-3rd-party-maven-repositories)部分。

## `ui.content`包中`ui.apps`之间的包依赖关系 {#package-dependencies}

为确保正确安装软件包，建议建立软件包间依赖关系。

一般规则是包含可变内容(`ui.content`)的包，这些内容应依赖于支持可变内容渲染和使用的不可变代码(`ui.apps`)。

此常规规则的一个显着例外是，如果不可变代码包（`ui.apps`或任何其他）、__仅__&#x200B;包含OSGi包，则会出现此常规规则。 如果是，则任何AEM包都不应声明对它的依赖关系。 这是因为不可变代码包&#x200B;__仅__&#x200B;包含OSGi包的AEM包未在AEM包管理器中注册，因此，任何依赖于它的包都将具有不满足的依赖关系，且无法安装。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-package-dependencies)部分。

内容包依赖关系的常见模式包括：

### 简单部署包依赖项 {#simple-deployment-package-dependencies}

简单的用例会将`ui.content`可变内容包设置为依赖于`ui.apps`不可变代码包。

+ `all` 没有依赖项
   + `ui.apps` 没有依赖项
   + `ui.content` 取决于  `ui.apps`

### 复杂的部署包依赖项 {#complex-deploxment-package-dependencies}

复杂的部署会根据简单的情况进行扩展，并设置相应可变内容和不可变代码包之间的依赖关系。 根据需要，还可以在不可变代码包之间建立依赖关系。

+ `all` 没有依赖项
   + `common.ui.apps.common` 没有依赖项
   + `site-a.ui.apps` 取决于  `common.ui.apps`
   + `site-a.ui.content` 取决于  `site-a.ui.apps`
   + `site-b.ui.apps` 取决于  `common.ui.apps`
   + `site-b.ui.content` 取决于  `site-b.ui.apps`

## 本地开发和部署 {#local-development-and-deployment}

本文概述的项目结构和组织是完全兼容的&#x200B;**本地开发AEM实例。**

## POM XML片段 {#pom-xml-snippets}

以下是可添加到Maven项目的Maven `pom.xml`配置片段，以符合上述建议。

### 包类型 {#xml-package-types}

作为子包部署的代码和内容包必须声明&#x200B;**应用程序**&#x200B;或&#x200B;**内容**&#x200B;包类型,具体取决于它们包含的内容。

#### 容器包类型 {#container-package-types}

容器`all/pom.xml`项目&#x200B;**未**&#x200B;声明`<packageType>`。

#### 代码（不可变）包类型 {#immutable-package-types}

代码包必须将其`packageType`设置为`application`。

在`ui.apps/pom.xml`中，`filevault-package-maven-plugin`插件声明的`<packageType>application</packageType>`生成配置指令声明了其包类型。

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
        <name>my-app.ui.apps</name>
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

内容包必须将其`packageType`设置为`content`。

在`ui.content/pom.xml`中，`filevault-package-maven-plugin`插件声明的`<packageType>content</packageType>`构建配置指令声明了其包类型。

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
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 为AdobeCloud Manager部署标记包 {#cloud-manager-target}

在生成包的每个项目中，**除**&#x200B;容器 (`all`) 项目外，将 `<cloudManagerTarget>none</cloudManagerTarget>` 添加到 `filevault-package-maven-plugin` 插件声明的 `<properties>` 配置中，以确保 Adobe Cloud Manager **不**&#x200B;部署这些它们。容器(`all`)包应是通过Cloud Manager部署的单个包，Cloud Manager又嵌入所有必需的代码和内容包。

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

### Repo Init{#snippet-repo-init}

包含Repo Init脚本的Repo Init脚本是通过`scripts`属性在`RepositoryInitializer` OSGi工厂配置中定义的。 请注意，由于这些脚本是在OSGi配置中定义的，因此可以使用通常的`../config.<runmode>`文件夹语义，通过运行模式轻松确定其范围。

请注意，由于脚本通常是多行声明，因此在`.config`文件中定义脚本比基于JSON的`.cfg.json`格式更容易。

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

`scripts` OSGi属性包含由[Apache Sling的Repo Init语言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)定义的指令。

### 存储库结构包 {#xml-repository-structure-package}

在声明代码包(`<packageType>application</packageType>`)的`ui.apps/pom.xml`和任何其他`pom.xml`中，将以下存储库结构包配置添加到FileVault Maven插件。 您可以[为项目创建自己的存储库结构包](repository-structure-package.md)。

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

在`all/pom.xml`中，将以下`<embeddeds>`指令添加到`filevault-package-maven-plugin`插件声明中。 请记住，**不**&#x200B;使用`<subPackages>`配置，因为这将包括`/etc/packages`中的子包，而不是`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`中的子包。

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

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
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

### 容器包的过滤器定义 {#xml-container-package-filters}

在 `all` 项目的 `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) 中，**包括**&#x200B;要部署的任何包含子包的 `-packages` 文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

如果在嵌入式目标中使用多个`/apps/*-packages`，则必须在此处枚举所有这些目标。

### 第三方Maven存储库 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>添加更多Maven存储库可能会延长Maven内部版本生成时间，因为将检查其他Maven存储库是否存在依赖关系。

在Reactor项目的`pom.xml`中，添加任何必要的第三方公共Maven存储库指令。 完整的`<repository>`配置应可从第三方存储库提供程序中获取。

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

### `ui.content`包中`ui.apps`之间的包依赖关系 {#xml-package-dependencies}

在`ui.content/pom.xml`中，将以下`<dependencies>`指令添加到`filevault-package-maven-plugin`插件声明中。

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

在`all/pom.xml`中添加`maven-clean-plugin`插件，该插件将在Maven内部版本之前清理目标目录。

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

+ [使用Maven管理资源包](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault Content Package Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
