---
title: New Relic One
description: 了解 AEM as a Cloud Service 的 New Relic One 应用程序性能监控 (APM) 服务，以及如何访问该服务。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 524212d1c68ef31d7fa01dc22296ddae54a0a3d1
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 100%

---


# New Relic One {#user-access}

了解 AEM as a Cloud Service 的 New Relic One 应用程序性能监控 (APM) 服务，以及如何访问该服务。

## 简介 {#introduction}

Adobe 非常重视应用程序的监控、可用性和性能。 AEM as a Cloud Service 作为标准产品的一部分，提供对自定义 New Relic One 监控套件的访问权限，以确保您的团队能够最大限度地了解 AEM as a Cloud Service 系统和环境性能量度。

本文档描述了如何管理对您的 AEM as a Cloud Service 环境上启用的 New Relic One 应用程序性能监控 (APM) 功能的访问，促进支持性能并让您最大限度地利用 AEM as a Cloud Service。

创建新的生产程序时，会自动创建与 AEM as a Cloud Service 程序关联的 New Relic One 子帐户。

## 功能 {#transaction-monitoring}

AEM as a Cloud Service 的 New Relic One APM 具有许多功能。

* 直接访问专用的 New Relic One 帐户

* 检测了 New Relic One APM 代理，该代理使用行号显示准确的方法调用，包括外部依赖项和数据库

* 通过结合基础架构级别监控和应用程序 (Adobe Experience Manager) 监控的关键指标，实现整体性能优化

* 将 AEM as a Cloud Service JMX Mbeans 和健康检查直接暴露在 New Relic Insights 量度中，支持深入检查应用程序堆栈性能和健康量度。

## 管理 New Relic One 用户 {#manage-users}

按照以下步骤定义您 AEM as a Cloud Service 程序关联的 New Relic One 子帐户用户。

>[!NOTE]
>
>必须登录具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户才能管理 New Relic One 用户。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要管理 New Relic One 用户的程序。

1. 在程序概述页面的&#x200B;**环境**&#x200B;信息卡上，单击省略号按钮，然后选择&#x200B;**管理用户**。

   ![管理用户](assets/newrelic-manage-users.png)

   * 您还可以通过程序的&#x200B;**环境**&#x200B;屏幕顶部的省略号按钮访问&#x200B;**管理用户**。

1. 在&#x200B;**管理 New Relic 用户**&#x200B;对话框中，输入要添加的用户的名字和姓氏，然后单击&#x200B;**添加**&#x200B;按钮。对要添加的所有用户重复此步骤。

   ![添加用户](assets/newrelic-add-users.png)

1. 要移除 New Relic One 用户，请单击代表该用户的行右端的删除按钮。

1. 单击&#x200B;**保存**，创建用户。

定义用户后，New Relic 会向您授予访问权限的每个用户发送一封确认电子邮件，以便用户完成设置过程并登录。

>[!NOTE]
>
>如果您正在管理 New Relic One 用户，您还必须将自己添加为用户，以便您也可以访问。作为&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;没有足够权限访问 New Relic One。 您还必须将自己创建为用户。

## 激活您的 New Relic One 用户帐户 {#activate-account}

