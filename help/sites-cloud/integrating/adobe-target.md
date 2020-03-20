---
title: 与 Adobe Target 集成
description: '与 Adobe Target 集成 '
translation-type: tm+mt
source-git-commit: 94ba99acf2d14219d63485e3443b7080b8ba32bd

---


# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为Adobe Marketing Cloud的一部分， [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) 允许您通过跨所有渠道定位和衡量来提高内容相关性。 营销人员使用Adobe Target设计和执行在线测试，根据行为创建实时受众细分，并自动定位内容和在线体验。 AEM作为云服务，已采用Adobe Target Standard中使用的定位工作流。 如果您使用Target，您将熟悉AEM中作为云服务的定位编辑环境。

将AEM站点与Adobe Target集成，以个性化页面中的内容：

* 实施内容定位。
* 使用Target受众创建个性化体验。
* 当访客与您的页面交互时，将上下文数据提交到Target。
* 跟踪转化率。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有Target帐户的云服务客户，可请求访问Target Foundation Pack for Experience Cloud。  Foundation Pack提供对Target的批量限制使用。


要与Target集成，请执行以下任务：

* [执行入门项目任务](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html):向Adobe Target注册并配置AEM作者实例的某些方面。 您的Adobe Target帐户必须至少具 **有** “审批者级别”权限。 此外，您还必须保护发布节点上的活动设置，以便用户无法访问该活动设置。

* Launch by Adobe是一个实际工具，用于借助Target功能（JS库）检测AEM站点。 因此，将AEM作为云服务与Launch和Adobe Target集成是相辅相成的（请参阅以下链接）。

   * [使用Adobe I/O与Adobe Target集成](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [集成Launch by Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [通过Adobe I/O将AEM与Adobe Launch集成](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [了解AEM与Launch By Adobe、Analytics和Target的集成](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>Launch by Adobe的IMS配置（技术帐户）在AEM中预配置为云服务。 用户不必创建此配置。

1. [配置活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html):将您的活动与Target云配置关联。

>[!CAUTION]
>
>在AEM中，将选件和活动从AEM同步到Adobe Target的复制代理在默认情况下处于禁用状态。 如果需要 [重新启用复制代理](https://helpx.adobe.com/contact/enterprise-support.ec.html#target) ，请与Adobe支持部门联系。

>[!NOTE]
>
>如果您使用具有自定义代理配置的Target，则需要配置两个HTTP客户端代理配置，因为AEM的某些功能使用3.x API，而其他一些功能使用4.x API:
>
>* 3.x已配置http://localhost:4502/system/console/configMgr/com.day.commons.httpclient [](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已配置http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator [](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. 该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>See [Prerequisites for Integrating with Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) for detailed information.

集成完成后，您可以创作将访 [客数据发送到](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) Adobe Target的目标内容。 请注意，页面组件需要特定代码才能启用内容定位。 (请参阅 [为目标内容开发](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html)。

>[!NOTE]
>
>在AEM作者中定位组件时，该组件会向Adobe Target发出一系列服务器端调用，以注册营销活动、设置选件和检索Adobe Target区段（如果已配置）。 不会从AEM发布到Adobe Target进行服务器端调用。

## 背景信息源 {#background-information-sources}

将AEM作为云服务与Adobe Target集成需要了解Adobe Target、AEM活动管理和AEM受众管理。 您应该熟悉以下信息：

* Adobe Target(请参阅 [Adobe Target文档](https://marketing.adobe.com/resources/help/en_US/target/))。
* AEM活动控制台(请参阅 [管理活动](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)。
* AEM受众(请参阅 [管理受众](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html)。

>[!NOTE]
>
>使用Adobe Target时，下面是营销活动中允许的最大对象数：
>
>* 50个地点
>* 2,000次体验
>* 50个指标
>* 50个报告分类
>


