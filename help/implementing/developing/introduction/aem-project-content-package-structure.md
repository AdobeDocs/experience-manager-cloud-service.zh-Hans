---
title: AEM 项目结构
description: 了解如何定义包结构以部署到Adobe Experience ManagerCloud Service。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 4%

---

# AEM 项目结构

>[!TIP]
>
>熟悉基本的[AEM项目原型use](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven插件](/help/implementing/developing/tools/maven-plugin.md)，因为本文是在这些知识和概念的基础上进行构建的。

本文概述了Adobe Experience Manager Maven项目要与AEM as a Cloud Service兼容所需的更改，需要确保这些项目尊重可变和不可变内容的拆分。 此外，建立依赖关系以创建无冲突的确定性部署，并将它们打包到可部署结构中。

AEM应用程序部署必须由单个AEM包组成。 此包继而应包含子包，这些子包包含应用程序正常运行所需的所有内容，包括代码、配置和任何支持的基线内容。

AEM要求将&#x200B;**content**&#x200B;和&#x200B;**code**&#x200B;分开，这意味着单个内容包&#x200B;**不能**&#x200B;部署到存储库的&#x200B;**同时** `/apps`和运行时可写区域（例如，`/content`、`/conf`、`/home`或非`/apps`区域）。 相反，应用程序必须将代码和内容分离到离散包中，以部署到 AEM 中。

本文档中概述的包结构与本地开发部署&#x200B;**和** AEM 云服务部署兼容。