按照预览部分[管理 New Relic One 用户](#manage-users)中所述创建 New Relic One 用户帐户后，New Relic 会向提供的地址发送确认电子邮件。 要使用这些帐户，用户必须首先通过重置密码来使用 New Relic 激活其帐户。

按照以下步骤以 New Relic 用户身份激活您的帐户。

1. 单击 New Relic 电子邮件中提供的链接。 这将打开浏览器，进入 New Relic 登录页面。

1. 在 New Relic 登录页面上，选择&#x200B;**忘记密码？**。

   ![New Relic 登录](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 输入您收到确认电子邮件的电子邮件地址，然后选择&#x200B;**发送我的重置链接**。

   ![输入电子邮件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic 将向您发送一封电子邮件，其中包含确认帐户的链接。

如果您没有收到 New Relic 的确认电子邮件，请参阅[故障排除部分。](#troubshooting)

## 正在访问 New Relic One {#accessing-new-relic}

一旦[激活了您的 New Relic 帐户，](#activate-account)您就可以通过云管理器或直接访问 New Relic One。

要通过 Cloud Manager 访问 New Relic One，请执行以下操作：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要访问 New Relic One 的程序。

1. 在程序概述页面的&#x200B;**环境**&#x200B;信息卡上，单击省略号按钮，然后选择&#x200B;**打开 New Relic**。

   ![管理用户](assets/newrelic-access.png)

   * 您还可以通过程序的&#x200B;**环境**&#x200B;屏幕顶部的省略号按钮访问 New Relic。

1. 在打开的新浏览器选项卡中，登录到 New Relic One。

要直接访问 New Relic One：

1. 导航至 New Relic 的登录页面，网址为 [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. 登录 New Relic One。

### 正在验证您的电子邮件 {#verify-email}

如果在登录 New Relic One 时要求您验证电子邮件，这意味着您的电子邮件与多个帐户关联。 这允许您选择要访问的帐户。

如果您不验证您的电子邮件地址，New Relic 将尝试使用与您的电子邮件关联的最近创建的用户记录登录。要避免在每次登录时验证您的电子邮件，请单击登录屏幕中的&#x200B;**记住我**&#x200B;复选框。

有关更多帮助，请通过 [AEM 支持门户](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)打开支持问题。

## New Relic One 访问故障排除 {#troubleshooting}

如果您按照[管理 New Relic One 用户](#manage-users)一节中所述被添加为 New Relic One 用户，并且无法找到原始帐户确认电子邮件，请执行以下步骤。

1. 导航至 New Relic 的登录页面，网址为 [`login.newrelic.com/login`](https://login.newrelic.com/login)。

1. 选择&#x200B;**忘记密码？**。

   ![New Relic 登录](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 输入用于创建帐户的电子邮件地址，然后选择&#x200B;**发送我的重置链接**。

   ![输入电子邮件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic 将向您发送一封电子邮件，其中包含确认帐户的链接。

如果您完成了注册过程，并且由于电子邮件或密码错误消息而无法登录到您的帐户，请通过 [Admin Console 提交支持请求工单。](https://adminconsole.adobe.com/)

如果您没有收到 New Relic 的电子邮件：

* 检查您的[垃圾邮件过滤器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/)。
* 如果适用，[请将 New Relic 添加到您的电子邮件允许列表中](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist)。
* 如果这两个建议都没有帮助，请提供有关支持请求工单的反馈，Adobe 支持团队将进一步帮助您。

## 限制 {#limitations}

以下限制适用于向 New Relic One 添加用户：

* 最多可以添加 30 个用户。 如果已达到最大用户数，请移除用户，以便能够添加新用户。
* 添加到 New Relic 的用户将属于&#x200B;**受限**&#x200B;类型。有关详细信息，请参阅 [New Relic 文档。](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Service 仅提供 New Relic One APM 解决方案，不支持警报、日志记录或 API 集成。

有关您的 AEM as a Cloud Service 程序的 New Relic One 产品的更多帮助或更多指导，请通过 [AEM 支持门户](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)打开支持请求工单。

## 关于 New Relic One 的常见问题 {#faqs}

### Adobe 使用 New Relic One 监控什么？ {#adobe-monitor}

Adobe 监控 AEM as a Cloud Service 作者，并通过 New Relic One 的 Java 插件发布和预览（如果可用）服务。 Adobe 支持跨非生产和生产 AEM as a Cloud Service 环境的自定义 New Relic One APM 遥测和监控。

您的 New Relic One 帐户连接到 Adobe 维护的主帐户，并有多个应用程序向其报告：每个 AEM as a Cloud Service 环境三个应用程序。

* 每个环境一个作者服务应用程序
* 每个环境一个发布服务应用程序（包括 Golden Publish）
* 每个环境一个预览服务应用程序

请注意：

* 每个应用程序使用一个许可证密钥。
* AEM as a Cloud Service 环境仅向一个 New Relic One 帐户报告。
* New Relic One 的全面监控指标和事件保留七天。

### 谁可以访问 New Relic One 云服务数据？ {#access-new-relic-cloud}

您的团队最多可以有 30 名成员获得完全读取权限。 读取权限将包括 New Relic One 代理收集的所有 APM 量度。

### 是否支持自定义 SSO 配置？ {#custom-sso}

Adobe 设置的 New Relic One 帐户不支持自定义 SSO 配置。

### 如果我已经有一个本地 New Relic 订阅怎么办？ {#new-relic-subscription}

New Relic One 是 New Relic 推出的新可观察性平台，它使 Adobe 支持和您的团队能够在一个地方观察、监控和查看指标和事件。

New Relic One 为用户提供了跨所有帐户搜索的能力，用户可以在一个视图中访问和可视化来自所有服务和主机的数据。

虽然 Adobe 支持人员将使用 New Relic One 和其他内部工具作为您服务的一部分，将 AEM as a Cloud Service 应用程序进行监控，但您的团队可以继续利用 New Relic 提供本地托管服务和基础设施。他们将能够以可视化图表形式查看来自 Adobe New Relic One 帐户和客户管理的 New Relic 帐户的数据。

>[!NOTE]
>
>要在 New Relic One 中查看这两个数据集，用户必须具有正确的权限，并对这两个帐户（Adobe New Relic One 和客户管理的 New Relic 帐户）使用相同的登录方法。
