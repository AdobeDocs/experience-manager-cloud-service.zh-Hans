---
title: 新增发布区域
description: 了解 AEM as a Cloud Service 如何支持附加的发布区域，以提高可用性并减少延迟。
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 88%

---


# 新增发布区域 {#additional-publish-regions}

可以在使用 AEM Sites 设置的程序上许可并启用附加发布区域。配置后，阶段和生产环境中的流量将路由到多个发布场，这具有以下好处：

* 减少延迟 – 从 CDN 路由到 AEM 发布实例的请求会被定向到最近的发布区域，这对于多个地理位置的用户访问的网站和应用程序是有利的。
* 更高的可用性 – 如果某个区域不可用，CDN 会将流量定向到其他可用区域。

组织最多可以许可三个附加发布区域。

>[!NOTE]
>
>此功能目前仅适用于 AEM Sites。它也不能应用于沙盒程序。此外，请注意，其他发布区域功能要求您的程序更新到AEM版本12142或更高版本。

## 用例 {#use-cases}

以下是组织可以从许可附加发布区域中受益的一些用例。

1. 对于从远离主要区域的用户接收大量或关键业务流量的组织，附加发布区域可以减少这些访问者遇到的延迟。
1. 对于在站点不可用时可能遭受重大金钱或声誉损失的组织，可以通过使用附加的发布区域来减轻这一损失，使 AEM 发布层可以在出现区域故障后快速恢复。
1. 对于内容作者所在的地理位置远离大多数发布层访问者的组织，可以在内容作者所在位置附近选择主要区域，并在发布端流量附近配置其他发布区域，使这两类受众都能从优化的体验中受益。

## 启用并配置 {#enabling-and-configuring}

在授权附加发布区域后，这些区域将使用 Cloud Manager 进行配置。有关详细说明，请参阅 [Cloud Manager 文档](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)。

附加发布区域适用于阶段和生产环境，但不适用于 RDE 或开发环境。

## 高级网络注意事项 {#advanced-networking-considerations}

在已配置高级网络的程序上启用附加发布区域时，与高级网络规则匹配的附加发布区域中的流量将默认路由通过主要区域。为了利用更高的可用性，建议在附加区域启用高级网络。

请参阅 [其他发布区域的高级联网配置](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) 部分，以了解详细信息，包括如何向其他区域添加高级联网配置而不会导致连接丢失。

## 限制 {#limitations}

在考虑使用其他发布区域时，请牢记以下限制。

* 附加发布区域只能添加到 AEM Sites。其他发布区域不会扩展到其他 AEM 解决方案或部署在同一程序中的相关功能（例如 AEM Forms 或 Adob&#x200B;&#x200B;e Learning Manager）。
* 仅当关联的权限在租户中可用但未使用时，才能添加附加区域。
* 最多可以向任何单个环境添加三个附加的发布区域。
* 附加区域仅适用于生产程序。该功能在沙盒程序中不可用。
* 附加发布区域仅适用于阶段和生产环境，不适用于 RDE 或开发环境。
* 要使用附加发布区域，您的程序需要更新到 12142 或更高版本的 AEM。
