---
title: 许可证功能板
description: Cloud Manager 提供了一个仪表板，用于轻松查看您的组织或租户可用的 AEMaaCS 产品权利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 95%

---

# 许可证功能板 {#license-dashboard}

Cloud Manager 提供了一个仪表板，用于轻松查看您的组织或租户可用的 AEMaaCS 产品权利。

## 概述 {#overview}

Cloud Manager 许可证仪表板可轻松访问以下信息：

1. 您可以在所有计划中获得解决方案权利，包括使用的内容和可用的内容
1. Sites 解决方案的内容请求消耗量度按月趋势

## 适用许可证仪表板 {#using-dashboard}

要访问许可证仪表板，请执行以下步骤。

>[!NOTE]
>
>必须登录具有&#x200B;**业务负责人**&#x200B;角色的用户才能查看许可证仪表板。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在产品概述页面上，切换到 **许可证**&#x200B;选项卡。

![许可证功能板](assets/license-dashboard.png)

仪表板分为三个部分，向您显示：

* **解决方案** – 此部分总结了您已授予许可的解决方案，如 Sites 或 Assets。
* **插件** – 此部分总结了您的许可解决方案中可用的插件。
* **沙盒和开发环境** – 此部分总结了您可用的环境。

每个部分总结了可用的内容以及当前的使用方式（如果有的话）。 目前，即使租户中存在其他解决方案，也只显示 Sites 解决方案。

* **状态**&#x200B;列显示租户未使用的权利数量与可用的总权利数量。
* **配置的**&#x200B;列指示已应用解决方案授权的程序。
   * 只有在创建了生产环境时，或者如果已经存在一个生产环境，并且在该环境上运行了更新管道，才能将授权视为已使用。
* **用途**&#x200B;列在单击时以图形形式显示过去 12 个月内消耗的内容请求。

>[!TIP]
>
>参见 [Admin Console概述](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 了解如何通过Admin Console管理整个组织的Adobe授权。

## 常见问题解答 {#faq}

### 什么是内容请求？ {#what-is-a-content-request}

内容请求是进入 AEM Sites 或任何客户提供的缓存系统（如内容交付网络）的请求，以 HTML 格式作为页面视图或 JSON 格式作为 API 调用交付内容或数据。

每个页面视图或每五个 API 调用计算一个内容请求，在第一个接收内容请求的缓存系统入口测量。 内容请求仅按生产环境计算。

内容请求不包括 Adobe 发起或代表 Adobe 发起的仅用于提供产品和服务的请求或活动。 Adobe 识别的用户代理流量也不包括与常见搜索引擎和社交媒体服务相关的机器人、爬虫和蜘蛛。

### Adobe Experience Manager 如何衡量内容请求？ {#how-are-content-requests-measured}

内容请求在 AEM as a Cloud Service 的边缘服务器进行跟踪。 源站流量不计入内容请求。 AEM as a Cloud Service 中内置的 CDN 跟踪有效的 HTML 和 JSON 请求。

AEM 还制定了排除知名机器人的规则，包括定期访问网站以刷新其搜索索引或服务的知名服务。

### 为什么我的分析报告显示的结果与 AEM 内容请求不同？ {#why-are-reports-different}

如本表所示，内容请求与组织的分析报告工具存在差异。

| 差异原因 | 解释 |
|---|---|
| 标记 | 作为 AEM 内容请求跟踪的所有页面可能会标记为 Analytics 跟踪，也可能不会。 组织的 Analytics 工具不会标记作为 AEM 内容请求跟踪的所有 API 调用。<br>页面或 API 调用可能会被标记以跟踪操作，或者只标记唯一的页面视图，而不是所有视图。 |
| Tag Management 规则 | Tag Management 规则设置可能会导致页面上的各种数据收集配置，从而导致与内容请求跟踪的某些差异组合。 |
| 机器人 | AEM 尚未预先识别和移除的未知机器人程序可能会导致跟踪不一致。 |
| 报告包 | 属于同一 AEM 实例和域的页面可能会将数据发送到不同的 Analytics 报告包。 |
| 第三方监控和安全工具 | 监控和安全扫描工具可能会为 AEM 生成 Analytics 报告中未跟踪的内容请求。 |
| 预获取请求 | 使用预获取服务预加载页面来提高速度，可能会导致内容请求流量显著增加。 |
| DDOS | 虽然 Adobe 竭尽全力自动检测和过滤 DDOS 攻击的流量，但无法保证检测到所有可能的 DDOS 攻击 |
| 流量拦截器 | 在浏览器中使用跟踪拦截器可能会选择不跟踪某些请求。 |
| 防火墙 | 防火墙可能会阻止分析跟踪。这在公司防火墙中更为常见。 |

### 如果我想了解有关我的内容请求量的更多信息怎么办？ {#current-request-volumes}

如果您想进一步了解许可证仪表板中显示的内容请求量，您的 Adob&#x200B;e 团队可以提供一份报告，其中会显示内容请求的主要驱动因素。请联系您的Adobe团队或Adobe客户关怀团队，以请求获取最佳使用报表。

### 如果我使用自己的 CDN 怎么办？ {#using-own-cdn}

许可证仪表板仅会显示 Cloud Service CDN 跟踪的数据。如果您选择使用自己的 CDN (BYOCDN)，您将按照合同中的规定每年向 Adob&#x200B;e 报告您的内容请求量。
