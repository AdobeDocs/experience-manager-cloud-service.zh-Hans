---
title: 在Cloud Manager中管理外部存储库的访问令牌
description: 了解如何在AEM Cloud Manager中查看、编辑和删除用于自带Git的访问令牌。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="率先采用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#manage-access-tokens"
source-git-commit: 9e2be3cabe0a93e6e357ceb5ecf4950c25d034d0
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 3%

---


# 管理外部存储库的访问令牌 {#manage-access-tokens}

Cloud Manager使用访问令牌管理在外部Git平台上托管的存储库。 以前，如果令牌过期，则必须重新载入关联的存储库才能保持可操作性。

现在，通过&#x200B;**管理访问令牌**&#x200B;功能，您可以更高效地管理令牌。 您可以查看、重命名或删除连接到受支持的外部Git提供程序（包括GitHub Enterprise、GitLab、Bitbucket和Azure DevOps）的令牌。

另请参阅[在Cloud Manager中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

>[!NOTE]
>
>本文中介绍的功能只能通过早期采用计划获得。 有关更多详细信息，以及要注册为早期采用者，请参阅[自带Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)。

## 查看访问令牌 {#view-access-tokens}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要管理其自带Git访问令牌的程序。
1. 在侧菜单的&#x200B;**程序**&#x200B;下，单击![文件夹大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **存储库**。
1. 在页面的右上角附近，单击&#x200B;**管理访问令牌**。

   仅当您的程序使用“自带Git”功能时，**管理访问令牌**&#x200B;按钮才可见。

   ![管理访问令牌对话框，其中列出一个处于活动状态的令牌和一个处于非活动状态的令牌](/help/implementing/cloud-manager/managing-code/assets/access-tokens-manage.png)

1. 在&#x200B;**管理访问令牌**&#x200B;对话框中：
   * 列出所有访问令牌。
   * 您可以&#x200B;**编辑**&#x200B;任何访问令牌。
   * 您只能&#x200B;**删除**&#x200B;当前未使用&#x200B;*的访问令牌*。 如果令牌正在使用中，则![删除大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)按钮将被禁用。

## 编辑访问令牌 {#edit-access-tokens}

1. 在&#x200B;**管理访问令牌**&#x200B;对话框中，单击令牌名称右侧的![编辑图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。
1. 在&#x200B;**编辑访问令牌**&#x200B;对话框的&#x200B;**令牌名称**&#x200B;文本字段中，更新令牌名称。

   无法编辑访问令牌密码本身。

   ![编辑访问令牌对话框](/help/implementing/cloud-manager/managing-code/assets/access-tokens-edit.png)

1. 如果令牌正在使用中，则会出现通知，警告您所有关联的存储库都会自动重新验证。

1. 单击&#x200B;**更新**&#x200B;以保存更改。

## 删除访问令牌 {#delete-access-token}

1. 在&#x200B;**管理访问令牌**&#x200B;对话框中，单击令牌名称右侧![删除图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)

   对于当前正在使用的令牌，该图标被禁用（![删除大纲图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)）。

1. 在&#x200B;**删除访问令牌**&#x200B;对话框中，单击&#x200B;**删除**&#x200B;以永久删除该令牌。
