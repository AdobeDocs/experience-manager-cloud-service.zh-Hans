---
title: AEM Repo 工具
description: AEM Repo Tool是一种简单的解决方案，可通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# AEM Repo 工具 {#aem-repo-tool}

AEM Repo Tool是一种简单的解决方案，可通过类似于FTP的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo工具类似于[Jackrabbit FileVault Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快，依赖项最少，而且是一个简单的bash脚本。

此工具简化了开发人员传输文件的过程，还可集成到Eclipse和IntelliJ中，以提高开发效率。

## 概述 {#overview}

对于文件系统上`jcr_root` FileVault结构内的给定路径，AEM Repo工具会为整个子树创建一个带有单个过滤器的包，并将该包推送到服务器（类似于FTP `put`），从服务器( `get`)获取该包，或者比较差异（`status`和`diff`）。

该工具不支持多个筛选器路径或FileVault的`filter.xml`。

>[!CAUTION]
>
>AEM Repo Tool始终覆盖指定的整个文件或目录。

## 下载和文档 {#download-and-documentation}

[AEM Repo Tool可通过此链接](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上获取，以及详细的安装和使用说明。

如果要下载AEM Repo Tool的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
