---
title: 许可证功能板
description: Cloud Manager 提供了一个仪表板，用于轻松查看您的组织或租户可用的 AEMaaCS 产品权利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 58%

---

# 许可证功能板 {#license-dashboard}

Cloud Manager 提供了一个仪表板，用于轻松查看您的组织或租户可用的 AEMaaCS 产品权利。

## 概述 {#overview}

Cloud Manager 许可证仪表板可轻松访问以下信息：

1. 您可以在所有程序中获得解决方案权利，包括使用的内容和可用的内容
1. Sites 解决方案的内容请求消耗量度按月趋势

## 适用许可证仪表板 {#using-dashboard}

要访问许可证仪表板，请执行以下步骤。

>[!NOTE]
>
>中的用户 **业务负责人** 必须登录角色才能查看许可证仪表板。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 屏幕，切换到 **许可证** 选项卡。

![许可证功能板](assets/license-dashboard.png)

仪表板分为三个部分，向您显示：

* **解决方案** – 此部分总结了您已授予许可的解决方案，如 Sites 或 Assets。
* **插件** – 此部分总结了您的许可解决方案中可用的插件。
* **沙盒和开发环境** – 此部分总结了您可用的环境。

每个部分总结了可用的内容及其使用方式（如果有的话）。 目前，即使租户中存在其他解决方案，也只显示 Sites 解决方案。

* 此 **状态** 列显示未使用的权利数量与租户可用的总权利数量。
* **配置的**&#x200B;列指示已应用解决方案授权的程序。
   * 只有在创建了生产环境时，或者如果存在生产环境，并且在该环境上运行了更新管道，才认为权利被使用。
* **用途**&#x200B;列在单击时以图形形式显示过去 12 个月内消耗的内容请求。

>[!TIP]
>
>要了解如何通过Admin Console管理整个组织的Adobe权利，请参阅 [Admin Console概述](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 常见问题解答 {#faq}

### 什么是内容请求？ {#what-is-a-content-request}

内容请求是进入AEM Sites或任何客户提供的缓存系统（如内容交付网络）的请求，以HTML格式作为页面视图或JSON格式作为API调用交付内容或数据。

每个页面视图或每五个 API 调用计算一个内容请求，在第一个接收内容请求的缓存系统入口测量。 内容请求仅按生产环境计算。

Content Request不包括仅出于提供产品和服务的目的而由Adobe发起或代表用户发起的请求或活动。 Adobe 识别的用户代理流量也不包括与常见搜索引擎和社交媒体服务相关的机器人、爬虫和蜘蛛。

另请参阅 [了解Cloud Service内容请求](/help/implementing/cloud-manager/content-requests.md).

### Adobe Experience Manager 如何衡量内容请求？ {#how-are-content-requests-measured}

内容请求在 AEM as a Cloud Service 的边缘服务器进行跟踪。 源站流量不计入内容请求。 AEM as a Cloud Service 中内置的 CDN 跟踪有效的 HTML 和 JSON 请求。

AEM 还制定了排除知名机器人的规则，包括定期访问网站以刷新其搜索索引或服务的知名服务。

另请参阅 [了解Cloud Service内容请求](/help/implementing/cloud-manager/content-requests.md).

### 为什么我的分析报告显示的结果与 AEM 内容请求不同？ {#why-are-reports-different}

内容请求可能与组织的Analytics报告工具不同。 有关更多信息，请参阅 [了解Cloud Service内容请求](/help/implementing/cloud-manager/content-requests.md).

### 如果我想了解有关我的内容请求量的更多信息怎么办？ {#current-request-volumes}

如果您想进一步了解许可证仪表板中显示的内容请求量，您的 Adob&#x200B;e 团队可以提供一份报告，其中会显示内容请求的主要驱动因素。请联系您的Adobe团队或Adobe客户支持以请求最佳使用报告。

### 如果我使用自己的 CDN 怎么办？ {#using-own-cdn}

许可证仪表板仅显示Cloud ServiceCDN跟踪的数据。 如果您选择使用自己的CDN (BYOCDN)，请按照合同中的规定每年向Adobe报告您的内容请求量。
