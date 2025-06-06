---
title: 如何提供对aem自适应表单规则编辑器的访问权限以选择用户组？
description: 有多种不同类型的用户具有不同的技能来使用自适应Forms。 了解如何根据用户的角色或职能限制用户对规则编辑器的访问权限。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# 向选定的用户组授予对规则编辑器的访问权限 {#grant-rule-editor-access-to-select-user-groups}

## 概述 {#overview}

有多种不同类型的用户具有不同的技能来使用自适应Forms。 虽然专家用户可能拥有处理脚本和复杂规则的正确知识，但可能有一些基础级别的用户必须仅处理自适应Forms的布局和基本属性。

[!DNL Experience Manager Forms]允许您根据用户的角色或职能限制用户对规则编辑器的访问权限。 在自适应Forms配置服务设置中，您可以指定可以查看和访问规则编辑器的[用户组](forms-groups-privileges-tasks.md)。

## 指定可以访问规则编辑器的用户组 {#specify-user-groups-that-can-access-rule-editor}

1. 以管理员身份登录到[!DNL Experience Manager Forms]。
1. 在创作实例中，单击![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager >工具![锤子](assets/hammer-icon.svg) > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 Web控制台将在新窗口中打开。

   ![1-2](assets/1-2.png)

1. 在[!UICONTROL Web控制台]窗口中，找到并单击&#x200B;**[!UICONTROL 自适应表单配置服务]**。 出现&#x200B;**[!UICONTROL 自适应表单配置服务]**&#x200B;对话框。 不要更改任何值，然后单击&#x200B;**[!UICONTROL 保存]**。

   它在CRX-repository中创建文件`/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config`。

1. 以管理员身份登录到CRXDE。 打开文件`/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config`进行编辑。
1. 使用以下属性指定可以访问规则编辑器的组的名称（例如，RuleEditorsUserGroup），然后单击&#x200B;**[!UICONTROL 全部保存]**。

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   要为多个组启用访问，请指定逗号分隔值列表：

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![创建用户](assets/create_user_new.png)

   现在，当某个用户不是指定用户组的一部分时(此处    `RuleEditorsUserGroup`)点击字段，编辑规则图标(![edit-rules1](assets/edit-rules1.png))在“组件”工具栏中不可用：

   ![componentstolbarwithre](assets/componentstoolbarwithre.png)

   对具有规则编辑器访问权限的用户可见的组件工具栏：

   ![componentstolbarwithoutre](assets/componentstoolbarwithoutre.png)

   对没有规则编辑器访问权限的用户可见的组件工具栏

   有关将用户添加到组的说明，请参阅[用户管理和安全性](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=zh-Hans)。

