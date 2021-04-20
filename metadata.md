---
product: adobe experience manager
description: Adobe Experience Manager作为Cloud Service文档。
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hans
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
cloud: Experience Cloud
translation-type: tm+mt
source-git-commit: 6908b5215dcbff0692d4e03dd1588ca5d34aeffe
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 7%

---


# 内部使用的元数据

GitHub创作系统中的元数据是分层的，定义为以下不断增加的先例级别。

1. metadata.md
1. ToC
1. 文章

metadata.md文件中定义的元数据适用于整个回购，但可以在ToC和文章级别覆盖。 对元数据的任何覆盖都应在尽可能低的级别执行。

experience-manager-cloud-service.en repo中的元数据是最低要求。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` (仅限核心资产内容下 `/help/assets`)
