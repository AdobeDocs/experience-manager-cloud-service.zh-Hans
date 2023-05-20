---
title: 编辑启动项
description: 為您的頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 52%

---

# 编辑启动项 {#editing-launches}

## 編輯啟動頁面 {#editing-launch-pages}

為某個頁面（或一組頁面）建立啟動後，您可以編輯頁面啟動副本中的內容。

1. [从“引用”（站点控制台）中访问启动项](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)以显示可用的操作。
1. 選取 **前往頁面** 以開啟頁面進行編輯。

在编辑页面时，您将看到顶部工具栏中的指示以及&#x200B;**离开**&#x200B;和&#x200B;**导航**&#x200B;选项：

![从页面编辑器中离开和导航启动项](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>您不能在启动项中移动页面。尝试此操作将触发警告消息：
>
>* 警告：此页面是启动项的源。不允许移动此页面。


### 编辑基于 Live Copy 的启动页面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的启动项基于 [Live Copy](/help/sites-cloud/administering/msm/overview.md)，那么您将会：

* 在编辑组件（内容和/或属性）时看到锁状符号（小挂锁）。
* 在&#x200B;**页面属性**&#x200B;中看到 **Live Copy** 选项卡

Live Copy 用于将&#x200B;**&#x200B;源分支&#x200B;**&#x200B;中的内容同步到启动分支（以使启动项与源中所做的更改保持最新）。

您可以使用與編輯標準即時副本相同的方式進行變更；例如：

* 按一下已關閉的掛鎖將會中斷此同步處理，並允許您對啟動項中的內容進行新的更新。 一旦解除鎖定（開啟掛鎖），您所做的變更將不會被來源分支內相同位置所做的任何變更覆寫。
* 特定页面的&#x200B;**暂停**（和&#x200B;**继续**）继承。

另請參閱 [變更即時副本內容](/help/sites-cloud/administering/msm/creating-live-copies.md) 以取得進一步資訊。

## 比較啟動頁面與其來源頁面 {#comparing-a-launch-page-to-its-source-page}

要跟踪您所做的更改，您可以在&#x200B;**引用**&#x200B;中查看启动项，并将启动页面与其源页面进行比较：

1. 在&#x200B;**站点**&#x200B;控制台中，[导航到启动项的源页面并选择其中一个源页面](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)。
1. 開啟 **[引用](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** 面板並選取 **啟動**.
1. 選取您的特定啟動，然後 **與來源比較**：

   ![比较启动项和源](/help/sites-cloud/authoring/assets/launches-compare.png)

1. 兩個頁面（啟動項和來源）將並排開啟。

   如需關於使用此功能的完整資訊，請參閱 [頁面差異](/help/sites-cloud/authoring/features/page-diff.md).

## 變更使用的來源頁面 {#changing-the-source-pages-used}

您可以随时向启动项的源页面范围中添加页面或从中删除页面：

1. 从以下任一位置访问并选择启动项：
   * [“启动项”控制台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：
      * 选择&#x200B;**编辑**。
   * [引用（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 若要顯示可用的動作：
      * 选择&#x200B;**编辑启动项**。
      * 將顯示來源頁面。
1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。

>[!NOTE]
>
>若要將頁面新增至啟動項，這些頁面必須位於共同語言根之下；即在單一網站內。

## 編輯Launch設定 {#editing-a-launch-configuration}

您可以随时编辑启动项的属性：

1. 从以下任一位置访问并选择启动项：
   * 此 [啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)：
      * 選取 **屬性**.
   * [引用（網站主控台）](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) 若要顯示可用的動作：
      * 选择&#x200B;**编辑属性**。
      * 將顯示詳細資料。
1. 进行所需的更改，然后使用&#x200B;**保存**&#x200B;进行确认。
   * 有关启 [动日期和生产就绪字段的用途和交互的信息](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)******** ，请参阅启动项——事件的顺序。

## 探索頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

當您從「參考」標籤中選取特定啟動時，會顯示狀態(請參閱 [在參照（網站主控台）中啟動](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console))。

![发现启动项状态](/help/sites-cloud/authoring/assets/launches-status.png)
