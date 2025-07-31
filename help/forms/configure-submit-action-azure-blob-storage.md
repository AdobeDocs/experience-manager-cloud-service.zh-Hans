---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Azure Blob Storage与AEM Forms集成，将数据提交到Azure Storage，在AEM Forms中创建Azure Storage配置，在自适应Forms中使用Azure Blob Storage提交操作
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
title: 如何为自适应表单配置提交操作？
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 46%

---

# 将自适应表单提交到 Azure Blob Storage

**[!UICONTROL 提交到 Azure Blob 存储]**&#x200B;提交操作将自适应表单与 Microsoft® Azure 门户连接起来。您可以将表单数据、文件、附件或记录文档提交到连接的Azure存储容器。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/aem-forms-submit-action.md)文章中了解有关这些选项的更多信息。

## 优点

Azure Blob Storage与AEM Forms集成的一些优势包括：

* 它有助于简化将自适应表单数据、文件、附件和记录文档提交到Azure存储容器的过程。
* 它使用Azure Blob Storage对自适应表单提交进行集中和有组织的存储。

## 将AEM Forms与Microsoft® Azure Blob Storage连接

要在自适应Forms提交操作中使用Azure Blob Storage，请执行以下操作：

1. [创建 Azure Blob 存储容器](#create-a-azure-blob-storage-container-create-azure-configuration)：它将 AEM Forms 连接到 Azure 存储容器。
2. [在自适应表单中使用 Azure 存储配置](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af)：它将自适应表单连接到配置的 Azure 存储容器。

### 创建 Azure Blob 存储容器 {#create-azure-configuration}

要将 AEM Forms 连接到 Azure 存储容器，请执行以下操作：

1. 转到 **AEM Forms 创作**&#x200B;实例 > **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure 存储]**。
1. 选定 **[!UICONTROL Azure 存储]**&#x200B;后，您将重定向到 **[!UICONTROL Azure 存储浏览器]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。这将显示“创建 Azure 存储配置”向导。

   ![Azure 存储配置](/help/forms/assets/azure-storage-configuration.png)

1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL Azure 存储帐户]**&#x200B;和 **[!UICONTROL Azure 访问密钥]**。

   * 您可以从 Microsoft® Azure 门户中的存储帐户检索 `Azure Storage Account`名称和 `Azure Access key`。
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. 单击&#x200B;**[!UICONTROL 保存]**。

现在，您可以在自适应表单中将此 Azure 存储容器配置用于提交操作。

### 在自适应表单中使用 Azure 存储配置 {#use-azure-storage-configuartion-in-af}

您可以在自适应表单中使用创建的Azure存储容器配置，以在Azure存储容器中保存数据或生成的记录文档。

>[!NOTE]
>
> * 为自适应表单选择相同的[!UICONTROL 配置容器]，您已在其中创建 OneDrive 存储。
> * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

>[!BEGINTABS]

>[!TAB 基础组件]

执行以下步骤，在基于基础组件的自适应表单中使用Azure存储容器配置，如下所示：

1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 提交到Azure Blob存储]**。

   ![Azure Blob Storage GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%，height=50%}

   您还可以将记录文档(DoR)保存到Azure Blob存储中。

1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

提交表单时，数据将保存在指定的 Azure 存储容器配置中。
用于保存数据的文件夹结构是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!TAB 核心组件]

执行以下步骤，在基于核心组件的自适应表单中使用Azure存储容器配置，如下所示：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 提交到Azure Blob存储]**。

   ![Azure Blob 存储 GIF](/help/forms/assets/azure-submit-video.gif)

   您还可以将记录文档(DoR)保存到Azure Blob存储中。

1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

提交表单时，数据将保存在指定的 Azure 存储容器配置中。
用于保存数据的文件夹结构是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!TAB 通用编辑器]

执行以下步骤，使用在Universal Editor中创作的自适应表单中的Azure存储容器配置：

1. 打开自适应表单进行编辑。
1. 单击编辑器上的&#x200B;**编辑表单属性**扩展。
出现**表单属性**&#x200B;对话框。

   >[!NOTE]
   >
   > * 如果您在通用编辑器界面中未看到&#x200B;**编辑表单属性**&#x200B;图标，请在Extension Manager中启用&#x200B;**编辑表单属性**&#x200B;扩展。
   > * 请参阅[Extension Manager功能亮点](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)一文，了解如何在通用编辑器中启用或禁用扩展。

1. 单击&#x200B;**提交**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 提交到Azure Blob存储]**提交操作。
   ![Azure Blob存储](/help/forms/assets/azure-blob-storage-ue.png)

   如果选择&#x200B;**保存具有原始名称的附件**，则附件会使用其原始文件名存储在文件夹中。 您还可以将记录文档(DoR)保存到Azure Blob存储中。

1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存提交设置。

提交表单时，数据将保存在指定的 Azure 存储容器配置中。
用于保存数据的文件夹结构是 `/configuration_container/form_name/year/month/date/submission_id/data`。

>[!ENDTABS]

## 相关文章

{{af-submit-action}}
