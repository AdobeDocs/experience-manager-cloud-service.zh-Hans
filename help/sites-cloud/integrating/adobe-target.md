---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 4%

---


# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分，Adobe [目标](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) 可让您通过在所有渠道中进行定位和衡量来提高内容相关性。 营销人员使用Adobe目标设计和执行在线测试，根据行为创建实时受众细分，并自动定位内容和在线体验。 AEM作为云服务，已采用Adobe目标标准版中使用的定位工作流。 如果您使用目标，您将熟悉AEM中作为云服务的定位编辑环境。

将AEM站点与Adobe目标集成，以个性化页面中的内容：

* 实施内容定位。
* 使用目标受众创造个性化体验。
* 当目标与您的页面交互时，向访客提交上下文数据。
* 跟踪转化率。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有目标帐户的云服务客户，可以请求访问适用于Experience Cloud的目标基础包。  Foundation Pack提供对目标的批量限制使用。


要与目标集成，请执行以下任务:

* [执行入门任务](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html): 向Adobe目标注册并配置AEM作者实例的某些方面。 您的Adobe目标帐户必 **须至少** 具有批准者级别权限。 此外，还必须保护发布节点上的活动设置，以便用户无法访问它。

* Launch by Adobe是一种实际工具，用于检测具有目标功能（JS库）的AEM站点。 因此，将AEM作为云服务与Launch和Adobe目标相集成（请参阅以下链接）。

   * [使用Adobe I/O与Adobe目标集成](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [将Launch by Adobe集成](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [通过Adobe I/O将AEM与Adobe Launch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [了解AEM与Launch By Adobe、Analytics和目标](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为云服务。 用户不必创建此配置。

1. [配置活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): 将活动与目标云配置关联。

>[!CAUTION]
>
>在AEM中，将优惠和活动从AEM同步到Adobe目标的复制代理默认处于禁用状态。 如果需要 [重新启用复](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) 制代理，请与Adobe支持团队联系。

>[!NOTE]
>
>如果您正在使用自定义代理配置的目标，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能则使用4.x API:
>
>* 3.x已配置为 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置为 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

集成完成后，您可以创作 [目标内容](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) ，将访客数据发送到Adobe目标。 请注意，页面组件需要特定代码才能启用内容定位。 (请参 [阅为目标内容开发](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>当您在AEM作者中目标组件时，该组件会向Adobe目标发出一系列服务器端调用，以注册活动、设置优惠和检索Adobe目标区段（如果已配置）。 AEM发布到Adobe目标时不会进行任何服务器端调用。

## 背景信息源 {#background-information-sources}

将AEM作为云服务与Adobe目标集成需要了解Adobe目标、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe目标(请参阅 [Adobe目标文档](https://marketing.adobe.com/resources/help/en_US/target/))。
* AEM活动控制台(请参 [阅管理活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)。
* AEM受众(请参阅 [管理受众](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe目标时，以下是活动中允许的最大工件数：
>
>* 50个地点
>* 2,000次体验
>* 50个指标
>* 50个报告细分
>


