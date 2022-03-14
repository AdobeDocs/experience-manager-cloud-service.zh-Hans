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

AEM Repo工具是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具类似于 [Jackrabbit FileVault Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快，具有最小的依赖项，并且是一个简单的bash脚本。

此工具可简化开发人员的文件传输，还可集成到Eclipse和IntelliJ中，以提高开发效率。

## 概述 {#overview}

对于 `jcr_root` 文件系统上的FileVault结构，AEM Repo工具会创建一个包，该包中包含用于整个子树的单个过滤器，并将该包推送到服务器（类似于FTP） `put`)，从服务器( `get`)或比较差异( `status` 和 `diff`)。

该工具不支持多个过滤器路径或FileVault的 `filter.xml`.

>[!CAUTION]
>
>请注意，AEM Repo工具将始终覆盖指定的整个文件或目录。

## 下载和文档 {#download-and-documentation}

的 [AEM Repo工具可通过此链接在GitHub上提供](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) 以及详细的安装和使用说明。

如果您要下载AEM Repo工具的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
