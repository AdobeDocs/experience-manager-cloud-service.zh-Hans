---
title: AEM 项目结构
description: 了解如何定义部署到Adobe Experience Manager Cloud Service的包结构。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
translation-type: tm+mt
source-git-commit: ba5817714d46511c75ec2dd796b2ebd90adecb57
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 13%

---

# AEM 项目结构

>[!TIP]
>
>熟悉基本的[AEM Project Archetype use](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)和[FileVault Content Maven Plug-in](/help/implementing/developing/tools/maven-plugin.md)，因为本文构建于这些学习和概念之上。

本文概述了Adobe Experience Manager Maven项目作为Cloud Service兼容项所需的更改，具体方法是确保它们遵守可变内容和不可变内容的拆分，建立依赖关系以创建不冲突的确定性部署，并将它们打包在可部署结构中。

AEM应用程序部署必须由单个AEM包组成。 此包又应包含子包，子包包含应用程序运行所需的一切，包括代码、配置和任何支持基准内容。

AEM 要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离，这意味着单个内容包&#x200B;**不能****同时**&#x200B;部署到存储库的 `/apps` 和到运行时可写区域（例如，`/content`、`/conf`、`/home` 或 `/apps` 以外的任何区域)。相反，应用程序必须将代码和内容分离到离散包中，以部署到 AEM 中。

本文档中概述的包结构与本地开发部署&#x200B;**和** AEM 云服务部署兼容。

