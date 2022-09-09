---
title: 多站点管理器和翻译
description: 了解如何在您的项目中重用内容并在 AEM 中管理多语言网站。
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 100%

---

# 多站点管理器和翻译 {#msm-and-translation}

利用 Adobe Experience Manager 的内置多站点管理器和翻译工具，可以轻松本地化内容。

* 多站点管理器 (MSM) 及其 Live Copy 功能可让您在多个位置使用相同的站点内容并允许以下变化：
   * [重用内容：多站点管理器和 Live Copy](msm/overview.md)
* 利用翻译工具，您可以自动化页面内容的翻译以创建和维护多语言网站：
   * [翻译多语言站点的内容](translation/overview.md)

可以结合使用这两种功能，以满足[跨国和多语言](#multinational-and-multilingual-sites)网站的需求。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅我们的[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

## 跨国和多语言站点 {#multinational-and-multilingual-sites}

通过结合使用多站点管理器和翻译工作流，您可以高效地为跨国和多语言站点创建内容。

通常，您将采用一种语言为特定的国家/地区创建主站点，然后将该内容用作其他站点的基础，并在需要时使用翻译。

1. 将主站点[翻译](translation/overview.md)成其他语言。
1. 使用[多站点管理器](msm/overview.md)可以：
   1. 重用主站点的内容及其翻译来针对其他国家/地区和文化创建站点。
   1. 如果需要，可以分离 Live Copy 的元素来添加本地化详细信息。

>[!TIP]
>
>仅允许将多站点管理器用于采用一种语言的内容。
>
>例如，使用英语母版为美国、加拿大、英国等创建英文版页面。使用法语母版为法国、瑞士、加拿大等创建法语版页面。

下图说明了主要概念的相交部分（但未显示涉及的所有级别/元素）：

![本地化概述](assets/localization-overview.png)

在此场景以及类似场景中，MSM 不会管理不同的语言版本。

* [MSM](msm/overview.md) 在语言范围内管理从 Blueprint（即全局母版）到 Live Copy（即本地站点）的已翻译内容的部署。
* AEM 的[翻译](translation/overview.md)集成功能与第三方翻译管理服务相结合，可以管理语言并将内容翻译成这些不同的语言。

在更高级的用例中，也可以跨语言母版使用 MSM。

>[!TIP]
>
>对于所有用例，建议阅读以下最佳实践：
>
>* [MSM 的最佳实践](msm/best-practices.md)
>* [翻译的最佳实践](translation/best-practices.md)

