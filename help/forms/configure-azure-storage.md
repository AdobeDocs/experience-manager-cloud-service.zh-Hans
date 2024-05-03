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

# 配置 [!DNL Azure] 存储 {#configure-azure-storage}


![数据集成](assets/data-integeration.png)

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 提供 [!DNL Azure] 用于集成表单的存储配置 [!DNL Azure] 存储服务。 表单数据模型(FDM)可用于创建与之交互的自适应Forms [!DNL Azure] 服务器启用业务工作流。 例如：

* 将数据写入 [!DNL Azure] 在提交自适应表单时。
* 将数据写入 [!DNL Azure] 通过表单数据模型(FDM)中定义的自定义实体，反之亦然。
* 查询 [!DNL Azure] 数据服务器并预填充Adaptive Forms。
* 从读取数据 [!DNL Azure] 服务器。

## 创建 [!DNL Azure] 存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您已 [!DNL Azure] 存储帐户和一个访问密钥，用于授权访问 [!DNL Azure] 存储帐户。

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure存储]**.
1. 选择一个文件夹以创建配置，然后选择 **[!UICONTROL 创建]**.
1. 在中指定配置的标题 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 中的存储帐户 **[!UICONTROL Azure存储帐户]** 字段。
1. 指定用于访问Azure存储帐户的密钥 **[!UICONTROL Azure访问密钥]** 字段并选择 **[!UICONTROL 保存]**.

## 创建表单数据模型 {#create-azure-form-data-model}

创建 [!DNL Azure] 存储配置，您可以 [创建表单数据模型](create-form-data-models.md). 指定包含 [!DNL Azure] 中的配置 **[!UICONTROL 数据源配置]** 创建表单数据模型(FDM)时的字段。 然后，您可以从指定文件夹名称中存在的配置列表中选择配置。

### 添加 [!DNL Azure] 表单数据模型的服务 {#add-azure-services}

创建表单数据模型(FDM)和数据模型对象后，您可以添加 [!DNL Azure] 表单数据模型(FDM)的服务。

添加 [!DNL Azure] 服务：

1. 在“编辑”模式下，从 **[!UICONTROL 服务]** 部分，然后选择 **[!UICONTROL 添加选定项]**. 所选服务将显示在 **[!UICONTROL 服务]** 表单数据模型(FDM)的选项卡。

   ![添加所选服务](assets/select-services.png)

1. 在 **[!UICONTROL 服务]** 选项卡，选择服务并 **[!UICONTROL 编辑属性]**. 根据服务，定义服务的输入或输出模型对象。

1. 选择 **[!UICONTROL 保存]** 以保存表单数据模型(FDM)。

   下表描述了可用的 [!DNL Azure] 服务：

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

1. 在 **[!UICONTROL 模型]** 选项卡，选择数据模型对象属性，然后选择 **[!UICONTROL 编辑属性]**.
1. 切换 **[!UICONTROL 搜索键]** 将选项切换到“开”状态。 此选项仅适用于主要数据类型。
1. 选择 **[!UICONTROL 完成]** 然后选择 **[!UICONTROL 保存]** 以保存表单数据模型(FDM)。

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