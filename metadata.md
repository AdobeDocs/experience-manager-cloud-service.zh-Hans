---
product: adobe experience manager
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.en
index: y
solution-title: 作为云服务的Adobe Experience Manager
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: 入门
getting-started-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/home.html
tutorials-title: 教程
tutorials-url: https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 99dce041a6d7554785fd43eb82c671643e903f23

---


# 元数据供内部使用

GitHub创作系统中的元数据是分层的，定义为以下不断增加的先例级别。

1. metadata.md
1. ToC
1. 文章

metadata.md文件中定义的元数据适用于整个存储库，但可以在ToC和文章级别覆盖。 对元数据的任何覆盖都应在尽可能低的级别上完成。

experience-manager-cloud-service.en存储库中的元数据是必需的最低值。

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
* `contentOwner` (仅限核心资产内容 `/help/assets`)

有关元数据的其他信息，请参阅内部 [创作指南。](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)