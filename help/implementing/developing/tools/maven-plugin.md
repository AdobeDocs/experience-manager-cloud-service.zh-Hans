---
title: Adobe内容包Maven插件
description: 使用内容包Maven插件部署AEM应用程序
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: a5eef46835e234bb47451693cf5fdcda66c5b26f
workflow-type: tm+mt
source-wordcount: '1842'
ht-degree: 6%

---

# Adobe内容包Maven插件 {#adobe-content-package-maven-plugin}

使用Adobe内容包Maven插件将包部署和管理任务集成到Maven项目中。

将构建的包部署到AEM由Adobe内容包Maven插件执行，并允许自动执行通常使用AEM执行的任务 [包管理器：](/help/implementing/developing/tools/package-manager.md)

* 从文件系统中的文件创建新包。
* 在AEM上安装并卸载包。
* 构建已在AEM上定义的包。
* 获取AEM上安装的软件包列表。
* 从AEM中删除包。

本文档详细介绍如何使用Maven管理这些任务。 但是，了解以下内容也很重要 [如何构建AEM项目及其包。](#aem-project-structure)

>[!NOTE]
>
>包 **创建** 现在归 [Apache Jackrabbit FileVault Package Maven插件。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* 此 `content-package-maven-plugin` 不再支持从1.0.2版打包。
>* 本文介绍 **部署** 将所构建的包打包到AEM的过程由Adobe内容包Maven插件执行。

## 包和AEM项目结构 {#aem-project-structure}

AEMas a Cloud Service遵循由最新的AEM项目原型实现的包管理和项目结构的最新最佳实践。

>[!TIP]
>
>欲知更多详情，请参见 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service文档中的文章以及 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans) 文档。 AEM 6.5完全支持这两种版本。

## 获取内容包Maven插件 {#obtaining-the-content-package-maven-plugin}

插件可从以下位置获取： [Maven中央存储库。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 内容包Maven插件目标和参数

要使用内容包Maven插件，请在POM文件的构建元素中添加以下插件元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

要使Maven能够下载插件，请使用 [获取内容包Maven插件](#obtaining-the-content-package-maven-plugin) 部分。

## 内容包Maven插件的目标 {#goals-of-the-content-package-maven-plugin}

内容包插件提供的目标和目标参数在以下部分中进行了描述。 “常用参数”部分中描述的参数可用于大多数目标。 适用于某个目标的参数在该目标的部分中进行了描述。

### 插件前缀 {#plugin-prefix}

插件前缀为 `content-package`. 使用该前缀可从命令行执行目标，如以下示例所示：

```shell
mvn content-package:build
```

### 参数前缀 {#parameter-prefix}

除非另有说明，否则插件目标和参数会使用 `vault` 前缀，如以下示例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用代理进行AEM的目标使用在Maven设置中找到的第一个有效代理配置。 如果未找到代理配置，则不使用代理。 请参阅 `useProxy` 中的参数 [常用参数](#common-parameters) 部分。

### 常用参数 {#common-parameters}

下表中的参数对所有目标都是通用的，除非在 **目标** 列。

| 名称 | 类型 | 必需 | 默认值 | 描述 | 目标 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值 `true` 出错时导致构建失败。 值 `false` 导致生成忽略该错误。 | 所有目标，但 `package` |
| `name` | `String` | `build`：是， `install`：否， `rm`：是 | `build`：无默认值， `install`：的值 `artifactId` Maven项目的属性 | 要执行操作的包的名称 | 所有目标，但 `ls` |
| `password` | `String` | 是 | `admin` | 用于通过AEM进行身份验证的密码 | 所有目标，但 `package` |
| `serverId` | `String` | 否 | 从中检索用于身份验证的用户名和密码的服务器ID | 所有目标，但 `package` |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM包管理器的HTTP服务API的URL | 所有目标，但 `package` |
| `timeout` | `int` | 否 | `5` | 用于与包管理器服务通信的连接超时（以秒为单位） | 所有目标，但 `package` |
| `useProxy` | `boolean` | 否 | `true` | 值 `true` 导致Maven使用找到的第一个活动代理配置，将请求代理到包管理器。 | 所有目标，但 `package` |
| `userId` | `String` | 是 | `admin` | 用于通过AEM进行身份验证的用户名 | 所有目标，但 `package` |
| `verbose` | `boolean` | 否 | `false` | 启用或禁用详细日志记录 | 所有目标，但 `package` |

### 生成 {#build}

构建已在AEM实例上定义的内容包。

>[!NOTE]
>
>此目标不需要在Maven项目中执行。

#### 参数 {#parameters}

有关构建目标的所有参数的说明，请参见 [常用参数](#common-parameters) 部分。

### 安装 {#install}

在存储库中安装包。 执行此目标不需要Maven项目。 目标已绑定到 `install` Maven构建生命周期的阶段。

#### 参数 {#parameters-1}

除了以下参数外，请参阅 [常用参数](#common-parameters) 部分。

| 名称 | 类型 | 必需 | 默认值 | 描述 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | 的值 `artifactId` Maven项目的属性 | 表单的字符串 `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 无 | 要安装的工件的ID |
| `groupId` | `String` | 否 | 无 | 此 `groupId` 要安装的工件的 |
| `install` | `boolean` | 否 | `true` | 确定在上传包时是否自动解压缩包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | 的值 `localRepository` 系统变量 | 无法使用插件配置配置的本地Maven存储库，因为始终使用系统属性 |
| `packageFile` | `java.io.File` | 否 | 为Maven项目定义的主要构件 | 要安装的包文件的名称 |
| `packaging` | `String` | 否 | `zip` | 要安装的工件的包装类型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 的值 `remoteArtifactRepositories` 为Maven项目定义的属性 | 无法使用插件配置配置来配置此值，必须在项目中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 为其配置插件的项目 | 隐式的Maven项目，因为该项目包含插件配置 |
| `repositoryId` (POM)， `repoID` （命令行） | `String` | 否 | `temp` | 从中检索工件的存储库ID |
| `repositoryUrl` (POM)， `repoURL` （命令行） | `String` | 否 | 无 | 从中检索工件的存储库URL |
| version | 字符串 | 否 | 无 | 要安装的工件的版本 |

### ls {#ls}

列出部署到的包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-2}

有关ls目标的所有参数的说明，请参见 [常用参数](#common-parameters) 部分。

### rm {#rm}

从删除包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-3}

rm目标的所有参数都在 [常用参数](#common-parameters) 部分。

### 卸载 {#uninstall}

卸载包。 软件包在服务器上保持未安装状态。

#### 参数 {#parameters-4}

有关卸载目标的所有参数的说明，请参见 [常用参数](#common-parameters) 部分。

### 包 {#package}

创建内容包。 程序包目标的默认配置包括保存编译文件的目录的内容。 程序包目标的执行要求编译构建阶段已完成。 包目标绑定到Maven构建生命周期的包阶段。

#### 参数 {#parameters-5}

除了以下参数外，请参阅 `name` 中的参数 [常用参数](#common-parameters) 部分。

| 名称 | 类型 | 必需 | 默认值 | 描述 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 无 | 要使用的存档配置 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven内部版本的输出目录的值 | 包含要包含在包中的内容的目录 |
| `dependencies` | `java.util.List` | 否 | 无 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 无 |  |
| `embeddeds` | `java.util.List` | 否 | 无 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 值 `true` 当在项目依赖关系中未找到嵌入工件时，会导致生成失败。 值 `false` 导致生成忽略此类错误。 |
| `filterSource` | `java.io.File` | 否 | 无 | 此参数定义一个文件，该文件指定工作区过滤器的源。 在配置中指定的过滤器并通过嵌入或子包注入，这些过滤器将与文件内容合并。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 无 | 此参数包含定义包内容的过滤器元素。 执行时，过滤器包含在 `filter.xml` 文件。 请参阅 [使用过滤器](#using-filters) 部分。 |
| `finalName` | `java.lang.String` | 是 | 此 `finalName` 在Maven项目中定义（构建阶段） | 生成的包ZIP文件的名称，不包含 `.zip` 文件扩展名 |
| `group` | `java.lang.String` | 是 | 此 `groupID` 在Maven项目中定义 | 此 `groupId` 生成的内容包的一部分，该内容包是内容包的目标安装路径的一部分 |
| `outputDirectory` | `java.io.File` | 是 | 在Maven项目中定义的生成目录 | 保存内容包的本地目录 |
| `prefix` | `java.lang.String` | 否 | 无 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 无 | Maven项目 |
| `properties` | `java.util.Map` | 否 | 无 | 这些参数定义了可在 `properties.xml` 文件。 这些属性无法覆盖以下预定义属性： `group` (使用 `group` 要设置的参数)， `name` (使用 `name` 要设置的参数)， `version` (使用 `version` 要设置的参数)， `description` （在项目描述中设置）， `groupId` (`groupId` Maven项目描述符)， `artifactId` (`artifactId` Maven项目描述符)， `dependencies` (使用 `dependencies` 要设置的参数)， `createdBy` (值 `user.name` 系统属性)， `created` （当前系统时间）、 `requiresRoot` (使用 `requiresRoot` 要设置的参数)， `packagePath` （自动从组和包名称生成） |
| `requiresRoot` | `boolean` | 是 | false | 定义包是否需要根。 成为 `requiresRoot` 的属性 `properties.xml` 文件。 |
| `subPackages` | `java.util.List` | 否 | 无 |  |
| `version` | `java.lang.String` | 是 | Maven项目中定义的版本 | 内容包的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven项目（构建阶段）中定义的目录 | 包含要包含在包中的内容的目录 |

#### 使用过滤器 {#using-filters}

使用filters元素定义资源包内容。 这些筛选器将添加到 `workspaceFilter` 中的元素 `META-INF/vault/filter.xml` 包的文件。

以下过滤器示例显示了要使用的XML结构：

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### 导入模式 {#import-mode}

此 `mode` 元素定义在导入包时，内容对存储库有何影响。 可以使用以下值：

* **合并：** 将添加存储库中尚未包含的包内容。 包和存储库中的内容保持不变。 不会从存储库中删除任何内容。
* **替换：** 包中不在存储库中的内容将添加到存储库中。 存储库中的内容替换为包中的匹配内容。 当内容在包中不存在时，将从存储库中删除该内容。
* **更新：** 包中不在存储库中的内容将添加到存储库中。 存储库中的内容替换为包中的匹配内容。

当过滤器不包含时 `mode` 元素，默认值 `replace` 已使用。

### 帮助 {#help}

#### 参数 {#parameters-6}

| 名称 | 类型 | 必需 | 默认值 | 描述 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 确定是否显示每个目标的所有可设置属性 |
| `goal` | `String` | 否 | 无 | 此参数定义要为其显示帮助的目标名称。 如果未指定值，则会显示所有目标的帮助。 |
| `indentSize` | `int` | 否 | `2` | 用于每个级别缩进的空格数（如果已定义，则必须为正） |
| `lineLength` | `int` | 否 | `80` | 显示线的最大长度（如果已定义，则必须为正数） |

## 在包中包含缩略图图像或属性文件 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替换默认软件包配置文件以自定义软件包属性。 例如，包含缩略图图像以区分中的包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

源文件可以位于文件系统中的任何位置。 在POM文件中，定义生成资源以将源文件复制到 `target/vault-work/META-INF` 以包含在包中。

以下POM代码将文件添加到 `META-INF` 包的项目源的文件夹：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

以下POM代码仅将缩略图图像添加到资源包。 必须命名缩略图图像 `thumbnail.png`，并且必须位于 `META-INF/vault/definition` 包的文件夹。 在此示例中，源文件位于 `/src/main/content/META-INF/vault/definition` 项目的文件夹：

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## 使用AEM项目原型生成AEM项目 {#using-archetypes}

最新的AEM项目原型为本地和AMS实施实施了最佳实践包结构，建议将其用于所有AEM项目。

>[!TIP]
>
>欲知更多详情，请参见 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service文档中的文章以及 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans) 文档。 AEM 6.5完全支持这两种版本。
