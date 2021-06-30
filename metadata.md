---
product: adobe experience manager
description: Adobe Experience Manager作为Cloud Service文档。
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hans
index: y
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: c19c15c4e71c8ead1c3cb05add052a8ffae79d0a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 6%

---


# 内部使用的元数据

GitHub创作系统中的元数据是分层的，并且按照以下不断增加的先例级别进行定义。

1. metadata.md
1. ToC
1. 文章

metadata.md文件中定义的元数据适用于整个存储库，但可以在ToC和文章级别覆盖。 任何元数据的覆盖操作都应在尽可能低的级别完成。

experience-manager-cloud-service.en存储库中的元数据是最低要求。

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
* `contentOwner` (仅适用于下的核心资产内 `/help/assets`容)
