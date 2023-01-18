---
title: 在示例 React 应用程序中自定义内容
description: 使用示例 React 应用程序以了解如何使用 AEM as a Cloud Service 中的 Headless 功能集自定义内容。
hidefromtoc: true
index: false
exl-id: 32290ad4-d915-41b7-a073-2637eb38e978
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 38%

---


# 在示例 React 应用程序中自定义内容 {#customize-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app"
>title="在示例 React 应用程序中自定义内容"
>abstract="您的AEM无头试用版与示例React应用程序集成，您可以对其进行自定义。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide"
>title="启动内容片段编辑器"
>abstract="您的AEM无头试用版与示例React应用程序集成在一起，这样您就可以看到，无需开发时间，任何人都可以轻松地独立管理内容。<br><br>在新选项卡中通过单击下面的，启动此模块，然后按照本指南操作。"
>additional-url="https://video.tv.adobe.com/v/328618" text="自定义应用程序简介视频"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_react_app_guide_footer"
>title="在本模块中，您已了解如何自定义示例 React 应用程序。<br><br>上市时间：加速！<br>开发周期：减少！<br><br>现在，您已了解无头内容对于由AEM无头功能提供支持的网站和应用程序而言是多么轻松。"
>abstract=""

## 预览应用程序 {#preview}

单击 **启动内容片段编辑器** 按钮可在新选项卡中打开内容片段编辑器。

![内容片段编辑器](assets/customize-app/content-fragment-editor.png)

随AEM无头试用版提供的示例应用程序由通过GraphQL提供的内容片段提供支持。 使用内容片段编辑器通过预览示例来熟悉内容。

1. 点按或单击编辑器屏幕右上角的&#x200B;**预览**&#x200B;按钮。

1. 演示应用程序将在新选项卡中打开。这款应用面向虚构的WKND户外生活方式品牌。 在周围单击以导航示例内容。

   ![演示应用程序预览](assets/customize-app/preview-demo-app.png)

1. 返回到内容片段编辑器的浏览器选项卡以继续。

## 编辑应用程序中的标题 {#edit-app}

内容片段编辑器将应用程序的基本布局显示为页面内容片段。 **面板**&#x200B;表示应用程序的不同页面，每个页面都是自己的内容片段。通过修改这些片段，可以更改应用程序的内容。

1. 在&#x200B;**面板**&#x200B;部分中点按或单击&#x200B;**峡谷中的山地车手**。

   ![点按“峡谷中的山地车手”片段](assets/customize-app/mtn-biker-in-canyon.png)

1. 编辑器会打开山地摩托车应用程序的标题面板。 每个面板都由图层组成，这些图层表示构成体验的不同图像和文本。

   ![面板](assets/customize-app/panels.png)

1. 选择文本图层&#x200B;**峡谷中的山地车手**。这将在编辑器中打开图层的详细信息。层由多个内容片段组成，这些内容片段可控制应用程序此面板中显示的文本。

   ![选择“峡谷中的山地车手”标题](assets/customize-app/mtn-biker-in-canyon-text-layer.png)

1. 选择&#x200B;**“峡谷中的山地车手”标题**&#x200B;文本项。这将打开内容片段编辑器。

   ![选择“峡谷中的山地车手”标题文本项](assets/customize-app/mtn-biker-in-canyon-title.png)

1. 将文本从 `Your next great adventure is calling` 更改为 `Choose your own adventure`。编辑器将自动保存此更改。

1. 点按或单击 **预览** 中，查看您所做的更改。 演示应用程序的预览将在新选项卡中打开。

   ![演示应用程序预览](assets/customize-app/preview-demo-app-text.png)

这就是将React应用程序中的内容集成到AEM无头CMS中后，如何轻松更新内容。

## 在应用程序中交换图像 {#change-image}

现在，您已修改应用程序中的标题，尝试更改图像。

1. 返回到内容片段编辑器的浏览器选项卡。

