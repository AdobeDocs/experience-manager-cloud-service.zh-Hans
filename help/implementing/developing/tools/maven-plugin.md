---
title: Adobe内容包Maven插件
description: 使用内容包Maven插件部署AEM应用程序
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d757c94475f257ee4b05092671ae5e6384b8342e
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---

# Adobe内容包Maven插件 {#adobe-content-package-maven-plugin}

使用Adobe内容包Maven插件将包部署和管理任务集成到Maven项目中。

将构造的包部署到AEM由Adobe内容包Maven插件执行，并使通常使用AEM [包管理器：](/help/implementing/developing/tools/package-manager.md)执行的任务实现自动化

* 从文件系统中的文件创建新包。
* 在AEM上安装并卸载包。
* 生成已在AEM上定义的包。
* 获取AEM上安装的软件包列表。
* 从AEM中删除包。

本文档详细介绍如何使用Maven管理这些任务。 但是，了解[AEM项目及其包的结构也非常重要。](#aem-project-structure)

>[!NOTE]
>
>请始终使用这些插件的最新可用版本。

>[!NOTE]
>
>包&#x200B;**创建**&#x200B;现在归[Apache Jackrabbit FileVault包Maven插件所有。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>
>本文介绍了由Adobe内容包Maven插件执行的将构造的包部署到AEM的&#x200B;**部署**。

## 包和AEM项目结构 {#aem-project-structure}

AEM as a Cloud Service遵循由最新的AEM项目原型实施的包管理和项目结构的最新最佳实践。

>[!TIP]
>
>请参阅AEM as a Cloud Service文档中的[AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章和[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)文档。 AEM 6.5完全支持这两种版本。

## 获取内容包Maven插件 {#obtaining-the-content-package-maven-plugin}

插件可从[Maven中央存储库中获取。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

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

要使Maven能够下载插件，请使用此页面上[获取内容包Maven插件](#obtaining-the-content-package-maven-plugin)部分中提供的配置文件。

## 内容包Maven插件的目标 {#goals-of-the-content-package-maven-plugin}

内容包插件提供的目标和目标参数在以下部分中进行了描述。 “常用参数”部分中描述的参数可用于大多数目标。 适用于一个目标的参数在该目标的部分中进行了描述。

### 插件前缀 {#plugin-prefix}

插件前缀为`content-package`。 使用此前缀可从命令行执行目标，如以下示例所示：

```shell
mvn content-package:build
```

### 参数前缀 {#parameter-prefix}

除非另有说明，否则插件目标和参数使用`vault`前缀，如以下示例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用代理进行AEM的目标使用在Maven设置中找到的第一个有效代理配置。 如果未找到代理配置，则不使用代理。 请参阅[公用参数](#common-parameters)部分中的`useProxy`参数。

### 常用参数 {#common-parameters}

下表中的参数对所有目标都是通用的，但在&#x200B;**目标**&#x200B;列中注明者除外。

| 名称 | 类型 | 必需 | 默认值 | 描述 | 目标 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 如果值为`true`，则会在发生错误时导致生成失败。 值为`false`会导致生成忽略该错误。 | 除`package`之外的所有目标 |
| `name` | `String` | `build`：是，`install`：否，`rm`：是 | `build`：无默认值，`install`： Maven项目的`artifactId`属性的值 | 要执行操作的包的名称 | 除`ls`之外的所有目标 |
| `password` | `String` | 是 | `admin` | 用于通过AEM进行身份验证的密码 | 除`package`之外的所有目标 |
| `serverId` | `String` | 否 | 从中检索用于身份验证的用户名和密码的服务器ID | 除`package`之外的所有目标 |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM包管理器的HTTP服务API的URL | 除`package`之外的所有目标 |
| `timeout` | `int` | 否 | `5` | 与包管理器服务通信的连接超时（以秒为单位） | 除`package`之外的所有目标 |
| `useProxy` | `boolean` | 否 | `true` | 值为`true`会导致Maven使用找到的第一个活动代理配置将请求代理到包管理器。 | 除`package`之外的所有目标 |
| `userId` | `String` | 是 | `admin` | 用于通过AEM进行身份验证的用户名 | 除`package`之外的所有目标 |
| `verbose` | `boolean` | 否 | `false` | 启用或禁用详细日志记录 | 除`package`之外的所有目标 |

### 生成 {#build}

构建已在AEM实例上定义的内容包。

>[!NOTE]
>
>此目标不需要在Maven项目中执行。

#### 参数 {#parameters}

生成目标的所有参数在[公共参数](#common-parameters)部分中进行了说明。

### 安装 {#install}

在存储库中安装包。 执行此目标不需要Maven项目。 目标绑定到Maven构建生命周期的`install`阶段。

#### 参数 {#parameters-1}

除了以下参数外，请参阅[常用参数](#common-parameters)部分中的说明。

| 名称 | 类型 | 必需 | 默认值 | 描述 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | Maven项目的`artifactId`属性的值 | `groupId:artifactId:version[:packaging]`形式的字符串 |
| `artifactId` | `String` | 否 | 无 | 要安装的工件的ID |
| `groupId` | `String` | 否 | 无 | 要安装的工件的`groupId` |
| `install` | `boolean` | 否 | `true` | 确定在上传包时是否自动解压缩包 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | `localRepository`系统变量的值 | 本地Maven存储库，由于始终使用系统属性，因此无法使用插件配置对其进行配置 |
| `packageFile` | `java.io.File` | 否 | 为Maven项目定义的主要构件 | 要安装的软件包文件的名称 |
| `packaging` | `String` | 否 | `zip` | 要安装的工件的包装类型 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 为Maven项目定义的`remoteArtifactRepositories`属性的值 | 此值不能使用插件配置进行配置，必须在项目中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 为其配置插件的项目 | 隐式的Maven项目，因为该项目包含插件配置 |
| `repositoryId` (POM)，`repoID` （命令行） | `String` | 否 | `temp` | 从中检索工件的存储库ID |
| `repositoryUrl` (POM)，`repoURL` （命令行） | `String` | 否 | 无 | 从中检索工件的存储库URL |
| 版本 | 字符串 | 否 | 无 | 要安装的工件的版本 |

### ls {#ls}

列出部署到[包管理器](/help/implementing/developing/tools/package-manager.md)的包。

#### 参数 {#parameters-2}

ls目标的所有参数在[公共参数](#common-parameters)部分中进行了说明。

### rm {#rm}

从[包管理器](/help/implementing/developing/tools/package-manager.md)中删除包。

#### 参数 {#parameters-3}

rm目标的所有参数在[公共参数](#common-parameters)部分中进行了说明。

### 卸载 {#uninstall}

卸载包。 软件包在服务器上保持未安装状态。

#### 参数 {#parameters-4}

卸载目标的所有参数在[公共参数](#common-parameters)部分中有说明。


### 帮助 {#help}

#### 参数 {#parameters-6}

| 名称 | 类型 | 必需 | 默认值 | 描述 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 确定是否显示每个目标的所有可设置属性 |
| `goal` | `String` | 否 | 无 | 此参数定义要为其显示帮助的目标名称。 如果未指定值，则会显示所有目标的帮助。 |
| `indentSize` | `int` | 否 | `2` | 用于每个级别缩进的空格数（如果已定义，则必须为正数） |
| `lineLength` | `int` | 否 | `80` | 显示线的最大长度（如果已定义，则必须为正数） |

## 在包中包含缩略图图像或属性文件 {#including-a-thumbnail-image-or-properties-file-in-the-package}

替换默认软件包配置文件以自定义软件包属性。 例如，在[包管理器](/help/implementing/developing/tools/package-manager.md)中包含用于区分包的缩略图图像。

源文件可以位于文件系统中的任何位置。 在POM文件中，定义生成资源以将源文件复制到`target/vault-work/META-INF`以包含在包中。

以下POM代码将项目源的`META-INF`文件夹中的文件添加到包中：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

以下POM代码仅将缩略图图像添加到包。 缩略图图像必须命名为`thumbnail.png`，并且必须位于包的`META-INF/vault/definition`文件夹中。 在此示例中，源文件位于项目的`/src/main/content/META-INF/vault/definition`文件夹中：

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

最新的AEM项目原型为内部部署和AMS实施实施了最佳实践包结构，建议将其用于所有AEM项目。

>[!TIP]
>
>请参阅AEM as a Cloud Service文档中的[AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)文章和[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)文档。 AEM 6.5完全支持这两种版本。
