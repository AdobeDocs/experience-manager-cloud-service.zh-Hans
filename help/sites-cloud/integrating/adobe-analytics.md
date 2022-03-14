---
title: '与 Adobe Analytics 集成 '
description: '与 Adobe Analytics 集成 '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 12%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics与AEMas a Cloud Service集成后，您可以跟踪网页活动：

* Adobe Analytics配置允许AEM通过Adobe Analytics进行身份验证。
* 框架可识别发送到Adobe Analytics报表包的数据。

数据包括页面和用户数据，例如：

* AEM组件收集的数据
* 链接点击
* 视频使用信息
* 来自Adobe Analytics的页面访问次数

下面列出的页面可帮助您配置集成。 请注意，Launch by Adobe是使用Analytics功能（JS库）检测AEM网站的实际工具。 因此，将AEMas a Cloud Service与Launch和Adobe Analytics集成在一起时，会一起使用。

* [连接到Adobe Analytics和创建框架](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html)  — 请注意，“Analytics框架”是AEM中的旧版框架，由于需要经典UI，因此在AEMas a Cloud Service中无法创建它们。 Launch by Adobe应用于变量映射和将JS库部署到页面。
* [集成Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [通过AEM将Adobe I/O与AdobeLaunch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [了解AEM与Launch by Adobe、Analytics和Target的集成](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [为Adobe Analytics配置链接跟踪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [使用Adobe Analytics属性映射组件数据](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [为Adobe Analytics配置视频跟踪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分类](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager as a Cloud Service客户如果没有现有的Analytics帐户，则可以请求访问Analytics Foundation Pack以进行Experience Cloud。  此Foundation Pack提供了对Analytics的卷限制使用。

>[!NOTE]
>
>用于Launch by Adobe的IMS配置（技术帐户）在AEMas a Cloud Service中进行了预配置。 用户无需创建此配置。

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics集成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) 有关开发可收集用户数据和自定义Adobe Analytics框架的组件的信息。 请注意，“Analytics框架”是AEM中的旧版框架，由于需要经典UI，因此在AEMas a Cloud Service中无法创建它们。 Launch by Adobe应用于变量映射和将JS库部署到页面。
* 知识库文章， [Adobe Analytics集成 — 疑难解答问题](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以了解有关对Adobe Analytics集成进行故障诊断的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置:
>
>* **Day Commons HTTP Client 3.1** 配置3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP组件代理配置** 配置4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

