---
title: '如何在AEM站点页面中嵌入自适应表单？ '
description: 您可以在AEM网站页面中嵌入自适应Forms。 用户无需离开网站页面即可填写和提交表单。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---


# 在AEM站点页面中嵌入自适应表单 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] 允许表单开发人员将自适应Forms无缝嵌入到AEM Sites页面或托管在AEM外的网页中。 嵌入式自适应表单功能齐全，用户无需离开页面即可填写并提交表单。 它有助于用户停留在网页上其他元素的上下文中，并同时与表单进行交互。

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

在AEM Sites页面中，您可以使用以下方法添加自适应表单：

* **[[!DNL AEM Forms] 容器组件](#af-component)**
   [!DNL AEM Forms] 提供了可添加到网站页面的组件。 的 [!DNL AEM Forms] 容器组件允许您嵌入自适应表单。

* **[资产浏览器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您创建的所有表单都可在资产下找到。 您可以将表单作为资产拖放到页面上。

## 前提条件 {#prerequisites}

要在使用可编辑模板的AEM站点页面中嵌入自适应表单，请确保将AEM表单组件配置为关联模板中允许使用的组件。 有关更多信息，请参阅 **策略和属性（布局容器）** 部分 [创建页面模板](/help/sites-authoring/templates.md).

如果站点页面使用静态模板，则需要在站点页面的段落系统中对其进行配置。 请参阅[在设计模式中配置组件](/help/sites-authoring/default-components-designmode.md)，以了解更多信息。

## 嵌入自适应表单  {#af-component}

要使用 [!DNL AEM Forms] 容器组件：

1. 在编辑模式下打开AEM站点页面，您要在该模式下嵌入自适应表单。
1. 从组件浏览器面板中，拖放 [!DNL AEM Forms] 页面上的容器组件。

   或者，您也可以在资产浏览器中搜索自适应表单，并将其拖放到站点页面。 它将表单嵌入到 [!DNL AEM Forms] 容器。

   >[!NOTE]
   >
   >多个 [!DNL AEM Forms] 不支持页面上的容器组件。

1. 点按嵌入的 [!DNL AEM Forms] 站点页面中的容器组件，然后点按 ![settings_icon](assets/settings_icon.png) 中。 的 **[!UICONTROL 编辑AEM Forms容器]** 对话框。
1. 在编辑中 [!DNL AEM Forms] 容器对话框中，请指定以下内容。

   * **资产类型：** 选择要嵌入的资产类型。 选项为“自适应表单”
   * **资产路径**:浏览并选择要嵌入的自适应表单。 如果您从资产浏览器中将其删除，则会自动填充该内容。
   * （仅限自适应表单） **帖子提交**:选择要在表单提交时触发的操作。 您可以选择显示感谢信或感谢页。

      * **感谢信**:使用富文本编辑器编写消息以在表单提交时显示。 仅当您选择显示感谢信时，此选项才可用。
      * **感谢页面**:浏览并选择要在表单提交时显示的页面。 仅当您选择显示感谢页面时，此选项才可用。
      * **提交时刷新页面**:启用以刷新包含嵌入的自适应表单的页面，以显示感谢页面。 否则，感谢页面将替换 [!DNL AEM Forms] 容器，而不刷新页面。 仅当您选择显示感谢页面时，此选项才可用。
   * **主题**:选择一个主题，以定义自适应表单组件的样式。 样式包括外观属性，如字体样式、背景颜色、尺寸和对齐方式。
   * **高度**:指定容器的高度。 将其留空以自动调整容器大小。
   * **CSS客户端库**:指定CSS客户端库的路径。


1. 保存设置。 自适应表单现在嵌入到页面中。

## 发布嵌入式自适应表单 {#publishing-embedded-adaptive-form}

让我们考虑以下方案，以在AEM站点页面中发布嵌入的资产（自适应表单）：

* 如果您是首次发布AEM站点页面，并且该页面包含嵌入的自适应表单，则发布站点页面和嵌入的资产。
* 如果您只修改了已发布站点页面中嵌入的自适应表单，则应发布原始资产，并且所做的更改会反映在已发布的站点页面中。 发布的网站页面包含对资产的引用，无需重新发布页面。
* 如果您修改了站点页面和嵌入的自适应表单，请重新发布站点页面和嵌入的资产。

## 修改嵌入的自适应表单 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM站点页面维护对 [!DNL AEM Forms] 容器。 因此，在原始自适应表单中配置的所有配置和属性（如主题、样式和提交操作）都将保留在嵌入的自适应表单中。

要修改嵌入的自适应表单的任何配置或属性，请执行以下操作之一。

* 在相应的编辑器中在自适应Forms中打开原始表单并对其进行修改。
* 在编辑模式下，从网站页面中点按自适应表单，然后点按 **[!UICONTROL 在新窗口中编辑]**. 原始表单会在编辑模式下打开，您可以对其进行修改。

>[!NOTE]
>
>在原始自适应表单中所做的更改会自动反映在嵌入的表单中。 但是，请重新发布自适应表单或网站页面，以反映已发布页面中的更改。

## 注意事项和最佳实践 {#considerations-and-best-practices}

在AEM网站页面中嵌入自适应Forms时，请牢记以下几点：

* 原始表单中的页眉和页脚未包含在嵌入的表单中。
* 支持用户草稿和提交嵌入的表单，这些草稿和提交内容显示在表单门户的“草稿”和“已提交”Forms选项卡中。
* 在原始表单上配置的提交操作将保留在嵌入表单中。
* 在原始表单上配置的体验定位和A/B测试在嵌入的表单中不起作用。 但是，您可以在站点页面上使用体验定位来根据用户配置文件显示不同的表单。
* 如果您为原始表单配置了Adobe Analytics，则会在Adobe Analytics中捕获嵌入表单的分析数据。 但是，它在表单分析报表中不可用。

