---
title: 将远程 AEM Assets 与 AEM Sites 集成
description: 了解如何配置AEM站点并将其与批准的AEM Assets连接。
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 15%

---

# 将远程 AEM Assets 与 AEM Sites 集成  {#integrate-approved-assets}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

有效管理数字资产对于在各种在线平台上提供引人入胜且一致的品牌体验至关重要。 具有OpenAPI功能的Dynamic Media通过实现AEM Sites与AEM Assetsas a Cloud Service之间的无缝集成，增强了数字资源管理。 这项创新功能允许您轻松地在多个AEM环境中共享和管理不同类型的已批准数字资产，从而简化站点作者和内容编辑器的工作流程。

通过具有OpenAPI功能的Dynamic Media，Sites作者可以直接在AEM页面编辑器和[内容片段](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)中使用来自远程DAM的资源，从而简化内容创建和管理过程。

用户可以不受最大数量限制将多个AEM Sites实例连接到远程DAM部署，这是优于[连接的Assets](use-assets-across-connected-assets-instances.md)功能的显着优势。

![图像](/help/assets/assets/connected-assets-rdam.png)

初始设置后，用户可以在AEM Sites实例上创建页面并根据需要添加资源。 添加资源时，用户可以选择存储在其本地DAM中的资源，也可以浏览并使用远程DAM中可用的资源。

具有OpenAPI功能的Dynamic Media提供了其他一些好处，例如访问和使用内容片段中的远程资源，获取远程资源的元数据等等。 与Connected Assets](/help/assets/dynamic-media-open-apis-faqs.md)相比，了解具有OpenAPI功能的Dynamic Media的其他[优势。

## 开始之前 {#pre-requisites-sites-integration}

要支持使用带有OpenAPI功能的Dynamic Media的远程资源，需要：

* AEM 6.5 SP 18 和更高版本或 AEM as a Cloud Service

* 核心组件版本 2.23.2 或更高版本

* 为AEM as a Cloud Service设置以下[环境变量](/help/implementing/cloud-manager/environment-variables.md#add-variables)：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX`引用程序ID <br>
     `eYYYY`引用环境ID

  这些变量是使用AEM as a Cloud Service环境的Cloud Manager用户界面设置的，充当本地Sites实例。

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]：您需要提交Adobe支持票证以获取IMS客户端ID。

     或者，按照以下步骤在AEM Sites实例中为AEM 6.5配置[OSGi设置](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html)：

   1. 登录到控制台，然后单击&#x200B;**[!UICONTROL OSGi] >**或
使用直接URL；例如： `https://localhost:4502/system/console/configMgr`

   1. 按如下方式配置&#x200B;**下一代Dynamic Media配置** (`NextGenDynamicMediaConfigImpl`) OSGi配置，将值替换为远程资源环境的值。

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg`不是强制输入。
      `repositoryId` = &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;
其中`pXXXX`引用项目ID
      `eYYYY`引用环境ID

      ![新一代 Dynamic Media 配置 OSGi 配置窗口](/help/assets/assets/remote-assets-osgi.png)

  了解有关[IMS身份验证](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html)的更多信息。

  有关如何配置 OSGi 的详细信息，请参见以下文档：

   * 为 AEM as a Cloud Service [配置 Adobe Experience Manager as a Cloud Service 的 OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html)
   * 为 AEM 6.5 [配置 OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html)

* 通过IMS访问登录到远程DAM AEM as a Cloud Service实例。 它是指对远程DAM环境具有IMS访问权限的Sites作者。

* 在AEM Sites实例中配置图像v3组件。 如果该组件不存在，请下载并安装[内容包](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0)。

## 配置 HTTPS {#https}

一般建议使用 HTTP 运行所有生产 AEM 实例。但是，可能并未这样设置您的本地开发环境。但是，使用带有 OpenAPI 的 Dynamic Media 远程资产需要 HTTPS 才能运行。

[使用本指南](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html)在您要使用远程资源的任何地方（包括开发环境）配置 HTTPS。

## 从远程DAM访问资产 {#fetch-assets}

通过具有OpenAPI功能的Dynamic Media，您可以访问本地AEM Sites页面编辑器和AEM内容片段上的远程DAM实例中可用的资产。

![图像](/help/assets/assets/open-APIs.png)

### 在AEM页面编辑器中访问远程资产 {#access-assets-page-editor}

请按照以下步骤在AEM Sites实例上的AEM页面编辑器中使用远程资产。 您可以在AEM as a Cloud Service和AEM 6.5中进行此集成。

1. 转到&#x200B;**[!UICONTROL Sites]** > _您的网站_，您需要在其中添加远程资产的AEM **[!UICONTROL 页面]**&#x200B;位于该网站。
1. 选择页面，然后单击&#x200B;**[!UICONTROL 编辑(_e_)]**。 AEM **[!UICONTROL 页面编辑器]**&#x200B;打开。
1. 单击布局容器并添加&#x200B;**[!UICONTROL 图像]**&#x200B;组件。
1. 单击&#x200B;**[!UICONTROL 图像]**&#x200B;组件并单击![设置图标](/help/assets/assets/do-not-localize/settings-icon.svg)图标。
1. 取消选中&#x200B;**[!UICONTROL 从页面]**&#x200B;继承精选图像选项。
1. 单击&#x200B;**[!UICONTROL 选择]**&#x200B;并选择&#x200B;**[!UICONTROL 远程]**。
   ![图像](/help/assets/assets/uncheck-inherit-option.jpg)

   系统会提示您登录。
1. 选择资产并单击&#x200B;**[!UICONTROL 选择]**。
1. 添加替换文本并单击&#x200B;**[!UICONTROL 完成]**。
   <br>远程资产显示在图像组件中。 您还可以在资产加载到页面上时验证该资产的投放URL，或者使用“预览”选项卡进行验证。 投放URL指示正在远程访问资产。

您只能在AEM页面编辑器中现成访问图像核心组件v3和Teaser核心组件v2中的远程资产。 对于包括自定义组件在内的其他组件，需要进行自定义才能将资产选择器与这些组件集成。

#### 视频：访问AEM页面编辑器中的远程资产

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### 访问AEM内容片段中的远程资源 {#access-assets-content-fragment}

请按照以下步骤在AEM Sites实例上的AEM内容片段中使用远程资产。 您可以在AEM 6.5中而不是在AEM as a Cloud Service上执行此集成。

1. 转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 文件]**。
1. 选择呈现内容片段的资源文件夹。
1. 选择内容片段并单击&#x200B;**[!UICONTROL 编辑(_e_)]**。

   >[!NOTE]
   >
   如果您没有AEM内容片段模型，则可能需要[创建一个](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en)。

1. 单击文本组件旁边的![复选标记图标](/help/assets/assets/do-not-localize/checkmark-icon.svg)图标。
1. 选择&#x200B;**[!UICONTROL 远程]**&#x200B;以从远程DAM获取资产。 <br>
您可以根据需要选择**[!UICONTROL 本地]**&#x200B;或&#x200B;**[!UICONTROL 远程]** DAM存储库。

   ![图像](/help/assets/assets/cf-pick.jpg)
系统会提示您登录。
1. 选择资产并单击&#x200B;**[!UICONTROL 选择]**。
   <br>远程资产URL显示在文本组件中。

#### 视频：访问AEM内容片段中的远程资产

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### 访问Edge Delivery Services中的远程资源 {#access-assets-eds}

您还可以访问Edge Delivery Services中的远程资源。 有关详细信息，请参阅[将来自Assets的资源与Dynamic Media的OpenAPI功能结合使用](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi)as a Cloud Service。
