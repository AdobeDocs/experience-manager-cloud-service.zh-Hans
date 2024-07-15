---
title: 使用路径浏览器进行路径选择
description: 了解如何使用路径浏览器在AEM中选择资源。
exl-id: 8eb52793-b709-4e66-832d-533ef06bc0e1
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 43%

---

# 路径选择 {#path-selection}

通常，在创作时，需要选择其他资源，例如定义指向其他页面的链接或选择图像时。 为了轻松选择路径，[路径字段](#path-fields)提供了自动完成功能，并且还可通过[路径浏览器](#path-browser)做出更可靠的选择。

## 路径字段 {#path-fields}

此处所用的说明示例是图像组件。有关使用和编辑组件的详细信息，请参阅[用于页面创作的组件。](/help/sites-cloud/authoring/page-editor/components.md)

路径字段具有自动完成和预见功能，可更轻松地查找资源。

单击路径字段中的&#x200B;**打开选择对话框**&#x200B;按钮可打开[路径浏览器](#path-browser)对话框，以查看更多详细选择选项。

![“打开选择对话框”按钮](assets/path-selection-open-selection-dialog.png)

或者您可以在路径字段中开始输入，AEM 将会在您输入的同时提供匹配的路径。

![“打开选择对话框”按钮](assets/path-selection-open-selection-dialog.png)

## 路径浏览器 {#path-browser}

路径浏览器的组织方式类似于&#x200B;[**站点**&#x200B;控制台的[列视图](/help/sites-cloud/authoring/basic-handling.md#column-view)，](/help/sites-cloud/authoring/sites-console/introduction.md)允许更详细的资源选择。

![路径浏览器](/help/sites-cloud/authoring/assets/path-browser.png)

* 选择资源后，对话框右上角的&#x200B;**选择**&#x200B;按钮变为活动状态。
   * 选择以确认选择，或&#x200B;**取消**&#x200B;以中止。
* 如果上下文允许选择多个资源，则选择某个资源也会激活&#x200B;**选择**&#x200B;按钮，但也会将选定资源的计数添加到窗口的右上角。
   * 单击该 **数字旁边的** X可取消选择全部。
* 在树中导航时，您的位置会反映在对话框顶部的痕迹导航中。
   * 还可使用这些痕迹导航在资源层次结构中快速跳转。
* 您可以随时使用对话框顶部的搜索字段。
   * 单击搜索字段中的 **X** 可清除搜索。
* 要缩小搜索范围，您可以显示过滤器选项并按特定路径筛选结果。

![过滤器选项](assets/path-selection-filters.png)
