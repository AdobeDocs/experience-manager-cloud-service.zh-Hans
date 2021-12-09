---
title: 用于共享资产的专用文件夹
description: 了解如何在 [!DNL Adobe Experience Manager Assets] 并与其他用户共享，并为其分配各种权限。
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
source-git-commit: 2a05822588cdb031a1fe25429910dd44f67f2d36
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---

# 中的专用文件夹 [!DNL Adobe Experience Manager Assets] {#private-folder}

您可以在 [!DNL Adobe Experience Manager Assets] 专门供您使用的用户界面。 您可以将此专用文件夹共享给其他用户，并为其分配各种权限。 根据您分配的权限级别，用户可以在文件夹中执行各种任务，例如查看文件夹中的资产或编辑资产。

>[!NOTE]
>
>专用文件夹至少具有一个具有“所有者”角色的成员。
>
>要创建专用文件夹，您需要读取并修改 [访问控制权限](/help/sites-administering/security.md#permissions-in-aem) 在要创建专用文件夹的父文件夹上。 如果您不是管理员，则在 `/content/dam`. 在这种情况下，请先获取用户ID/组的这些权限，然后再尝试创建专用文件夹。

## 创建和共享专用文件夹  {#create-share-private-folder}

创建和共享专用文件夹：

1. 在 [!DNL Assets] 控制台中，单击 **[!UICONTROL 创建]** 按钮，然后选择 **[!UICONTROL 文件夹]** 中。

   ![创建资产文件夹](assets/create-folder.png)

1. 在 **[!UICONTROL 创建文件夹]** 对话框，输入 `Title` 和 `Name` （可选）。

   选择 **[!UICONTROL 私有]** 复选框，单击 **[!UICONTROL 创建]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   将创建专用文件夹。 您现在可以 [添加资产](add-assets.md#upload-assets) 文件夹，并与其他用户或组共享该文件夹。 在您共享文件夹并为其分配权限之前，文件夹不对任何其他用户可见。

1. 要共享文件夹，请选择文件夹，然后单击 **[!UICONTROL 属性]** 中。

1. 在 **[!UICONTROL 文件夹属性]** ，请从 **[!UICONTROL 添加用户]** 列表，分配角色(`Viewer`, `Editor`或 `Owner`)，然后单击 **[!UICONTROL 添加]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   您可以分配各种角色，例如 `Editor`, `Owner`或 `Viewer` 共享文件夹的用户。 如果您为 `Owner` 角色，则用户具有 `Editor` 文件夹的权限。 此外，用户还可以与他人共享该文件夹。 如果您为 `Editor` 角色，用户可以编辑您专用文件夹中的资产。 如果您为用户分配了查看者角色，则用户只能查看您专用文件夹中的资产。

   >[!NOTE]
   >
   >专用文件夹至少具有一个成员，其中 `Owner` 角色。 因此，管理员无法从专用文件夹中删除所有所有者成员。 但是，要从专用文件夹中删除现有所有者（以及管理员本身），管理员必须将其他用户添加为所有者。

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。根据您分配的角色，用户在登录到时，会为您的专用文件夹分配一组权限 [!DNL Assets].
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭确认消息。
1. 与您共享文件夹的用户在其用户界面中会收到共享通知。

1. 单击 [!UICONTROL 通知] 打开通知列表。

   ![通知](assets/notification-icon.png)

1. 单击管理员共享的专用文件夹的条目以打开该文件夹。

## 删除专用文件夹 {#delete-private-folder}

您可以通过选择文件夹并选择 [!UICONTROL 删除] 选项，或者使用键盘上的Backspace键。

![顶部菜单中的删除选项](assets/delete-option.png)

>[!CAUTION]
>
>如果从CRXDE Lite中删除专用文件夹，则存储库中会保留冗余用户组。

>[!NOTE]
>
>如果使用上述方法从用户界面中删除文件夹，则关联的用户组也会被删除。
>
>但是，可以使用从存储库中删除冗余、未使用和自动生成的现有用户组 `clean` 方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
