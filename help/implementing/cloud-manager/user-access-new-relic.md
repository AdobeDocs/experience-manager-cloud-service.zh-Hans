---
title: 新遗迹一号
description: 了解用于AEMas a Cloud Service的New Relic One应用程序性能监控(APM)服务以及如何访问该服务。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 2%

---


# 新遗迹一号 {#user-access}

了解用于AEMas a Cloud Service的New Relic One应用程序性能监控(APM)服务以及如何访问该服务。

## 简介 {#introduction}

Adobe非常重视应用程序的监控、可用性和性能。 为帮助实现此目标，AEMas a Cloud Service提供对自定义New Relic One监视包的访问，这是标准产品产品的一部分，可确保您的团队能够最大程度地了解您的AEMas a Cloud Service系统和环境性能指标。

本文档介绍了在您的AEMas a Cloud Service环境中启用的新Relic One应用程序性能监控(APM)功能，以帮助支持性能并让您充分利用AEMas a Cloud Service。

## 功能 {#transaction-monitoring}

New Relic One APM for AEMas a Cloud Service具有许多功能。

* 直接访问专用的New Relic One帐户(由Adobe支持管理的访问)

* 分析New Relic One APM代理，它显示具有行号的精确方法调用，包括外部依赖关系和数据库

* 通过将基础架构级别监控和应用程序(Adobe Experience Manager)监控中的关键量度整合在一起，实现整体性能优化

* 直接在“新旧物分析”量度中显示AEMas a Cloud ServiceJMX Mbeans和运行状况检查，从而可以深入检查应用程序堆栈性能和运行状况量度。

## 访问New Relic One {#accessing-new-relic}

请按照以下步骤访问与您的AEMas a Cloud Service计划关联的New Relic One子帐户。

1. 请访问Admin Console中的支持选项卡以打开请求。
1. 在您的请求中，包括您的计划ID的详细信息以及需要访问新旧版的用户列表。
   * 必须提供所有用户的完整名称和有效电子邮件地址。

请参阅文档 [AEM支持门户以Experience Cloud](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) 有关开票的更多详细信息。

提供访问权限后，New Relic会向每个用户发送确认电子邮件，以便用户完成设置过程并登录。

如果用户找不到原始帐户确认电子邮件，请按照以下步骤操作。

1. 导航到New Relic的登录页面： [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. 选择 **忘记密码了？**.

   ![新旧版登录](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 键入帐户电子邮件地址，然后选择 **发送我的重置链接**.

   ![输入电子邮件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic将向用户发送一封包含确认帐户链接的电子邮件。

如果您完成注册过程，并且由于电子邮件或密码错误消息而无法登录帐户，请通过 [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>如果您没有收到New Relic发送的电子邮件：
>
>* 检查 [垃圾过滤器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* 如果适用， [将新旧内容添加到电子邮件允许列表](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* 如果这两个建议都不有帮助，请提供有关支持票证的反馈，Adobe支持团队将进一步帮助您。


### 验证电子邮件 {#verify-email}

如果在登录期间要求您验证电子邮件，则表示您的电子邮件与多个帐户关联。 这允许您选择要访问的帐户。

如果您未验证您的电子邮件地址，New Relic将尝试使用与您的电子邮件地址关联的最近创建的用户记录登录。 要避免在每次登录期间验证您的电子邮件，请单击 **记住我** 复选框。

如需更多帮助，请通过 [AEM支持门户](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## 例外 {#exceptions}

AEM as a Cloud Service仅提供New Relic One APM解决方案，不支持警报、日志记录或API集成。

要获取有关New Relic One产品的AEMas a Cloud Service计划的更多帮助或其他指导，请通过 [AEM支持门户](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## 有关新旧帐户的常见问题解答 {#faqs}

### Adobe用New Relic One监视什么？ {#adobe-monitor}

Adobe通过New Relic One的Java插件监控AEMas a Cloud Service的创作、发布和预览（如果可用）服务。 Adobe支持跨非生产和生产AEMas a Cloud Service环境的自定义New Relic One APM遥测和监控。

您的New Relic One帐户已附加到由Adobe维护的主帐户，并有多个应用程序报告到该帐户中：每个AEMas a Cloud Service环境3个。

* 每个环境有一个用于创作服务的应用程序
* 每个环境（包括Golden Publish）有一个用于发布服务的应用程序
* 每个环境有一个用于预览服务的应用程序

请注意：

* 每个应用程序都使用一个许可证密钥。
* AEMas a Cloud Service环境仅报告给一个New Relic One帐户。
* New Relic One的完整监控量度和事件将保留7天。

### 谁可以访问New Relic One云服务数据？ {#access-new-relic-cloud}

您团队的成员最多可以获得10个的完全读取访问权限。 读取访问将包括New Relic One代理收集的所有APM量度。

### 是否支持自定义SSO配置？ {#custom-sso}

由Adobe设置的New Relic One帐户不支持自定义SSO配置。

### 如果我已经拥有内部New Relic订购，该怎么办？ {#new-relic-subscription}

New Relic One是New Relic的新可观测平台，它使Adobe支持和您的团队能够在一个位置观察、监控和查看量度和事件。

New Relic One使用户能够在他们有权访问的所有帐户中进行搜索，并在一个视图中显示所有服务和主机的数据。

虽然Adobe支持将使用New Relic One和其他内部工具监控AEMas a Cloud Service应用程序作为服务的一部分，但您的团队可以继续利用New Relic进行本地托管服务和基础架构。 他们将能够将AdobeNew Relic One帐户和客户管理的New Relic帐户中的数据可视化。

>[!NOTE]
>
>要在New Relic One中查看两个数据集，用户必须拥有正确的权限，并对两个帐户(AdobeNew Relic One和客户管理的New Relic帐户)使用相同的登录方法。
