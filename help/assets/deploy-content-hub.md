---
title: 部署 [!DNL Content Hub]
description: 了解如何部署和激活Content Hub，并为具有不同类型权限(上传资源和Adobe Express用户)的用户提供访问权限，以及如何为用户提供管理员权限。
role: Admin
exl-id: 58194858-6e1c-460b-bab3-3496176b2851
source-git-commit: 772afa3fa409af63698585e139d1efdc026272d8
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 6%

---

# 部署 Content Hub {#deploy-content-hub}

Content Hub作为Experience Manager Assets as a Cloud Service的一部分提供，用于实现组织及其业务合作伙伴对品牌上内容的访问大众化。

在Experience Manager Assets as a Cloud Service上标记为“已批准”的资源可用于Content Hub上的资源分发。

本文提供了一个端到端的工作流，以向用户提供Content Hub访问权限，包括根据用户的需求提供各种权限。

请观看以下视频，了解如何为Experience Manager Assets启用Content Hub：

>[!VIDEO](https://video.tv.adobe.com/v/3469851)

Content Hub上各种权限的变体包括：

* [Content Hub用户](#onboard-content-hub-users)：访问Content Hub门户上的品牌批准资源。

* [Content Hub管理员](#onboard-content-hub-administrator)：除了访问品牌批准的资源、将资源上传到Content Hub、Adobe Express集成以编辑图像之外，还访问Content Hub上的[配置用户界面](/help/assets/configure-content-hub-ui-options.md)(如果您拥有Adobe Express权限)。

* [有权添加资产的Content Hub用户](#onboard-content-hub-users-add-assets)：除了访问Content Hub门户上的品牌批准资产外，还可以[将资产上传到Content Hub](/help/assets/upload-brand-approved-assets.md)。

* [有权将资源重新混合到新变体的Content Hub用户](#onboard-content-hub-users-remix-assets)： [Adobe Express集成](/help/assets/edit-images-content-hub.md)(如果您拥有Adobe Express权限)，并且有权访问Content Hub门户上的品牌批准资源。

* [Experience Manager Assets用户](#experience-manager-assets-users)：能够在Experience Manager Assets as a Cloud Service上批准资源，以便这些资源可在Content Hub上使用。

下表汇总了可用的Content Hub用户类型、这些用户拥有的权限以及获取这些权限所需的产品配置文件：

| 用户角色 | Content Hub用户 | 有权添加资源的Content Hub用户 | 有权重新组合资源的Content Hub用户 | Content Hub管理员 |
|---------------|----------|----------|-------------------------|---|
| **功能** |
| 在 Content Hub 门户中访问获得品牌批准的资产 | ✓ | ✓ | ✓ | ✓ |
| 从Content Hub门户上传资源 | − | ✓ | ✓ | ✓ |
| 使用Adobe Express集成编辑图像 | − | − | ✓ | − |
| 访问Content Hub配置用户界面 | − | − | − | ✓ |
| **用户需要位于这些产品配置文件中 (Admin Console)** |
| AEM > 传递实例 > AEM Assets 有限用户 | ✓ | ✓ | ✓ | ✓ |
| AEM >生产创作实例> AEM用户 | − | ✓ | ✓ | − |
| AEM > 生产作者实例 > AEM 管理员 | − | − | − | ✓ |
| Adobe Express | − | − | ✓ | − |
| **更多信息** | 查看[Content Hub用户](#onboard-content-hub-users) | 查看有权添加资源的[Content Hub用户](#onboard-content-hub-users-add-assets) | 查看有权将资源重新混合到新变体的[Content Hub用户](#onboard-content-hub-users-remix-assets) | 查看[Content Hub管理员](#onboard-content-hub-administrator) |

>[!NOTE]
>
>[Experience Manager Assets用户](#experience-manager-assets-users)能够在Experience Manager Assets as a Cloud Service环境中批准资源，以便这些资源可在Content Hub上使用。 必须使用Admin Console将这些用户添加到AEM >生产创作实例> AEM用户产品配置文件中。

## 步骤1：使用Cloud Manager启用适用于Experience Manager Assets的Content Hub {#enable-content-hub}


要访问Content Hub门户，管理员首先需要使用Cloud Manager为Experience Manager Assets as a Cloud Service启用Content Hub。

### 权限 {#permissions-edit-program}

您必须具有业务负责人角色才能在Cloud Manager中编辑项目。 有关详细信息，请参阅[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。

要为Experience Manager Assets启用Content Hub：

1. 登录到Cloud Manager。 确保在登录时选择正确的组织。 Cloud Manager列出了您的所有程序。

1. 导航到Experience Manager Assets as a Cloud Service程序，单击更多选项图标(...)，然后选择&#x200B;**[!UICONTROL 编辑程序]**。

   ![在Cloud Manager中编辑项目](assets/edit-program-cloud-manager.png)

1. 在[!UICONTROL 编辑程序]对话框中，选择&#x200B;**[!UICONTROL 解决方案和加载项]**&#x200B;选项卡。

1. 展开&#x200B;**[!UICONTROL Assets]**&#x200B;并选择&#x200B;**[!UICONTROL Content Hub]**。
   ![选择Cloud Manager中的Content Hub](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >如果在选择Content Hub后没有为您启用&#x200B;**[!UICONTROL 更新]**，请确保您已为项目指定上线设置。

1. 单击&#x200B;**[!UICONTROL 更新]**。

Content Hub现已为Experience Manager Assets as a Cloud Service启用。 在生产环境中启用Content Hub后，您将无法以自助方式禁用它。

>[!NOTE]
>
>您最多可以对250个Content Hub用户访问和使用Content Hub。 如果您还有其他问题，请联系您的Adobe代表。


如果您是Experience Manager Assets的新用户，请单击&#x200B;**[!UICONTROL 添加程序]**，然后提供程序详细信息（程序名称，为生产设置），然后单击&#x200B;**[!UICONTROL 继续]**。 然后在&#x200B;**[!UICONTROL 解决方案和加载项]**&#x200B;选项卡中选择&#x200B;**[!UICONTROL Assets]**&#x200B;和&#x200B;**[!UICONTROL Content Hub]**。

### Admin Console上的Content Hub实例和产品配置文件{#content-hub-instance-product-profile}

使用Cloud Manager[为Assets as a Cloud Service启用Content Hub](#enable-content-hub)后，Admin Console上的AEM Assets as a Cloud Service中创建了一个新实例，后缀为`delivery`：

![Content Hub的新实例](assets/new-instance-content-hub.png)

>[!NOTE]
>
>如果您在2024年8月14日之前配置了Content Hub，则会创建新实例，并将`contenthub`作为后缀。

请注意，Content Hub的实例名称中没有`author`或`publish`。

单击实例名称以查看Content Hub产品配置文件。

![Content Hub产品配置文件](assets/content-hub-product-profile.png)

>[!NOTE]
>
>如果您在2024年8月14日之前配置了Content Hub，则Content Hub产品配置文件在`contenthub`之后提及`Limited Users`，而不是`delivery`。

## 步骤2：载入Content Hub管理员 {#onboard-content-hub-administrator}

除了访问品牌批准的资源、将资源上传到Content Hub、Adobe Express集成以编辑图像之外，Content Hub管理员还可以访问Content Hub上的[配置用户界面](/help/assets/configure-content-hub-ui-options.md)(如果您拥有Adobe Express权限)。

要载入Content Hub管理员：

1. [访问并单击Content Hub用户产品配置文件](#content-hub-instance-product-profile)。

1. 单击&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将用户或用户组添加到产品配置文件。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

1. 将用户添加到Content Hub产品配置文件后，单击Admin Console产品列表中的AEM as a Cloud Service产品名称以访问Experience Manager Assets产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击管理员产品配置文件，然后单击&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将用户添加到产品配置文件。
   ![管理员产品配置文件](assets/aem-cs-admin-product-profile.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

## 步骤3：载入Content Hub用户 {#onboard-content-hub-users}

Content Hub用户可以访问门户上可用的资源，但无法添加任何新资源或修改现有资源。

载入Content Hub用户：

1. [访问并单击Content Hub用户产品配置文件](#content-hub-instance-product-profile)。

1. 单击&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将用户或用户组添加到产品配置文件。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

这些用户现在可以访问Content Hub门户中提供的资源。

>[!NOTE]
>
>可以使用所有高级企业功能，如与外部身份提供程序同步。

### 如何访问 Content Hub？ {#access-content-hub}

可通过以下方式访问Content Hub：

* 使用以下链接访问 Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登录到`experience.adobe com`，然后单击&#x200B;**[!UICONTROL 快速访问]**&#x200B;部分中的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub Access](assets/access-content-hub.png)

* 登录到`experience.adobe com`，然后单击产品切换器中可用的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub 访问方法 3](assets/access-content-hub-alternate.png)

### 禁用发送给用户的电子邮件通知 {#disable-email-notifications}

如果管理员在将其添加到Content Hub产品配置文件时需要禁用发送给用户的电子邮件通知：

单击产品配置文件名称旁边的搜索图标，并禁用&#x200B;**[!UICONTROL 通过电子邮件通知用户]**&#x200B;切换开关。

![禁用电子邮件通知](assets/disable-email-notifications.png)


## 步骤4：让有权添加资产的Content Hub用户上线（可选） {#onboard-content-hub-users-add-assets}

有权添加资产的Content Hub用户可以[将新的品牌批准的资产](/help/assets/upload-brand-approved-assets.md)上传到Content Hub。

要载入具有添加用户权限的Content Hub用户，请执行以下操作：

1. [将用户添加到Content Hub产品配置文件后](#onboard-content-hub-users)，单击Admin Console产品列表中的AEM as a Cloud Service产品名称以访问Experience Manager Assets产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击“用户”产品配置文件，然后单击“**[!UICONTROL 添加用户]**”以将该用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

## 步骤4：让有权将资源重新混合到新变体的Content Hub用户上线（可选） {#onboard-content-hub-users-remix-assets}

有权将资源重新混合到新变体的Content Hub用户可以[使用Adobe Express修改现有资源并将资源保存到存储库](/help/assets/edit-images-content-hub.md)。 仅当用户拥有Adobe Express权限时，使用Adobe Express编辑资源才可用。

要载入有权将资产重新混合到新变体的Content Hub用户，请执行以下操作：

1. [将用户添加到Content Hub产品配置文件后](#onboard-content-hub-users)，单击Admin Console产品列表中的AEM as a Cloud Service产品名称以访问Experience Manager Assets产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击“用户”产品配置文件，然后单击“**[!UICONTROL 添加用户]**”以将该用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

## Experience Manager Assets用户 {#experience-manager-assets-users}

Experience Manager Assets用户可以批准AEM as a Cloud Service上的资源，以便这些资源在Content Hub上可用。

配置Experience Manager Assets用户：

1. 通过单击Experience Manager Assets产品列表中的AEM as a Cloud Service产品名称，访问Admin Console产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

   Admin Console显示AEM as a Cloud Service的两个产品配置文件：管理员和用户。
1. 单击“用户”产品配置文件，然后单击“**[!UICONTROL 添加用户]**”以将该用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-cs-user-product-profile.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

   >[!NOTE]
   >
   > 您无需添加到Experience Manager Assets用户的[Content Hub产品配置文件](#onboard-content-hub-users)。
