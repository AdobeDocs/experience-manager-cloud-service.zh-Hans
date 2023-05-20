---
title: 管理项目
description: 通过“项目”，您可以将资源分组到一个实体中，以便在“项目”控制台中对其进行访问和管理，从而组织项目
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 51%

---

# 管理项目 {#managing-projects}

專案可讓您將資源分組到一個實體中，以組織您的專案。

在 **專案** 主控台，您可存取專案並對其執行動作：

![“项目”控制台](/help/sites-cloud/authoring/assets/projects-console.png)

在「專案」中，您可以建立專案、將資源與專案相關聯，也可以刪除專案或資源連結。 您可以開啟圖磚來檢視其內容以及將專案新增至圖磚。 本主題說明這些程式。

## 创建项目 {#creating-a-project}

AEM提供下列立即可用的範本，供您在建立專案時選擇：

* 简单项目
* 媒体项目
* 翻译项目

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

从项目到项目，创建项目的过程相同。 项目类型之间的差异包括可用的用户角 [色](/help/sites-cloud/authoring/projects/overview.md) 和工 [作流](/help/sites-cloud/authoring/projects/workflows.md)。  要创建新项目，请执行以下操作：

1. 在“ **项目**”中，点按／单 **击创建** ，以打开创 **建项目向导** :
1. 选择模板并单击&#x200B;**下一步**。

   ![创建项目](/help/sites-cloud/authoring/assets/projects-create.png)

1. 定义&#x200B;**标题**&#x200B;和&#x200B;**描述**，然后根据需要添加&#x200B;**缩略图**&#x200B;图像。您也可以新增或刪除使用者，以及使用者所屬的群組。 此外，按一下 **進階** 以新增在URL中使用的名稱。

   ![添加项目详细信息](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 点按/单击&#x200B;**创建**。確認會詢問您是要開啟新專案，還是返回主控台。

### 將資源與專案建立關聯 {#associating-resources-with-your-project}

由於專案可讓您將資源分組到一個實體中，因此您想要將資源與專案相關聯。 這些資源稱為 **圖磚**. 您可以新增的資源型別在中說明 [專案動態磚](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

若要將資源與專案建立關聯，請執行下列動作：

1. 從開啟您的專案 **專案** 主控台。
1. 點選/按一下 **新增圖磚** 並選取您要連結至專案的圖磚。 您可以选择多种类型的拼贴。

   ![将拼贴添加到项目](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >有关可与项目关联的项目拼贴的详细说明，请参阅[项目拼贴](/help/sites-cloud/authoring/projects/overview.md#project-tiles)。

1. 点按/单击&#x200B;**创建**。您的资源随即会链接到项目，从现在开始，您便可以从项目中访问该资源。

### 删除项目或资源链接 {#deleting-a-project-or-resource-link}

可使用同样的方法从控制台中删除项目或项目中的链接资源：

1. 導覽至適當位置：

   * 若要刪除專案，請前往 **專案** 主控台。
   * 要删除项目中的资源链接，请在&#x200B;**项目**&#x200B;控制台中打开相应的项目。

1. 单击&#x200B;**选择**&#x200B;并选择您的项目或资源链接，以进入选择模式。
1. 点按/单击&#x200B;**删除**。

1. 您必須在對話方塊中確認刪除。 若已確認，則會刪除專案或資源連結。 点按/单击&#x200B;**取消选择**&#x200B;可退出选择模式。

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。

### 新增專案至圖磚 {#adding-items-to-a-tile}

在某些圖磚中，您可能會想要新增多個專案。 例如，您可能會同時執行多個工作流程，或執行多個體驗。

若要新增專案至圖磚：

1. 在&#x200B;**项目**&#x200B;中，导航到相应的项目，然后点按或单击要将项目添加到的拼贴上的向下 V 形。

   ![将项目添加到拼贴](/help/sites-cloud/authoring/assets/project-workflows.png)

1. 新增專案至圖磚，就像建立新圖磚時一樣。 說明專案拼貼 [此處](/help/sites-cloud/authoring/projects/overview.md#project-tiles). 在此範例中，已新增另一個工作流程。

### 開啟圖磚 {#opening-a-tile}

您可能想要檢視目前圖磚中包含哪些專案，或修改或刪除圖磚中的專案。

若要開啟圖磚，以便檢視或修改專案，請執行下列動作：

1. 在「專案」主控台中，點選/按一下卡片底部的省略符號(...)圖示。

   ![打开拼贴](/help/sites-cloud/authoring/assets/project-links.png)

1. AEM會列出該圖磚中的專案。 您可以進入選擇模式來修改或刪除專案。

   ![已打开拼贴](/help/sites-cloud/authoring/assets/projects-add-link.png)

## 查看项目统计信息 {#viewing-project-statistics}

您可以在&#x200B;**项目**&#x200B;控制台中查看项目统计信息。

### 查看项目时间线 {#viewing-a-project-timeline}

项目时间线提供了项目中的资产上次使用时间的相关信息。要查看项目时间线，请单击/点按&#x200B;**时间线**，然后进入选择模式并选择项目。资产会显示在左侧窗格中。单击/点按&#x200B;**时间线**&#x200B;可返回到&#x200B;**项目**&#x200B;控制台。

![项目时间线](/help/sites-cloud/authoring/assets/projects-timeline.png)

### 查看活动/不活动的项目 {#viewing-active-inactive-projects}

要在活动和不活动的项目之间切换，请在&#x200B;**项目**&#x200B;控制台中单击&#x200B;**切换活动的项目**。如果该图标旁边显示有复选标记，则显示的是活动的项目。

![“切换活动项目”按钮](/help/sites-cloud/authoring/assets/projects-active.png)

如果该图标旁边显示有一个 x，则显示的是不活动的项目。

![“切换不活动项目”按钮](/help/sites-cloud/authoring/assets/projects-inactive.png)

## 讓專案為非使用中或使用中 {#making-projects-inactive-or-active}

如果您已完成專案，但仍想保留專案上的資訊，您可以讓專案非作用中。

若要使專案非作用中（或作用中），請執行下列動作：

1. 在 **專案** 主控台，開啟您的專案，然後找到 **專案資訊** 圖磚。

   >[!NOTE]
   如果您的專案中尚未出現此動態磚，您可能需要加以新增。 另請參閱 [新增圖磚](#adding-items-to-a-tile).

1. 点按/单击&#x200B;**编辑**。
1. 将选择器从&#x200B;**活动**&#x200B;更改为&#x200B;**不活动**（反之亦然）。

   ![激活项目](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. 点按/单击&#x200B;**完成**&#x200B;以保存更改。
