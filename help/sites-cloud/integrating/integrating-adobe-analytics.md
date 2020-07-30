---
title: 与 Adobe Analytics 集成
description: '与 Adobe Analytics 集成 '
translation-type: tm+mt
source-git-commit: f2ed74afd2df43e31ff1002cd42a60f372d0b769
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics和AEM集成为Cloud Service，使您能够跟踪网页活动。 集成需要：

* 使用触屏UI在AEM中创建Analytics配置作为Cloud Service。
* 在Adobe Analytics启动中添加和配置Adobe [作为扩展]。(https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)。

与AEM的先前版本相比，在AEM的Analytics配置中不作为Cloud Service提供框架支持。 现在，它通过Adobe启动来完成，该工具是检验具有Analytics功能的AEM站点（JS库）的实际工具。 在Adobe启动中，将创建一个属性，在该属性中可以配置Adobe Analytics扩展，并创建规则以将数据发送到Adobe Analytics。 Adobe启动已取代sitecatalyst提供的分析任务。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有Analytics帐户的Cloud Service客户，可以请求访问Analytics基础包以进行Experience Cloud。 此Foundation Pack提供对Analytics的批量限制使用。

## 创建Analytics配置 {#analytics-configuration}

1. 导航到 **工具** → **Cloud Service**。
2. 选择 **Adobe Analytics配置**。
   ![Analytics](assets/analytics_screen1.png "窗口分析窗口")
3. 选择“创 **建** ”按钮。
4. 填写详细信息（请参阅下面的内容），然后单击“ **连接**”。

### 配置参数 {#configuration-parameters}

“Adobe Analytics配置”窗口中的配置字段包括：

![配置参](assets/properties_field1.png "数配置参数")

| 属性 | 描述 |
|---|---|
| 公司 | Adobe Analytics登录公司 |
| 用户名 | Adobe AnalyticsAPI用户 |
| 密码 | Adobe Analytics密码用于身份验证 |
| 数据中心 | 您的帐户与Adobe Analytics数据中心关联（例如，San Jose, London） |
| 区段 | 选项可用于使用在当前Analytics套件中定义的报告段。 Analytics报表将根据区段进行筛选。 有关其 [他详细信息](https://docs.adobe.com/content/help/en/analytics/components/segmentation/seg-overview.html) ，请参阅本页。 |
| 报表包 | 用于发送数据和提取报告的存储库。 报表包定义所选网站、网站集或网站页面子集上完整、独立的报告。 您可以视图从单个报表包获取的报表，并可以根据需要随时在配置中编辑此字段。 |

### 向站点添加配置 {#add-configuration}

要将触屏UI配置应用到站点，请转至： **站点** 选择任何站点 **页面** →属 **性** →高级 **→配置** →→ **** 选择配置租户。

## 通过使用Adobe启动将Adobe Analytics整合到AEM站点

Adobe Analytics可以作为扩展添加到启动属性中。 可以定义规则以执行映射和向Adobe Analytics发出帖子：

* 观 [看此视频](https://docs.adobe.com/content/help/en/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) ，了解如何在Launch中为基本站点配置Analytics扩展。

* 有关 [如何创建规则](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) 和将数据发送到Adobe Analytics的详细信息，请参阅本页。

>[!NOTE]
>
>现有（旧版）框架仍然有效，但无法在触屏UI中配置。 建议在启动中重新构建变量映射配置。

>[!NOTE]
>
>在AEM中，Launch的IMS配置（技术帐户）预配置为Cloud Service。 用户不必创建此配置。
