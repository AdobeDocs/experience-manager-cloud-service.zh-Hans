---
title: 准备内容以进行翻译
description: 了解如何准备内容以进行翻译。
feature: Language Copy
role: Admin
exl-id: afc577a2-2791-481a-ac77-468011e4302e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 100%

---

# 准备内容以进行翻译 {#preparing-content-for-translation}

多语言网站通常以多种语言提供一定数量的内容。使用一种语言创作该站点的内容，然后将此内容翻译成其他语言。通常，多语言站点包含多个页面分支，每个分支均包含采用其他语言的站点页面。

>[!TIP]
>
>如果不熟悉如何翻译内容，请参阅我们的[站点翻译历程](/help/journey-sites/translation/overview.md)，将指导您使用 AEM 强大的翻译工具翻译您的 AEM Sites 内容，非常适合没有 AEM 或翻译经验的人士。

[WKND 教程站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md)包括几个语言分支并使用以下结构：

```text
/content
    |- wknd
        |- language-masters
            |- en
            |- de
            |- es
            |- fr
            |- it
        |- us
            |- en
            |- es
        |- ca
            |- en
            |- fr
        |- ch
            |- de
            |- fr
            |- it
        |- de
            |- de
        |- fr
            |- fr
        |- es
            |- es
        |- it
            |- it
```

您最初为其创作站点内容的语言副本是语言母版。语言母版是翻译成其他语言的源。

站点的每个语言分支均称为语言副本。语言副本的根页面（称为语言根）标识了语言副本中内容的语言。例如，`/content/wknd/fr` 是法语副本的语言根。语言副本必须使用[准确配置的语言根](preparation.md#creating-a-language-root)，以便在翻译源站点内容时使用正确的语言。

使用以下步骤可准备站点以进行翻译：

1. 创建语言母版的语言根。例如，英语 WKND 演示站点的语言根为 `/content/wknd/language-masters/en`。确保根据[创建语言根](preparation.md#creating-a-language-root)中的信息来正确配置语言根。
1. 创作语言母版的内容。
1. 创建站点的每个语言副本的语言根。例如，WKND 示例站点的法语副本为 `/content/wknd/language-masters/fr`。

准备好内容以进行翻译后，您可以在语言副本和相关翻译项目中自动创建缺失的页面。（请参阅[创建翻译项目](managing-projects.md)。）有关 AEM 中内容翻译过程的概述，请参阅[翻译多语言网站的内容](overview.md)。

## 创建语言根 {#creating-a-language-root}

创建语言根作为标识了内容语言的语言副本的根页。创建语言根后，您可以创建包含语言副本的翻译项目。

要创建语言根，您需要创建一个页面并使用 ISO 语言代码作为&#x200B;**名称**&#x200B;属性的值。语言代码必须采用下列格式之一：

* `<language-code>` – 支持的语言代码是由 ISO-639-1 定义的两字母代码，例如 `en`。
* `<language-code>_<country-code>` 或 `<language-code>-<country-code>` – 支持的国家/地区代码是由 ISO 3166 定义的小写或大写形式的两字母代码，例如 `en_US`、`en_us`、`en_GB`、`en-gb`。

根据您为全球站点选择的结构，您可以使用任一格式。例如，WKND 站点的法语副本的根页面将 `fr` 用作&#x200B;**名称**&#x200B;属性。请注意，**名称**&#x200B;属性用作存储库中页面节点的名称，从而确定页面的路径 (`http://<host>:<4502>/content/wknd/language-masters/fr.html`)。

1. 导航到站点。
1. 单击或点按要为其创建语言副本的站点。
1. 单击或点按&#x200B;**创建**，然后单击或点按&#x200B;**页面**。

   ![创建页面](../assets/create-page.png)

1. 选择页面模板，然后单击或点按&#x200B;**下一步**。
1. 在&#x200B;**名称**&#x200B;字段中，用 `<language-code>` 或 `<language-code>_<country-code>` 格式键入国家/地区代码，例如 `en`、`en_US`、`en_us`、`en_GB`、`en_gb`。为页面键入标题。

   ![创建语言根页面](../assets/create-language-root.png)

1. 单击或点按&#x200B;**创建**。在确认对话框中，单击或点按&#x200B;**完成**&#x200B;以返回站点控制台，或者单击或点按&#x200B;**打开**&#x200B;打开语言副本。

## 查看语言根的状态 {#seeing-the-status-of-language-roots}

AEM 提供了一个&#x200B;**引用**&#x200B;边栏来显示已创建的语言根的列表。

![语言根](../assets/language-roots.png)

使用[边栏选择器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)通过以下过程查看页面的语言副本。

1. 在站点控制台上，选择站点的页面，然后单击或点按&#x200B;**引用**。

   ![打开引用边栏](../assets/opening-references-rail.png)

1. 在引用边栏中，单击或点按&#x200B;**语言副本**。边栏显示网站的语言副本。

## 多个级别的语言副本 {#multiple-levels}

语言根也可在节点下进行分组（例如按区域），同时仍被识别为语言副本的根。

```text
/content
    |- wknd
        |- language-masters
            |- europe
                |- de
                |- fr
                |- it
                |- es
                ]- pt
            |- americas
                |- en
                |- es
                |- fr
                |- pt
            |- asia
                |- ...
            |- africa
                |- ...
            |- oceania
                |- ...
        |- europe
        |- americas
        |- asia
        |- africa
        |- oceania            
```

>[!NOTE]
>
>仅允许一个级别。例如，以下内容将不允许 `es` 页面解析为语言副本：
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`
>
> 将无法检测到此 `es` 语言副本，因为它与 `en` 节点相差 2 个级别 (`americas/central-america`)。

>[!TIP]
>
>在此类设置中，语言根可以具有任何页面名称，而不仅仅是语言的 ISO 代码。AEM 将始终首先检查路径和名称，但如果页面名称未标识语言，则 AEM 将在页面的 `cq:language` 属性中检查语言标识。
