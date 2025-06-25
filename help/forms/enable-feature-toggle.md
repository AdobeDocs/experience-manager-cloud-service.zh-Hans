---
title: 启用功能切换以集成早期采用者和预发行版功能
description: 功能切换是AEM中的一项功能，它允许管理员在运行时环境中启用新功能。
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
source-git-commit: cc4fccc51f487170bf6c14e4b302a8d5912c33a0
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 在Adobe Experience Software Development Kit (AEM SDK)上启用功能切换

AEM中的功能切换允许管理员在运行时启用或禁用功能，非常适合在不更改代码的情况下管理早期采用者和预发行版功能。 它支持逐步转出、A/B测试和快速停用不稳定特征。

本文介绍如何在AEM本地SDK设置中启用功能切换，该设置使用SDK和Dispatcher模拟AEM as a Cloud Service。 此设置可帮助团队先在类似生产的环境中进行测试，然后再部署到云。

## 为何在AEM SDK设置中使用功能切换？

在AEM SDK设置中工作时，功能可切换以下帮助：

* 安全地测试实验功能。

* 分阶段推出新组件。

* 跨多个环境维护单个代码库。

* 减少部署和升级期间的风险。

## 先决条件

在AEM SDK设置中启用功能切换之前，请确保以下各项：

* 用户是`forms-users`组的成员。

* 导航到`http://<author-instance-url>:portnumber/system/console/bundles`并检查&#x200B;**(com.adobe.granite.toggle.impl.dev-1.1.2.jar)**&#x200B;包是否存在。 如果不存在，请[从链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar)下载包。

  ![功能切换](/help/forms/assets/aem-web-console-bundle.png)

### 启用功能切换

请按照以下步骤在AEM SDK实例中启用功能切换：

1. 登录到您的AEM Forms实例。

1. 导航到 `http://author-instance-url:portnumber/system/console/configMgr`。

1. 在配置管理器中搜索Adobe Granite动态切换提供程序。

   ![功能切换](/help/forms/assets/aem-web-console-confi.png)

1. 单击图标✏️ 。
1. 在Enabled Toggles部分中，单击➕ 。
1. 为功能添加功能切换ID，如下图所示。
   ![功能切换](/help/forms/assets/feature-toggle.png)

1. 单击“保存”

>[!NOTE]
>
> 您可以在文档中找到特定于早期采用者功能的功能切换ID。


### 禁用功能切换

要禁用启用了切换功能的功能切换，请执行以下步骤：

1. 登录到您的AEM Forms实例。
1. 导航到 `http://author-instance-url:portnumber/system/console/configMgr`。
1. 在配置管理器中搜索Adobe Granite动态切换提供程序。
1. 单击图标✏️。
1. 在“已禁用切换”部分中，单击➕。
1. 为要禁用的功能添加切换号码。

   ![功能切换](/help/forms/assets/disable-toggle-feature.png)

### 技术考虑

功能切换由运行时管理，最适合开发或测试设置。 在AEM SDK设置中，确保切换由版本控制并与CI/CD同步。 可能需要刷新页面或清除缓存才能反映更改。

>[!NOTE]
>
> 要为生产环境启用功能切换，请联系Adobe支持团队。

