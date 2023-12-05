---
title: 如何为AEM Forms配置统一存储连接器(USC)？
description: 了解如何为AEM Forms管理Unified Storage Connector (USC)。 使用统一存储连接器(USC)将AEM Forms连接到外部数据存储。
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# 管理AEM Forms的统一存储连接器(USC) {#manage-unified-storage-connector}

您可以使用统一存储连接器(USC)将AEM Forms连接到外部数据存储。

例如，您可以在自适应表单中填写字段值并将其提交到AEM Workflow。 您可以进一步配置AEM Workflow以将数据存储在外部存储中，例如Microsoft Azure Storage Server。 使用统一存储连接器(USC)在AEM Workflow和外部存储之间创建连接。

## 将AEM工作流连接到Microsoft Azure Storage Server {#connect-workflows-with-azure}

创建Azure存储配置并使用统一存储连接器(USC)引用该配置。 然后，您可以配置AEM Workflow模型以外部化数据存储以将其连接到Azure存储服务器。

### 创建 [!DNL Azure] 存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您已 [!DNL Azure] 存储帐户和一个访问密钥，用于授权访问 [!DNL Azure] 存储帐户。

执行以下步骤以创建 [!DNL Azure] 存储配置：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure存储]**.
1. 选择一个文件夹以创建配置，然后选择 **[!UICONTROL 创建]**.
1. 在中指定配置的标题 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 中的存储帐户 **[!UICONTROL Azure存储帐户]** 字段。
1. 指定用于访问Azure存储帐户的密钥 **[!UICONTROL Azure访问密钥]** 字段并选择 **[!UICONTROL 保存]**.

### 为AEM Workflow配置统一存储连接器(USC) {#configure-unified-storage-connector-workflows}

执行以下步骤为AEM Workflow配置统一存储连接器(USC)：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 统一存储连接器]**.

1. 在 **[!UICONTROL 工作流]** 部分，选择 **[!UICONTROL Azure]** 从“存储”下拉列表中。
1. 指定 [Azure存储配置的配置路径](#create-azure-storage-configuration) 在 **[!UICONTROL 存储配置路径]** 字段。
1. 选择 **[!UICONTROL Publish]** 然后选择 **[!UICONTROL 保存]** 以保存配置。

### 为外部数据存储配置AEM Workflow模型 {#configure-workflow-external-data-storage}

执行以下步骤可为外部数据存储配置AEM Workflow模型：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 选择模型名称并选择 **[!UICONTROL 编辑]**.
1. 选择页面信息图标并选择 **[!UICONTROL 打开属性]**.
1. 选择 **[!UICONTROL 将工作流数据存储外部化]**.
1. 选择 **[!UICONTROL 保存并关闭]** 以保存属性。

>[!NOTE]
>
>为外部数据存储配置AEM Workflow模型时，将分配任务步骤保存为草稿并检索分配任务步骤历史记录的选项将被禁用。

### 外部数据存储的AEM工作流准则 {#guidelines-workflows-external-data-storage}

以下是使用AEM Workflow并将数据存储到外部数据存储(如Microsoft Azure Storage Server)时的准则：

* 在工作流模型步骤中定义输入和输出数据文件及附件时，使用变量来存储数据。 不选择 **[!UICONTROL 相对于有效负荷]** 和 **[!UICONTROL 在绝对路径上可用]** 选项。 此 **[!UICONTROL 相对于有效负荷]** 和 **[!UICONTROL 在绝对路径上可用]** 选项不会自动显示一次 [为外部数据存储配置AEM Workflow模型](#configure-workflow-external-data-storage).

* 向AEM Workflow提交自适应表单时，使用变量存储数据文件和附件。 不选择 **[!UICONTROL 相对于有效负荷]** 选项在将自适应表单提交到AEM工作流时。 此 **[!UICONTROL 相对于有效负荷]** 选项不会自动显示一次 [为外部数据存储配置AEM Workflow模型](#configure-workflow-external-data-storage).

* 请勿在工作流模型中使用自定义AEM工作流步骤来将数据存储在CRX DE存储库中。

* 当您 [为外部数据存储配置AEM Workflow模型](#configure-workflow-external-data-storage)时，请不要为AEM收件箱创建自定义列，因为如果AEM收件箱中的工作项目属于标记为外部存储的工作流，则不会获取自定义列的值。

>[!MORELIKETHIS]
>
>* [为AEM Forms配置数据源](/help/forms/configure-data-sources.md)
>* [为AEM Forms配置Azure存储](/help/forms/configure-azure-storage.md)
>* [将Microsoft Dynamics 365和Salesforce与自适应Forms集成](/help/forms/configure-msdynamics-salesforce.md)
>  [将Forms Portal添加到AEM Sites页面](/help/forms/configure-forms-portal.md)
