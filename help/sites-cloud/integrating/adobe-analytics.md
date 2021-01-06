---
title: '与 Adobe Analytics 集成 '
description: '与 Adobe Analytics 集成 '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 14%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics和AEM集成为Cloud Service，使您能够跟踪网页活动:

* Adobe Analytics配置使AEM能够与Adobe Analytics进行身份验证。
* 框架标识发送到您的Adobe Analytics报告包的数据。

数据包括页面和用户数据，例如：

* aem组件收集的数据
* 链接点击
* 视频使用信息
* 来自Adobe Analytics的页面访问次数

下面列出的页面可以帮助您配置集成。 需要指出的是，Launch by Adobe是检验具有Analytics功能（JS库）的AEM站点的实际工具。 因此，将AEM作为Cloud Service与Launch和Adobe Analytics相结合。

* [连接到Adobe Analytics和创建框架](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-connect.html) -请注意，“Analytics框架”是AEM的传统，其创建在AEM中不起作用，因为它需要经典UI。应将Launch by Adobe用于变量映射和将JS库部署到页面。
* [集成Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [通过Adobe I/O将AEM与Adobe启动集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
* [了解AEM与Launch by Adobe、分析和目标的集成](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [为Adobe Analytics配置链接跟踪](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [使用Adobe Analytics属性映射组件数据](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [为Adobe Analytics配置视频跟踪](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe分类](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>Adobe Experience Manager作为没有现有Analytics帐户的Cloud Service客户，可以请求访问Analytics Foundation Pack进行Experience Cloud。  此Foundation Pack提供对Analytics的批量有限使用。

>[!NOTE]
>
>Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为Cloud Service。 用户不必创建此配置。

## 更多信息 {#further-information}

请参阅：

* [扩展Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html) 集成，以了解有关开发收集用户数据的组件和自定义Adobe Analytics框架的信息。请注意，“Analytics frameworks”是AEM的传统，其创建在AEM中不起作用，因为它需要经典UI。 应将Launch by Adobe用于变量映射和将JS库部署到页面。
* 知识库文章[Adobe Analytics集成——疑难排解问题](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，以了解有关Adobe Analytics集成疑难排解的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/deploying/configuring/configuring-osgi.html)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置:
>
>* **Day Commons HTTP Client 3.1** 配置3.x API;
>  例如[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP Components Proxy** Configuration配置4.x API;
>  例如[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


