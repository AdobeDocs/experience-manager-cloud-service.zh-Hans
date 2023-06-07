---
title: 新增发布区域
description: 了解AEMas a Cloud Service如何支持其他发布区域以提高可用性和减少延迟。
source-git-commit: 9fccc1672aad243b648115e657396be1ce4ed614
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---


# 新增发布区域 {#additional-publish-regions}

通过AEM Sites设置的程序，可以许可和启用其他发布区域。 配置后，暂存和生产环境中的流量将路由到多个发布场，这具有以下好处：

* 减少延迟 — 从CDN路由到AEM发布实例的请求将定向到最近的发布区域，这对于多个地理区域内的用户访问的网站和应用程序有利。
* 可用性更高 — 如果某个区域不可用，则CDN会将流量定向到其他可用区域。

组织最多可以授权三个额外的发布区域。

>[!NOTE]
>
>此功能当前仅适用于AEM Sites。 也不能应用于沙盒程序。 此外，请注意，其他发布区域功能要求您的程序更新到AEM版本12142或更高版本。

## 用例 {#use-cases}

以下是一些使用案例，组织可以从许可其他发布区域中获益。

1. 对于从远离主要区域的用户那里获得大量流量或业务关键型流量的组织，附加发布区域可以减少这些访客遇到的延迟。
1. 对于在站点不可用时可能遭受重大金钱或声誉损失的组织，可以通过使用其他发布区域来减轻，以使AEM发布层更容易抵御区域故障。
1. 对于其内容作者位于远离大多数发布层访客的地理位置的组织，可以在内容作者的位置附近选择主要区域，而在发布端流量附近可以配置其他发布区域，使两个受众都受益于优化的体验。

## 启用和配置 {#enabling-and-configuring}

在许可附加发布区域后，将使用Cloud Manager配置这些区域。 请参阅 [Cloud Manager文档](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) 以获取详细说明。

其他发布区域适用于暂存和生产环境，但不适用于RDE或开发环境。

## 高级联网注意事项 {#advanced-networking-considerations}

在已配置高级联网的程序上启用附加发布区域时，附加发布区域中与高级联网规则匹配的流量将默认路由通过主区域。 为了利用更高的可用性，建议在其他区域启用高级联网。

请参阅 [其他发布区域的高级联网配置](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) 部分，以了解详细信息，包括如何向其他区域添加高级联网配置而不会导致连接丢失。

## 限制 {#limitations}

在考虑使用其他发布区域时，请记住这些限制。

* 只能将其他发布区域添加到AEM Sites。 其他发布区域不适用于在同一项目中部署的其他AEM解决方案或相关功能(例如AEM Forms或Adobe学习管理器)。
* 仅当租户中有可用的关联权利且未使用时，才能添加其他区域。
* 最多可以向任何单个环境添加三个其他发布区域。
* 其他区域仅适用于生产程序。 该功能在沙盒程序中不可用。
* 其他发布区域仅适用于暂存和生产环境，而不适用于RDE或开发环境。
* 其他发布区域要求将您的程序更新到AEM版本12142或更高版本。
