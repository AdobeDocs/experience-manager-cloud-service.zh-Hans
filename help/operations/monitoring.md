---
title: AEM as a Cloud Service 中的基础设施和服务监控
description: AEM as a Cloud Service 中的基础设施和服务监控
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 5%

---

# AEM as a Cloud Service 中的基础设施和服务监控 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供基础架构、服务和用户体验的可观察性和监控。 由于使用了各种解决方案，并且监控有若干层，因此本页分为三个部分：

* [外部可用性](#external-availability)
* [内部模块监控](#module-monitoring)
* [客户可观察性](#customer-observability)

AEMas a Cloud Service使用数百个云原生监视器，以每年365天不间断地报告每个环境的状态(24/7)。 监控器定义不是静态的，它们会不断被审查以提高早期检测能力。 此外，Adobe还设置了呼叫过程来响应警报。

如果您需要有关其他类型监视的信息（如通过Cloud Manager进行日志记录或监视），请参阅 [其他资源](#resources).

## 外部可用性 {#external-availability}

外部可用性由两部分组成：服务边缘和自定义监控。

### 服务边缘 {#service-edge}

您的所有AEMas a Cloud Service环境都受监控以保持可用性。 但是， Service Edge Monitoring仅针对生产环境设置，并且量度用于计算客户的SLA。 它考虑到了环境运行时和AEMas a Cloud ServiceCDN。 Service Edge Monitoring采用五个不同的位置靠近您选择的区域，并定期检查可用性。 站点的不可用性会触发警报，并吸引Adobe的待命支持团队和流程。

### 自定义监测 {#custom-monitoring}

通过自定义监控，客户可以选择提供之前最多五个不同的Web属性URL [上线](/help/journey-migration/go-live.md). 这些URL应有效，并返回HTTP 200响应代码。 这些监视器支持以下客户 [自带CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 在AdobeCDN之前以及在AEMas a Cloud Service之前采用且未受Adobe控制的任何外部流量路由。 由自定义监控检查生成的警报会与Adobe的支持团队和流程接洽。

>[!NOTE]
>
> 此功能仅面向具有以下特征的客户： [高级云支持。](https://experienceleague.adobe.com/docs/support-resources/data-sheets/overview.html#support-add-ons) 如果您有任何疑问，请通过Admin Console提出支持案例。

## 内部模块监控 {#module-monitoring}

虽然外部可用性侧重于最终用户监控，但内部模块监控可观察体系结构子系统是否名义上运行且特性或性能不会降低。 如果发生问题，则会触发警报，以便能够自动进行修复或通过运营团队的参与进行修复，从而防止可用性受损。 有各种类别的监视器，下面提供了一些示例检查：

* CPU iowait百分比未超过特定阈值。
* 实例重新部署不超过特定频率。
* 磁盘使用率低于某个阈值。
* 作者存储库大小在特定范围内。
* 已成功完成备份操作。
* 监视数据库运行状况和性能。
* AEM Cloud Services按预期运行，包括无阻止的复制队列、一致的数据和性能查询。

向为Forms配置的环境添加了其他检查。 检查定义不是静态的，可能会发生更改和更新。

## 客户可观察性 {#customer-observability}

客户可以使用 [New Relic应用程序性能监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 该套件提供了实时性能数据，这些数据会被收集并绘制在图表上以供分析和故障排除。 通过使用监控套件，客户可以直接观察各种量度，例如：JVM性能量度、Java™事务时间、后台外部调用和数据库调用。

## 其他资源 {#resources}

* [New Relic应用程序性能监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [AEM日志as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [监控环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
