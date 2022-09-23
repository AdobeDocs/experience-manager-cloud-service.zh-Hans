---
title: 通知用户组
description: 了解如何在Admin Console中创建用户组以管理重要电子邮件通知的接收情况。
feature: Onboarding
role: Admin, User, Developer
source-git-commit: b56bb15f8330deefc11d19e784e36590ef674dd8
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 1%

---


# 通知用户组 {#user-groups}

了解如何在Admin Console中创建用户组以管理重要电子邮件通知的接收情况。

## 概述 {#overview}

Adobe需要不时就其AEMas a Cloud Service环境与用户联系。 除了产品内通知之外，Adobe有时还会使用电子邮件发送通知。 此类电子邮件通知有两种类型：

* **事件通知**  — 这些通知在事件期间或Adobe发现AEMas a Cloud Service环境存在潜在可用性问题时发送。
* **主动通知**  — 当Adobe支持团队成员希望就可能对AEMas a Cloud Service环境有益的优化或推荐提供指导时，将发送这些通知。

为了让正确的用户接收这些通知，您需要配置和分配用户组，如本文档中所述。

## 前提条件 {#prerequisites}

由于用户组是在Admin Console中创建和维护的，因此在为通知创建用户组之前，您必须：

* 有权添加和编辑组成员关系。
* 拥有有效的Adobe Admin Console配置文件。

## 创建新的Cloud Manager产品配置文件 {#create-groups}

要正确设置通知接收，您需要创建两个用户组。 这些步骤只能完成一次。

1. 登录Admin Console: [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. 从 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![用户组](assets/products_services.png)

1. 导航到 **Cloud Manager** 实例。

   ![创建用户组](assets/cloud_manager_instance.png)

1. 您将看到所有已配置的Cloud Manager产品配置文件的列表。

   ![创建用户组](assets/cloud_manager_profiles.png)

1. 单击 **新建用户档案** 并提供以下详细信息：

   * **产品配置文件名称**: `Incident Notification - Cloud Service`
   * **显示名称**: `Incident Notification - Cloud Service`
   * **描述**:Cloud Manager配置文件，用于在事件期间或Adobe发现AEMas a Cloud Service环境存在潜在可用性问题时接收通知的用户

1. 单击“**保存**”。

1. 单击 **新建用户档案** ，并提供以下详细信息：

   * **产品配置文件名称**: `Proactive Notification - Cloud Service`
   * **显示名称**: `Proactive Notification - Cloud Service`
   * **描述**:Cloud Manager配置文件，当Adobe支持团队成员希望就可能的优化或建议以处理AEMas a Cloud Service环境配置提供指导时，将会收到通知的用户

1. 单击“**保存**”。

将创建两个新通知组。

>[!NOTE]
>
>Cloud Manager必须 **产品配置文件名称** 与提供的完全相同。 请复制并粘贴提供的产品配置文件名称，以避免出现错误。 任何偏差或拼写错误都会导致通知未按需要发送。
>
>如果出现错误或尚未定义用户档案，则默认Adobe通知分配给 **Cloud Manager开发人员** 或 **部署管理器** 用户档案。

## 将用户分配给新通知产品配置文件 {#add-users}

创建群组后，您必须分配相应的用户。 您可以在创建新用户或更新现有用户时执行此操作。

### 将新用户添加到群组 {#new-user}

请按照以下步骤添加尚未设置Federated ID的用户。

1. 确定应接收事件通知或主动通知的用户。

1. 登录Admin Console: [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) 如果您尚未登录。

1. 从 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

   ![用户](assets/product_services.png)

1. 如果尚未设置团队成员的Federated ID，请选择 **用户** 选项卡，然后选择 **添加用户**. 否则，跳至部分 [将现有用户添加到群组。](#existing-users)

   ![用户](assets/cloud_manager_add_user.png)

1. 在 **将用户添加到您的团队** 对话框中，输入要添加的用户的电子邮件ID并选择 `Adobe ID` 对于 **ID类型**.

1. 单击 **选择产品** 标题以开始产品选择。

1. 选择 **Adobe Experience Manager as a Cloud Service** 并将一个或两个新组分配给用户。

   * **事件通知 — Cloud Service**
   * **主动通知 — Cloud Service**

1. 单击 **保存** 并向您添加的用户发送欢迎电子邮件。

受邀用户现在将收到通知。 对团队中要接收通知的用户重复这些步骤。

### 将现有用户添加到群组 {#existing-user}

请按照以下步骤添加已存在联合ID的用户。

1. 确定应接收事件通知或主动通知的用户。

1. 登录Admin Console: [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) 如果您尚未登录。

1. 从 **概述** 页面，选择 **Adobe Experience Manager as a Cloud Service** 从 **产品和服务** 卡。

1. 选择 **用户** 选项卡。

1. 如果要添加到通知组的团队成员已存在联合ID，请在列表中找到该用户，然后单击该用户。 否则，跳至部分 [将新用户添加到群组。](#add-user)

1. 在 **产品** 在“用户详细信息”窗口的部分中，单击省略号按钮，然后选择 **编辑**.

1. 在 **编辑产品** ，单击 **选择产品** 标题以开始产品选择。

1. 选择 **Adobe Experience Manager as a Cloud Service** 并将一个或两个新组分配给用户。

   * **事件通知 — Cloud Service**
   * **主动通知 — Cloud Service**

1. 单击 **保存** 并向您添加的用户发送欢迎电子邮件。

受邀用户现在将收到通知。 对团队中要接收通知的用户重复这些步骤。
