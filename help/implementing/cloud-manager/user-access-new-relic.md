---
title: 用户访问新旧版
description: 请阅读本页，了解New Relic Application Performance Monitoring for AEMas a Cloud Service
source-git-commit: 696b86e9e88ca1fd7c0a5b688fa78f46227df3a4
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---


# 用户访问新旧版 {#user-access}

## 简介 {#introduction}

Adobe高度重视应用程序的监控、可用性和性能。 为帮助实现此目标，AEM as a Cloud Service提供了对自定义New Relic监控包的访问，这是标准产品产品的一部分，可确保您的团队能够最大程度地了解您的Adobe Experience ManagerCloud Service系统和环境性能指标。 本节介绍在您的AEMas a Cloud Service环境中启用的New Relic监控功能，以帮助提高性能并让您充分利用AEMas a Cloud Service。

## AEMas a Cloud Service交易监控的新历史 — 价值主张 {#transaction-monitoring}

以下是New Relic Application Performance Monitoring for AEMas a Cloud Service的价值主张摘要：

* 直接访问专用的New Relic One帐户(由Adobe支持管理的访问)。

* 分析了New Relic APM代理，该代理显示具有行号的精确方法调用，包括外部依赖关系和数据库。

* 通过将基础架构级别监控和应用程序(Adobe Experience Manager)监控中的关键量度整合在一起，实现整体性能优化。

* 将AEMas a Cloud ServiceJMX Mbeans和运行状况检查直接暴露到新的Relic Insights量度中，以便对应用程序堆栈性能和运行状况量度进行深入检查。

## 访问您的AEMas a Cloud ServiceNew Relic帐户 {#accessing-new-relic}

您的专用New Relic帐户将通过客户关怀团队的参与由Adobe进行配置和管理。 Adobe将仍然是所有者和管理员，并将代表您配置帐户以提供对专用子帐户的访问权限。

要访问与您的AEMas a Cloud Service计划关联的New Relic子帐户，请执行以下操作：

* 请访问Admin Console中的支持选项卡以打开请求。
* 确保您的票证中包含项目ID的详细信息以及请求Adobe团队打开新旧版物访问权限的用户列表。
* 必须向所有用户提供全名和有效的电子邮件地址。

   >[!NOTE]
   >请参阅 [AEM支持门户以Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 以了解更多详细信息。

提供访问权限后，New Relic会向每个用户发送确认电子邮件，以便用户完成设置过程并登录。

如果用户找不到原始帐户确认电子邮件：

1. 导航到New Relic的登录页面： [login.newrelic.com/login](https://login.newrelic.com/login).

1. 选择 **忘记密码**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 键入帐户电子邮件地址，然后选择 **发送我的重置链接**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. 当New Relic的系统返回电子邮件时，请选择其中的链接以再次确认您的帐户。

   >[!NOTE]
   >如果您没有收到New Relic发送的电子邮件：
   >检查 [垃圾过滤器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/). 如果适用， [将新旧内容添加到电子邮件允许列表](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
   >请提供有关支持票证的反馈，Adobe支持团队将进一步帮助您。

1. 如果您完成注册过程，并且由于电子邮件或密码错误消息而无法登录帐户，请通过记录支持票证 [Admin Console](https://adminconsole.adobe.com/).

### 验证电子邮件 {#verify-email}

如果在登录期间要求您验证电子邮件，则表示您的电子邮件与多个帐户关联，并且在登录期间，您将可以选择验证电子邮件。 这将允许您选择要访问的帐户。 如果您未验证您的电子邮件地址，New Relic将尝试使用与您的电子邮件地址关联的最近创建的用户记录登录。 要避免在每次登录期间验证您的电子邮件，请单击登录屏幕中的记住我复选框。

如需更多帮助，请通过 [AEM支持门户](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## 例外 {#exceptions}

AEM as a Cloud Service仅将产品重点放在New Relic APM解决方案上，不支持警报、日志记录或API集成功能。

有关AEMas a Cloud Service计划的New Relic产品的更多帮助或其他指导，请通过 [AEM支持门户](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 以寻求帮助。

## 有关新旧帐户的常见问题解答 {#faqs}

### Adobe用New Relic监视什么？ {#adobe-monitor}

Adobe通过New Relic APM Java插件监控AEMas a Cloud Service创作、发布和预览（如果可用）服务。 Adobe支持跨非生产和生产AEMas a Cloud Service环境的自定义New Relic APM遥测和监控。 您的New Relic帐户已附加到主Adobe维护帐户，并有多个应用程序报告到该帐户中。

每个AEMas a Cloud Service环境各3个：

* 每个环境有一个用于创作服务的应用程序
* 每个环境（包括Golden Publish）有一个用于发布服务的应用程序
* 每个环境有一个用于预览服务的应用程序
   >[!IMPORTANT]
   >每个应用程序使用一个许可证密钥，AEMas a Cloud Service环境将仅报告给一个New Relic帐户。 New Relic APM的完整监控量度和事件将保留7天。

### 谁可以访问New RelicCloud Service数据？ {#access-new-relic-cloud}

您团队的成员最多可以获得10个的完全读取访问权限。 读取访问权限将包括由New Relic代理收集的所有APM量度。

### 是否支持自定义SSO配置？ {#custom-sso}

当前，由Adobe设置的新旧帐户不支持自定义SSO配置。

### 如果您已经拥有内部新旧物品订购，该怎么办？ {#new-relic-subscription}

New Relic One的新可观测性平台称为New Relic One ，使Adobe支持小组和您的团队能够在一个位置观察、监控和查看量度和事件。 New Relic One使用户能够在他们有权访问的所有帐户中进行搜索，并在一个视图中显示所有服务和主机的数据。 虽然Adobe支持团队将使用New Relic和其他内部工具监控AEMas a Cloud Service应用程序，作为您服务的一部分，但您的团队可以继续利用New Relic进行本地托管服务和基础架构。 他们将能够显示Adobe和客户管理的New Relic帐户的数据。

>[!NOTE]
>用户必须拥有相应的权限，并对这两个帐户(Adobe和客户管理的New Relic帐户)使用相同的登录方法。


