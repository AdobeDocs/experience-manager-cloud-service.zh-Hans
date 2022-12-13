---
title: 在示例 React 应用程序中自定义内容
description: 使用示例 React 应用程序以了解如何使用 AEM as a Cloud Service 中的 Headless 功能集自定义内容。
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: 6204830f30c28daba3ff87ba60acd0150847b523
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 97%

---

# 在示例 React 应用程序中自定义内容 {#customize-app}

针对 Headless 的 AEM 试用预加载了一个简单的 React 应用程序来显示 Headless 内容。在本模块中，您将了解如何预览该应用程序，以及如何通过交换图像并为其创建购物时刻来修改其内容。

该应用程序本身基于内容片段的结构。您可以使用 AEM 中的内容片段编辑器来修改您的应用程序内容。为了帮助您了解如何执行此操作，AEM 试用版的本模块将通过一个快速的交互式导览引导您完成这一过程。本文档旨在对交互式导览进行补充，其中涵盖了相同的步骤，并会在适当时链接到其他资源。

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="自定义React应用程序示例中的内容"
>abstract="我们已设置了一个现代化的React应用程序，您可以使用该应用程序了解如何使用无头功能集自定义内容。"

## 内容片段编辑器 {#fragment-editor}

对于示例应用程序，从内容片段编辑器开始操作。

![内容片段编辑器](assets/customize-app/content-fragment-editor.png)

如果您想在应用程序内指南之外自行导航到内容片段编辑器，可以使用页面左上角的 Adobe 图标来找到它。这将打开 AEM 全局导航。从该位置，选择&#x200B;**导航**&#x200B;选项卡，然后选择&#x200B;**内容片段**。

![在内容片段控制台中导航到应用程序](assets/customize-app/navigate-to-app.png)

这将打开内容片段控制台。从该位置，您可以使用左侧面板中的内容树来导航到应用程序内容的位置。在此情况下，在&#x200B;**内容片段** -> **示例 WKND 应用程序** -> **英语** -> **内容片段** -> **页面**&#x200B;下。

点按或单击内容树右侧的控制台中显示的 **WKND 主页**&#x200B;页面片段以启动应用程序内容编辑器。

