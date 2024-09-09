---
title: ' [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的资源选择器'
description: 将资源选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 46%

---

# 使用 Vanilla JS 集成资源选择器 {#integration-using-vanilla-js}

您可以将任何[!DNL Adobe]或非Adobe应用程序与[!DNL Experience Manager Assets]存储库集成并从应用程序中选择资源。 请参阅[资产选择器与各种应用程序的集成](#asset-selector-integration-with-apps)。

通过导入资源选择器包并使用 Vanilla JavaScript 库连接到 Assets as a Cloud Service 来实现集成。编辑应用程序中的`index.html`或任何适当的文件，以：

* 定义身份验证详细信息
* 访问 Assets as a Cloud Service 存储库
* 配置资源选择器显示属性

在以下情况下，您无需定义某些 IMS 属性即可执行身份验证：

* 您正在 [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hans) 上集成 [!DNL Adobe] 应用程序。
* 您已生成用于身份验证的 IMS 令牌。

## 将资产选择器与各种应用程序集成 {#asset-selector-integration-with-apps}

您可以将Asset Selector与各种应用程序集成，例如：

* [将资产选择器与 [!DNL Adobe] 应用程序集成](/help/assets/integrate-asset-selector-adobe-app.md)
* [将资源选择器与非Adobe应用程序集成](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [资产选择器自定义项](/help/assets/asset-selector-customization.md)
>* [资产选择器属性](/help/assets/asset-selector-properties.md)
>* [将资源选择器与Dynamic Media与OpenAPI功能集成](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
