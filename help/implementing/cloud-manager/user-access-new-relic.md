---
title: New Relic One
description: 了解 AEM as a Cloud Service 的 New Relic One 应用程序性能监控 (APM) 服务，以及如何访问该服务。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0712ba8918696f4300089be24cad3e4125416c02
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 40%

---


# New Relic One {#user-access}

了解 AEM as a Cloud Service 的 New Relic One 应用程序性能监控 (APM) 服务，以及如何访问该服务。

## 关于New Relic One {#introduction}

Adobe 非常重视应用程序的监控、可用性和性能。AEM as a Cloud Service包括访问New Relic One监控，作为标准产品的一部分，它使团队能够全面了解系统和环境性能指标。

本文档概述了如何在AEM as a Cloud Service环境中管理对New Relic One应用程序性能监控(APM)功能的访问。 有效管理这些功能可支持最佳性能并最大限度地发挥AEM as a Cloud Service的优势。

创建新的生产程序时，会自动创建与您的AEM as a Cloud Service程序关联的New Relic One子帐户。 [必须激活此子帐户](#activate-sub-account)才能开始摄取数据。

## 功能 {#transaction-monitoring}

AEM as a Cloud Service 的 New Relic One APM 具有许多功能。

* 直接访问专用的 New Relic One 帐户

* 检测了 New Relic One APM 代理，该代理使用行号显示准确的方法调用，包括外部依赖项和数据库

* 通过结合基础架构级别监控和应用程序 (Adobe Experience Manager) 监控的关键指标，实现整体性能优化

* AEM as a Cloud Service直接在New Relic Insights中公开Java管理扩展(JMX) MBean和执行状况检查，从而能够深入检查应用程序性能和运行状况指标。

## 激活您的New Relic One子帐户 {#activate-sub-account}

对于新创建的项目，将为您创建New Relic One子帐户。 但是，您必须激活它才能摄取数据。 此激活不是自动的。 按照以下步骤激活您的子帐户。

>[!NOTE]
>
>必须登录具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的用户才能管理New Relic One子帐户。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，单击要为其管理New Relic One用户的程序。

1. 在程序概述页面的&#x200B;**环境**&#x200B;信息卡上，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后选择&#x200B;**激活New Relic**。

   ![管理用户](assets/newrelic-activate-sub-account.png)

   * 您还可以访问&#x200B;**管理用户**&#x200B;选项。 在程序的&#x200B;**环境**&#x200B;屏幕顶部，单击![更多蒙版图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. [为同一环境运行管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)以成功完成子帐户激活。

停用子帐户时，不会摄取任何数据。

## 管理New Relic One用户 {#manage-users}

按照以下步骤定义您 AEM as a Cloud Service 程序关联的 New Relic One 子帐户用户。

>[!NOTE]
>
>必须登录具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的用户才能管理New Relic One用户。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要管理New Relic One用户的程序。

1. 在程序概述页面的&#x200B;**环境**&#x200B;卡片底部，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)并选择&#x200B;**管理用户**。

   ![管理用户](assets/newrelic-manage-users.png)

   * 您还可以访问&#x200B;**管理用户**&#x200B;选项。 在程序的&#x200B;**环境**&#x200B;屏幕顶部，单击![更多蒙版图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在&#x200B;**管理New Relic用户**&#x200B;对话框中，输入要添加的用户的名字和姓氏，然后单击&#x200B;**添加**&#x200B;按钮。 对要添加的所有用户重复此步骤。

   ![添加用户](assets/newrelic-add-users.png)

1. 要移除 New Relic One 用户，请单击代表该用户的行右端的删除按钮。

1. 单击&#x200B;**保存**，创建用户。

定义用户后，New Relic 会向您授予访问权限的每个用户发送一封确认电子邮件，以便用户完成设置过程并登录。

>[!NOTE]
>
>如果您正在管理New Relic One用户，则还必须将自己添加为用户，以便您自己具有访问权限。 作为&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;没有足够权限访问 New Relic One。您还必须将自己创建为用户。

## 激活您的New Relic One用户帐户 {#activate-user-account}

按照预览部分[管理 New Relic One 用户](#manage-users)中所述创建 New Relic One 用户帐户后，New Relic 会向提供的地址发送确认电子邮件。要使用这些帐户，用户必须首先通过重置密码来使用 New Relic 激活其帐户。

**激活您的New Relic One用户帐户：**

1. 单击来自New Relic的电子邮件中提供的链接。

1. 在New Relic登录页面上，单击&#x200B;**忘记密码？**

   ![New Relic 登录](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 输入您收到确认电子邮件的电子邮件地址，然后选择&#x200B;**发送我的重置链接**。

   ![输入电子邮件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic会向您发送一封电子邮件，其中包含确认帐户的链接。

如果未收到来自New Relic的确认电子邮件，请参阅[疑难解答部分](#troubshooting)。

## 访问New Relic One {#accessing-new-relic}

在您[激活您的New Relic帐户](#activate-account)后，您可以通过Cloud Manager或直接访问New Relic One。

**通过Cloud Manager访问New Relic One：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要访问New Relic One的程序。

1. 在程序概述页面的&#x200B;**环境**&#x200B;卡片底部，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后选择&#x200B;**打开New Relic**。

   ![管理用户](assets/newrelic-access.png)

   * 您还可以访问New Relic。 在程序的&#x200B;**环境**&#x200B;屏幕顶部，单击![更多蒙版图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在打开的新浏览器选项卡中，登录到 New Relic One。

**要直接访问New Relic One，请执行以下操作：**

1. 导航至 New Relic 的登录页面，网址为 [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. 登录 New Relic One。

### 验证您的电子邮件 {#verify-email}

如果在登录New Relic One期间要求您验证电子邮件，则意味着您的电子邮件与多个帐户相关联。 您可以选择要访问的帐户。

如果您不验证您的电子邮件地址，New Relic 会尝试使用与您的电子邮件关联的最近创建的用户记录登录。要避免在每次登录时验证您的电子邮件，请单击登录屏幕中的&#x200B;**记住我**&#x200B;复选框。

有关更多帮助，请通过 [AEM 支持门户](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)打开支持问题。

## New Relic One用户访问权限疑难解答 {#troubleshooting}

如果您被添加为New Relic One用户(如[管理New Relic One用户](#manage-users)中所述)，并且找不到原始帐户确认电子邮件，则可以执行以下疑难解答步骤。

**要对New Relic One用户访问权限进行故障排除：**

1. 导航至 New Relic 的登录页面，网址为 [`login.newrelic.com/login`](https://login.newrelic.com/login)。

1. 单击&#x200B;**[!UICONTROL 忘记密码？]**。

   ![New Relic 登录](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 输入用于创建帐户的电子邮件地址，然后选择&#x200B;**发送我的重置链接**。

   ![输入电子邮件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic会向您发送一封电子邮件，其中包含确认帐户的链接。

如果您完成了注册过程，并且由于电子邮件或密码错误消息而无法登录到您的帐户，请通过[Admin Console](https://adminconsole.adobe.com/)提交支持工单。

如果您没有收到来自New Relic的电子邮件，请执行以下操作：

* 检查您的[垃圾邮件过滤器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/)。
* 如果适用，[将New Relic添加到您的电子邮件允许列表](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist)。
* 如果这两个建议都没有帮助，请提供有关支持票证的反馈。

## 使用说明 {#usage-notes}

* 最多可以添加 30 个用户。如果已达到最大用户数，请移除用户，以便能够添加新用户。
* 添加到New Relic的用户为&#x200B;**Basic**&#x200B;类型。 有关详细信息，请参阅[New Relic文档](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-type/)。
* AEM as a Cloud Service 仅提供 New Relic One APM 解决方案，不支持警报、日志记录或 API 集成。

>[!NOTE]
>
>如果在您的New Relic One子帐户中连续超过30天未检测到&#x200B;**用户登录**&#x200B;活动，则APM代理将停止。 数据不会从AEM Cloud Service发送到New Relic。 *在重新激活您的子帐户之前，不会再次发送数据。*
>
>按照本文档的[激活您的New Relic One子帐户](#activate-sub-account)部分中的相同步骤重新激活您的New Relic One子帐户。

有关AEM as a Cloud Service计划的New Relic One产品的更多帮助或更多指导，请通过[AEM支持门户](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)打开支持工单。

## 常见问题解答 {#faqs}

+++**Adobe使用New Relic One监视什么？**

Adobe 监控 AEM as a Cloud Service 作者，并通过 New Relic One 的 Java 插件发布和预览（如果可用）服务。Adobe 支持跨非生产和生产 AEM as a Cloud Service 环境的自定义 New Relic One APM 遥测和监控。

您的New Relic One帐户附加到Adobe维护的主帐户，并有多个应用程序向其报告；每个AEM as a Cloud Service环境三个。

* 每个环境一个Author服务应用程序
* 每个环境一个`Publish`服务应用程序（包括Golden Publish）
* 每个环境一个预览服务应用程序

注意:

* 每个应用程序使用一个许可证密钥。
* AEM as a Cloud Service 环境仅向一个 New Relic One 帐户报告。
* New Relic One的全面监控指标和事件将保留三个月。

+++

+++**Adobe是否从New Relic One发送警报通知？**

Adobe仅出于可观察性目的提供New Relic One访问权限，不将其用于客户警报或内部运营警报。 使用[用户通知配置文件](/help/journey-onboarding/notification-profiles.md)发送任何事件的通知。
+++

+++**谁可以访问New Relic One云服务数据？**

您的团队最多可以有 30 名成员获得完全读取权限。读取权限包括由New Relic One代理收集的所有APM指标。
+++

+++**是否支持自定义SSO配置？**

Adobe 设置的 New Relic One 帐户不支持自定义 SSO 配置。
+++

+++**如果我已有本地New Relic订阅，该怎么办？**

New Relic One 是 New Relic 推出的新可观察性平台，它使 Adobe 支持和您的团队能够在一个地方观察、监控和查看指标和事件。

New Relic One 为用户提供了跨所有帐户搜索的能力，用户可以在一个视图中访问和可视化来自所有服务和主机的数据。

Adobe支持使用New Relic One和其他工具监控AEM as a Cloud Service，而您的团队仍然可以使用New Relic提供本地服务和基础架构。 他们能够以可视化图表形式查看来自 Adobe New Relic One 帐户和客户管理的 New Relic 帐户的数据。

>[!NOTE]
>
>要在 New Relic One 中查看这两个数据集，用户必须具有正确的权限，并对这两个帐户（Adobe New Relic One 和客户管理的 New Relic 帐户）使用相同的登录方法。

+++

+++**我的New Relic One帐户的APM代理已停止。 发生什么情况？**

如果在 30 天或更长时间内未检测到任何活动，[APM 代理将停止](#limitations)。按照本文档的[激活您的New Relic One子帐户](#activate-sub-account)部分中的相同步骤重新激活您的New Relic One子帐户。
+++
