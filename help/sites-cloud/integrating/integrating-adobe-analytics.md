---
title: 与 Adobe Analytics 集成
description: '与 Adobe Analytics 集成 '
translation-type: tm+mt
source-git-commit: 76db5314369ca0f854482586d5c96474014a47af
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 4%

---


# 与 Adobe Analytics 集成{#integrating-with-adobe-analytics}

将Adobe Analytics和AEM集成为Cloud Service，使您能够跟踪网页活动。 集成需要：

* 使用触屏UI在AEM中创建Analytics配置作为Cloud Service。
* 在[Adobe启动](#analytics-launch)中添加和配置Adobe Analytics作为扩展。 有关Adobe启动的详细信息，请参阅[此页](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)。

与AEM的先前版本相比，AEM中的分析配置中不作为Cloud Service提供框架支持。 现在，它通过Adobe启动来完成，该启动工具实际上是用于借助Analytics功能（JS库）检验AEM站点的工具。 在Adobe启动中，将创建一个属性，在该属性中可以配置Adobe Analytics扩展，并创建规则以将数据发送到Adobe Analytics。 Adobe启动已取代sitecatalyst提供的分析任务。

>[!NOTE]
>
>Adobe Experience Manager作为没有现有Analytics帐户的Cloud Service客户，可以请求访问Analytics Foundation Pack进行Experience Cloud。 此Foundation Pack提供对Analytics的批量有限使用。

## 创建Adobe Analytics配置{#analytics-configuration}

1. 导航到&#x200B;**工具**→ **Cloud Services**。
2. 选择&#x200B;**Adobe Analytics**。
   ![Adobe Analytics](assets/analytics_screen2.png "窗口Adobe Analytics窗口")
3. 选择&#x200B;**创建**&#x200B;按钮。
4. 填写详细信息（请参见下文），然后单击&#x200B;**Connect**。

### 配置参数{#configuration-parameters}

“Adobe Analytics配置”窗口中的配置字段包括：

![配置参](assets/properties_field1.png "数配置参数")

| 属性 | 描述 |
|---|---|
| 公司 | Adobe Analytics登录公司 |
| 用户名 | Adobe AnalyticsAPI用户 |
| 密码 | Adobe Analytics密码用于身份验证 |
| 数据中心 | 您的帐户与Adobe Analytics数据中心关联（例如，San Jose, London） |
| 区段 | 使用当前报告套件中定义的Analytics区段的选项。 将根据区段过滤Analytics报告。 有关更多详细信息，请参阅[此页](https://docs.adobe.com/content/help/en/analytics/components/segmentation/seg-overview.html)。 |
| 报表包 | 用于发送数据和提取报告的存储库。 报表包定义所选网站、网站集或网站页面子集上完整、独立的报告。 您可以视图从单个报表包获取的报表，并可以根据需要随时在配置中编辑此字段。 |

### 将配置添加到站点{#add-configuration}

要将触屏UI配置应用到站点，请转至：**站点**→ **选择任何站点页面**→ **属性**→ **高级**→配置&#x200B;**→选择配置租户。**

## 通过使用Adobe启动{#analytics-launch}在Adobe Analytics站点上集成AEM

Adobe Analytics可以作为扩展添加到启动属性中。 可以定义规则以执行映射和向Adobe Analytics发出帖子：

* 观看[此视频](https://docs.adobe.com/content/help/en/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html)，了解如何在Launch中为基本站点配置Analytics扩展。

* 有关如何创建规则和将数据发送到Adobe Analytics的详细信息，请参阅[此页](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html)。

>[!NOTE]
>
>现有（旧版）框架仍然有效，但无法在触屏UI中配置。 建议在启动中重新构建变量映射配置。

>[!NOTE]
>
>在AEM中，Launch的IMS配置（技术帐户）预配置为Cloud Service。 用户不必创建此配置。