>[!TIP]
>
>本文档中概述的配置由[AEM项目Maven Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 存储库的可变与不可变区域 {#mutable-vs-immutable}

AEM的`/apps`和`/libs`区域被视为&#x200B;**不可变**，因为在AEM启动（即在运行时）后无法对其进行更改（创建、更新、删除）。 在运行时更改不可变区域的任何尝试都将失败。

存储库中的其他所有内容，`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等都是&#x200B;**可变的**&#x200B;区域，这意味着可在运行时更改这些区域。

>[!WARNING]
>
>与在AEM的早期版本中一样，不应修改`/libs`。 只有AEM产品代码可以部署到`/libs`。

### Oak索引 {#oak-indexes}

Oak索引(`/oak:index`)由AEM as a Cloud Service部署过程管理。 这是因为Cloud Manager必须等到部署任何新索引并完全重新索引后，才能切换到新代码图像。

因此，尽管Oak索引在运行时是可变的，但必须将其部署为代码，以便在安装任何可变包之前可以安装这些索引。 因此`/oak:index`配置是代码包的一部分，而不是内容包[的一部分，如下所述](#recommended-package-structure)。

>[!TIP]
>
>有关AEM as a Cloud Service中索引的更多详细信息，请参阅[内容搜索和索引](/help/operations/indexing.md)。

## 推荐的包结构 {#recommended-package-structure}

![Experience Manager的项目包结构](assets/content-package-organization.png)

此图概述了推荐的项目结构和包部署对象。

推荐的应用程序部署结构如下：

### 代码包/OSGi包

+ 将生成OSGi捆绑包Jar文件，并直接将其嵌入所有项目中。

+ `ui.apps`包包含要部署的所有代码，并且只部署到`/apps`。 `ui.apps`包的常见元素包括但不限于：
   + [组件定义和HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)脚本
      + `/apps/my-app/components`
   + JavaScript和CSS （通过[客户端库](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [叠加](/help/implementing/developing/introduction/overlays.md)/`/libs`
      + `/apps/cq`、`/apps/dam/`等。
   + 回退上下文感知配置
      + `/apps/settings`
   + ACL（权限）
      + `/apps`下的任何路径的任何`rep:policy`
   + [预编译的捆绑脚本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>必须将相同的代码部署到所有环境中。 此代码可确保某个置信度级别，以便暂存环境中的验证也处于生产状态。 有关详细信息，请参阅[运行模式](/help/implementing/deploying/overview.md#runmodes)部分。


### 内容包

+ `ui.content`包包含所有内容和配置。 内容包包含不在`ui.apps`或`ui.config`包中的所有节点定义，换言之，包含不在`/apps`或`/oak:index`中的所有节点定义。 `ui.content`包的常见元素包括但不限于：
   + 上下文感知配置
      + `/conf`
   + 必需的复杂内容结构（即基于并扩展过去在Repo Init中定义的基准内容结构的内容构建）。
      + `/content`、`/content/dam`等。
   + 受控制的标记分类
      + `/content/cq:tags`
   + 旧版etc节点（理想情况下，将这些节点迁移到非/etc位置）
      + `/etc`

### 容器包

+ `all`包是一个容器包，其中仅包含可部署的项目、OSGI捆绑Jar文件、`ui.apps`、`ui.config`和`ui.content`包作为嵌入。 `all`包不得具有&#x200B;**自己的任何内容或代码**，而是将所有部署委派到存储库的子包或OSGi捆绑包Jar文件。

  包现在使用Maven [FileVault Package Maven插件的嵌入配置](#embeddeds)而非`<subPackages>`配置包含。

  对于复杂的Experience Manager部署，可能需要在AEM中创建表示特定站点或租户的多个`ui.apps`、`ui.config`和`ui.content`项目/包。 如果完成了此方法，请确保遵循可变和不可变内容之间的拆分，并将所需的内容包和OSGi捆绑Jar文件作为子包嵌入到`all`容器内容包中。

  例如，复杂的部署内容包结构可能如下所示：

   + `all`内容包嵌入以下包，以创建单个部署构件
      + `common.ui.apps`部署&#x200B;**站点A和站点B均所需的代码**
      + 网站A所需的`site-a.core` OSGi包Jar
      + `site-a.ui.apps`部署站点A所需的代码
      + `site-a.ui.config`部署站点A所需的OSGi配置
      + `site-a.ui.content`部署站点A所需的内容和配置
      + 站点B所需的`site-b.core` OSGi包Jar
      + `site-b.ui.apps`部署站点B所需的代码
      + `site-b.ui.config`部署站点B所需的OSGi配置
      + `site-b.ui.content`部署站点B所需的内容和配置

+ `ui.config`包包含所有[OSGi配置](/help/implementing/deploying/configuring-osgi.md)：
   + 被视为代码并属于OSGi包，但不包含常规内容节点。 因此，它被标记为容器包装
   + 包含特定于运行模式的OSGi配置定义的组织文件夹
      + `/apps/my-app/osgiconfig`
   + 公共OSGi配置文件夹，其中包含适用于所有目标AEM as a Cloud Service部署目标的默认OSGi配置
      + `/apps/my-app/osgiconfig/config`
   + 运行特定于模式的OSGi配置文件夹，其中包含适用于所有目标AEM as a Cloud Service部署目标的默认OSGi配置
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi配置脚本
      + [Repo Init](#repo-init)是部署（可变）内容的推荐方法，这些内容在逻辑上是AEM应用程序的一部分。 Repo Init OSGi配置应放置在如上所述的相应`config.<runmode>`文件夹中，并用于定义：
         + 基线内容结构
         + 用户
         + 服务用户
         + 组
         + ACL（权限）

### 额外的应用程序包{#extra-application-packages}

如果AEM部署使用其他AEM项目（项目本身由自己的代码和内容包组成），则其容器包应嵌入到项目的`all`包中。

例如，包含两个供应商AEM应用程序的AEM项目可能如下所示：

+ `all`内容包嵌入以下包，以创建单个部署构件
   + AEM应用程序所需的`core` OSGi包Jar
   + `ui.apps`部署AEM应用程序所需的代码
   + `ui.config`部署AEM应用程序所需的OSGi配置
   + `ui.content`部署AEM应用程序所需的内容和配置
   + `vendor-x.all`部署供应商X应用程序所需的一切（代码和内容）
   + `vendor-y.all`部署供应商Y应用程序所需的一切（代码和内容）

## 包类型 {#package-types}

将为其声明的包类型标记包。 包类型有助于阐明包的用途和部署。

+ 容器包必须将其`packageType`设置为`container`。 容器包不得包含常规节点。 仅允许OSGi包、配置和子包。 AEM as a Cloud Service中的容器不允许使用[安装挂接](https://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代码（不可变）包必须将其`packageType`设置为`application`。
+ 内容（可变）包必须将其`packageType`设置为`content`。


有关详细信息，请参阅下面的[Apache Jackrabbit FileVault - Package Maven插件文档](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)、[Apache Jackrabbit包类型](https://jackrabbit.apache.org/filevault/packagetypes.html)和[FileVault Maven配置片段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-package-types)部分。

## 将包标记为通过AdobeCloud Manager进行部署 {#marking-packages-for-deployment-by-adoube-cloud-manager}

默认情况下，AdobeCloud Manager会收集由Maven内部版本生成的所有包。 但是，由于容器(`all`)包是包含所有代码和内容包的单个部署对象，因此您必须确保仅&#x200B;**部署**&#x200B;容器(`all`)包。 要确保这一点，Maven 内部版本生成的其他包必须使用 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` 的 FileVault Content Package Maven Plug-In 配置进行标记。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#pom-xml-snippets)部分。

## 存储库初始{#repo-init}

Repo Init提供定义JCR结构的说明或脚本，这些说明或脚本涵盖了公用节点结构（如文件夹树）以及用户、服务用户、组和ACL定义。

Repo Init的主要优势在于，它们具有执行由其脚本定义的所有操作的隐式权限。 而且，此类脚本会在部署生命周期的早期调用，以确保在运行代码时存在所有必需的JCR结构。

虽然Repo Init脚本本身作为脚本存在于`ui.config`项目中，但它们可以而且应该用于定义以下可变结构：

+ 基线内容结构
+ 服务用户
+ 用户
+ 组
+ ACL

Repo Init脚本存储为`RepositoryInitializer` OSGi工厂配置的`scripts`个条目。 因此，它们可以通过运行模式隐式定位，从而在AEM Author和AEM Publish Services的Repo Init脚本之间甚至环境之间（Dev、Stage和Prod）实现差异。

Repo Init OSGi配置最好采用[`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)编写，因为它们支持多行，这与使用[`.cfg.json`定义OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)的最佳实践不同。

在定义用户和组时，只有组被视为应用程序的一部分，并且是其功能的组成部分。 您仍然可以在AEM中在运行时定义“组织用户和组”。 例如，如果自定义工作流将工作分配给指定的组，请在AEM应用程序中通过Repo Init定义该组。 但是，如果分组仅是组织性的，例如“Wendy&#39;s Team”和“Sean&#39;s Team”，则最好在AEM中在运行时定义和管理这些组。

>[!TIP]
>
>存储库初始化脚本&#x200B;*必须*&#x200B;在内联`scripts`字段中定义，否则`references`配置不起作用。

[Apache Sling Repo Init文档](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)上提供了Repo Init脚本的完整词汇。

>[!TIP]
>
>有关完整代码片段，请参阅下面的[Repo Init代码片段](#snippet-repo-init)部分。

## 存储库结构包 {#repository-structure-package}

代码包需要配置FileVault Maven插件的配置以引用强制结构依赖关系正确性的`<repositoryStructurePackage>`（以确保一个代码包不会安装在另一个代码包上）。 您可以[为您的项目](repository-structure-package.md)创建自己的存储库结构包。

**仅代码包需要**，这意味着任何标有`<packageType>application</packageType>`的包。

要了解如何为应用程序创建存储库结构包，请参阅[开发存储库结构包](repository-structure-package.md)。

内容包(`<packageType>content</packageType>`) **不**&#x200B;需要此存储库结构包。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-repository-structure-package)部分。

## 在容器软件包中嵌入子包{#embeddeds}

内容或代码包将放置在一个特殊的“side-car”文件夹中，并可使用FileVault Maven插件的`<embeddeds>`配置定向到AEM author和/或AEM Publish上进行安装。 不要使用`<subPackages>`配置。

常见用例包括：

+ AEM作者用户和AEM发布用户之间的ACL/权限不同
+ 仅用于支持AEM创作活动的配置
+ 仅需要在AEM创作实例上运行的代码，例如与后台系统的集成

![嵌入包](assets/embeddeds.png)

要定位AEM创作、AEM发布或两者，包将嵌入到特殊文件夹位置的`all`容器包中，格式如下：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

划分此文件夹结构：

+ 第一级文件夹&#x200B;**必须为** `/apps`。
+ 第二级文件夹表示应用程序，该应用程序已将`-packages`后固定到文件夹名称。 通常，所有子包都嵌入在仅有一个第二级文件夹下，但可以创建任意数量的第二级文件夹以最好地表示应用程序的逻辑结构：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >按照惯例，子包嵌入式文件夹的名称带有后缀`-packages`。 此命名可确保部署代码和内容包&#x200B;**不是**&#x200B;部署任何子包`/apps/<app-name>/...`的目标文件夹，从而导致破坏性的循环安装行为。

+ 第三级文件夹必须为
  `application`、`content`或`container`
   + `application`文件夹包含代码包
   + `content`文件夹包含内容包
   + `container`文件夹包含AEM应用程序可能包含的任何[额外应用程序包](#extra-application-packages)。
此文件夹名称对应于它包含的[包类型](#package-types)。
+ 第4级文件夹包含子包，并且必须是以下包之一：
   + `install`，以便您同时在&#x200B;**上安装** AEM作者和AEM发布
   + `install.author`，以便在AEM作者上安装&#x200B;**only**
   + `install.publish`，以便在AEM发布上安装&#x200B;**only**
仅`install.author`和`install.publish`受支持的目标。 不支持其 **他运行模式** 。

例如，包含AEM创作和发布特定包的部署可能如下所示：

+ `all`容器包嵌入以下包，以创建单个部署对象
   + 嵌入到`/apps/my-app-packages/application/install`中的`ui.apps`将代码部署到AEM作者和AEM发布
   + 嵌入到`/apps/my-app-packages/application/install.author`中的`ui.apps.author`将代码仅部署到AEM作者
   + `/apps/my-app-packages/content/install`中嵌入的`ui.content`将内容和配置部署到AEM创作和AEM发布
   + `/apps/my-app-packages/content/install.publish`中嵌入的`ui.content.publish`将内容和配置仅部署到AEM发布

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-embeddeds)部分。

### 容器包的过滤器定义 {#container-package-filter-definition}

由于在容器包中嵌入了代码和内容子包，因此必须将嵌入的目标路径添加到容器项目的`filter.xml`中。 这样可以确保在构建容器包时将嵌入的包包含在容器包中。

只需为包含要部署的子包的任何第二级文件夹添加`<filter root="/apps/<my-app>-packages"/>`条目即可。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-container-package-filters)部分。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包必须可通过[Adobe的公共Maven对象存储库](https://repo1.maven.org/maven2/com/adobe/)或可访问的公共、可引用的第三方Maven对象存储库使用。

如果第三方包位于&#x200B;**Adobe的公共Maven对象存储库**&#x200B;中，则无需进一步配置即可AdobeCloud Manager以解决对象。

如果第三方包位于&#x200B;**公共第三方Maven对象存储库**&#x200B;中，则必须在该项目的`pom.xml`中注册此存储库，并将其嵌入到上面概述的方法[之后](#embeddeds)。

第三方应用程序/连接器应使用其`all`包作为项目容器(`all`)包中的容器进行嵌入。

添加Maven依赖项遵循标准Maven实践，嵌入第三方工件（代码和内容包）的步骤如上所述[](#embedding-3rd-party-packages)。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-3rd-party-maven-repositories)部分。

## `ui.content`包中`ui.apps`之间的包依赖关系 {#package-dependencies}

为确保正确安装包，建议建立包间依赖关系。

一般规则是包含可变内容的包(`ui.content`)应依赖于支持呈现和使用可变内容的不可变代码(`ui.apps`)。

此常规规则的显着例外是如果不可变代码包（`ui.apps`或任何其他包），__only__&#x200B;包含OSGi包。 如果是，则任何AEM包都不应声明其依赖项。 原因是&#x200B;__仅__&#x200B;包含OSGi捆绑包的不可变代码包未向AEM [包管理器](/help/implementing/developing/tools/package-manager.md)注册。 因此，任何依赖于它的AEM包都存在未满足的依赖关系，无法安装。

>[!TIP]
>
>有关完整的代码片段，请参阅下面的[POM XML代码片段](#xml-package-dependencies)部分。

内容包依赖项的常见模式包括：

### 简单部署包依赖关系 {#simple-deployment-package-dependencies}

简单用例将`ui.content`可变内容包设置为依赖于`ui.apps`不可变代码包。

+ `all`没有依赖项
   + `ui.apps`没有依赖项
   + `ui.content`依赖于`ui.apps`

### 复杂的部署包依赖关系 {#complex-deploxment-package-dependencies}

复杂的部署会根据简单的用例进行扩展，并设置相应可变内容和不可变代码包之间的依赖关系。 根据需要，还可以在不可变代码包之间建立依赖关系。

+ `all`没有依赖项
   + `common.ui.apps.common`没有依赖项
   + `site-a.ui.apps`依赖于`common.ui.apps`
   + `site-a.ui.content`依赖于`site-a.ui.apps`
   + `site-b.ui.apps`依赖于`common.ui.apps`
   + `site-b.ui.content`依赖于`site-b.ui.apps`

## 本地开发和部署 {#local-development-and-deployment}

本文中概述的项目结构和组织是&#x200B;**完全兼容的**&#x200B;本地开发AEM实例。

## POM XML片段 {#pom-xml-snippets}

以下是Maven `pom.xml`配置片段，可添加到Maven项目中以与上述建议保持一致。

### 包类型 {#xml-package-types}

作为子包部署的代码和内容包必须声明&#x200B;**应用程序**&#x200B;或&#x200B;**内容**&#x200B;的包类型，具体取决于它们包含的内容。

#### 容器包类型 {#container-package-types}

容器`all/pom.xml`项目&#x200B;**不**&#x200B;声明`<packageType>`。

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

在`ui.content/pom.xml`中，`filevault-package-maven-plugin`插件声明的`<packageType>content</packageType>`生成配置指令声明了其包类型。

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

### 将包标记为AdobeCloud Manager部署 {#cloud-manager-target}

在生成包的每个项目中，**除**&#x200B;容器 (`all`) 项目外，将 `<cloudManagerTarget>none</cloudManagerTarget>` 添加到 `filevault-package-maven-plugin` 插件声明的 `<properties>` 配置中，以确保 Adobe Cloud Manager **不**&#x200B;部署这些它们。容器(`all`)包应该是通过Cloud Manager部署的单个包，该包又嵌入了所有必需的代码和内容包。

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

### 存储库初始{#snippet-repo-init}

包含Repo Init脚本的Repo Init脚本是通过`scripts`属性在`RepositoryInitializer` OSGi工厂配置中定义的。 由于这些脚本是在OSGi配置中定义的，因此可以使用常用的`../config.<runmode>`文件夹语义通过运行模式轻松限定其作用域。

由于脚本通常是多行声明，因此在`.config`文件中定义脚本比基于JSON的`.cfg.json`格式更容易。

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

在`ui.apps/pom.xml`以及声明代码包(`<packageType>application</packageType>`)的任何其他`pom.xml`中，将以下存储库结构包配置添加到FileVault Maven插件。 您可以[为您的项目](repository-structure-package.md)创建自己的存储库结构包。

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

### 在容器软件包中嵌入子包 {#xml-embeddeds}

在`all/pom.xml`中，将以下`<embeddeds>`指令添加到`filevault-package-maven-plugin`插件声明。 请记住，**不要**&#x200B;使用`<subPackages>`配置。 原因是它包含`/etc/packages`中的子包，而不是`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

在`all`项目的`filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`)中，**包含**&#x200B;要部署的包含子包的任何`-packages`文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

如果在嵌入目标中使用多个`/apps/*-packages`，则必须在此处枚举所有这些。

### 第三方Maven存储库 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>添加更多Maven存储库可能会延长Maven构建时间，因为会检查其他Maven存储库的依赖项。

在Reactor项目的`pom.xml`中，添加任何必要的第三方公共Maven存储库指令。 完整的`<repository>`配置应该可以从第三方存储库提供程序中获得。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public Third-Party Repository</name>
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

在`ui.content/pom.xml`中，将以下`<dependencies>`指令添加到`filevault-package-maven-plugin`插件声明。

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

在`all/pom.xml`中，添加在Maven生成之前清理目标目录的`maven-clean-plugin`插件。

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

+ [使用Maven管理包](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault Content Package Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
