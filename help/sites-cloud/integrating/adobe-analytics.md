---
title: '与 Adobe Analytics 集成 '
description: '与 Adobe Analytics 集成 '
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: ht
source-wordcount: '545'
ht-degree: 100%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

通过将 Adobe Analytics 与 AEM as a Cloud Service 集成，您可以跟踪您的网页活动：

* Adobe Analytics 配置可让 AEM 通过 Adobe Analytics 进行身份验证。
* 框架标识发送到 Adobe Analytics 报告包的数据。

该数据包括页面和用户数据，例如：

* AEM 组件收集的数据
* 链接点击次数
* 视频使用信息
* 来自 Adobe Analytics 的页面访问次数

下面列出的页面可帮助您配置集成。需要注意的是，Adobe Launch 是用于通过 Analytics 功能（JS 库）检测 AEM 站点的实际工具。因此，将 AEM as a Cloud Service 与 Launch 和 Adobe Analytics 集成是密切相关的。

* [连接到 Adobe Analytics 并创建框架](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-connect.html) – 请注意，“Analytics 框架”是 AEM 中的旧式框架，无法在 AEM as a Cloud Service 中创建它们，因为这需要经典 UI。应改用 Adobe Launch 以映射变量并将 JS 库部署到页面。
* [集成 Adobe Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
* [通过 Adobe I/O 将 AEM 与 Adobe Launch 集成](https://helpx.adobe.com/cn/experience-manager/using/aem_launch_adobeio_integration.html)
* [了解 AEM 与 Adobe Launch、Analytics 和 Target 的集成](https://helpx.adobe.com/cn/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)
* [为 Adobe Analytics 配置链接跟踪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-link.html)
* [建立组件数据与 Adobe Analytics 属性的映射](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-mapping.html)
* [为 Adobe Analytics 配置视频跟踪](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-video.html)
* [Adobe 分类](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/adobeanalytics-classifications.html)

>[!CAUTION]
>
>不具有现有 Analytics 帐户的 Adobe Experience Manager as a Cloud Service 客户可以请求对 Analytics Foundation Pack for Experience Cloud 的访问权限。此 Foundation Pack 提供了对 Analytics 的限量使用。

>[!NOTE]
>
>已在 AEM as a Cloud Service 中预配置 Adobe Launch 的 IMS 配置（技术帐户）。用户无需创建此配置。

## 更多信息 {#further-information}

请参阅：

* [扩展 Adobe Analytics 集成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-analytics/extending-analytics.html)，了解有关开发用于收集用户数据的组件和自定义 Adobe Analytics 框架的信息。请注意，“Analytics 框架”是 AEM 中的旧式框架，无法在 AEM as a Cloud Service 中创建它们，因为这需要经典 UI。应改用 Adobe Launch 以映射变量并将 JS 库部署到页面。
* 知识库文章 [Adobe Analytics 集成 – 解决问题](https://helpx.adobe.com/cn/experience-manager/kb/sitecatalystintegrationtroubleshooting.html)，了解有关排查 Adobe Analytics 集成问题的信息。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的 Adobe Analytics，则需要配置 **Apache HTTP Client** 代理配置所需的[两个 OSGi 包](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html)（例如，使用 Web Console）。这两个包都是必需的，因为 AEM 的某些功能使用 3.x API，而其他功能使用 4.x API。配置：
>
>* **Day Commons HTTP 客户端 3.1** 以配置 3.x API；
>  例如，[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP 组件代理配置**以配置 4.x API；
>  例如，[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

