---
title: 如何向选定的用户组授予规则编辑器访问权限？
description: 有各种类型的用户需要掌握各种不同的技能，才能使用自适应Forms。 了解如何根据用户的角色或职能限制用户对规则编辑器的访问权限。
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

有各种类型的用户需要掌握各种不同的技能，才能使用自适应Forms。 虽然专家用户可能拥有处理脚本和复杂规则的正确知识，但可能有基础级别用户，他们只能处理自适应Forms的布局和基本属性。

[!DNL Experience Manager Forms] 允许您根据用户的角色或职能限制用户对规则编辑器的访问权限。 在自适应Forms配置服务设置中，您可以指定 [用户组](forms-groups-privileges-tasks.md) 可以查看和访问规则编辑器。

## 指定可以访问规则编辑器的用户组 {#specify-user-groups-that-can-access-rule-editor}

1. 登录 [!DNL Experience Manager Forms] 作为管理员。
1. 在创作实例中，单击 ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具 ![锤子](assets/hammer-icon.svg) > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**. Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. In [!UICONTROL Web控制台] 窗口，找到并单击 **[!UICONTROL 自适应表单配置服务]**. **[!UICONTROL 自适应表单配置服务]** 对话框。 不更改任何值并单击 **[!UICONTROL 保存]**.

   它会创建一个文件 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 在CRX存储库中。

1. 以管理员身份登录到CRXDE。 打开文件 `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` 进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如，RuleEditorsUserGroup），然后单击 **[!UICONTROL 全部保存]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问，请指定逗号分隔值的列表：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，当某个用户不是指定用户组的一部分时(此处    `RuleEditorsUserGroup`)点按字段，编辑规则图标( ![edit-rules1](assets/edit-rules1.png))在“组件”工具栏中不可用：

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   对具有规则编辑器访问权限的用户可见的组件工具栏：

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   对没有规则编辑器访问权限的用户可见的组件工具栏

   有关将用户添加到组的说明，请参阅 [用户管理和安全性](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

