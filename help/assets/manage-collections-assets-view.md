---
title: 管理收藏集
description: 收藏集是Experience Manager Assets视图中的一组资源。 使用收藏集可在用户之间共享资源。
exl-id: 540dc1d9-eaf4-4e08-8087-dc58da23a6e8
feature: Collections, Asset Management
role: User
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 90%

---

# 管理收藏集 {#manage-collections}

>[!CONTEXTUALHELP]
>id="assets_collections"
>title="管理收藏集"
>abstract="收藏集是 Assets 视图中的一组资源、文件夹或其他收藏集。使用收藏集可在用户之间共享资源。收藏集与文件夹的不同之处是可包含来自不同位置的资源。您可以与一个用户共享多个收藏集。每个收藏集都包含对资源的引用。收藏集中会保持资源的引用完整性。"

收藏集是Adobe Experience Manager Assets视图中的一组资源、文件夹或其他收藏集。 使用收藏集可在用户之间共享资源。

与文件夹不同，一个收藏集可以包含来自不同位置的资源。

<!--
You can share collections with various users that are assigned different levels of privileges, including viewing, editing, and so on.
-->

您可以与一个用户共享多个收藏集。每个收藏集都包含对资源的引用。收藏集中会保持资源的引用完整性。

![收藏集](assets/collections.png)

您可以执行以下任务来管理和使用收藏集：

