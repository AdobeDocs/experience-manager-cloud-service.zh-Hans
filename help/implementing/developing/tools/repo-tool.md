---
title: AEM Repo工具
description: AEM Repo Tool是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# AEM Repo Tool {#aem-repo-tool}

AEM Repo Tool是一种简单的解决方案，可通过与FTP类似的命令行在本地文件系统和AEM服务器之间传输JCR内容。 AEM Repo Tool类似于[Jackrabbit FileVault Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin)，但速度更快，相关性最小，并且是一个简单的bash脚本。

此工具为开发人员简化了文件传输，还可集成到Eclipse和IntelliJ中，使开发更高效。

## 概述 {#overview}

对于文件系统上`jcr_root` FileVault结构内的给定路径，AEM Repo Tool会为整个子树创建一个具有单个筛选器的包，并将其推送到服务器（类似于FTP `put`），从服务器(`get`)获取它或比较差异（`status`和`diff`）。

该工具不支持多个筛选器路径或FileVault的`filter.xml`。

>[!CAUTION]
>
>请注意，AEM Repo Tool将始终覆盖指定的整个文件或目录。

## 下载和文档{#download-and-documentation}

[AEM Repo Tool可通过此链接](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)在GitHub上提供，并提供详细的安装和使用说明。

如果您希望下载AEM Repo Tool的源，请参阅下面链接的GitHub项目。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开工具项目](https://github.com/Adobe-Marketing-Cloud/tools)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
