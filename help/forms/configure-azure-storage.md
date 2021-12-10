---
title: 如何配置Azure存储？
description: 了解如何将表单与Azure存储服务器集成。
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---

# 配置 [!DNL Azure] 存储 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 提供 [!DNL Azure] 存储配置，将表单与 [!DNL Azure] 存储服务。 表单数据模型可用于创建与交互的自适应Forms [!DNL Azure] 服务器启用业务工作流。 例如：

* 将数据写入 [!DNL Azure] 在自适应表单提交时。
* 将数据写入 [!DNL Azure] 通过在表单数据模型中定义的自定义实体，反之亦然。
* 查询 [!DNL Azure] 服务器，并预填充自适应Forms。
* 从读取数据 [!DNL Azure] 服务器。

## 创建 [!DNL Azure] 存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您具有 [!DNL Azure] 存储帐户和访问密钥，以授权访问 [!DNL Azure] 存储帐户。

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure存储]**.
1. 选择要创建配置的文件夹，然后点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 存储帐户 **[!UICONTROL Azure存储帐户]** 字段。
1. 在中指定用于访问Azure存储帐户的密钥 **[!UICONTROL Azure访问密钥]** 字段和点按 **[!UICONTROL 保存]**.

## 创建表单数据模型 {#create-azure-form-data-model}

创建 [!DNL Azure] 存储配置，您可以 [创建表单数据模型](create-form-data-models.md). 指定包含 [!DNL Azure] 配置 **[!UICONTROL 数据源配置]** 字段。 然后，您可以从指定文件夹名称中存在的配置列表中选择配置。

### 添加 [!DNL Azure] 表单数据模型服务 {#add-azure-services}

创建表单数据模型和数据模型对象后，可以添加 [!DNL Azure] 服务到表单数据模型。

添加 [!DNL Azure] 服务：

1. 在编辑模式下，从 **[!UICONTROL 服务]** 部分，然后点按 **[!UICONTROL 添加选定项]**. 所选服务显示在 **[!UICONTROL 服务]** 选项卡。

   ![添加选定的服务](assets/select-services.png)

1. 在 **[!UICONTROL 服务]** 选项卡，选择服务和 **[!UICONTROL 编辑属性]**. 根据服务，定义服务的输入或输出模型对象。

1. 点按 **[!UICONTROL 保存]** 保存表单数据模型。

   下表描述了 [!DNL Azure] 服务：

   <table>
    <tbody>
     <tr>
      <th><strong>服务名称</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>从Azure获取Blob</td>
      <td>使用ID或名称检索Azure存储中作为Blob存储的数据</td>
     </tr>
     <tr>
      <td>从Azure获取包含二进制文件URL的Blob</td>
      <td>使用ID或名称，检索Azure存储中用于二进制文件的URL作为Blob存储的数据</td>
     </tr>
     <tr>
      <td>在Azure中保存Blob</td>
      <td>使用Blob ID在Azure存储中保存数据</td>
     </tr>
     <tr>
      <td>在Azure中更新Blob</td>
      <td>使用Blob ID更新Azure存储中的数据</td>
     </tr>
     <tr>
      <td>从Azure检索Blob ID列表</td>
      <td>根据输入请求中定义的数字，从Azure检索Blob ID列表。</td>
     </tr>
     <tr>
      <td>从Azure中检索Blob的SAS URL</td>
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

1. 在 **[!UICONTROL 模型]** 选项卡，选择数据模型对象属性并点按 **[!UICONTROL 编辑属性]**.
1. 切换 **[!UICONTROL 搜索键]** 将选项切换为“开”状态。 此选项仅适用于主数据类型。
1. 点按 **[!UICONTROL 完成]** 然后点按 **[!UICONTROL 保存]** 保存表单数据模型。

将数据模型对象属性定义为搜索键后，这些键将作为元数据保存在Azure存储中。
