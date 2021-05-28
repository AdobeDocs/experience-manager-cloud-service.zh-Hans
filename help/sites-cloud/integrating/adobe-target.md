---
title: 与 Adobe Target 集成
description: 与 Adobe Target 集成
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 4%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分，[Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html)允许您通过跨所有渠道进行定位和测量来提高内容相关性。 营销人员使用Adobe Target来设计和执行在线测试、创建即时受众区段（基于行为）并自动定位内容和在线体验。 AEM as aCloud Service已采用Adobe Target Standard中使用的定位工作流。 如果您使用Target，您将会熟悉AEM as a Cloud Service中的定位编辑环境。

将您的AEM网站与Adobe Target集成，以个性化页面中的内容：

* 实施内容定位。
* 使用Target受众创建个性化体验。
* 当访客与您的页面进行交互时，将上下文数据提交到Target。
* 跟踪转化率。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有Target帐户的Cloud Service客户，可以请求访问Target Foundation Pack以进行Experience Cloud。  Foundation Pack提供了对Target的卷限制使用。


要与Target集成，请执行以下任务：

* [执行先决任务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html):在Adobe Target中注册并配置AEM创作实例的某些方面。您的Adobe Target帐户必须至少具有&#x200B;**审批者**&#x200B;级别权限。 此外，您还必须保护发布节点上的活动设置，以便用户无法访问该活动设置。

* Launch by Adobe是使用Target功能（JS库）检测AEM网站的实际工具。 因此，将AEM as a Launch与Launch和Adobe Target集成时，会一起使用（请参阅以下链接）。

   * [使用Adobe Target与Adobe I/O集成](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [集成Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [通过AEM将Adobe I/O与AdobeLaunch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [了解AEM与Launch by Adobe、Analytics和Target的集成](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>用于Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为Cloud Service。 用户无需创建此配置。

1. [配置活动](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html):将您的活动与Target云配置关联。

>[!CAUTION]
>
>在AEM as a Cloud Service中，默认情况下会禁用将选件和活动从AEM同步到Adobe Target的复制代理。 如果需要重新启用复制代理，请联系[Adobe支持](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager)团队。

>[!NOTE]
>
>如果您使用的是具有自定义代理配置的Target，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能使用4.x API:
>
>* 3.x配置了[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置了[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>您必须保护发布实例上的活动设置节点&#x200B;**cq:ActivitySettings**，以便普通用户无法访问该节点。 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>有关详细信息，请参阅[与Adobe Target集成的先决条件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node)。

集成完成后，您可以[创作目标内容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html)以将访客数据发送到Adobe Target。 请注意，页面组件需要特定代码才能启用内容定位。 (请参阅[为目标内容开发](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>在AEM作者中定位某个组件时，该组件会向Adobe Target发起一系列服务器端调用，以注册该促销活动、设置选件和检索Adobe Target区段（如果已配置）。 不会从AEM发布到Adobe Target中进行服务器端调用。

## 背景信息源{#background-information-sources}

将AEM as a A Audience与Adobe Target集成需要了解Adobe Target、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe Target(请参阅[Adobe Target文档](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* AEM活动控制台(请参阅[管理活动](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)。
* AEM受众(请参阅[管理受众](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe Target时，以下是营销活动中允许的最大工件数：
>
>* 50个位置
>* 2,000个体验
>* 50个量度
>* 50个报告区段

>


