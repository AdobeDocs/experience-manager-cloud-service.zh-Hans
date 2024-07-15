---
title: 如何配置Azure存储？
description: 了解如何将表单与Azure Storage Server集成。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# 配置[!DNL Azure]存储 {#configure-azure-storage}


![数据集成](assets/data-integeration.png)

[[!DNL Experience Manager Forms] 数据集成](data-integration.md)提供[!DNL Azure]存储配置以将表单与[!DNL Azure]存储服务集成。 表单数据模型(FDM)可用于创建与[!DNL Azure]服务器交互以启用业务工作流的自适应Forms。 例如：

* 在提交自适应表单时将数据写入[!DNL Azure]。
* 通过表单数据模型(FDM)中定义的自定义实体在[!DNL Azure]中写入数据，反之亦然。
* 查询[!DNL Azure]服务器以获取数据并预填充Adaptive Forms。
* 从[!DNL Azure]服务器读取数据。

## 创建[!DNL Azure]存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您拥有[!DNL Azure]存储帐户和访问密钥，以授权对[!DNL Azure]存储帐户的访问。

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure存储]**。
1. 选择要创建配置的文件夹，然后选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中指定配置的标题。
1. 在&#x200B;**[!UICONTROL Azure存储帐户]**&#x200B;字段中指定[!DNL Azure]存储帐户的名称。
1. 在&#x200B;**[!UICONTROL Azure访问密钥]**&#x200B;字段中指定用于访问Azure存储帐户的密钥，然后选择&#x200B;**[!UICONTROL 保存]**。

## 创建表单数据模型 {#create-azure-form-data-model}

创建[!DNL Azure]存储配置后，您可以[创建表单数据模型](create-form-data-models.md)。 创建表单数据模型(FDM)时，在&#x200B;**[!UICONTROL 数据Source配置]**&#x200B;字段中指定包含[!DNL Azure]配置的文件夹。 然后，您可以从指定文件夹名称中存在的配置列表中选择配置。

### 将[!DNL Azure]服务添加到表单数据模型 {#add-azure-services}

创建表单数据模型(FDM)和数据模型对象后，您可以将[!DNL Azure]服务添加到表单数据模型(FDM)。

要添加[!DNL Azure]服务：

1. 在编辑模式下，从左窗格的&#x200B;**[!UICONTROL 服务]**&#x200B;部分中选择服务，然后选择&#x200B;**[!UICONTROL 添加选定项]**。 所选服务显示在表单数据模型(FDM)的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡中。

   ![添加选定的服务](assets/select-services.png)

1. 在&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡中，选择该服务并&#x200B;**[!UICONTROL 编辑属性]**。 根据服务，定义服务的输入或输出模型对象。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存表单数据模型(FDM)。

   下表描述了可用的[!DNL Azure]服务：

   <table>
    <tbody>
     <tr>
      <th><strong>服务名称</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>从Azure获取Blob</td>
      <td>使用ID或名称检索作为Azure存储中的Blob存储的数据</td>
     </tr>
     <tr>
      <td>从Azure获取具有二进制文件URL的Blob</td>
      <td>使用ID或名称在Azure存储中检索作为Blob存储的数据以及二进制文件的URL</td>
     </tr>
     <tr>
      <td>在Azure中保存Blob</td>
      <td>使用Blob ID将数据保存在Azure存储中</td>
     </tr>
     <tr>
      <td>在Azure中更新Blob</td>
      <td>使用Blob ID更新Azure存储中的数据</td>
     </tr>
     <tr>
      <td>从Azure检索Blob ID列表</td>
      <td>根据输入请求中定义的编号从Azure检索Blob ID列表。</td>
     </tr>
     <tr>
      <td>从Azure检索Blob的SAS URL</td>
      <td>根据输入请求中的Blob ID从Azure检索Blob的SAS URL。</td>
     </tr>
     <tr>
      <td>从Azure中删除Blob</td>
      <td>使用Blob ID从Azure存储中删除数据</td>
     </tr>
    </tbody>
   </table>

### 将数据模型对象属性定义为搜索键 {#define-data-model-object-as-metadata}

要将数据模型对象属性定义为搜索键，请执行以下操作：

1. 在&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡中，选择数据模型对象属性，然后选择&#x200B;**[!UICONTROL 编辑属性]**。
1. 将&#x200B;**[!UICONTROL 搜索键]**&#x200B;切换选项切换到“开启”状态。 此选项仅适用于主要数据类型。
1. 选择&#x200B;**[!UICONTROL 完成]**，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存表单数据模型(FDM)。

将数据模型对象属性定义为搜索键后，哈希值存储在Azure索引标记中，Base64编码值存储在Azure元数据中。

>[!NOTE]
>
>每个Azure实体只允许使用10个搜索键，因为Azure仅允许每个Blob使用10个标记，并且标记为搜索键的属性值在经过哈希处理后存储在Azure索引标记中。

<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->