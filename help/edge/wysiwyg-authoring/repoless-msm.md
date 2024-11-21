---
title: 重写多站点管理
description: 了解有关如何以可靠的方式利用单个代码库通过多语言站点设置项目的最佳实践建议。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 重写多站点管理 {#repoless-msm}

本文档假设您已经为名为`my-aem-site`的项目创建了基础站点，并且希望使用AEM的MSM功能将其本地化。

如果您已为重写使用案例设置了项目，则云配置将在根页面`/content/my-aem-site`级别分配。 对于多语言站点，此配置分配必须更改为语言根，如`/content/my-aem-site/language-master/de`。

