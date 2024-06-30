---
title: 部署 [!DNL Content Hub]
description: 了解如何部署和激活Content Hub，并为具有不同类型权限(上传资源、Adobe Express用户)的用户提供访问权限，以及如何为用户提供管理员权限。
role: Admin
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 0%

---


# 部署Content Hub {#deploy-content-hub}

![部署Content Hub](assets/deploy-content-hub.png)

Content Hub作为Experience Manager Assets as a Cloud Service的一部分提供，用于实现组织及其业务合作伙伴对品牌上内容的访问大众化。

在Experience Manager Assetsas a Cloud Service上标记为“已批准”的资源可用于Content Hub上的资源分发。

本文提供了一个端到端的工作流，以向用户提供Content Hub访问权限，包括根据用户的需求提供各种权限。

Content Hub上各种权限的变体包括：

* [Content Hub用户](#onboard-content-hub-users)：在Content Hub门户上访问品牌批准的资源。

* [Content Hub管理员](#onboard-content-hub-administrator)：访问 [配置用户界面](/help/assets/configure-content-hub-ui-options.md) 在Content Hub上，除了访问品牌批准的资源、将资源上传到Content Hub、Adobe Express集成以编辑图像(如果您具有Adobe Express权限)之外。

* [有权添加资源的Content Hub用户](#onboard-content-hub-users-add-assets)：能够 [将资源上传到Content Hub](/help/assets/upload-brand-approved-assets.md) 除了访问Content Hub门户上的品牌批准资产之外。

* [有权将资源重新混合到新变体的Content Hub用户](#onboard-content-hub-users-remix-assets)： [Adobe Express集成](/help/assets/edit-images-content-hub.md) (如果您拥有Adobe Express权限)以及访问Content Hub portal上的品牌批准资源。

* [Experience Manager Assets用户](#experience-manager-assets-users)：能够在Experience Manager Assets上批准资源as a Cloud Service，以便这些资源在Content Hub上可用。

## 步骤1：使用Cloud Manager启用适用于Experience Manager Assets的Content Hub {#enable-content-hub}

要访问Content Hub门户，管理员首先需要使用Cloud Manager启用Content Hub for Experience Manager Assetsas a Cloud Service。 执行以下步骤：

1. 登录到Cloud Manager。 确保在登录时选择正确的组织。 Cloud Manager列出了您的所有程序。

1. 导航到Experience Manager Assetsas a Cloud Service程序，单击更多选项图标(...)，然后选择 **[!UICONTROL 编辑项目]**.

   ![在Cloud Manager中编辑项目](assets/edit-program-cloud-manager.png)

1. 在 [!UICONTROL 编辑项目] 对话框，选择 **[!UICONTROL 解决方案和加载项]** 选项卡。

1. 展开 **[!UICONTROL Assets]** 并选择 **[!UICONTROL Content Hub]**.
   ![在Cloud Manager中选择Content Hub](assets/edit-program-cloud-manager-content-hub.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。

Content Hub现已为Experience Manager Assetsas a Cloud Service启用。

如果您是Experience Manager Assets的新用户，请单击 **[!UICONTROL 添加项目]** 然后提供项目详细信息（项目名称，为生产设置）并单击 **[!UICONTROL 继续]**. 然后，您可以选择 **[!UICONTROL Assets]** 和 **[!UICONTROL Content Hub]** 在 **[!UICONTROL 解决方案和加载项]** 选项卡。

### Admin Console上的Content Hub实例和产品配置文件{#content-hub-instance-product-profile}

之后 [使用Cloud Manager为Assets启用Content Hubas a Cloud Service](#enable-content-hub)，则会在AEM Assets中新建一个实例，as a Cloud ServiceAdmin Console于 `contenthub` 作为后缀：

![Content Hub的新实例](assets/new-instance-content-hub.png)

请注意，不存在 `author` 或 `publish` 在Content Hub的实例名称中。

单击实例名称以查看Content Hub产品配置文件。

![Content Hub产品配置文件](assets/content-hub-product-profile.png)

## 步骤2：载入Content Hub管理员 {#onboard-content-hub-administrator}

Content Hub管理员可以访问 [配置用户界面](/help/assets/configure-content-hub-ui-options.md) 在Content Hub上，除了访问品牌批准的资源、将资源上传到Content Hub、Adobe Express集成以编辑图像(如果您具有Adobe Express权限)之外。

要载入Content Hub管理员：

1. [访问并单击Content Hub用户产品配置文件](#content-hub-instance-product-profile).

1. 单击 **[!UICONTROL 添加用户]** 以将用户或用户组添加到产品配置文件。

1. 单击 **[!UICONTROL 保存]** 以保存更改。

1. 将用户添加到Content Hub产品配置文件后，单击Admin Console上产品列表中的AEM as a Cloud Service产品名称以访问Experience Manager Assets产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   ![AEM as a Cloud Service的产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击管理员产品配置文件，然后单击 **[!UICONTROL 添加用户]** 以将用户添加到产品配置文件。
   ![管理员产品配置文件](assets/aem-cs-admin-product-profile.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。

## 步骤3：载入Content Hub用户 {#onboard-content-hub-users}

Content Hub用户可以访问门户上可用的资源，但无法添加任何新资源或修改现有资源。

载入Content Hub用户：

1. [访问并单击Content Hub用户产品配置文件](#content-hub-instance-product-profile).

1. 单击 **[!UICONTROL 添加用户]** 以将用户或用户组添加到产品配置文件。

1. 单击 **[!UICONTROL 保存]** 以保存更改。

这些用户现在可以访问Content Hub门户中提供的资源。

>[!NOTE]
>
>可以使用所有高级企业功能，如与外部身份提供程序同步。

使用Admin Console添加适当的用户后，这些用户可以使用以下链接访问Content Hub：

`https://experience.adobe.com/#/assets/contenthub`

### 禁用发送给用户的电子邮件通知 {#disable-email-notifications}

如果管理员在将其添加到Content Hub产品配置文件时需要禁用发送给用户的电子邮件通知：

单击产品配置文件名称旁边的搜索图标，然后禁用 **[!UICONTROL 通过电子邮件通知用户]** 切换。

![禁用电子邮件通知](assets/disable-email-notifications.png)


## 步骤4：让有权添加资产的Content Hub用户上线（可选） {#onboard-content-hub-users-add-assets}

有权添加资源的Content Hub用户可以 [将品牌批准的新资产上传到Content Hub](/help/assets/upload-brand-approved-assets.md).

要载入具有添加用户权限的Content Hub用户，请执行以下操作：

1. [将用户添加到Content Hub产品配置文件后](#onboard-content-hub-users)中，通过单击Admin Console上产品列表中的Experience Manager Assets产品名称来访问AEM as a Cloud Service产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   ![AEM as a Cloud Service的产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击用户产品配置文件，然后单击 **[!UICONTROL 添加用户]** 以将用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。

## 步骤4：让有权将资源重新混合到新变体的Content Hub用户上线（可选） {#onboard-content-hub-users-remix-assets}

有权将资源重新组合到新变体的Content Hub用户可以 [使用Adobe Express修改现有资源并将资源保存到存储库](/help/assets/edit-images-content-hub.md). 仅当Adobe Express具有Adobe Express权限时，使用User编辑资源才可用。

要载入有权将资产重新混合到新变体的Content Hub用户，请执行以下操作：

1. [将用户添加到Content Hub产品配置文件后](#onboard-content-hub-users)中，通过单击Admin Console上产品列表中的Experience Manager Assets产品名称来访问AEM as a Cloud Service产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   ![AEM as a Cloud Service的产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击用户产品配置文件，然后单击 **[!UICONTROL 添加用户]** 以将用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。

## Experience Manager Assets用户 {#experience-manager-assets-users}

Experience Manager Assets用户可以批准AEM as a Cloud Service上的资源，以便这些资源在Content Hub上可用。

配置Experience Manager Assets用户：

1. 通过单击Admin Console上产品列表中的Experience Manager Assets产品名称来访问AEM as a Cloud Service产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   ![AEM as a Cloud Service的产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击用户产品配置文件，然后单击 **[!UICONTROL 添加用户]** 以将用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击 **[!UICONTROL 保存]** 以保存更改。

   >[!NOTE]
   >
   > 您无需添加到 [Content Hub产品配置文件](#onboard-content-hub-users) Experience Manager Assets用户。



