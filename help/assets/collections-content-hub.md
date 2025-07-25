---
title: 在Content Hub中管理收藏集
description: 了解如何在Content Hub中管理收藏集
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 3%

---

# 管理[!DNL Content Hub]中的收藏集 {#manage-collections}

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![管理收藏集](assets/manage-collection.png)

收藏集是指可在用户之间共享的一组资源。 收藏集可以包含来自不同位置的资产，同时保持其引用完整性。

[!DNL Content Hub]允许您创建公共收藏集。 这些收藏集可供所有授权用户访问，从而创建多个用户可以高效地访问和利用内容的共享空间。 收藏集促进了资源的协作使用，以提高效率和便利性。 在收藏集浏览页面中，您可以：

* **创建**：创建一个或多个收藏集。
* **查看**：查看资源及其属性。
* **共享**：将资源作为链接与他人共享。
* **下载**：下载资源。
* **移除**：从收藏集中移除特定资产。
* **删除**：删除整个收藏集。

它帮助用户轻松访问和管理[!DNL Content Hub]中可用的各种资源。

## 先决条件 {#prerequisites}

[Content Hub用户](deploy-content-hub.md#onboard-content-hub-users)可以执行本文中提到的操作。

## 创建集合{#create-collections}

您可以在管理治理时选择[创建新收藏集](#create-new-collection)或[将资产添加到现有收藏集](#add-assets-to-existing-collection)。

### 新建收藏集{#create-new-collection}

执行以下步骤可在创建收藏集时控制访问权限：

1. 转到&#x200B;**[!DNL Collections]**&#x200B;选项卡，然后单击&#x200B;**[!UICONTROL 创建收藏集]**。 此时将显示“新建收藏集”窗口。

1. 为集合添加&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**。

   ![收藏集权限](assets/collection-permissions.png)

1. 在&#x200B;**[!UICONTROL 谁可以访问]**&#x200B;下拉菜单下，选择访问控制类型。 以下选项可供选择：

   | 访问方法 | 访问类型 | 描述 |
   |---|---|---|
   | **只有您和管理员可以编辑** | 专用 | 只有创建者和管理员才能编辑和访问此收藏集。 |
   | **任何人都可以查看** | 公共 | 所有人都可以访问此收藏集，但只有创建者和管理员可以编辑。 |
   | **任何人都可以查看和编辑** | 公共 | 此收藏集对所有人开放，无限制地授予完全访问和编辑权限。 |

   >[!NOTE]
   >
   > [!DNL Content Hub]管理员可以查看&#x200B;**[!UICONTROL 谁可以访问]**&#x200B;下拉列表下的所有可用选项，而对于常规用户，您需要[指定并配置](configure-content-hub-ui-options.md)他们可以访问的选项。

1. 单击&#x200B;**[!UICONTROL 创建]**。完成后，您可以[将资产添加到收藏集](#add-assets-to-existing-collection)。

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

<!--
>[!NOTE]
>
>Collections governance is a limited availability feature. You can get it enabled  by creating a support ticket. Once enabled, you need to [Configure Collections in Content Hub](configure-content-hub-ui-options.md#configure-collections-content-hub).-->

<!--To create a new collection, navigate to the **[!UICONTROL Collections]** tab and click **[!UICONTROL Create new collection]**. Enter the **[!UICONTROL Title]** and provide an optional **[!UICONTROL Description]** for the assets. Click **[!UICONTROL Create]**.
![Create collection](assets/add-assets-collection.jpg)          
-->

### 将资源添加到现有收藏集{#add-assets-to-existing-collection}

要将资源添加到现有收藏集，请选择要添加到收藏集的资源。 单击&#x200B;**[!UICONTROL 添加到收藏集]**。 系统会提示您选择收藏集。

![创建新收藏集](assets/create-add-collection.jpg)

选择需要在其中添加资产的收藏集。 您还可以使用搜索栏搜索现有收藏集。 <br>选择需要添加资产的收藏集，然后单击&#x200B;**[!UICONTROL 添加到收藏集]**。

## 查看收藏集{#view-collections}

导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;选项卡并搜索收藏集名称。 您可以使用过滤器通过选择特定标准来优化搜索结果，从而帮助您快速找到最相关的收藏集。

要查看收藏集中可用的资产列表，请单击收藏集名称。 您还可以在收藏集中应用过滤器以缩小资产结果的范围。 单击需要在收藏集中查看的资产。 [!DNL Content Hub]显示资产的详细视图。 [查看资源详细信息](asset-properties-content-hub.md)。

### 筛选收藏集视图 {#filter-collections-view}

通过Content Hub，可筛选收藏集视图，根据您的偏好缩小选项范围，轻松找到所需内容。 确保Content Hub[&#128279;](configure-content-hub-ui-options.md#configure-collections-content-hub)中集合的配置。

要筛选收藏集视图，请转到&#x200B;**[!DNL Collections]**&#x200B;选项卡并导航到收藏集下拉列表。 从以下选项中进行选择：

* **[!UICONTROL 所有收藏集]：**&#x200B;选择此选项可查看和编辑所有收藏集，包括那些与您共享或私有的收藏集。
* **[!UICONTROL 只有我]：**&#x200B;选择此选项可查看您有权访问的收藏集。
* **[!UICONTROL 任何人都可以查看]：**&#x200B;此选项允许您筛选每个人都可以访问但只有创建者才能编辑的收藏集。
* **[!UICONTROL 任何人都可以编辑]：**&#x200B;选择此选项可筛选每个人都可以访问和编辑的收藏集。

  ![筛选集合视图](assets/filter-collection-view.png)

此外，要根据访问权限筛选收藏集视图，请转到&#x200B;**[!DNL Collections]**&#x200B;选项卡并导航到以下选项之一：

* **[!UICONTROL 由任何人创建]：**&#x200B;此筛选器限制您查看由任何用户创建的收藏集。

* **[!UICONTROL 由我创建]：**&#x200B;此筛选器限制您查看由您创建的收藏集。

  ![筛选集合视图](assets/filter-collection-view1.png)

<!--
![Asset details](assets/view-collection.jpg)

* **A**: Details and metadata of the asset 
* **B**: Zoom In or Zoom Out the asset 
* **C**: Reset Zoom view 
* **D**: View the previous or next asset 
* **E**: Download the asset 
* **F**: Open the asset in Adobe Express 
* **G**: Hide the metadata of the asset 
* **H**: Share the asset as a link 
-->

## 下载收藏集中可用的资产{#download-assets-within-collection}

要下载收藏集中可用的资产，请导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;选项卡。\
单击收藏卡上的![下载图标](assets/download-icon.svg)图标。

![收藏集选项卡](assets/download-collection.png)

收藏集中的所有资产均已下载。

您还可以打开收藏集以单独下载资产。 单击包含您需要下载的资源的收藏集。 选择资源并单击&#x200B;**[!UICONTROL 下载]**。

了解如何[从 [!DNL Content Hub]](download-assets-content-hub.md)下载资产。

## 共享收藏集中可用的资产 {#share-assets-available-within-collection}

您还可以共享收藏集中可用的资产。 确保在Content Hub[&#128279;](configure-content-hub-ui-options.md#enable-public-link-sharing)中启用公共链接共享。 导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;选项卡。 选择收藏卡上的![共享图标](assets/share.svg)图标。 将复制共享链接。 您可以与收件人共享复制的链接。 了解有关[在 [!DNL Content Hub]](share-assets-content-hub.md)中共享资产的更多信息。

Content Hub收藏集提供了全面的治理工具以实现有效的资产管理，包括可自定义的共享权限和协作功能。 从只读访问到完全管理控制，这些设置支持对资产分发进行精细管理。 单独或作为收藏集的一部分共享资产时，访问范围由分配给用户的收藏集当前访问级别确定。 或者，您无法共享专用收藏集。

## 编辑收藏集的详细信息 {#edit-details-of-collection}

要编辑收藏集的&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**，请单击收藏集名称，然后单击![信息图标](assets/info-icon.svg)图标。 将显示[!UICONTROL 收藏集详细信息]屏幕，允许您编辑收藏集的&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**。 单击&#x200B;**[!UICONTROL 保存更改]**&#x200B;以确认修改。 此外，您还可以通过编辑收藏集对话框更新对收藏集的访问权限，具体取决于配置。

![收藏集详细信息](assets/collection-details.png)

## 从收藏集删除资源{#remove-assets-from-a-collection}

以下用户可以从收藏集中删除单个或多个资源：

* 管理员
* 收藏集的所有者
* 具有编辑权限的非管理员用户

要从收藏集中删除资产，请单击需要从中删除资产的收藏集，选择资产，然后单击&#x200B;**[!UICONTROL 从收藏集中删除]**。

![删除收藏集](assets/remove-collection-new.jpg)

系统会提示您确认资产移除操作。 单击&#x200B;**[!UICONTROL 删除]**。\
已成功从收藏集中删除选定的资产。

## 删除收藏集{#delete-collection}

只有管理员和创建者才能删除收藏集。 要删除收藏集，请导航到&#x200B;**[!UICONTROL 收藏集]**&#x200B;选项卡，然后单击需要删除的收藏集。 单击![删除图标](assets/delete-icon.svg)图标可删除收藏集。



