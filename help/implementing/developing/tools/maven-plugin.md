---
title: Adobe内容包Maven插件
description: 使用内容包Maven插件部署AEM应用程序
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ba4e2427873fc9f5d91ee4f520df01018000a4c7
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 6%

---

# Adobe内容包Maven插件 {#adobe-content-package-maven-plugin}

使用Adobe内容包Maven插件将包部署和管理任务集成到您的Maven项目中。

将已构建的包部署到AEM由Adobe内容包Maven插件执行，并且支持使用AEM正常执行的任务的自动化 [包管理器：](/help/implementing/developing/tools/package-manager.md)

* 从文件系统中的文件创建新包。
* 在AEM上安装和卸载包。
* 生成已在AEM上定义的包。
* 获取安装在AEM上的包列表。
* 从AEM中删除资源包。

本文档详细介绍了如何使用Maven管理这些任务。 但是，了解这一点也很重要 [如何构建AEM项目及其包。](#aem-project-structure)

>[!NOTE]
>
>包 **创建** 现在由 [Apache Jackrabbit FileVault Package Maven插件。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* 的 `content-package-maven-plugin` 不再支持从1.0.2版开始的打包。
>* 本文介绍 **部署** 构建的AEM包中的包由Adobe内容包Maven插件执行。


## 包和AEM项目结构 {#aem-project-structure}

AEM as a Cloud Service遵循由最新AEM项目原型实施的包管理和项目结构的最新最佳实践。

>[!TIP]
>
>有关更多详细信息，请参阅 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service文档中的文章，以及 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 文档。 AEM 6.5完全支持这两种方法。

## 获取内容包Maven插件 {#obtaining-the-content-package-maven-plugin}

插件可从 [Maven中央存储库。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 内容包Maven插件目标和参数

要使用内容包Maven插件，请在POM文件的生成元素中添加以下插件元素：

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

要启用Maven下载插件，请使用 [获取内容包Maven插件](#obtaining-the-content-package-maven-plugin) 部分。

## 内容包Maven插件的目标 {#goals-of-the-content-package-maven-plugin}

内容包插件提供的目标和目标参数在后面的部分中进行了描述。 “常用参数”部分中描述的参数可用于大多数目标。 适用于一个目标的参数在该目标的部分中进行了描述。

### 插件前缀 {#plugin-prefix}

插件前缀为 `content-package`. 如以下示例所示，使用此前缀从命令行执行目标：

```shell
mvn content-package:build
```

### 参数前缀 {#parameter-prefix}

除非另有说明，否则插件目标和参数将使用 `vault` 前缀，如以下示例中所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用AEM代理的目标使用Maven设置中找到的第一个有效代理配置。 如果未找到代理配置，则不使用代理。 请参阅 `useProxy` 参数 [常用参数](#common-parameters) 中。

### 常用参数 {#common-parameters}

下表中的参数对所有目标都是通用的，但如 **目标** 列。

| 名称 | 类型 | 必填 | 默认值 | 描述 | 目标 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值 `true` 在发生错误时导致生成失败。 值 `false` 会导致生成忽略错误。 | 除 `package` |
| `name` | `String` | `build`:是的， `install`:不， `rm`:是 | `build`:没有默认值， `install`:的值 `artifactId` Maven项目的属性 | 要执行操作的包的名称 | 除 `ls` |
| `password` | `String` | 是 | `admin` | 用于对AEM进行身份验证的密码 | 除 `package` |
| `serverId` | `String` | 否 | 用于检索用户名和密码以进行身份验证的服务器ID | 除 `package` |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM包管理器的HTTP服务API的URL | 除 `package` |
| `timeout` | `int` | 否 | `5` | 与包管理器服务通信的连接超时（以秒为单位） | 除 `package` |
| `useProxy` | `boolean` | 否 | `true` | 值 `true` 导致Maven使用找到的第一个活动代理配置来将请求代理到包管理器。 | 除 `package` |
| `userId` | `String` | 是 | `admin` | 要通过AEM进行身份验证的用户名 | 除 `package` |
| `verbose` | `boolean` | 否 | `false` | 启用或禁用详细日志记录 | 除 `package` |

### 构建 {#build}

生成已在AEM实例上定义的内容包。

>[!NOTE]
>
>无需在Maven项目中执行此目标。

#### 参数 {#parameters}

构建目标的所有参数均在 [常用参数](#common-parameters) 中。

### 安装 {#install}

在存储库中安装包。 执行此目标不需要Maven项目。 目标与 `install` Maven生成生命周期的阶段。

#### 参数 {#parameters-1}

除了以下参数之外，请参阅 [常用参数](#common-parameters) 中。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | 的值 `artifactId` Maven项目的属性 | 表单的字符串 `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 无 | 要安装的对象的ID |
| `groupId` | `String` | 否 | 无 | 的 `groupId` 要安装的物品 |
| `install` | `boolean` | 否 | `true` | 确定是否在上载包时自动解包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | 的值 `localRepository` 系统变量 | 始终使用插件配置作为系统属性时无法配置的本地Maven存储库 |
| `packageFile` | `java.io.File` | 否 | 为Maven项目定义的主对象 | 要安装的包文件的名称 |
| `packaging` | `String` | 否 | `zip` | 要安装的对象的包装类型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 的值 `remoteArtifactRepositories` 为Maven项目定义的属性 | 此值无法使用插件配置进行配置，必须在项目中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 为其配置插件的项目 | Maven项目，由于项目包含插件配置，因此它是隐式的 |
| `repositoryId` (POM)、 `repoID` （命令行） | `String` | 否 | `temp` | 从中检索对象的存储库的ID |
| `repositoryUrl` (POM)、 `repoURL` （命令行） | `String` | 否 | 无 | 从中检索对象的存储库的URL |
| 版本 | 字符串 | 否 | 无 | 要安装的项目的版本 |

### ls {#ls}

列出部署到的包 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-2}

ls目标的所有参数均在 [常用参数](#common-parameters) 中。

### rm {#rm}

从 [包管理器。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-3}

rm目标的所有参数均在 [常用参数](#common-parameters) 中。

### 卸载 {#uninstall}

卸载包。 包将保留在服务器上处于“未安装”状态。

#### 参数 {#parameters-4}

卸载目标的所有参数均在 [常用参数](#common-parameters) 中。

### 软件包 {#package}

创建内容包。 包目标的默认配置包括保存编译文件的目录的内容。 要执行包目标，需要完成编译生成阶段。 包目标将绑定到Maven内部版本生命周期的包阶段。

#### 参数 {#parameters-5}

除了以下参数之外，请参阅 `name` 参数 [常用参数](#common-parameters) 中。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 无 | 要使用的存档配置 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven内部版本的输出目录的值 | 包含要包含在包中的内容的目录 |
| `dependencies` | `java.util.List` | 否 | 无 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 无 |  |
| `embeddeds` | `java.util.List` | 否 | 无 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 值 `true` 在项目依赖关系中找不到嵌入的对象时，会导致生成失败。 值 `false` 会导致生成忽略此类错误。 |
| `filterSource` | `java.io.File` | 否 | 无 | 此参数定义一个文件，用于指定工作区过滤器的源。 在配置中指定并通过嵌入或子包插入的过滤器将与文件内容合并。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 无 | 此参数包含定义包内容的过滤器元素。 执行时，过滤器将包含在 `filter.xml` 文件。 请参阅 [使用过滤器](#using-filters) 部分。 |
| `finalName` | `java.lang.String` | 是 | 的 `finalName` 在Maven项目（构建阶段）中定义 | 生成的包ZIP文件的名称，不包含 `.zip` 文件扩展 |
| `group` | `java.lang.String` | 是 | 的 `groupID` 在Maven项目中定义 | 的 `groupId` 内容包的目标安装路径的一部分 |
| `outputDirectory` | `java.io.File` | 是 | Maven项目中定义的生成目录 | 保存内容包的本地目录 |
| `prefix` | `java.lang.String` | 否 | 无 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 无 | Maven项目 |
| `properties` | `java.util.Map` | 否 | 无 | 这些参数定义了可在 `properties.xml` 文件。 这些属性无法覆盖以下预定义属性： `group` (使用 `group` 参数), `name` (使用 `name` 参数), `version` (使用 `version` 参数), `description` （根据项目描述设置）、 `groupId` (`groupId` （Maven项目描述符）， `artifactId` (`artifactId` （Maven项目描述符）， `dependencies` (使用 `dependencies` 参数), `createdBy` ( `user.name` 系统属性), `created` （当前系统时间）， `requiresRoot` (使用 `requiresRoot` 参数), `packagePath` （自动从组和包名称生成） |
| `requiresRoot` | `boolean` | 是 | false | 定义包是否需要根。 这将成为 `requiresRoot` 属性 `properties.xml` 文件。 |
| `subPackages` | `java.util.List` | 否 | 无 |  |
| `version` | `java.lang.String` | 是 | Maven项目中定义的版本 | 内容包的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven项目（构建阶段）中定义的目录 | 包含要包含在包中的内容的目录 |

#### 使用过滤器 {#using-filters}

使用过滤器元素定义包内容。 过滤器会添加到 `workspaceFilter` 元素 `META-INF/vault/filter.xml` 文件。

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

的 `mode` 元素定义导入资源包时对存储库的影响。 可以使用以下值：

* **合并：** 将添加资源包中尚未包含在存储库中的内容。 包和存储库中的内容将保持不变。 不会从存储库中删除任何内容。
* **替换：** 包中不在存储库中的内容会添加到存储库。 存储库中的内容将替换为包中的匹配内容。 内容在包中不存在时，会从存储库中删除该内容。
* **更新：** 包中不在存储库中的内容会添加到存储库。 存储库中的内容将替换为包中的匹配内容。 现有内容将从存储库中删除。

当过滤器不包含时 `mode` 元素，默认值 `replace` 中，将使用。

### 帮助 {#help}

#### 参数 {#parameters-6}

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 确定是否显示每个目标的所有可设置属性 |
| `goal` | `String` | 否 | 无 | 此参数定义要显示帮助的目标名称。 如果未指定任何值，则会显示所有目标的帮助。 |
| `indentSize` | `int` | 否 | `2` | 用于每个级别缩进的空格数（如果定义，则必须为正数） |
| `lineLength` | `int` | 否 | `80` | 显示行的最大长度（如果定义，则必须为正） |

## 在包中包含缩略图图像或属性文件 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替换默认的包配置文件以自定义包属性。 例如，包含缩略图以区分 [包管理器。](/help/implementing/developing/tools/package-manager.md)

源文件可以位于文件系统中的任意位置。 在POM文件中，定义生成资源以将源文件复制到 `target/vault-work/META-INF` 以包含在包中。

以下POM代码会将文件添加到 `META-INF` 项目源的文件夹添加到包中：

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

以下POM代码仅向包添加缩略图图像。 缩略图必须命名 `thumbnail.png`，且必须位于 `META-INF/vault/definition` 文件夹。 在本例中，源文件位于 `/src/main/content/META-INF/vault/definition` 项目的文件夹：

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

最新的AEM项目原型为内部部署和AMS实施实施实施了最佳实践包结构，并建议用于所有AEM项目。

>[!TIP]
>
>有关更多详细信息，请参阅 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service文档中的文章，以及 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 文档。 AEM 6.5完全支持这两种方法。