* [创建收藏集](#create-collection)

* [将资源添加到收藏集](#add-assets-to-collection)

* [从收藏集删除资源](#remove-assets-from-collection)

* [创建智能收藏集](#create-smart-collection)

* [编辑智能收藏集](#edit-smart-collection)

* [查看和编辑收藏集元数据](#view-edit-collection-metadata)

* [共享收藏集的链接](#share-collection-links)

* [下载收藏集](#download-collection)

* [删除收藏集](#delete-collection)

* [管理专用收藏集的权限](#manage-permissions-to-a-private-collection)

## 创建收藏集 {#create-collection}

要创建收藏集，请执行以下操作：

1. 单击左边栏中的&#x200B;**[!UICONTROL 收藏集]**，然后单击&#x200B;**[!UICONTROL 创建收藏集]**。

1. 指定收藏集的标题和可选描述。

1. 选择需要创建专用收藏集还是公共收藏集。公共收藏集可供所有用户查看和编辑。但是，专用收藏集仅供创建者和具有管理员权限的用户使用。

1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建收藏集。

![创建收藏集](assets/create-collection.png)

<!--
   
   for viewing and editing only to users with the appropriate [permissions](#manage-collection-access).

-->

## 将资源添加到收藏集 {#add-assets-to-collection}

要将资源添加到收藏集，请执行以下操作：

1. 在左侧边栏中单击&#x200B;**[!UICONTROL 资源]**，然后选择要添加到某个收藏集的资源。

1. 单击&#x200B;**[!UICONTROL 添加到收藏集]**。

1. 在[!UICONTROL 收藏集]对话框上，选择要将所选资源添加到的收藏集。

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;以将资源添加到所选收藏集。

## 从收藏集中移除资源 {#remove-assets-from-collection}

要从收藏集中移除资源，请执行以下操作：

1. 单击左边栏中的&#x200B;**[!UICONTROL 收藏集]**&#x200B;以查看收藏集列表。

1. 单击该收藏集，然后选择要从该收藏集中删除的项。

1. 单击&#x200B;**[!UICONTROL 删除]**。

## 管理智能收藏集 {#manage-smart-collection}

将搜索结果保存为智能收藏集以动态更新收藏集内容。如果有添加到Assets视图存储库的资源符合在创建智能收藏集时定义的搜索条件，则智能收藏集的内容将在您打开智能收藏集时自动更新。

### 创建智能收藏集 {#create-smart-collection}

要创建智能收藏集，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL 筛选条件]**&#x200B;和[定义搜索条件](search-assets-view.md#refine-search-results)。

1. 单击&#x200B;**[!UICONTROL 另存为]**，然后选择&#x200B;**[!UICONTROL 智能收藏集]**。

   ![创建智能收藏集](assets/create-smart-collection.png)

1. 在[!UICONTROL 创建智能收藏集]对话框上，指定智能收藏集的标题和描述。

1. 如果需要所有用户均可访问该收藏集，请选择&#x200B;**[!UICONTROL 公共收藏集]**。如果需要一组数量有限的用户访问该收藏集，请选择&#x200B;**[!UICONTROL 专用收藏集]**。

1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建该智能收藏集。

### 编辑智能收藏集 {#edit-smart-collection}

要编辑智能收藏集：

1. 单击左栏中的&#x200B;**[!UICONTROL 收藏集]**，然后双击需要编辑的收藏集的名称。

1. 单击&#x200B;**[!UICONTROL “编辑智能收藏集”]**。

1. 在[!UICONTROL “编辑智能收集过滤器”]对话框中，[更新智能收藏集的搜索条件](search-assets-view.md#refine-search-results)。

1. 单击&#x200B;**[!UICONTROL 保存]**。

<!--

## Manage access to a Private collection {#manage-collection-access}

The permission management for collections function in the same manner as folders in [!DNL Assets view]. Administrators can manage the access levels for collections available in the repository. As an administrator, you can create user groups and assign permissions to those groups to manage access levels. You can also delegate the permission management privileges to user groups at the collection-level.

For more information, see [Manage permissions for folders and collections](manage-permissions.md).

-->

<!--

## Search a collection {#search-collections}

Click **[!UICONTROL Collections]** in the left rail and use the Search box to specify a text as the criteria to search for a collection. [!DNL Assets view] uses the specified text to search collection names, metadata including tags defined for a collection and returns appropriate results.

>[!NOTE]
>
>Assets view performs search in collections available at the root level. It does not perform search in assets and folders available in collections.

-->

## 查看和编辑收藏集元数据 {#view-edit-collection-metadata}

收藏集元数据包括有关收藏集的数据，例如标题和描述。

要查看和编辑收藏集元数据，请执行以下操作：

1. 单击左边栏中的&#x200B;**[!UICONTROL 收藏集]**，选择一个收藏集，然后单击&#x200B;**[!UICONTROL 详细信息]**。
1. 使用&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡查看收藏集元数据。
1. 根据需要修改元数据字段。您可以修改[!UICONTROL 标题]和[!UICONTROL 描述]字段。

![收藏集元数据](assets/collection-metadata.png)

## 共享收藏集的链接 {#share-collection-links}

[!DNL Assets view] 使您能够生成链接并与无权访问 [!DNL Assets view] 应用程序的外部利益相关者共享收藏集及其资源。您可以定义链接的到期日期，然后使用您喜欢的通信方式（如电子邮件或消息服务）与他人共享。链接的接收者可以预览并下载资源。

![共享资源链接](assets/share-link-collections.png)

有关如何与外部利益相关者共享收藏集链接的更多信息，请参阅[共享资源链接](/help/assets/share-links-for-assets-view.md)。

## 下载收藏集 {#download-collection}

要下载收藏集，请执行以下操作：

1. 在左边栏中单击&#x200B;**[!UICONTROL 收藏集]**。

1. 选择需要下载的收藏集，然后单击&#x200B;**[!UICONTROL 下载]**。

1. 在[!UICONTROL 正在下载资源]对话框中，单击&#x200B;**[!UICONTROL 确定]**。

收藏集将以 .ZIP 文件的形式下载到您的本地计算机上。

## 删除收藏集 {#delete-collection}

要删除收藏集，请执行以下操作：

1. 单击左边栏中的&#x200B;**[!UICONTROL 收藏集]**。

1. 选择要删除的收藏集。

1. 单击&#x200B;**[!UICONTROL 删除]**。

## 管理私人收藏集的权限{#manage-permissions-private-collection}

您可以允许管理员管理存储库中专用收藏集的[访问级别](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)。您可以向用户组或用户分配诸如 `Can View` 和 `Can Edit` 等权限。您还可以将权限管理权限委派给用户组。创建专用收藏集的用户是这些收藏的所有者。他们可以使用“[!UICONTROL 管理权限]”操作向其他用户授予访问权限。此外，管理员可以查看和管理 [!DNL Experience Manager] 存储库中专用收藏集的权限。
<!--
>[!NOTE]
>
>Adobe does not recommend to assign permissions to users.
-->
有关如何向用户组分配可用权限的信息，请参阅[向用户组添加权限](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)。

有关端到端工作流程的更多信息，请参阅[管理权限](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/get-started-admins/folder-access/manage-permissions)。

## 后续步骤 {#next-steps}

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)
