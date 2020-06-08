---
title: 与 Adobe Analytics 集成
description: '与 Adobe Analytics 集成 '
translation-type: tm+mt
source-git-commit: 6754693da488b0bc44a71aa9f0402fc1308b703a
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics和AEM集成为云服务后，您可以跟踪网页活动:

* Adobe Analytics配置使AEM能够使用Adobe Analytics进行身份验证。
* 框架可标识发送到Adobe Analytics报表包的数据。

数据包括页面和用户数据，例如：

* AEM组件收集的数据
* 链接点击
* 视频使用信息
* 从Adobe Analytics访问页面的次数

下面列出的页面可以帮助您配置集成。 请注意，Launch by Adobe是实际工具，用于借助Analytics功能（JS库）检测AEM站点。 因此，将AEM作为云服务与Launch和Adobe Analytics相集成是相辅相成的。

* [连接到Adobe Analytics和创建框架](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) -请注意，“Analytics框架”是AEM中的旧版，其创建在AEM中不起作为云服务的作用，因为它需要经典UI。 Launch by Adobe应用于变量映射和将JS库部署到页面。
* [将Launch by Adobe集成](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [通过Adobe I/O将AEM与Adobe Launch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [了解AEM与Launch By Adobe、Analytics和目标](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [为Adobe Analytics配置链接跟踪](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [使用Adobe Analytics属性映射组件数据](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [为Adobe Analytics配置视频跟踪](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分类](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager作为没有现有Analytics帐户的云服务客户，可请求访问适用于Experience Cloud的Analytics Foundation Pack。  此Foundation Pack提供对Analytics的批量有限使用。

>[!NOTE]
>
>Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为云服务。 用户不必创建此配置。

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics集成](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) ，以了解有关开发收集用户数据的组件和自定义Adobe Analytics框架的信息。 请注意，“Analytics框架”是AEM中的旧版框架，其创建在AEM中不能作为云服务使用，因为它需要经典UI。 Launch by Adobe应用于变量映射和将JS库部署到页面。
* 知识库文章，Adobe [Analytics集成——疑难排解问题](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以了解有关Adobe Analytics集成疑难解答的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/deploying/configuring/configuring-osgi.html)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置:
>
>* **Day Commons HTTP Client 3.1** ，用以配置3.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Apache HTTP Components代理配置** ，以配置4.x API;
   >  例如， [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