1. 您需要返回到内容片段编辑器中正确的位置。 该编辑器左上角的痕迹导航将显示您在内容层次结构中所处的位置。在痕迹导航中点按或单击&#x200B;**峡谷中的山地车手**&#x200B;以返回该页面。

   ![痕迹导航](assets/customize-app/breadcrumbs.png)

1. 选择&#x200B;**山地自行车 - 车手**&#x200B;图像图层。这将打开内容片段编辑器

   ![编辑图像片段](assets/customize-app/mtn-biking-biker.png)

1. 点按或单击 **X** 可删除车手图像。该图像将消失，并且编辑器会显示一个错误，因为图像是此内容片段模型所需的数据。

   ![从片段中删除的图像](assets/customize-app/mtn-biking-biker-no-image.png)

1. 点按或单击 **添加资产**.

1. 的 **选择资产** 对话框打开，路径 **sample-wknd-app** > **en** > **图像文件** 会自动为您选择。

1. 选择图像 `biker-yellow.png` 然后，点按或单击 **选择**.

   ![选择资源](assets/customize-app/select-asset.png)

1. 骑行者的图像被替换为所选图像。 该编辑器将自动保存更改。

   ![编辑后的车手图像片段](assets/customize-app/mtn-biking-biker-edited.png)

1. 点按或单击 **预览** 中，查看您所做的更改。 演示应用程序的预览将在新选项卡中打开。 在浏览器上单击刷新，您应该会在应用程序中看到带有黄色短裤的新骑车者图像。

使用AEM无头CMS，可以轻松更新应用程序中的图像和资产。

## 在应用程序中添加对新内容片段的引用 {#create-moment}

现在，您已更新骑车者的图像，下面让我们逐步了解如何通过创建和引用新的内容片段来向应用程序添加新内容。 您会将由“购物时刻”内容片段管理的产品调用添加到应用程序的第二个面板中。

![购物瞬间的示例](assets/customize-app/example-shoppable-moment.png)

1. 返回到内容片段编辑器的浏览器选项卡。

1. 您需要返回到内容片段编辑器中正确的位置。 该编辑器左上角的痕迹导航将显示您在内容层次结构中所处的位置。在痕迹导航中点按或单击 **WKND 主页**&#x200B;返回该页面。

   ![导航回版面屏幕](assets/customize-app/breadcrumbs-2.png)

1. 选择 **WKND 上的山地车手（黄色）**&#x200B;面板。

   ![创建购物时刻](assets/customize-app/mtn-biker-on-wknd-yellow.png)

1. 选择 **Mtn Biking — 购物** 图层。

   ![选择购物时刻图层](assets/customize-app/mtn-biking-shoppable.png)

1. 要在此面板上创建新的标注，必须创建新的购物时刻内容片段。 点按或单击 **+创建新片段** 按钮。

   ![添加购物时刻](assets/customize-app/create-new-fragment.png)

1. 您必须首先选择新内容片段所依据的模型。 从&#x200B;**内容片段模型**&#x200B;下拉列表中选择&#x200B;**购物时刻项目**&#x200B;模型。

1. 为内容片段提供一个名称。 例如，在&#x200B;**名称**&#x200B;字段中输入 `Shorts`。

   ![为购物时刻命名](assets/customize-app/new-content-fragment.png)

1. 点按或单击&#x200B;**创建并打开**。

1. 这将为新的内容片段打开编辑器。

1. 在&#x200B;**文本**&#x200B;字段中为购物时刻命名，例如 `Yellow shorts`。

1. 为设置值 **X** 和 **Y**. 此时，该呼出应覆盖在面板上。 编辑器将自动保存对片段进行的更改。
   * **X**：`-18`
   * **Y**：`-28`

   ![编辑购物时刻](assets/customize-app/edit-shoppable-moment.png)

1. 点按或单击 **预览** 中，查看您所做的更改。 演示应用程序的预览将在新选项卡中打开。 单击浏览器中的刷新以测试定位并在编辑器中根据需要进行调整。

现在，您了解如何在应用程序中完成创建新内容并将其作为内容片段进行引用，而无需进行任何开发周期。
