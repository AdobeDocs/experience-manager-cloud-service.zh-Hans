---
title: AEM Repo 工具
description: AEM Repo工具是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# AEM Repo 工具 {#aem-repo-tool}

AEM Repo工具是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具类似于[Jackrabbit FileVault Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快，依赖关系最小，是一个简单的bash脚本。

此工具可简化开发人员的文件传输，还可集成到Eclipse和IntelliJ中，以提高开发效率。

## 概述 {#overview}

对于文件系统上`jcr_root` FileVault结构内的给定路径，AEM Repo工具会为整个子树创建一个包含单个筛选器的包，并将其推送到服务器（类似于FTP `put`），从服务器(`get`)获取，或比较差异（`status`和`diff`）。

该工具不支持多个过滤器路径或FileVault的`filter.xml`。

>[!CAUTION]
>
>请注意，AEM Repo工具将始终覆盖指定的整个文件或目录。

## 下载和文档{#download-and-documentation}

在GitHub上，可通过此链接](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)获取[AEM Repo工具，并提供详细的安装和使用说明。

如果您要下载AEM Repo工具的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
