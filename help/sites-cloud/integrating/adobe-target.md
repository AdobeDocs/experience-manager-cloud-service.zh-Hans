---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 4%

---


# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分， [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) 允许您通过在所有渠道中进行定位和衡量来提高内容相关性。 Adobe Target由营销人员用来设计和执行在线测试、创建实时受众细分（基于行为）以及自动定位内容和在线体验。 AEM作为Cloud Service已采用Adobe Target标准中使用的定位工作流。 如果您使用目标，您将熟悉AEM中的定位编辑环境作为Cloud Service。

将AEM站点与Adobe Target集成，以个性化页面中的内容：

* 实施内容定位。
* 使用目标受众创造个性化体验。
* 当目标与您的页面交互时，向访客提交上下文数据。
* 跟踪转化率。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有目标帐户的Cloud Service客户，可以请求访问目标基础包以进行Experience Cloud。  Foundation Pack提供对目标的批量限制使用。


要与目标集成，请执行以下任务:

* [执行入门任务](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html): 向Adobe Target注册并配置AEM作者实例的某些方面。 您的Adobe Target帐户必 **须至少** 具有批准者级别权限。 此外，还必须保护发布节点上的活动设置，以便用户无法访问它。

* Launch by Adobe是一种实际工具，用于检测具有目标功能（JS库）的AEM站点。 因此，将AEM作为Cloud Service与Launch和Adobe Target相集成将相互配合（请参阅以下链接）。

   * [使用Adobe I/O与Adobe Target集成](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [将Launch by Adobe集成](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [通过Adobe I/O将AEM与Adobe Launch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [了解AEM与Launch By Adobe、Analytics和目标](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为Cloud Service。 用户不必创建此配置。

1. [配置活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): 将活动与目标云配置关联。

>[!CAUTION]
>
>在AEM中，将Cloud Service和活动从AEM同步到Adobe Target的复制代理默认处于禁用状态。 如果需要 [重新启用复](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager) 制代理，请与Adobe支持团队联系。

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

集成完成后，您可以创作 [目标内容](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) ，将访客数据发送给Adobe Target。 请注意，页面组件需要特定代码才能启用内容定位。 (请参 [阅为目标内容开发](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>在AEM作者中目标组件时，该组件会向Adobe Target发出一系列服务器端调用，以注册活动、设置优惠和检索Adobe Target段（如果已配置）。 AEM发布到Adobe Target时不会进行任何服务器端调用。

## 背景信息源 {#background-information-sources}

将AEM作为Cloud Service与Adobe Target集成需要了解Adobe Target、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe Target(请参阅 [Adobe Target文档](https://docs.adobe.com/content/help/en/target/using/target-home.html))。
* AEM活动控制台(请参 [阅管理活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)。
* AEM受众(请参阅 [管理受众](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe Target时，以下是活动中允许的最大伪数：
>
>* 50个地点
>* 2,000次体验
>* 50个指标
>* 50个报告细分

>


