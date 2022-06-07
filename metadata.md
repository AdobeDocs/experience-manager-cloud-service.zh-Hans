---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service文档。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.zh-Hans
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 5bc43af20dc8893303b1d1f4dc70939631933eb7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 68%

---


# 内部使用的元数据

GitHub 创作系统中的元数据为层级式的，并定义了以下相对于前一项的递增级别。

1. metadata.md
1. ToC
1. 文章

在 metadata.md 文件中的定义的元数据应用到整个存储库，但可以在 ToC 和文章级别覆盖。任何覆盖元数据的操作应在尽可能最低的级别进行。

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

ToC

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` (仅适用于 `/help/assets`)