>[!TIP]
>
>如果您想详细了解 AEM 中的导航，请参阅本文档的[“其他资源”部分](#additional-resources)，了解有关 AEM 基本处理的更多信息。

## 预览应用程序 {#preview}

在开始修改应用程序之前，请先通过预览应用程序的当前状态来熟悉它。点按或单击编辑器屏幕右上角的&#x200B;**预览**&#x200B;按钮。

演示应用程序将在新选项卡中打开。

![演示应用程序预览](assets/customize-app/preview-demo-app.png)

该应用程序本身是一个简单的电子商务应用程序，适用于在 React 中实现的虚构 WKND 户外生活方式品牌。在周围单击以导航示例内容。

返回到内容片段编辑器的选项卡以继续。

## 在应用程序中编辑文本 {#edit-app}

如前所述，应用程序本身由内容片段构成。这些片段在一个结构中链接在一起，从而构成了应用程序。

内容片段编辑器将应用程序的基本版面显示为页面。此页面是一个内容片段，它本身是其他片段的集合。**面板**&#x200B;表示应用程序的不同页面，每个页面都是自己的内容片段。通过修改这些片段，可以更改应用程序的内容。

1. 在&#x200B;**面板**&#x200B;部分中点按或单击&#x200B;**峡谷中的山地车手**。

   ![点按“峡谷中的山地车手”片段](assets/customize-app/mtn-biker-in-canyon.png)

1. 编辑器将打开山地车手的标题面板。每个面板由图层构成，表示应用程序页面中的不同内容。

   ![面板](assets/customize-app/panels.png)

1. 选择文本图层&#x200B;**峡谷中的山地车手**。这将在编辑器中打开图层的详细信息。图层由多个内容片段构成。

   ![选择“峡谷中的山地车手”标题](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. 选择&#x200B;**“峡谷中的山地车手”标题**&#x200B;文本项。该操作将打开内容片段编辑器，其中显示该片段的内容并允许进行修改。

   ![选择“峡谷中的山地车手”标题文本项](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 将文本从 `Your next great adventure is calling` 更改为 `Choose your own adventure`。编辑器将自动保存此更改。

1. 单击“预览”可查看更改。演示应用程序将在新选项卡中打开。

   ![演示应用程序预览](assets/customize-app/preview-demo-app-text.png)

返回到内容片段编辑器的选项卡以继续本模块。

## 更改应用程序的主图像 {#change-image}

现在，您已修改应用程序中的一些文本，请尝试更改应用程序的主图像。首先，您需要找到该内容。

该编辑器左上角的痕迹导航将显示您在内容层次结构中所处的位置。

1. 在痕迹导航中点按或单击&#x200B;**峡谷中的山地车手**&#x200B;以返回该页面。

   ![痕迹导航](assets/customize-app/breadcrumbs.png)

1. 返回到包含应用程序的各个图层的面板。这些图层不只是表示文本内容。它们表示您的应用程序中的所有内容。因此，您也可以使用内容片段编辑器来交换图像。

   ![面板](assets/customize-app/panels.png)

1. 选择&#x200B;**山地自行车 - 车手**&#x200B;图像图层。该操作将打开内容片段编辑器，其中显示该片段的内容并允许进行修改。

   ![编辑图像片段](assets/customize-app/mtn-biking-biker.png)

1. 点按或单击 **X** 可删除车手图像。该图像将消失，并且编辑器会显示一个错误，因为图像是此内容片段模型所需的数据。

   ![从片段中删除的图像](assets/customize-app/mtn-biking-biker-no-image.png)

1. 点按或单击&#x200B;**添加资源**&#x200B;并在 **sample-wknd-app** > **en** > **image-files** 中找到黄色车手图像。使用&#x200B;**选择资源**&#x200B;对话框左侧的树视图来导航内容层次结构。

   ![“选择资源”对话框](assets/customize-app/select-assets.png)

1. 筛选文本 `yellow`。使用&#x200B;**选择资源**&#x200B;窗口顶部的&#x200B;**搜索所有资源**&#x200B;字段来搜索图像。输入搜索文本，然后按 Enter 进行搜索。

   ![搜索资源](assets/customize-app/search-assets.png)

1. 点按或单击以选择 `biker-yellow.png` 图像，然后点按或单击&#x200B;**选择**。

   ![选择资源](assets/customize-app/select-asset.png)

1. 车手图像已替换为所选图像。该编辑器将自动保存更改。

   ![编辑后的车手图像片段](assets/customize-app/mtn-biking-biker-edited.png)

## 创造购物时刻 {#create-moment}

现在，您已更新车手图像，可以为车手的黄色短裤添加购物时刻。

1. 首先，返回到页面片段的内容片段编辑器。该编辑器左上角的痕迹导航将显示您在内容层次结构中所处的位置。在痕迹导航中点按或单击 **WKND 主页**&#x200B;返回该页面。

   ![导航回版面屏幕](assets/customize-app/breadcrumbs-2.png)

1. 选择 **WKND 上的山地车手（黄色）**&#x200B;面板。

   ![创建购物时刻](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. 您现在可以看到构成车手图像的图层。通过选择&#x200B;**山地自行车 - 购物**&#x200B;图层，为车手的黄色短裤添加购物时刻。

   ![选择购物时刻图层](assets/customize-app/mtn-biking-shoppable.png)

1. 要创建一个购物时刻，您必须创建一个新的内容片段来表示该时刻。点按或单击 **+ 新建片段**&#x200B;按钮，为车手短裤添加购物时刻。

   ![添加购物时刻](assets/customize-app/create-new-fragment.png)

1. 由于内容片段表示结构化的 Headless 数据，因此，在创建内容片段时，必须首先选择一个模型作为基础。从&#x200B;**内容片段模型**&#x200B;下拉列表中选择&#x200B;**购物时刻项目**&#x200B;模型。

   ![选择内容片段模型](assets/customize-app/new-content-fragment.png)

1. 为将表示此新的购物时刻的内容片段命名。例如，在&#x200B;**名称**&#x200B;字段中输入 `Shorts`。

   ![为购物时刻命名](assets/customize-app/new-content-fragment.png)

1. 点按或单击&#x200B;**创建并打开**。

1. 这将为新的内容片段打开编辑器。
   * 在&#x200B;**文本**&#x200B;字段中为购物时刻命名，例如 `Yellow shorts`。
   * 设置 X 和 Y 来确定将覆盖购物时刻的位置。
      * **X**：`-18`
      * **Y**：`-28`
   * 编辑器将自动保存对片段进行的更改

   ![编辑购物时刻](assets/customize-app/edit-shoppable-moment.png)

1. 点按或单击&#x200B;**预览**，测试此定位并根据需要进行调整。

   ![预览您的新购物时刻](assets/customize-app/preview-demo-app-shoppable.png)

## 您已了解如何自定义示例 React 应用程序！ {#conclusion}

在本模块中，您已了解如何自定义示例 React 应用程序。首先，您了解了如何编辑现有文本。之后，了解了如何将一个图像与其另一个实例交换。最后，您了解了如何创建和定位购物时刻项目。

请务必查看[“其他资源”部分](#additional-resources)，了解有关使用 AEM 及其内容片段的其他资源。

如果您想了解如何创建内容片段和 Headless 内容以供自定义应用程序使用，您可以先查看模块[为您的应用程序创建内容结构](content-structure.md)。

您可以通过单击导航栏右上角的&#x200B;**解决方案**&#x200B;按钮并选择 **Experience Manager** 来返回到试用主屏幕。

![导航主页](assets/customize-app/home.png)

## 其他资源 {#additional-resources}

有关内容片段和 AEM 的更多信息，请考虑查看本附加文档。

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) – 有关内容片段模型的完整文档
* [内容片段](/help/assets/content-fragments/content-fragments.md) – 内容片段概述以及有关内容片段的完整文档的链接
* [基本处理](/help/sites-cloud/authoring/getting-started/basic-handling.md) – 介绍新用户如何导航和使用 AEM 的文档
