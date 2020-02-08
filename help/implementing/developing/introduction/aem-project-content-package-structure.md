---
title: 了解项目的内容包结构
description: 了解如何正确定义部署到Adobe Experience Manager Cloud service的包结构。
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# 了解Adobe Experience Manager云服务中项目内容包的结构 {#understand-cloud-service-package-structure}

>[!TIP]
>
>熟悉基本的 [AEM Project Archetype使用](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)，以及 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Maven插件，因为本文构建于这些学习和概念之上。

本文概述了Adobe Experience Manager Maven项目为兼容AEM Cloud service所需的更改，具体方法是确保它们遵守可变内容和不可变内容的拆分；建立必要的依赖关系以创建不冲突的确定性部署；它们被装在一个可展开的结构里。

AEM应用程序部署必须由单个AEM包组成。 此包应包含子包，这些子包包含应用程序运行所需的所有功能，包括代码、配置和任何支持基准内容。

AEM要求将内 **容和代码分** 离 **，这意味着单个内容包不**&#x200B;能同时部 ********`/apps` 署到运行时可写区域(例如， `/content`、 `/conf`、 `/home`或其他非 `/apps`)。 相反，应用程序必须将代码和内容分离到离散的包中，以部署到AEM中。

本文档中概述的包结构与本地开 **发部署** 和AEM cloud服务部署兼容。

