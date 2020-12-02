---
title: Adobe内容包Maven插件
description: 使用内容包Maven插件部署AEM应用程序
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 7%

---


# Adobe内容包Maven插件{#adobe-content-package-maven-plugin}

使用Adobe内容包Maven插件将包部署和管理任务集成到Maven项目中。

构建的包部署到AEM由Adobe内容包Maven插件执行，并支持通常使用AEM包管理器执行的任务的自动化：

* 从文件系统中的文件创建新包。
* 在AEM上安装和卸载包。
* 构建已在AEM上定义的包。
* 获取安装在AEM上的列表包。
* 从AEM中删除包。

此文档详细介绍如何使用Maven管理这些任务。 但是，了解[AEM项目及其包的结构方式也很重要。](#aem-project-structure)

>[!NOTE]
>
>包创建现在归[Apache Jackrabbit FileVault包Maven插件所有。 ](https://jackrabbit.apache.org/filevault-package-maven-plugin/)构建的包部署到AEM由Adobe内容包Maven插件执行，如此处所述。

## 包和AEM项目结构{#aem-project-structure}

AEM 6.5遵循最新的软件包管理和项目结构最佳实践，由最新的AEM Project Archetype在本地和AMS实施中实施。

>[!TIP]
>
>有关更多详细信息，请参阅AEM中的[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章作为Cloud Service文档以及[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)文档。 两者都完全支持AEM 6.5。

## 获取内容包Maven插件{#obtaining-the-content-package-maven-plugin}

该插件可从[Maven Central存储库访问。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 内容包Maven插件目标和参数

要使用内容包管理插件，请在POM文件的构建元素中添加以下插件元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

要启用Maven下载插件，请使用本页的[获取内容包Maven插件](#obtaining-the-content-package-maven-plugin)部分中提供的用户档案。

## 内容包Maven插件{#goals-of-the-content-package-maven-plugin}的目标

“内容包”插件提供的目标和目标参数在后面几节中有介绍。 “常用参数”部分中描述的参数可用于大多数目标。 适用于一个目标的参数在该目标的一节中进行了说明。

### 插件前缀{#plugin-prefix}

插件前缀为`content-package`。 使用此前缀从命令行执行目标，如下例所示：

```shell
mvn content-package:build
```

### 参数前缀{#parameter-prefix}

除非另有说明，否则插件目标和参数使用`vault`前缀，如下例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理{#proxies}

使用AEM代理的目标使用在Maven设置中找到的第一个有效代理配置。 如果未找到代理配置，则不使用代理。 请参见[ Common Parameters](#common-parameters)部分中的`useProxy`参数。

### 常见参数{#common-parameters}

下表中的参数对于所有目标都是通用的，但&#x200B;**目标**&#x200B;列中注明的除外。

| 名称 | 类型 | 必填 | 默认值 | 描述 | 目标 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 如果值`true`，则在出错时生成将失败。 值`false`会导致生成忽略错误。 | 除`package`之外的所有目标 |
| `name` | `String` | `build`:是， `install`:不， `rm`:是 | `build`:无默认值 `install`:Maven项目 `artifactId` 的属性值 | 要执行操作的包的名称 | 除`ls`之外的所有目标 |
| `password` | `String` | 是 | `admin` | 用于AEM身份验证的口令 | 除`package`之外的所有目标 |
| `serverId` | `String` | 否 | 要从中检索用户名和密码以进行身份验证的服务器ID | 除`package`之外的所有目标 |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM包管理器的HTTP服务API的URL | 除`package`之外的所有目标 |
| `timeout` | `int` | 否 | `5` | 与包管理器服务通信的连接超时（以秒为单位） | 除`package`之外的所有目标 |
| `useProxy` | `boolean` | 否 | `true` | 值`true`使Maven使用找到的第一个活动代理配置，以便向包管理器代理请求。 | 除`package`之外的所有目标 |
| `userId` | `String` | 是 | `admin` | 要与AEM进行身份验证的用户名 | 除`package`之外的所有目标 |
| `verbose` | `boolean` | 否 | `false` | 启用或禁用详细记录 | 除`package`之外的所有目标 |

### 构建{#build}

构建已在AEM实例上定义的内容包。

>[!NOTE]
>
>无需在Maven项目内执行此目标。

#### 参数 {#parameters}

构建目标的所有参数在[公用参数](#common-parameters)部分中均有介绍。

### 安装{#install}

在存储库中安装包。 执行此目标不需要Maven项目。 该目标将绑定到Maven构建生命周期的`install`阶段。

#### 参数 {#parameters-1}

除以下参数外，请参阅[Common Parameters](#common-parameters)部分中的说明。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|---|
| `artifact` | `String` | 否 | Maven项目的`artifactId`属性的值 | 形式`groupId:artifactId:version[:packaging]`的字符串 |
| `artifactId` | `String` | 否 | 无 | 要安装的对象的ID |
| `groupId` | `String` | 否 | 无 | 要安装的对象的`groupId` |
| `install` | `boolean` | 否 | `true` | 确定是否在上传包时自动解包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | `localRepository`系统变量的值 | 无法使用插件配置配置配置的本地Maven存储库，因为始终使用系统属性 |
| `packageFile` | `java.io.File` | 否 | 为Maven项目定义的主对象 | 要安装的包文件的名称 |
| `packaging` | `String` | 否 | `zip` | 要安装的对象的打包类型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 为Maven项目定义的`remoteArtifactRepositories`属性的值 | 此值不能使用插件配置进行配置，并且必须在项目中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 为其配置插件的项目 | 由于项目包含插件配置而隐含的Maven项目 |
| `repositoryId` (POM)、 `repoID` （命令行） | `String` | 否 | `temp` | 从中检索对象的存储库的ID |
| `repositoryUrl` (POM)、 `repoURL` （命令行） | `String` | 否 | 无 | 从中检索对象的存储库的URL |
| 版本 | 字符串 | 否 | 无 | 要安装的对象的版本 |

### ls {#ls}

列表部署到包管理器的包。

#### 参数 {#parameters-2}

ls目标的所有参数在[Common Parameters](#common-parameters)部分中均有介绍。

### rm {#rm}

从包管理器中删除包。

#### 参数 {#parameters-3}

[公用参数](#common-parameters)部分介绍了rm目标的所有参数。

### 卸载{#uninstall}

卸载包。 软件包将保留在已卸载状态的服务器上。

#### 参数 {#parameters-4}

卸载目标的所有参数都在[公用参数](#common-parameters)一节中进行了说明。

### 包{#package}

创建内容包。 包目标的默认配置包括保存已编译文件的目录的内容。 执行包目标需要编译构建阶段已完成。 包目标绑定到Maven构建生命周期的包阶段。

#### 参数 {#parameters-5}

除以下参数外，请参阅[ Common Parameters](#common-parameters)部分中`name`参数的说明。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 无 | 要使用的存档配置 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven内部版本的输出目录的值 | 包含要包含在包中的内容的目录 |
| `dependencies` | `java.util.List` | 否 | 无 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 无 |  |
| `embeddeds` | `java.util.List` | 否 | 无 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 如果值`true`在项目依赖关系中找不到嵌入的项目，则会导致生成失败。 值`false`会导致生成忽略此类错误。 |
| `filterSource` | `java.io.File` | 否 | 无 | 此参数定义一个指定工作区过滤器源的文件。 在配置中指定并通过嵌入式或子包注入的过滤器与文件内容合并。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 无 | 此参数包含定义包内容的筛选器元素。 执行过滤器时，这些数据将包含在`filter.xml`文件中。 请参阅下面的[使用过滤器](#using-filters)部分。 |
| `finalName` | `java.lang.String` | 是 | 在Maven项目（构建阶段）中定义的`finalName` | 生成的包ZIP文件的名称，不带`.zip`文件扩展名 |
| `group` | `java.lang.String` | 是 | Maven项目中定义的`groupID` | 作为内容包目标安装路径一部分的生成内容包的`groupId` |
| `outputDirectory` | `java.io.File` | 是 | Maven项目中定义的构建目录 | 保存内容包的本地目录 |
| `prefix` | `java.lang.String` | 否 | 无 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 无 | 马文项目 |
| `properties` | `java.util.Map` | 否 | 无 | 这些参数定义可在`properties.xml`文件中设置的其他属性。 这些属性不能覆盖以下预定义属性：`group`（使用`group`参数设置）、`name`（使用`name`参数设置）、`version`（使用`version`参数设置）、`description`（从项目描述设置）、`groupId`（Maven项目描述符的`groupId`）、`artifactId`（`artifactId`Maven项目描述符）、`dependencies`（使用`dependencies`参数设置）、`createdBy`（`user.name`系统属性的值）、`created`（当前系统时间）、`requiresRoot`（使用`requiresRoot`参数设置）、`packagePath`（自动从组和包名称生成） |
| `requiresRoot` | `boolean` | 是 | false | 定义包是否需要根。 这将成为`properties.xml`文件的`requiresRoot`属性。 |
| `subPackages` | `java.util.List` | 否 | 无 |  |
| `version` | `java.lang.String` | 是 | Maven项目中定义的版本 | 内容包的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven项目（构建阶段）中定义的目录 | 包含要包含在包中的内容的目录 |

#### 使用过滤器{#using-filters}

使用过滤器元素定义包内容。 过滤器将添加到包`META-INF/vault/filter.xml`文件中的`workspaceFilter`元素。

以下筛选器示例显示要使用的XML结构：

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

`mode`元素定义导入包时对存储库的影响。 可以使用以下值：

* **合并：** 添加包中尚未在存储库中的内容。包和存储库中的内容将保持不变。 不会从存储库中删除任何内容。
* **替换：** 将不在存储库中的包中的内容添加到存储库。存储库中的内容将替换为包中的匹配内容。 当内容在包中不存在时，内容将从存储库中删除。
* **更新：** 将不在存储库中的包中的内容添加到存储库。存储库中的内容将替换为包中的匹配内容。 现有内容会从存储库中删除。

当筛选器不包含`mode`元素时，将使用默认值`replace`。

### 帮助 {#help}

#### 参数 {#parameters-6}

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 确定是否显示每个目标的所有可设置属性 |
| `goal` | `String` | 否 | 无 | 此参数定义要显示帮助的目标名称。 如果未指定任何值，则显示所有目标的帮助。 |
| `indentSize` | `int` | 否 | `2` | 用于每个级别缩进的空格数（如果定义，则必须为正） |
| `lineLength` | `int` | 否 | `80` | 显示线的最大长度（如果定义，则必须为正） |

## 在包{#including-a-thumbnail-image-or-properties-file-in-the-package}中包含缩略图或属性文件

替换默认的包配置文件以自定义包属性。 例如，包含缩略图图像以区分包管理器和包共享中的包。

源文件可位于文件系统中的任意位置。 在POM文件中，定义构建资源以将源文件复制到`target/vault-work/META-INF`以包含在包中。

以下POM代码将项目源`META-INF`文件夹中的文件添加到包中：

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

以下POM代码仅向包添加缩略图图像。 缩略图图像必须命名为`thumbnail.png`，并且必须位于包的`META-INF/vault/definition`文件夹中。 在本示例中，源文件位于项目的`/src/main/content/META-INF/vault/definition`文件夹中：

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

## 使用AEM Project Archetype生成AEM项目{#using-archetypes}

最新的AEM Project Archetype为内部实施和AMS实施实施实施了最佳实践包结构，并建议所有AEM项目使用。

>[!TIP]
>
>有关更多详细信息，请参阅AEM中的[AEM项目结构](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章作为Cloud Service文档以及[AEM项目原型](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)文档。 两者都完全支持AEM 6.5。
