---
title: 如何授與規則編輯器存取權給選定的使用者群組？
description: 有多種不同型別的使用者，他們擁有各種不同的技能，能使用最適化Forms。 瞭解如何根據使用者的角色或功能限制使用者的規則編輯器存取權。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 5%

---


# 向选定的用户组授予对规则编辑器的访问权限 {#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

有多種不同型別的使用者，他們擁有各種不同的技能，能使用最適化Forms。 雖然專家使用者可能擁有使用指令碼和複雜規則的正確知識，但可能有基本級別的使用者必須只使用最適化Forms的版面和基本屬性。

[!DNL Experience Manager Forms] 可讓您根據使用者的角色或功能，限制使用者的規則編輯器存取權。 在最適化Forms組態服務設定中，您可以指定 [使用者群組](forms-groups-privileges-tasks.md) 可檢視和存取規則編輯器的屬性。

## 指定可存取規則編輯器的使用者群組 {#specify-user-groups-that-can-access-rule-editor}

1. 登入 [!DNL Experience Manager Forms] 作為管理員。
1. 在作者執行個體中，按一下 ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![槌子](assets/hammer-icon.svg) > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**. Web主控台會在新視窗中開啟。

   ![1-2](assets/1-2.png)

1. 在 [!UICONTROL 網頁主控台] 視窗，找到並按一下 **[!UICONTROL 最適化表單設定服務]**. **[!UICONTROL 最適化表單設定服務]** 對話方塊隨即顯示。 不要變更任何值並按一下 **[!UICONTROL 儲存]**.

   它會建立檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 在CRX-repository中。

1. 以管理員身分登入CRXDE。 開啟檔案 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 進行編輯。
1. 使用下列屬性來指定可存取規則編輯器的群組名稱（例如RuleEditorsUserGroup），然後按一下 **[!UICONTROL 全部儲存]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   若要啟用多個群組的存取權，請指定逗號分隔值清單：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   現在，當使用者不是指定使用者群組的一部分時(此處    `RuleEditorsUserGroup`)點選欄位，編輯規則圖示( ![edit-rules1](assets/edit-rules1.png))在「元件」工具列中無法使用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   具有規則編輯器存取許可權的使用者看得見的元件工具列：

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   沒有規則編輯器存取權的使用者看得見的元件工具列

   如需新增使用者至群組的指示，請參閱 [使用者管理與安全性](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

