---
title: 多站点管理器和翻译
description: 了解如何在您的项目中重复使用您的内容并在AEM中管理多语言网站。
feature: 管理
role: 管理员
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# 多站点管理器和翻译{#msm-and-translation}

Adobe Experience Manager内置的多站点管理器和翻译工具简化了内容本地化。

* 多站点管理器(MSM)及其Live Copy功能使您能够在多个位置使用相同的站点内容，同时允许以下各种不同：
   * [重用内容：多站点管理器和Live Copy](msm/overview.md)
* 翻译使您能够自动翻译页面内容，以创建和维护多语种网站：
   * [翻译多语言站点的内容](translation/overview.md)

这两个功能可以结合使用，以满足[跨国网站和多语言网站](#multinational-and-multilingual-sites)的需要。

## 跨国和多语种站点{#multinational-and-multilingual-sites}

通过结合使用多站点管理器和翻译工作流程，您可以高效地为跨国和多语言站点创建内容。

通常，您会使用一种语言和特定国家/地区创建一个主控站点，然后将该内容用作其他站点的基础，并在需要时使用翻译。

1. [将主控](translation/overview.md) 站点翻译为不同的语言。
1. 使用[多站点管理器](msm/overview.md)可以：
   1. 重复使用主控站点及其翻译中的内容，为其他国家/地区和文化创建站点。
   1. 根据需要分离Live Copy的元素以添加本地化详细信息。

>[!TIP]
>
>将多站点管理器的使用限制在一种语言中的内容。
>
>例如，使用英语主控为美国、加拿大、英国等国创建英文版页面。 页面并使用法语主控为法国、瑞士、加拿大等创建法语版页面。

下图说明了主要概念如何交叉（但不显示涉及的所有级别/元素）：

![本地化概述](assets/localization-overview.png)

在这种情况下，MSM不会管理不同的语言版本。

* [MSM](msm/overview.md) 管理从蓝图(即全局主控)到Live Copy（即本地站点）（语言边界内）的已翻译内容的部署。
* AEM的[翻译](translation/overview.md)集成功能与第三方翻译管理服务一起管理语言并将内容翻译成这些不同语言。

对于更高级的用例，MSM也可以跨语言主页使用。

>[!TIP]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM的最佳实践](msm/best-practices.md)
>* [翻译最佳实践](translation/best-practices.md)

