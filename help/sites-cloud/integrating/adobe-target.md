---
title: 与 Adobe Target 集成
description: 与 Adobe Target 集成
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: ht
source-wordcount: '727'
ht-degree: 100%

---

# 与 Adobe Target 集成{#integrating-with-adobe-target}

作为 Adobe Marketing Cloud 的一部分，[Adobe Target](https://www.adobe.com/cn/solutions/testing-targeting/testandtarget.html) 允许您通过在所有渠道中进行定位和衡量来提高内容相关性。营销人员使用 Adobe Target 来设计和执行在线测试、创建动态受众区段（基于行为）以及自动定位内容和在线体验。AEM as a Cloud Service 采用了 Adobe Target Standard 中使用的定位工作流。如果您使用 Target，您将熟悉 AEM as a Cloud Service 中的定位编辑环境。

将 AEM Sites 与 Adobe Target 集成以个性化页面中的内容：

* 实施内容定位。
* 使用 Target 受众创建个性化体验。
* 在访客与您的页面交互时，将上下文数据提交到 Target。
* 跟踪转化率。

>[!NOTE]
>
>不具有现有 Target 帐户的 Adobe Experience Manager as a Cloud Service 客户可以请求对 Target Foundation Pack for Experience Cloud 的访问权限。此 Foundation Pack 提供了对 Target 的限量使用。


要与 Target 集成，请执行以下任务：

* [执行必备任务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html)：向 Adobe Target 注册并配置 AEM 创作实例的某些方面。您的 Adobe Target 帐户必须至少具有&#x200B;**批准者**&#x200B;级别权限。此外，您必须保护发布节点上的活动设置，以便用户无法访问。

* Adobe Launch 是用于通过 Target 功能（JS 库）检测 AEM 站点的实际工具。因此，将 AEM as a Cloud Service 与 Launch 和 Adobe Target 集成是密切相关的（请参阅下面的链接）。

   * [使用 Adobe I/O 与 Adobe Target 集成](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims-adobe-io.html)
   * [集成 Adobe Launch](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [通过 Adobe I/O 将 AEM 与 Adobe Launch 集成](https://docs.adobe.com/content/help/zh-Hans/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)
   * [了解 AEM 与 Adobe Launch、Analytics 和 Target 的集成](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html)

>[!NOTE]
>
>已在 AEM as a Cloud Service 中预配置 Adobe Launch 的 IMS 配置（技术帐户）。用户无需创建此配置。

1. [配置活动](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)：将您的活动与 Target 云配置相关联。

>[!CAUTION]
>
>在 AEM as a Cloud Service 中，默认情况下，将选件和活动从 AEM 同步到 Adobe Target 的复制代理处于禁用状态。如果您需要重新启用此复制代理，请联系 [Adobe 支持](https://experienceleague.adobe.com/?support-solution=General#support)团队。

>[!NOTE]
>
>如果您将 Target 与自定义代理配置一起使用，则需要配置 HTTP 客户端代理配置，因为 AEM 的某些功能使用的是 3.x API，而其他一些功能使用的是 4.x API：
>
>* 3.x 通过 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 进行配置
>* 4.x 通过 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) 进行配置
>


>[!CAUTION]
>
>您必须确保发布实例中的活动设置节点 **cq:ActivitySettings** 安全，以使其不可由普通用户访问。该活动设置节点应当只能由负责将活动同步到 Adobe Target 的服务访问。
>
>请参阅[与 Adobe Target 集成的先决条件](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node)，以了解详细信息。

在集成完成后，您可以[创作目标内容](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html)来将访客数据发送到 Adobe Target。请注意，页面组件需要特定代码才能启用内容定位。（请参阅[针对目标内容进行开发](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html)。）

>[!NOTE]
>
>在 AEM 创作实例中定位组件时，该组件会对 Adobe Target 进行一系列的服务器端调用，以便注册活动、设置选件和检索 Adobe Target 区段（如果已配置）。没有从 AEM Publish 到 Adobe Target 的服务器端调用。

## 背景信息源 {#background-information-sources}

将 AEM as a Cloud Service 与 Adobe Target 集成需要了解 Adobe Target、AEM Activities 管理和 AEM Audiences 管理。您应熟悉以下信息：

* Adobe Target（请参阅 [Adobe Target 文档](https://experienceleague.adobe.com/docs/target/using/target-home.html)）。
* AEM Activities 控制台（请参阅[管理活动](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)）。
* AEM Audiences（请参阅[管理受众](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html)）。

>[!NOTE]
>
>使用 Adobe Target 时，以下是活动中允许的最大构件数：
>
>* 50 个位置
>* 2,000 个体验
>* 50 个量度
>* 50 个报告区段