>[!TIP]
>
>本文档中概述的配置由[AEM Project Maven Archetype 24或更高版本](https://github.com/adobe/aem-project-archetype/releases)提供。

## 存储库{#mutable-vs-immutable}的可变区与不可变区

`/apps` 和 `/libs`**被视为 AEM 中的不可变区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。**&#x200B;运行时对不可改变区域所做的任何更改尝试都将失败。

存储库中的其他所有项，`/content`、`/conf`、`/var`、`/etc`、`/oak:index`、`/system`、`/tmp`等。 是所有&#x200B;**mutable**&#x200B;区域，这意味着它们可以在运行时进行更改。

>[!WARNING]
>
>与AEM的早期版本一样，`/libs`不应被修改。 只有AEM产品代码可以部署到`/libs`。

### Oak索引{#oak-indexes}

Oak索引(`/oak:index`)由AEM专门管理，作为Cloud Service部署过程。 这是因为Cloud Manager必须等到部署任何新索引并完全重新编制索引后才能切换到新代码映像。

因此，尽管Oak索引在运行时是可变的，但必须将其部署为代码，以便在安装任何可变的包之前安装它们。 因此，`/oak:index`配置是代码包的一部分，而不是内容包[的一部分，如下所述](#recommended-package-structure)。

>[!TIP]
>
>有关在AEM中作为Cloud Service建立索引的更多详细信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md)。

## 建议的包结构{#recommended-package-structure}

![Experience Manager项目包结构](assets/content-package-organization.png)

此图概述了建议的项目结构和包部署对象。

建议的应用程序部署结构如下：

### 代码包/OSGi包

+ 将生成OSGi bundle Jar文件，并直接嵌入到所有项目中。

+ `ui.apps`包包含要部署的所有代码，并且仅部署到`/apps`。 `ui.apps`包的常见元素包括但不限于：
   + [组件定义和](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) HTLscript
      + `/apps/my-app/components`
   + JavaScript和CSS（通过[客户端库](/help/implementing/developing/introduction/clientlibs.md)）
      + `/apps/my-app/clientlibs`
   + [叠](/help/implementing/developing/introduction/overlays.md) 加  `/libs`
      + `/apps/cq`, `/apps/dam/`, 等.
   + 回退上下文感知配置
      + `/apps/settings`
   + ACL（权限）
      + `/apps`下任何路径的任何`rep:policy`

+ `ui.config`包包含所有[OSGi配置](/help/implementing/deploying/configuring-osgi.md):
   + 包含特定于运行模式的OSGi配置定义的组织文件夹
      + `/apps/my-app/osgiconfig`
   + 公用OSGi配置文件夹，包含默认OSGi配置，这些配置作为Cloud Service部署目标应用于所有目标 AEM
      + `/apps/my-app/osgiconfig/config`
   + 运行特定于模式的OSGi配置文件夹，其中包含应用于所有目标 AEM的默认OSGi配置作为Cloud Service部署目标
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + 回购初始化OSGi配置脚本
      + [回购](#repo-init) 可变性是部署（可变）内容(逻辑上是AEM应用程序的一部分)的推荐方式。回购初始化OSGi配置应位于上述的相应`config.<runmode>`文件夹中，并用于定义：
         + 基线内容结构
         + 用户
         + 服务用户
         + 组
         + ACL（权限）

>[!NOTE]
>
>必须将同一代码部署到所有环境。 这是为了确保在生产中也对舞台环境进行一定程度的置信度验证所必需的。 有关详细信息，请参阅[Runmodes](/help/implementing/deploying/overview.md#runmodes)上的一节。


### 内容包

+ `ui.content`包包含所有内容和配置。 内容包中包含所有不在`ui.apps`或`ui.config`包中的节点定义，换言之，不在`/apps`或`/oak:index`中的任何内容。 `ui.content`包的常见元素包括但不限于：
   + 上下文感知配置
      + `/conf`
   + 必需的复杂内容结构(即 在回购初始化中定义的基线内容结构的基础上构建并扩展的内容外部。)
      + `/content`, `/content/dam`, 等.
   + 受管制的标记分类
      + `/content/cq:tags`
   + 旧式等节点（理想情况下，将这些节点迁移到非/等位置）
      + `/etc`

### 容器包

+ `all`包是一个容器包，它仅包含可部署的伪像、OSGI包Jar文件、`ui.apps`、`ui.config`和`ui.content`包作为嵌入。 `all`包不得具有自己的&#x200B;**任何内容或代码**，而是将所有部署委派到存储库的子包或OSGi捆绑Jar文件。

   现在，包是使用Maven [FileVault Package Maven插件的嵌入式配置](#embeddeds)而不是`<subPackages>`配置包含的。

   对于复杂的Experience Manager部署，可能需要创建多个`ui.apps`、`ui.config`和`ui.content`项目/包，它们代表AEM中的特定站点或租户。 如果这样做，请确保在可变内容和不可变内容之间进行拆分，并将所需的内容包和OSGi bundle Jar文件作为子包嵌入`all` 容器内容包中。

   例如，复杂的部署内容包结构可能如下所示：

   + `all` 内容包嵌入以下包，以创建单个部署伪像
      + `common.ui.apps` 部署站点A和 **** 站点B所需的代码
      + `site-a.core` 站点A需要的OSGi bundle Jar
      + `site-a.ui.apps` 部署站点A所需的代码
      + `site-a.ui.config` 部署站点A所需的OSGi配置
      + `site-a.ui.content` 部署站点A所需的内容和配置
      + `site-b.core` 站点B需要的OSGi bundle Jar
      + `site-b.ui.apps` 部署站点B所需的代码
      + `site-b.ui.config` 部署站点B所需的OSGi配置
      + `site-b.ui.content` 部署站点B所需的内容和配置

### 额外的应用程序包{#extra-application-packages}

如果AEM部署使用其他AEM项目（它们本身由自己的代码和内容包组成），则其容器包应嵌入项目的`all`包中。

例如，包含2个供应商AEM应用程序的AEM项目可能如下所示：

+ `all` 内容包嵌入以下包，以创建单个部署伪像
   + `core` AEM应用程序需要的OSGi bundle Jar
   + `ui.apps` 部署AEM应用程序所需的代码
   + `ui.config` 部署AEM应用程序所需的OSGi配置
   + `ui.content` 部署AEM应用程序所需的内容和配置
   + `vendor-x.all` 部署供应商X应用程序所需的一切（代码和内容）
   + `vendor-y.all` 部署供应商Y应用程序所需的一切（代码和内容）

## 包类型{#package-types}

包将用其声明的包类型进行标记。

+ 容器包必须将其`packageType`设置为`container`。 容器包不能直接包含OSGi包和OSGi配置，不允许使用[安装挂接](http://jackrabbit.apache.org/filevault/installhooks.html)。
+ 代码（不可变）包必须将其`packageType`设置为`application`。
+ 内容（可变）包必须将其`packageType`设置为`content`。


有关详细信息，请参阅下面的[Apache Jackrabbit FileVault - Package Maven Plugin文档](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)和[ FileVault Maven配置代码段](#marking-packages-for-deployment-by-adoube-cloud-manager)。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-package-types)部分。

## 通过Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}标记要部署的包

默认情况下，Adobe Cloud Manager 会收集由 Maven 内部版本生成的所有包，但是，由于容器 (`all`) 包是包含所有代码和内容包的单个部署对象，因此我们必须确保&#x200B;**仅**&#x200B;部署容器 (`all`) 包。要确保这一点，Maven 内部版本生成的其他包必须使用 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` 的 FileVault Content Package Maven Plug-In 配置进行标记。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#pom-xml-snippets)部分。

## 回购初始化{#repo-init}

回购初始化提供了定义JCR结构的指令（或脚本），这些结构从文件夹树等常见节点结构到用户、服务用户、组和ACL定义。

回购初始化的主要好处是，它们具有执行其脚本定义的所有操作的隐式权限，并在部署生命周期的早期被调用，以确保执行时间代码时存在所有必需的JCR结构。

虽然回购初始化脚本本身作为脚本存在于`ui.config`项目中，但它们可以而且应该用于定义以下可变结构：

+ 基线内容结构
+ 服务用户
+ 用户
+ 组
+ ACL

回购初始化脚本存储为`RepositoryInitializer` OSGi工厂配置的`scripts`条目，因此可以通过运行模式隐式定位，从而允许AEM作者和AEM发布服务的回购初始化脚本之间或甚至环境（开发、舞台和生产）之间的差异。

回购初始化OSGi配置最好以[`.config` OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1)编写，因为它们支持多行，这是使用[`.cfg.json`定义OSGi配置](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)的最佳实践的例外。

请注意，定义“用户”和“组”时，只有组被视为应用程序的一部分，并且应在此处定义其功能的组成部分。 组织用户和用户组在运行时仍应在AEM中定义；例如，如果自定义工作流将工作分配给指定的组，则该组应通过AEM应用程序中的回购初始化进行定义，但是，如果该组只是组织形式（如“Wendy&#39;s Team”和“Sean&#39;s Team”），则最好在AEM中定义并在运行时进行管理。

>[!TIP]
>
>回购初始化脚本&#x200B;*必须在内联`scripts`字段中定义*，且`references`配置将无法工作。

[Apache Sling Repo Init文档](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)中提供了回购初始化脚本的完整词汇。

>[!TIP]
>
>有关完整的片段，请参见下面的[回购初始化片段](#snippet-repo-init)部分。

## 存储库结构包{#repository-structure-package}

“代码包”要求配置FileVault Maven插件的配置以引用强制结构依赖关系正确性的`<repositoryStructurePackage>`（以确保一个代码包不会安装在另一个代码包上）。 您可以[为项目](repository-structure-package.md)创建您自己的存储库结构包。

此操作&#x200B;**仅适用于**&#x200B;代码包，即任何标有 `<packageType>application</packageType>` 的包。

要了解如何为应用程序创建存储库结构包，请参阅[开发存储库结构包](repository-structure-package.md)。

请注意，内容包(`<packageType>content</packageType>`)**不**&#x200B;需要此存储库结构包。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-repository-structure-package)部分。

## 在容器包中嵌入子包{#embeddeds}

内容或代码包放在特殊的“侧车”文件夹中，可以使用FileVault Maven插件的`<embeddeds>`配置在AEM作者或AEM发布或两者上进行安装。 请注意，不应使用`<subPackages>`配置。

常见用例包括：

+ AEM作者用户和AEM发布用户之间的ACL/权限不同
+ 仅用于支持AEM作者的活动的配置
+ 代码（如与后台系统集成）仅在AEM作者上运行

![嵌入包](assets/embeddeds.png)

要目标AEM作者、AEM发布或两者，将包嵌入到`all`容器包中的一个特殊文件夹位置，格式如下：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

划分此文件夹结构：

+ 第1级文件夹&#x200B;**必须为** `/apps`。
+ 第2级文件夹表示文件夹名称中具有`-packages`后置固定的应用程序。 通常，只有一个2级文件夹所有子包都嵌入其中，但可以创建任意数量的2级文件夹以最好地表示应用程序的逻辑结构：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >按照惯例，子包嵌入式文件夹的名称带有后缀 `-packages`。这样可确保部署代码和内容包&#x200B;**不会**&#x200B;部署到任何子包 `/apps/<app-name>/...` 的目标文件夹，否则将会导致破坏性的循环安装行为。

+ 第3级文件夹必须
   `application`、 `content` 或  `container`
   + `application`文件夹包含代码包
   + `content`文件夹包含内容包
   + `container`文件夹包含AEM应用程序可能包含的任何[其他应用程序包](#extra-application-packages)。
此文件夹名称对应于它包含的包的[包类型](#package-types)。
+ 第 4 级文件夹包含子包，且必须是以下包之一：
   + `install`，以在 AEM 作者&#x200B;**和** AEM 发布上安装
   + `install.author`，以&#x200B;**仅**&#x200B;在 AEM 作者上安装
   + `install.publish` to only  **** install on AEM publish注意，仅 `install.author` 支持 `install.publish` 和是支持目标。不支持其 **他运行模式** 。

例如，包含AEM作者和发布特定包的部署可能如下所示：

+ `all` 容器包嵌入以下包，以创建单一部署伪像
   + `ui.apps` 已嵌入 `/apps/my-app-packages/application/install` 到部署代码到AEM作者和AEM发布
   + `ui.apps.author` 嵌入到 `/apps/my-app-packages/application/install.author` 仅将代码嵌入到AEM作者
   + `ui.content` 嵌入到 `/apps/my-app-packages/content/install` 部署内容和配置到AEM作者和AEM发布
   + `ui.content.publish` 嵌入 `/apps/my-app-packages/content/install.publish` 到仅AEM发布中的部署内容和配置

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-embeddeds)部分。

### 容器包的筛选器定义{#container-package-filter-definition}

由于在容器包中嵌入了代码和内容子包，嵌入的目标路径必须添加到容器项目的`filter.xml`中，以确保在构建时将嵌入的包包含在容器包中。

只需为包含要部署的子包的任何2级文件夹添加`<filter root="/apps/<my-app>-packages"/>`条目。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-container-package-filters)部分。

## 嵌入第三方包{#embedding-3rd-party-packages}

所有包必须通过[Adobe的公共Maven对象存储库](https://repo.adobe.com/nexus/content/groups/public/com/adobe/)或可访问的可引用的第三方Maven对象存储库可用。

如果第三方包位于 **Adobe 的公共 Maven 对象存储库**，则 Adobe Cloud Manager 无需进一步配置即可解析对象。

如果第三方包位于&#x200B;**公共的第三方 Maven 对象存储库**，则必须在项目的 `pom.xml` 中注册此存储库，并将其嵌入到[以上所述](#embeddeds)的以下方法中。

应将第三方应用程序/连接器作为项目容器(`all`)包中的容器，使用其`all`包进行嵌入。

添加Maven依赖项遵循标准Maven惯例，嵌入第三方对象（代码和内容包）为[，如上所述](#embedding-3rd-party-packages)。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-3rd-party-maven-repositories)部分。

## `ui.content`包{#package-dependencies}中`ui.apps`之间的包依赖关系

为确保正确安装软件包，建议建立软件包间依赖关系。

一般规则是包含可变内容(`ui.content`)的包，这些内容应取决于支持可变内容的呈现和使用的不可变代码(`ui.apps`)。

此一般规则的一个显着例外是，如果不可变的代码包（`ui.apps`或任何其他代码包），__仅__&#x200B;包含OSGi包。 如果是，则任何AEM包都不应声明对它的依赖关系。 这是因为不可变的代码包&#x200B;__仅__&#x200B;包含OSGi包未在AEM包管理器中注册，因此，任何依赖于它的AEM包都将具有不满足的依赖关系，并且无法安装。

>[!TIP]
>
>有关完整的片段，请参阅下面的[POM XML代码片段](#xml-package-dependencies)部分。

内容包依赖关系的常见模式有：

### 简单部署包依赖项{#simple-deployment-package-dependencies}

简单的案例将`ui.content`可变内容包设置为取决于`ui.apps`不可变代码包。

+ `all` 没有依赖关系
   + `ui.apps` 没有依赖关系
   + `ui.content` 取决于  `ui.apps`

### 复杂部署包依赖项{#complex-deploxment-package-dependencies}

复杂的部署会根据简单情况进行扩展，并设置相应可变内容和不可变代码包之间的依赖关系。 根据需要，还可以在不可变的代码包之间建立依赖关系。

+ `all` 没有依赖关系
   + `common.ui.apps.common` 没有依赖关系
   + `site-a.ui.apps` 取决于  `common.ui.apps`
   + `site-a.ui.content` 取决于  `site-a.ui.apps`
   + `site-b.ui.apps` 取决于  `common.ui.apps`
   + `site-b.ui.content` 取决于  `site-b.ui.apps`

## 本地开发和部署{#local-development-and-deployment}

本文中概述的项目结构和组织是&#x200B;**完全兼容的**&#x200B;本地开发AEM实例。

## POM XML代码片段{#pom-xml-snippets}

以下是可添加到Maven项目以符合上述建议的Maven `pom.xml`配置片段。

### 包类型{#xml-package-types}

作为子包部署的代码和内容包必须声明&#x200B;**应用程序**&#x200B;或&#x200B;**内容**&#x200B;包类型,具体取决于它们包含的内容。

#### 容器包类型{#container-package-types}

容器`all/pom.xml`项目&#x200B;**不**&#x200B;声明`<packageType>`。

#### 代码（不可变）包类型{#immutable-package-types}

代码包必须将其`packageType`设置为`application`。

在`ui.apps/pom.xml`中，`filevault-package-maven-plugin`插件声明的`<packageType>application</packageType>`构建配置指令声明其包类型。

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

#### 内容（可变）包类型{#mutable-package-types}

内容包必须将其`packageType`设置为`content`。

在`ui.content/pom.xml`中，`filevault-package-maven-plugin`插件声明的`<packageType>content</packageType>`构建配置指令声明其包类型。

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

### 标记Adobe Cloud Manager部署的包{#cloud-manager-target}

在生成包的每个项目中，**除**&#x200B;容器 (`all`) 项目外，将 `<cloudManagerTarget>none</cloudManagerTarget>` 添加到 `filevault-package-maven-plugin` 插件声明的 `<properties>` 配置中，以确保 Adobe Cloud Manager **不**&#x200B;部署这些它们。容器(`all`)包应是通过Cloud Manager部署的单个包，而Cloud Manager又嵌入所有必需的代码和内容包。

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

包含回购初始化脚本的回购初始化脚本通过`scripts`属性在`RepositoryInitializer` OSGi工厂配置中定义。 请注意，由于这些脚本是在OSGi配置中定义的，因此可以使用通常的`../config.<runmode>`文件夹语义，通过运行模式轻松确定这些脚本的作用范围。

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

### 存储库结构包{#xml-repository-structure-package}

在`ui.apps/pom.xml`和声明代码包(`<packageType>application</packageType>`)的任何其他`pom.xml`中，将以下存储库结构包配置添加到FileVault Maven插件。 您可以[为项目](repository-structure-package.md)创建您自己的存储库结构包。

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

### 在容器包{#xml-embeddeds}中嵌入子包

在`all/pom.xml`中，将以下`<embeddeds>`指令添加到`filevault-package-maven-plugin`插件声明中。 请记住，**不要**&#x200B;使用`<subPackages>`配置，因为这将包括`/etc/packages`中的子包，而不是`/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`。

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

### 容器包的筛选器定义{#xml-container-package-filters}

在 `all` 项目的 `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) 中，**包括**&#x200B;要部署的任何包含子包的 `-packages` 文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

如果在嵌入目标中使用多个`/apps/*-packages`，则必须在此处枚举它们。

### 第3方Maven存储库{#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>添加更多Maven存储库可能会延长大量构建时间，因为将检查其他Maven存储库是否存在依赖关系。

在反应堆项目的`pom.xml`中，添加任何必要的第三方公共Maven存储库指令。 完全`<repository>`配置应可从第三方存储库提供程序中使用。

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

### `ui.content`包{#xml-package-dependencies}中`ui.apps`之间的包依赖关系

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

### 清理容器项目的目标文件夹{#xml-clean-container-package}

在`all/pom.xml`中，添加`maven-clean-plugin`插件，该插件将在Maven构建之前清理目标目录。

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
+ [FileVault内容包Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
