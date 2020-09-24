---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hans
index: y
solution-title: Adobe Experience Manager 云服务
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: 入门
getting-started-url: https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/overview/home.html
tutorials-title: 教程
tutorials-url: https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 967d0993ba2114d0dd081724cf5e7754899b5c8e
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 20%

---


# 元数据供内部使用

GitHub创作系统中的元数据是分层的，定义为以下不断增加的先例级别。

1. metadata.md
1. ToC
1. 文章

metadata.md文件中定义的元数据适用于整个回购区，但可以在ToC和文章级别覆盖。 对元数据的任何覆盖都应在尽可能低的级别执行。

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

有关元数据的其他信息，请参阅内 [部创作指南。](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)
