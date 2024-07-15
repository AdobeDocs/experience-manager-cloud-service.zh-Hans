---
title: 批准Experience Manager中的资源
description: 了解如何在 [!DNL Experience Manager]中批准资源。
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 2%

---

# 批准[!DNL Experience Manager]中的资源

品牌经理和营销人员对品牌资产进行严格控制。 只有获得批准的最新版本的资产才可供使用，从而确保跨所有渠道和应用程序的品牌一致性。

您可以在AEM Assets中批准资源以简化资源管理，确保处理资源流程的受控高效性。

## 开始之前 {#pre-requisites}

您必须有权访问AEM Assetsas a Cloud Service，并且有权编辑资源的&#x200B;**[!UICONTROL 审核状态]**&#x200B;属性。

## 配置

在批准资产之前，您需要一次性更新管理员视图中适用的元数据架构。 您可以为Assets视图跳过此配置。 按照以下步骤配置元数据架构：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据架构]**。
1. 选择适用的元数据架构并单击&#x200B;**[!UICONTROL 编辑]**。 <br>将打开&#x200B;**[!UICONTROL 元数据架构表单编辑器]**，并突出显示&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡。
1. 向下滚动并单击&#x200B;**[!UICONTROL 审核状态]**。
1. 单击右侧面板上的&#x200B;**[!UICONTROL 规则]**&#x200B;选项卡。
1. 取消选中&#x200B;**[!UICONTROL 禁用编辑]**，然后单击&#x200B;**[!UICONTROL 保存]**。
如果需要查看**[!UICONTROL 审阅状态]**&#x200B;字段映射到的属性，请导航到&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡，并查看&#x200B;**[!UICONTROL 映射到属性]**&#x200B;字段中的`./jcr:content/metadata/dam:status`值。

>[!NOTE]
>
>如果您的资源或文件夹具有不同的默认架构，请确保在该特定架构中进行此更新。

## 审批资源 {#approve-assets}

您可以同时批准[!DNL Experience Manager]和[!DNL Experience Manager Assets]中的资源。 要在[!DNL Experience Manager]中批准资源，请执行以下步骤：

1. 选择资产并单击顶部窗格中的&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，向下滚动到&#x200B;**[!UICONTROL 审核状态]**。
1. 将审阅状态更改为&#x200B;**[!UICONTROL 已批准]**。
   ![图像](/help/assets/assets/approve-old-ui.png)
1. 单击“**[!UICONTROL 保存并关闭]**”。

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   同样，您可以使用[新的Assets视图](/help/assets/manage-organize-assets-view.md)批准资源。

## 批量审批资产 {#bulk-approve-assets}

通过一次快速批准多个资产来简化您的工作流。 您可以批量批准资产以加快批准流程，从而节省时间并提高工作效率。
<br>按照以下步骤在[!DNL Experience Manager]中批准批量资产：

1. 在创作环境(https://author-pXXX-eYYY.adobeaemcloud.com)中创建文件夹。 将&#x200B;_XXX_&#x200B;替换为您的项目ID，将&#x200B;_YYY_&#x200B;替换为Experience Manager中的环境ID。
1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 元数据配置文件]**。
1. 单击页面右上方的&#x200B;**[!UICONTROL 创建]**。
1. 添加配置文件标题并单击&#x200B;**[!UICONTROL 创建]**。 已成功创建元数据配置文件。
1. 选择新创建的元数据配置文件，然后单击&#x200B;**[!UICONTROL 编辑&#x200B;_(e)_]**。 <br>将打开&#x200B;**[!UICONTROL 编辑元数据配置文件]**表单，其中突出显示&#x200B;**[!UICONTROL 基本]**选项卡。
1. 将&#x200B;**[!UICONTROL 单行文本字段]**&#x200B;从右侧的&#x200B;**[!UICONTROL 构建表单]**&#x200B;分区拖放到表单中的元数据分区。
1. 单击新添加的字段，然后在&#x200B;**[!UICONTROL 设置]**&#x200B;面板中进行以下更新：
   1. 将&#x200B;**[!UICONTROL 字段标签]**&#x200B;更改为&#x200B;_已批准的Assets_。
   1. 将&#x200B;**[!UICONTROL 映射到属性]**&#x200B;的更新为&#x200B;_。/jcr：content/metadata/dam：status_。
   1. 将默认值更改为&#x200B;_已批准_。

1. 单击&#x200B;**[!UICONTROL 保存]**。
1. 在&#x200B;**[!UICONTROL 元数据配置文件]**&#x200B;页面中，选择新创建的元数据配置文件。
1. 单击顶部操作栏中的&#x200B;**[!UICONTROL 将元数据配置文件应用到文件夹]**。
1. 选择要批准的文件夹，然后单击&#x200B;**[!UICONTROL 应用]**。
   <br>已将整个文件夹的权限设置为审批，并且任何上传到此文件夹的资产都会自动审批。

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>此方法可批准文件夹中新创建的资产。 对于文件夹中的现有资源，您需要手动选择并批准它们。 <br>或者，您可以使用&#x200B;**[!UICONTROL 重新处理]**&#x200B;选项将更改从元数据配置文件应用到较旧的资源。

同样，要在Assets视图中批量批准文件夹内的资源，请执行以下操作：

1. 选择资源并单击&#x200B;**[!UICONTROL 批量元数据编辑]**。

1. 在右窗格的[!UICONTROL 属性]部分中的&#x200B;**[!UICONTROL 状态]**&#x200B;字段中选择&#x200B;**[!UICONTROL 已批准]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 复制已批准资产的投放URL {#copy-delivery-url-approved-assets}

如果您在AEM as a Cloud Service实例上启用了[!UICONTROL Dynamic Media的OpenAPI功能]，则存储库中所有已批准资源的投放URL均可用。

要在存储库中复制已批准资产的投放URL，请执行以下操作：

1. 选择资产并单击&#x200B;**[!UICONTROL 详细信息]**。

1. 单击右窗格中可用的“格式副本”图标。

1. 选择&#x200B;**[!UICONTROL Dynamic]**&#x200B;部分中提供的&#x200B;**[!UICONTROL 带有OpenAPI的Dynamic Media]**。

1. 单击&#x200B;**[!UICONTROL 复制URL]**以复制资产的投放URL。
   ![复制投放URL](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >仅在Assets视图中提供了复制已批准资源的投放URL的选项。

