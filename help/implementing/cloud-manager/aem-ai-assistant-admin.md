---
title: 在Adobe Experience Manager中配置AI助手
description: 了解如何使用Adobe Experience Manager中的Admin Console设置和配置AI助手。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: a216777f6d5bb3dd1afe5d7cdb88ec41435c0500
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---

# 在Adobe Experience Manager中配置AI助手 {#aem-ai-asst-admin-setup}

管理员必须配置访问权限、权限和设置，组织中的用户才能使用AEM (Adobe Experience Manager) AI助手中的功能。 本文介绍了如何为您的组织启用AI助手、设置所需凭据以及保存配置更改。

**AEM AI Assistant配置过程概述**

配置过程包含以下步骤：

1. [在Adobe Admin Console中创建新产品配置文件](#create-profile)。
1. [启用AI助理产品知识权限](#enable-permission)。
1. [创建新用户组（或使用现有用户组）](#create-user-group)。
1. [将用户添加到用户组](#add-users)。
1. [将产品配置文件分配给用户组](#assign-product-profile)。

**先决条件**

在开始之前，请确保已满足以下先决条件：

* 您在Adobe Admin Console中必须至少具有产品管理员权限。
* 您了解组织的用户管理结构。

## 1 — 在Adobe Admin Console中创建新产品配置文件{#create-profile}

1. 按照Experience Platform文档中的[在Adobe Admin Console中创建新产品配置文件](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile)中的详细说明操作。

1. 创建新的产品配置文件时，您可以为AI助手使用以下建议值。

   | 文本字段 | 建议值 |
   | --- | --- |
   | 产品配置文件名称 | `AEM AI Assistant`（或您的首选描述性名称） |
   | 显示名称（可选） | `AI Assistant` |
   | 描述（可选） | `Product profile for managing AEM AI Assistant access` |
   | 通知 | 根据贵组织的首选项进行配置 |




## 2 — 启用“AI助手产品知识”权限{#enable-permission}

将自定义权限分配给产品配置文件的过程遵循标准Adobe Cloud Manager自定义权限工作流程。

参考文章： [将自定义权限分配给新产品配置文件](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. 在Admin Console中，单击新创建的产品配置文件的名称(`AEM AI Assistant`)

   ![屏幕快照](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. 要查看可编辑权限列表，请单击&#x200B;**权限**&#x200B;选项卡。

1. 在表列表中，找到`AI Assistant Product Knowledge`权限。

   Admin Console中的![AI助手权限选项卡](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. 在权限名称的右侧，单击![铅笔图标或编辑图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg)。

1. 在&#x200B;**编辑AI助理的权限**&#x200B;页面上，打开&#x200B;**AI助理产品知识**&#x200B;切换开关。

   ![AI助手产品知识切换选项的“编辑权限”页面](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. 在页面的右下角，单击&#x200B;**保存**。

   您的产品配置文件现在已启用“AI助手产品知识”权限。


## 3 — 创建新用户组（或使用现有用户组）{#create-user-group}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 创建新用户组]

1. 在Admin Console中，单击&#x200B;**用户** > **用户组**。

   ![用户组](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. 在&#x200B;**用户组**&#x200B;页面上，单击&#x200B;**新建用户组**。

   “用户组”页面上的![新建用户组按钮](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. 在&#x200B;**创建新用户组**&#x200B;页面上，提供以下信息：

   | 选项 | 建议值 |
   | --- | --- |
   | 用户组名称 | `AEM AI Assistant`（或您的首选名称） |
   | 描述（可选） | `User group for managing AEM AI Assistant access` |

   ![创建新的用户组页面](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. 在页面的右下角，单击&#x200B;**保存**。

>[!TAB 使用现有用户组]

如果现有AEM用户组符合AI Assistant访问要求，则可以使用该用户组，而不是创建新组。

>[!ENDTABS]

## 4 — 将用户添加到用户组{#add-users}

1. 执行下列操作之一：

>[!BEGINTABS]

>[!TAB 添加个人用户]

1. 在&#x200B;**用户组**&#x200B;页面的&#x200B;**组名称**&#x200B;表中，单击您新创建的用户组名称或现有用户组名称。

   ![用户组页面显示表中的AEM AI助手用户组名称](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. 在&#x200B;**AEM AI助手**&#x200B;的&#x200B;**用户组**&#x200B;页面中，单击&#x200B;**用户**&#x200B;选项卡，然后单击&#x200B;**添加用户**。

   ![AEM AI Assistant用户组页面，显示“用户”选项卡和“添加用户”按钮](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. 在&#x200B;**`Add users to this user group`**&#x200B;页面上，搜索并选择需要访问AEM AI助手的用户。

   ![将用户添加到此用户组页面](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. 在页面的右下角，单击&#x200B;**保存**。

>[!TAB 批量添加用户]

您可以使用Admin Console中的批量上传功能。

1. 准备包含用户信息的CSV文件。

1. 使用&#x200B;**`Add users by CSV`**&#x200B;选项进行高效的批量添加。

>[!ENDTABS]




## 5 — 将产品配置文件分配给用户组{#assign-product-profile}




