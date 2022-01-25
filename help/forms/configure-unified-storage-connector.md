---
title: 如何为AEM Forms配置统一存储连接器？
description: 了解如何管理AEM Forms的统一存储连接器。 使用统一存储连接器将AEM Forms连接到外部数据存储。
source-git-commit: da3cef0a0a28dd16e627a157f02bbe6a84f59da5
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---


# 管理AEM Forms的统一存储连接器 {#manage-unified-storage-connector}

您可以使用Unified Storage Connector将AEM Forms连接到外部数据存储。

例如，您可以填写自适应表单中字段的值，并将其提交到AEM工作流。 您可以进一步配置AEM工作流，以将数据存储在外部存储中，如Microsoft Azure存储服务器。 使用统一存储连接器在AEM工作流和外部存储之间创建连接。

## 将AEM工作流与Microsoft Azure存储服务器连接 {#connect-workflows-with-azure}

创建Azure存储配置，并使用统一存储连接器引用该配置。 然后，您可以配置AEM工作流模型以将数据存储外部化，以将其连接到Azure存储服务器。

### 创建 [!DNL Azure] 存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您具有 [!DNL Azure] 存储帐户和访问密钥，以授权访问 [!DNL Azure] 存储帐户。

执行以下步骤以创建 [!DNL Azure] 存储配置：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure存储]**.
1. 选择要创建配置的文件夹，然后点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 存储帐户 **[!UICONTROL Azure存储帐户]** 字段。
1. 在中指定用于访问Azure存储帐户的密钥 **[!UICONTROL Azure访问密钥]** 字段和点按 **[!UICONTROL 保存]**.

### 为AEM工作流配置统一存储连接器 {#configure-unified-storage-connector-workflows}

执行以下步骤来为AEM工作流配置统一存储连接器：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 统一存储连接器]**.

1. 在 **[!UICONTROL 工作流]** 选择 **[!UICONTROL Azure]** 从存储下拉列表中。
1. 指定 [Azure存储配置的配置路径](#create-azure-storage-configuration) 在 **[!UICONTROL 存储配置路径]** 字段。
1. 点按 **[!UICONTROL 发布]** 然后点按 **[!UICONTROL 保存]** 以保存配置。

### 为外部数据存储配置AEM工作流模型 {#configure-workflow-external-data-storage}

执行以下步骤为外部数据存储配置AEM工作流模型：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 选择模型名称并点按 **[!UICONTROL 编辑]**.
1. 点按页面信息图标，然后点按 **[!UICONTROL 打开属性]**.
1. 选择 **[!UICONTROL 将工作流数据存储外部化]**.
1. 点按 **[!UICONTROL 保存并关闭]** 以保存属性。

>[!NOTE]
>
>在为外部数据存储配置AEM工作流模型时，将“分配任务”步骤另存为草稿并检索“分配任务”步骤历史记录的选项会被禁用。

### AEM外部数据存储工作流准则 {#guidelines-workflows-external-data-storage}

以下是使用AEM工作流将数据存储到外部数据存储(如Microsoft Azure存储服务器)时的准则：

* 在工作流模型步骤中定义输入和输出数据文件及附件时，使用变量存储数据。 不选择 **[!UICONTROL 相对于有效负载]** 和 **[!UICONTROL 在绝对路径下可用]** 选项。 的 **[!UICONTROL 相对于有效负载]** 和 **[!UICONTROL 在绝对路径下可用]** 选项在您 [为外部数据存储配置AEM工作流模型](#configure-workflow-external-data-storage).

* 在向AEM工作流提交自适应表单时，使用变量存储数据文件和附件。 不选择 **[!UICONTROL 相对于有效负载]** 选项。 的 **[!UICONTROL 相对于有效负载]** 选项不会自动显示 [为外部数据存储配置AEM工作流模型](#configure-workflow-external-data-storage).

* 请勿在工作流模型中使用自定义AEM工作流步骤来将数据存储在CRX DE存储库中。

* 当您 [为外部数据存储配置AEM工作流模型](#configure-workflow-external-data-storage)，请勿为AEM收件箱创建自定义列，因为如果AEM收件箱中的工作项属于标记为外部存储的工作流，则不会获取自定义列的值。