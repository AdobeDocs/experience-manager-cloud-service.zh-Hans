---
title: 共用資產的私人資料夾
description: 瞭解如何在中建立私人資料夾 [!DNL Adobe Experience Manager Assets] 並與其他使用者共用，且指派各種許可權給他們。
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 5%

---

# 中的私人資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在中建立私人資料夾 [!DNL Adobe Experience Manager Assets] 您專屬的使用者介面。 您可以與其他使用者共用此私人資料夾，並為其指派各種許可權。 根據您指派的許可權層級，使用者可以在資料夾上執行各種工作，例如檢視資料夾內的資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個成員具有擁有者角色。
>
>若要建立私人資料夾，您需要 `Read` 和 `Modify` 您建立私人資料夾的父資料夾許可權。 如果您不是管理員，預設不會在上啟用這些許可權 `/content/dam`. 在這種情況下，請先取得這些使用者ID/群組的許可權，然後再嘗試建立私人資料夾。

## 建立和共用私人資料夾  {#create-share-private-folder}

若要建立並共用私人資料夾：

1. 在 [!DNL Assets] 主控台，按一下 **[!UICONTROL 建立]** 按鈕，然後選取 **[!UICONTROL 資料夾]** 功能表中的。

   ![建立資產資料夾](assets/create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話方塊，輸入 `Title` 和 `Name` （選擇性）用於資料夾。

   選取 **[!UICONTROL 私人]** 核取方塊並按一下 **[!UICONTROL 建立]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   已建立私人資料夾。 您現在可以 [新增資產](add-assets.md#upload-assets) 至資料夾，並與其他使用者或群組共用資料夾。 除非您共用資料夾並為其指派許可權，否則其他使用者看不到該資料夾。

1. 若要共用資料夾，請選取資料夾，然後按一下 **[!UICONTROL 屬性]** （從工具列）。

1. 在 **[!UICONTROL 資料夾屬性]** 頁面上，從中選擇使用者或群組 **[!UICONTROL 新增使用者]** 清單，指派角色(`Viewer`， `Editor`，或 `Owner`)，然後按一下 **[!UICONTROL 新增]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   您可以指派各種角色，例如 `Editor`， `Owner`，或 `Viewer` 共用資料夾的使用者。 如果您指派 `Owner` 角色至使用者，使用者具有 `Editor` 檔案夾的許可權。 此外，使用者可以與其他人共用資料夾。 如果您指派 `Editor` 角色，則使用者可編輯您私人資料夾中的資產。 如果您指派檢視器角色，則使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾至少有一個成員具有 `Owner` 角色。 因此，管理員無法從私人資料夾中移除所有擁有者成員。 但是，若要從私人資料夾中移除現有的擁有者（以及管理員本身），管理員必須新增另一個使用者作為擁有者。

1. 单击“**[!UICONTROL 保存并关闭]**”。根據您指派的角色，當使用者登入時，會指派一組許可權給使用者您的私人資料夾 [!DNL Assets].
1. 按一下 **[!UICONTROL 確定]** 以關閉確認訊息。
1. 共用資料夾的使用者會在使用者介面中收到共用通知。

1. 按一下 [!UICONTROL 通知] 以開啟通知清單。

   ![通知](assets/notification-icon.png)

1. 按一下管理員共用的私人資料夾專案，開啟該資料夾。

## 私人資料夾刪除 {#delete-private-folder}

您可以選取資料夾並選取「 」，刪除資料夾 [!UICONTROL 刪除] 選項，或使用鍵盤上的退格鍵。

![刪除頂端選單中的選項](assets/delete-option.png)

>[!CAUTION]
>
>如果您從CRXDE Lite中刪除私人資料夾，則多餘的使用者群組會留在存放庫中。

>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則相關聯的使用者群組也會被刪除。
>
>但是，現有的備援、未使用和自動產生的使用者群組可以使用從存放庫中移除 `clean` 編寫執行個體中的JMX方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
