---
title: 将远程AEM Assets与AEM Sites集成
description: 了解如何在Creative Cloud中配置AEM站点并将其与批准的AEM Assets连接。
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# 将远程AEM Assets与AEM Sites集成  {#integrate-approved-assets}

有效管理数字资产对于在各种在线平台上提供引人入胜且一致的品牌体验至关重要。 具有OpenAPI功能的Dynamic Media通过实现AEM Sites与远程AEM Assets之间的无缝集成，增强了数字资源管理。 这项创新功能允许您轻松地在多个AEM环境中共享和管理不同类型的已批准数字资产，从而简化站点作者和内容编辑器的工作流程。

通过具有OpenAPI功能的Dynamic Media，Sites作者可以直接在AEM页面编辑器中使用远程DAM中的资源，并且 [内容片段](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)，简化了内容创建和管理过程。

用户可以不受最大数量限制地将多个AEM Sites实例连接到远程DAM部署，这是优于 [连接的资产](use-assets-across-connected-assets-instances.md) 功能。

![图像](/help/assets/assets/connected-assets-rdam.png)

初始设置后，用户可以在AEM Sites实例上创建页面并根据需要添加资源。 添加资源时，用户可以选择存储在其本地DAM中的资源，也可以浏览并使用远程DAM中可用的资源。

具有OpenAPI功能的Dynamic Media提供了其他一些好处，例如访问和使用内容片段中的远程资源，获取远程资源的元数据等等。 了解更多关于另一条的信息 [Dynamic Media与Connected Assets相比具有OpenAPI功能的优势](/help/assets/new-dynamic-media-apis-faqs.md).

## 开始之前

* 设置以下内容 [环境变量](/help/implementing/cloud-manager/environment-variables.md#add-variables) 对于AEMas a Cloud Service：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` 是指项目ID <br>
     `eYYYY` 是指环境ID

   * 资产交付IMS客户端= [IMSClientId]

  或配置 [OSGi设置](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) 对于AEM Sites实例中的AEM 6.5，请执行以下步骤：

   1. 登录到控制台并单击 **[!UICONTROL osgi] >** 或使用直接URL；例如： `http://localhost:4502/system/console/configMgr`

   1. 添加 **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;和 **[!UICONTROL imsClient]**= [IMSClientId]
了解有关 [IMS身份验证](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* 通过IMS访问登录到远程DAM AEMas a Cloud Service实例。

* 在远程DAM中打开具有OpenAPI功能的Dynamic Media切换开关。

* 在AEM Sites实例中配置图像v3组件。 如果该组件不存在，请下载并安装 [内容包](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## 从远程DAM访问资产 {#fetch-assets}

通过具有OpenAPI功能的Dynamic Media，您可以访问本地AEM Sites页面编辑器和AEM内容片段上的远程DAM实例中可用的资产。

![图像](/help/assets/assets/open-APIs.png)

### 在AEM页面编辑器中访问远程资产

请按照以下步骤在AEM Sites实例上的AEM页面编辑器中使用远程资产。 您可以在AEMas a Cloud Service和AEM 6.5中执行此集成。

1. 转到 **[!UICONTROL 站点]** > _您的网站_ 其中AEM **[!UICONTROL 页面]** 存在，您需要在该处添加远程资产。
1. 导航到特定的AEM **[!UICONTROL 页面]** 在您网站中的 **[!UICONTROL 站点]** 您打算在其中添加远程资产的部分。
1. 选择页面并单击 **[!UICONTROL 编辑(_e_)]**. AEM **[!UICONTROL 页面编辑器]** 打开。
1. 单击布局容器并添加 **[!UICONTROL 图像]** 组件。
1. 单击 **[!UICONTROL 图像]** 组件并单击 ![“设置”图标](/help/assets/assets/do-not-localize/settings-icon.svg) 图标。
1. 取消选中 **[!UICONTROL 从页面继承精选图像]** 选项。
1. 单击 **[!UICONTROL 选取]** 并选择 **[!UICONTROL 远程]**.
   ![图像](/help/assets/assets/uncheck-inherit-option.jpg)

   系统会提示您登录。
1. 选择资源并单击 **[!UICONTROL 选择]**.
1. 添加替换文本并单击 **[!UICONTROL 完成]**.
   <br> 远程资产会显示在图像组件中。 您还可以在资产加载到页面上时验证该资产的投放URL，或者使用“预览”选项卡进行验证。 投放URL指示正在远程访问资产。

#### 视频：访问AEM页面编辑器中的远程资产

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### 访问AEM内容片段中的远程资源

请按照以下步骤在AEM Sites实例上的AEM内容片段中使用远程资产。 您可以在AEM 6.5中而不是在AEMas a Cloud Service上执行此操作。

1. 转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 选择呈现内容片段的资源文件夹。
1. 选择内容片段并单击 **[!UICONTROL 编辑(_e_)]**.

   >[!NOTE]
   >
   >如果您没有AEM内容片段模型，您可能需要 [创建一个](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. 单击 ![复选标记图标](/help/assets/assets/do-not-localize/checkmark-icon.svg) 图标图标。
1. 选择 **[!UICONTROL 远程]** 以从远程DAM获取资产。 <br>
您可以选择 **[!UICONTROL 本地]** 或 **[!UICONTROL 远程]** 根据您的需求，创建DAM存储库。

   ![图像](/help/assets/assets/cf-pick.jpg)
系统会提示您登录。
1. 选择资产并单击 **[!UICONTROL 选择]**.
   <br> 远程资产URL会显示在文本组件中。

#### 视频：访问AEM内容片段中的远程资产

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
