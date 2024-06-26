---
title: 批准Experience Manager中的资源
description: 了解如何批准中的资源 [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# 批准中的资产 [!DNL Experience Manager]

品牌经理和营销人员对品牌资产进行严格控制。 只有获得批准的最新版本的资产才可供使用，从而确保跨所有渠道和应用程序的品牌一致性。

您可以在AEM Assets中批准资源以简化资源管理，确保处理资源流程的受控高效性。

## 开始之前 {#pre-requisites}

您必须有权访问AEM Assetsas a Cloud Service，并且有权编辑 **[!UICONTROL 审核状态]** 资产的属性。

## 配置

在批准资产之前，您需要一次性更新管理员视图中适用的元数据架构。 您可以为Assets视图跳过此配置。 按照以下步骤配置元数据架构：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**.
1. 选择适用的元数据架构并单击 **[!UICONTROL 编辑]**. <br>此 **[!UICONTROL 元数据架构表单编辑器]** 打开时显示 **[!UICONTROL 基本]** 制表符突出显示。
1. 向下滚动并单击 **[!UICONTROL 审核状态]**.
1. 单击 **[!UICONTROL 规则]** 选项卡。
1. 取消选中 **[!UICONTROL 禁用编辑]** 并单击 **[!UICONTROL 保存]**.
如果您需要查看 **[!UICONTROL 审核状态]** 字段已映射到，导航到 **[!UICONTROL 设置]** 选项卡并查看 `./jcr:content/metadata/dam:status` 中的值 **[!UICONTROL 映射到属性]** 字段。

>[!NOTE]
>
>如果您的资源或文件夹具有不同的默认架构，请确保在该特定架构中进行此更新。

## 批准资源 {#approve-assets}

您可以同时审批以下两个项目中的资产 [!DNL Experience Manager] 和 [!DNL Experience Manager Assets]. 要审批中的资产，请执行以下操作 [!DNL Experience Manager]，请按照以下步骤操作：

1. 选择资产并单击 **[!UICONTROL 属性]** 在顶部窗格中。
1. 在 **[!UICONTROL 基本]** 选项卡，向下滚动到 **[!UICONTROL 审核状态]**.
1. 将审核状态更改为 **[!UICONTROL 已批准]**.
   ![图像](/help/assets/assets/approve-old-ui.png)
1. 单击“**[!UICONTROL 保存并关闭]**”。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同样，您可以使用批准资源 [新的Assets视图](/help/assets/manage-organize-assets-view.md).

## 批量审批资产 {#bulk-approve-assets}

通过一次快速批准多个资产来简化您的工作流。 您可以批量批准资产以加快批准流程，从而节省时间并提高工作效率。
<br>执行以下步骤以审批中的批量资产 [!DNL Experience Manager]：

1. 在创作环境(https://author-pXXX-eYYY.adobeaemcloud.com)中创建文件夹。 替换 _XXX_ 包含您的项目ID和 _YYYY_ Experience Manager中的环境ID。
1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据配置文件]**.
1. 单击 **[!UICONTROL 创建]** 页面右上角的。
1. 添加配置文件标题并单击 **[!UICONTROL 创建]**. 已成功创建元数据配置文件。
1. 选择新创建的元数据配置文件，然后单击 **[!UICONTROL 编辑 _(e)_]**. <br>此&#x200B;**[!UICONTROL 编辑元数据配置文件]**表单打开，其中&#x200B;**[!UICONTROL 基本]**制表符突出显示。
1. 拖放 **[!UICONTROL 单行文本字段]** 从 **[!UICONTROL 构建表单]** 区域到表单中的元数据区域的位置。
1. 单击新添加的字段，然后在 **[!UICONTROL 设置]** 面板：
   1. 更改 **[!UICONTROL 字段标签]** 到 _已批准的Assets_.
   1. 更新 **[!UICONTROL 映射到属性]** 到 _./jcr：content/metadata/dam：status_.
   1. 将默认值更改为 _已批准_.

1. 单击&#x200B;**[!UICONTROL 保存]**。
1. 在 **[!UICONTROL 元数据配置文件]** 页面上，选择新创建的元数据配置文件。
1. 单击 **[!UICONTROL 将元数据配置文件应用到文件夹]** 从顶部操作栏中。
1. 选择要批准的文件夹，然后单击 **[!UICONTROL 应用]**.
   <br> 对整个文件夹的权限设置为进行审批，并且任何上传到此文件夹的资产都会自动获得批准。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>此方法可批准文件夹中新创建的资产。 对于文件夹中的现有资源，您需要手动选择并批准它们。 <br> 或者，您可以使用 **[!UICONTROL 重新处理]** 选项，用于将元数据配置文件中的更改应用于旧资源。

同样，要在Assets视图中批量批准文件夹内的资源，请执行以下操作：

1. 选择资产并单击 **[!UICONTROL 批量元数据编辑]**.

1. 选择 **[!UICONTROL 已批准]** 在 **[!UICONTROL 状态]** 中的可用字段 [!UICONTROL 属性] 区段。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 复制已批准资产的投放URL {#copy-delivery-url-approved-assets}

存储库中所有已批准资产的投放URL在以下情况下可用： [!UICONTROL 具有OpenAPI功能的Dynamic Media] 已在AEM as a Cloud Service实例中启用。

要在存储库中复制已批准资产的投放URL，请执行以下操作：

1. 选择资源并单击 **[!UICONTROL 详细信息]**.

1. 单击右窗格中可用的“格式副本”图标。

1. 选择 **[!UICONTROL 带有OpenAPI的Dynamic Media]** 中提供 **[!UICONTROL 动态]** 部分。

1. 单击 **[!UICONTROL 复制URL]** 以复制资产的投放URL。
   ![复制投放URL](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >仅在Assets视图中提供了复制已批准资源的投放URL的选项。