>[!TIP]
>
>本文档中概述的配置由 [AEM Project Maven Archetype 21或更高版本提供](https://github.com/adobe/aem-project-archetype/releases)。

## 存储库的可变区域与不可变区域 {#mutable-vs-immutable}

`/apps` 并且 `/libs` 由于AEM启 **动后** （即在运行时）无法更改（创建、更新、删除）AEM的不可变区域，因此它们会被视为AEM的不可变区域。 在运行时更改不可改变区域的任何尝试都将失败。

存储库中的其他所 `/content`有内 `/conf`容， `/var``/home`、 `/etc`、 `/oak:index`、 `/system`、 `/tmp`、等等。 都是可 **变的** ，这意味着它们可以在运行时更改。

>[!WARNING]
>
> 与AEM的先前版本一样， `/libs` 不应进行修改。 只有AEM产品代码可部署到 `/libs`。

## 推荐的包结构 {#recommended-package-structure}

![Experience Manager项目包结构](assets/content-package-organization.png)

此图概述了建议的项目结构和包部署对象。

建议的应用程序部署结构如下：

+ 该 `ui.apps` 包或内容包包含要部署的所有代码，并且仅部署到 `/apps`。 包的常见元 `ui.apps` 素包括但不限于：
   + OSGi捆绑
      + `/apps/my-app/install`
   + OSGi配置
      + `/apps/my-app/config`
   + HTL脚本
      + `/apps/my-app/components`
   + JavaScript和CSS（通过客户端库）
      + `/apps/my-app/clientlibs`
   + /libs的叠加
      + `/apps/cq`, `/apps/dam/`, 等.
   + 备份上下文感知配置
      + `/apps/settings`
   + ACL（权限）
      + 任意 `rep:policy` 路径位于 `/apps`
+ 该包 `ui.content` 或代码包包含所有内容和配置。 包的常见元 `ui.content` 素包括但不限于：
   + 上下文感知配置
      + `/conf`
   + 基线内容结构（资产文件夹、站点根页面）
      + `/content`, `/content/dam`, 等.
   + 受管制的标记分类
      + `/content/cq:tags`
   + 服务用户
      + `/home/users`
   + 用户组
      + `/home/groups`
   + Oak索引
      + `/oak:indexes`
   + 等等传统节点
      + `/etc`
   + ACL（权限）
      + 任何 `rep:policy` 路径的任何 **路径**`/apps`
+ 该包 `all` 是一个容器包，它仅包含作为嵌入 `ui.apps` 的和 `ui.content` 包。 该 `all` 包不得具有 **任何自己的内容** ，而是将所有部署委派到存储库的子包。

   包现在使用Maven [FileVault Package Maven插件的嵌入式配置](#embeddeds)，而不是配置 `<subPackages>` 包含。

   对于复杂的Experience manager部署，可能需要在AEM中创建多个 `ui.apps` 和项 `ui.content` 目／包，它们代表特定站点或租户。 如果这样做，则确保保留可变内容和不可变内容之间的拆分，并将所需的内容包添加为容器内容包中的 `all` 子包。

   例如，复杂的部署内容包结构可能如下：

   + `all` 内容包嵌入以下包，以创建单一部署对象
      + `ui.apps.common` 部署站点A和 **站点** B所需的代码
      + `ui.apps.site-a` 部署站点A所需的代码
      + `ui.content.site-a` 部署站点A所需的内容和配置
      + `ui.apps.site-b` 部署站点B所需的代码
      + `ui.content.site-b` 部署站点B所需的内容和配置

## 包类型 {#package-types}

包将用其声明的包类型进行标记。

+ 容器包不能有 `packageType` 集。
+ 代码（不可变）包必须将其 `packageType` 设置为 `application`。
+ 内容（可变）包必须将其设 `packageType` 置为 `content`。

有关详细信息，请参 [阅以下Apache Jackrabbit fileVault - Package Maven Plugin文档](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) ，以及 [FileVault Maven配置代码片段](#marking-packages-for-deployment-by-adoube-cloud-manager) 。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-package-types) POM XML代码片断部分。

## 标记要由Adobe Cloud manager部署的包 {#marking-packages-for-deployment-by-adoube-cloud-manager}

默认情况下，Adobe Cloud manager会收集由Maven内部版本生成的所有包，但是，由于容器(`all`)包是包含所有代码和内容包的单一部署对象，因此我们必须确保仅部署容器( ****`all`)包。 要确保这一点，Maven构建生成的其他包必须使用的FileVault内容包Maven插件配置进行标记 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#pom-xml-snippets) POM XML代码片断部分。

## 存储库结构包 {#repository-structure-package}

“代码包”要求将FileVault Maven插件的配置配置为引用一个强制结构依赖关系正确的插件（以确保一个代码包不会安装在另一个代码包上）。 `<repositoryStructurePackage>` 您可以 [为项目创建自己的存储库结构包](repository-structure-package.md)。

这仅是代 **码包必需的** ，即任何标有的包 `<packageType>application</packageType>`。

要了解如何为应用程序创建存储库结构包，请参阅 [开发存储库结构包](repository-structure-package.md)。

请注意，内容包(`<packageType>content</packageType>`)不 **需要** 此存储库结构包。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-repository-structure-package) POM XML代码片断部分。

## 在容器包中嵌入子包{#embeddeds}

内容或代码包放在特殊的“侧车”文件夹中，并可以使用FileVault Maven插件的配置在AEM作者或AEM发布中进行安装或同时在两者上进行安 `<embeddeds>` 装。 请注意， `<subPackages>` 不应使用该配置。

常见用例包括：

+ AEM作者用户与AEM发布用户之间的ACL/权限不同
+ 仅用于支持AEM作者上的活动的配置
+ 代码（如与后台系统集成），仅在AEM作者上运行

![嵌入包](assets/embeddeds.png)

要定位AEM作者、AEM发布或两者，该包将嵌入到容器包中的一个特殊文件夹位置，格式如下： `all`

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

将此文件夹结构细分：

+ 一级文件夹必 **须是**`/apps`。
+ 第2级文件夹表示文件夹名称后 `-packages` 修复的应用程序。 通常，只有一个2级文件夹所有子包都嵌入在下面，但是可以创建任意数量的2级文件夹以最好地表示应用程序的逻辑结构：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >按照惯例，子包嵌入式文件夹的名称带有后缀 `-packages`。 这可确保部署代码和内容包不 **会部署** ，而是部署到任何子包的目标文件夹，这会导致 `/apps/<app-name>/...` 破坏性的循环安装行为。

+ 3级文件夹必须是
   `application` 或 `content`
   + 文件 `application` 夹包含代码包
   + 文件 `content` 夹gelds内容包此文件夹名称必须与它包 [含的包的包](#package-types) 类型相对应。
+ 第4级文件夹包含子包，且必须是以下文件夹之一：
   + `install` 在AEM作者和AEM **发布** 上安装
   + `install.author` 仅 **安装** 在AEM作者上
   + `install.publish` to **only** install on AEM publish请注意，仅 `install.author` 和是受 `install.publish` 支持的目标。 不支持其 **他运行模式** 。

例如，包含AEM作者和发布特定包的部署可能如下所示：

+ `all` 容器包嵌入以下包，以创建单一部署伪像
   + `ui.apps` 嵌入到部 `/apps/my-app-packages/application/install` 署代码中，将代码同时发布到AEM作者和AEM发布
   + `ui.apps.author` 嵌入到部 `/apps/my-app-packages/application/install.author` 署代码中，仅可将代码嵌入到AEM作者
   + `ui.content` 已嵌入到将 `/apps/my-app-packages/content/install` 内容和配置部署到AEM作者和AEM发布中
   + `ui.content.publish` 嵌入到部 `/apps/my-app-packages/content/install.publish` 署内容和配置中，仅发布到AEM

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-embeddeds) POM XML代码片断部分。

### 容器包的过滤器定义 {#container-package-filter-definition}

由于在容器包中嵌入了代码和内容子包，因此必须将嵌入的目标路径添加到容器项目，以确保在构建时将嵌入的包包含在容器包中。 `filter.xml`

只需为包 `<filter root="/apps/<my-app>-packages"/>` 含要部署的子包的任何2级文件夹添加条目。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-container-package-filters) POM XML代码片断部分。

## 嵌入第三方包 {#embedding-3rd-party-packages}

所有包都必须通过 [Adobe的公共Maven对象存储库或可访问的公共](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) 、引用的第三方Maven对象存储库可用。

如果第三方包位于 **Adobe的公共Maven对象存储库中**，则Adobe Cloud Manager无需进一步配置即可解析对象。

如果第三方包位于公共的第 **三方Maven对象存储库中**，则必须按照上述方法将此存储库注册到项目 `pom.xml` 并嵌入 [其中](#embeddeds)。 如果第三方应用程序／连接器同时需要代码和内容包，则必须将每个代码包嵌入到容器(`all`)包中的正确位置。

添加Maven依赖项遵循标准的Maven惯例，并嵌入第三方对象（代码和内容包）如 [上所述](#embedding-3rd-party-packages)。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-3rd-party-maven-repositories) POM XML代码片断部分。

## 从包之间的包 `ui.apps` 依赖关 `ui.content` 系 {#package-dependencies}

为了确保正确安装包，建议建立包间依赖关系。

一般规则是包含可变内容(`ui.content`)的包，该可变内容(`ui.apps`)应取决于支持可变内容的呈现和使用的不可变内容()。

>[!TIP]
>
>有关完整 [的代码片断，请参见下面的](#xml-package-dependencies) POM XML代码片断部分。

内容包依赖关系的常见模式有：

### 简单的部署包依赖关系 {#simple-deployment-package-dependencies}

简单的案例将可变内 `ui.content` 容包设置为取决于不可变 `ui.apps` 的代码包。

+ `all` 没有依赖关系
   + `ui.apps` 没有依赖关系
   + `ui.content` 取决于 `ui.apps`

### 复杂的部署包依赖关系 {#complex-deploxment-package-dependencies}

复杂的部署会根据简单的情况进行扩展，并设置相应可变内容与不可变代码包之间的依赖关系。 根据需要，还可以在不可变的代码包之间建立依赖关系。

+ `all` 没有依赖关系
   + `ui.apps.common` 没有依赖关系
   + `ui.apps.site-a` 取决于 `ui.apps.common`
   + `ui.content.site-a` 取决于 `ui.apps.site-a`
   + `ui.apps.site-b` 取决于 `ui.apps.common`
   + `ui.content.site-b` 取决于 `ui.apps.site-b`

## 本地开发和部署 {#local-development-and-deployment}

本文中概述的项目结构和组织完全兼容 **本地开发** AEM实例。

## POM XML片段 {#pom-xml-snippets}

以下是Maven配置 `pom.xml` 片段，可添加到Maven项目以符合上述建议。

### 包类型 {#xml-package-types}

作为子包部署的代码和内容包必须声明应用程序或内容的包类 **型** , ****&#x200B;具体取决于它们包含的内容。

#### 容器包类型 {#container-package-types}

容器项 `all/pom.xml` 目 **不声明** (a) `<packageType>`。

#### 代码（不可变）包类型 {#immutable-package-types}

代码包必须将其设 `packageType` 置为 `application`。

在中， `ui.apps/pom.xml`插件声 `<packageType>application</packageType>` 明的构建配置指令 `filevault-package-maven-plugin` 声明其包类型。

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

内容包必须将其设 `packageType` 置为 `content`。

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

在生成包的每个项目中，除 **容器** (`all`)项目外， `<cloudManagerTarget>none</cloudManagerTarget>` 将插件声明的配置添加到该声明中，以确保Adobe Cloud `<properties>``filevault-package-maven-plugin`**** Manager不部署这些插件。 容器(`all`)包应是通过Cloud manager部署的单个包，Cloud manager又嵌入所有必需的代码和内容包。

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

### 存储库结构包 {#xml-repository-structure-package}

在声明 `ui.apps/pom.xml` 代码包()的 `pom.xml``<packageType>application</packageType>`和任何其他代码包中，将以下存储库结构包配置添加到FileVault Maven插件。 您可以 [为项目创建自己的存储库结构包](repository-structure-package.md)。

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
              <artifactId>repository-structure-pkg</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### 在容器包中嵌入子包 {#xml-embeddeds}

在中， `all/pom.xml`将以下指令添 `<embeddeds>` 加到插件 `filevault-package-maven-plugin` 声明中。 请记 **住** ，不要使 `<subPackages>` 用配置，因为这将包括子包，而 `/etc/packages` 不是 `/apps/my-app-packages/<application|content>/install(.author|.publish)?`。

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

在项目 `all` 的( `filter.xml` )中，包`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`含要部署的子 ****`-packages` 包的所有文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

如果在嵌 `/apps/*-packages` 入目标中使用多个，则必须在此处枚举所有这些目标。

### 第三方Maven存储库 {#xml-3rd-party-maven-repositories}

在反应堆项目中，添 `pom.xml`加任何必需的第三方公共Maven存储库指令。 完整配 `<repository>` 置应可从第三方存储库提供程序中访问。

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

### 从包之间的包 `ui.apps` 依赖关 `ui.content` 系 {#xml-package-dependencies}

在中， `ui.content/pom.xml`将以下指令添 `<dependencies>` 加到插件 `filevault-package-maven-plugin` 声明中。

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

在中添 `all/pom.xml` 加将在Maven `maven-clean-plugin` 构建之前清理目标目录的插件。

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
+ [FileVault Content Package Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
