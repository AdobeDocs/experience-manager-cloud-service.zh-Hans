---
title: 准备翻译内容
description: 了解如何准备翻译内容。
feature: 语言复制
role: 管理员
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---


# 准备翻译内容{#preparing-content-for-translation}

多语言网站通常提供多种语言的大量内容。 站点以一种语言创作，然后翻译为其他语言。 通常，多语言站点由页面分支组成，其中每个分支包含不同语言的站点页面。

[WKND教程站点](/help/implementing/developing/introduction/develop-wknd-tutorial.md)包含多个语言分支，并使用以下结构：

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

最初为其创作站点内容的语言副本是语言主控。 语言“主控”是翻译成其他语言的源。

站点的每个语言分支称为语言副本。 语言副本的根页面（称为语言根页面）标识语言副本中内容的语言。 例如，`/content/wknd/fr`是法语语言副本的语言根。 语言副本必须使用[正确配置的语言根](preparation.md#creating-a-language-root)，以便在执行源站点的翻译时锁定正确的语言。

使用以下步骤准备翻译您的站点：

1. 创建语言的语言根主控。 例如，英语WKND演示站点的语言根目录为`/content/wknd/language-masters/en`。 确保根据[创建语言根](preparation.md#creating-a-language-root)中的信息正确配置语言根。
1. 创作您语言的内容，主控。
1. 为站点创建每个语言副本的语言根目录。 例如，WKND示例站点的法语语言副本为`/content/wknd/language-masters/fr`。

在准备翻译内容后，您可以在语言副本和关联的翻译项目中自动创建缺失的页面。 （请参阅[创建翻译项目](managing-projects.md)。） 有关AEM中内容翻译过程的概述，请参阅[多语言网站内容翻译](overview.md)。

## 创建语言根{#creating-a-language-root}

创建一个语言根目录作为标识内容语言的语言副本的根页面。 创建语言根目录后，可以创建包含语言副本的翻译项目。

要创建语言根，请创建页面并使用ISO语言代码作为&#x200B;**Name**&#x200B;属性的值。 语言代码必须采用以下格式之一：

* `<language-code>`  — 例如，支持的语言代码是ISO-639-1定义的双字母代码 `en`。
* `<language-code>_<country-code>` 或 —  `<language-code>-<country-code>` 支持的国家/地区代码是ISO 3166定义的小写或大写双字母代码， `en_US`例如 `en_us`, `en_GB`、 `en-gb`。

您可以根据您为全局站点选择的结构，使用任一格式。  例如，WKND站点的法语语言副本的根页面具有`fr`作为&#x200B;**Name**&#x200B;属性。 请注意，**Name**&#x200B;属性用作存储库中页面节点的名称，因此会确定页面的路径(`http://<host>:<4502>/content/wknd/language-masters/fr.html`)。

1. 导航到站点。
1. 单击或点按要创建语言副本的站点。
1. 单击或点按&#x200B;**创建**，然后单击或点按&#x200B;**页面**。

   ![创建页面](../assets/create-page.png)

1. 选择页面模板，然后单击或点按&#x200B;**下一步**。
1. 在&#x200B;**名称**&#x200B;字段中，键入格式为`<language-code>`或`<language-code>_<country-code>`的国家/地区代码，例如`en`、`en_US`、`en_us`、`en_GB`、`en_gb`。 键入页面标题。

   ![创建语言根页面](../assets/create-language-root.png)

1. 单击或点按&#x200B;**创建**。在确认对话框中，单击或点按&#x200B;**完成**&#x200B;以返回站点控制台，或单击或点按&#x200B;**打开**&#x200B;以打开语言副本。

## 语言根{#seeing-the-status-of-language-roots}的现状

AEM提供了一个&#x200B;**引用**&#x200B;边栏，其中显示已创建的语言根的列表。

![语言根](../assets/language-roots.png)

使用[边栏选择器，使用以下过程视图页面的语言副本。](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

1. 在站点控制台上，选择站点的页面，然后单击或点按&#x200B;**引用**。

   ![打开引用边栏](../assets/opening-references-rail.png)

1. 在引用边栏中，单击或点按&#x200B;**语言副本**。 边栏显示网站的语言副本。

## 多级语言副本{#multiple-levels}

语言根也可以分组在节点下，例如按区域，同时仍被识别为语言副本的根。

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
>只允许一个级别。 例如，以下内容将不允许`es`页面解析为语言副本：
>
>* `/content/wknd/language-masters/en`
>* `/content/wknd/language-masters/americas/central-america/es`

>
> 
此`es`语言副本将不被检测，因为它离`en`节点只有2个级别(`americas/central-america`)。

>[!TIP]
>
>在这种设置中，语言根可以具有任何页面名称，而不仅仅是该语言的ISO代码。 AEM将始终首先检查路径和名称，但如果页面名称不识别语言，AEM将检查页面的`cq:language`属性以识别语言。
