---
title: AEM as a Cloud Service 中的基础设施和服务监控
description: AEM as a Cloud Service 中的基础设施和服务监控
exl-id: 82432c11-37ec-48ac-a52b-487abdc859fa
source-git-commit: 34fed4e64b49ab32e7025c9654d930e3fa362a52
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# AEM as a Cloud Service 中的基础设施和服务监控 {#monitoring-in-aem-as-a-cloud-service}

Adobe Experience Manager as a Cloud Service提供以下功能的可观察性和监控：基础架构、服务和用户体验。 由于使用了各种解决方案，并且有多个监控层，因此本页分为三个部分：

* [外部可用性](#external-availability)
* [内部模块监控](#module-monitoring)
* [客户可观察性](#customer-observability)

AEM as a Cloud Service使用数百个云原生监视器，每年365天持续报告每个环境(24/7)的状态。 监视器定义不是静态的，会不断对其进行审查以提高早期检测能力。 此外，Adobe还设置了应用程序来响应警报。

如果您需要了解有关其他类型的监控（如通过Cloud Manager进行日志记录或监控）的信息，请参阅 [其他资源](#resources) 中。

## 外部可用性 {#external-availability}

外部可用性由两部分组成：服务边缘和自定义监控。

### 服务边缘 {#service-edge}

您的所有AEMas a Cloud Service环境都受到监控以获得可用性。 但是，服务边缘监控仅针对生产环境进行设置，并且量度用于计算客户的SLA。 它考虑了环境运行时和AEMas a Cloud ServiceCDN。 Service Edge Monitoring在您选定的区域附近使用五个不同的位置，并定期检查可用性。 站点的不可用将触发警报，并会吸引Adobe的电话技术支持团队和流程。

### 自定义监控 {#custom-monitoring}

通过自定义监控，客户可以选择在 [正式启用](/help/journey-migration/go-live.md). 这些URL应有效，并返回HTTP 200响应代码。 这些监视器支持 [自带CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) 在AdobeCDN之前，以及在AEMas a Cloud Service之前采用且不受Adobe控制的任何外部流量路由。 自定义监控检查产生的警报将吸引Adobe的支持团队和流程。

>[!NOTE]
>
> 此功能仅面向具有高级云支持的客户提供。 如果您有任何问题，请通过管理控制台提出支持案例。

## 内部模块监控 {#module-monitoring}

虽然外部可用性侧重于最终用户监控，但内部模块监控会观察体系结构子系统是否在名义上运行而没有功能或性能下降。 如果出现问题，将触发警报，以便能够自动或通过运营团队的参与进行修复，以防止损坏可用性。 监视器有多种类别，下面显示了一些示例检查：

* CPU超时百分比未超过特定阈值。
* 实例重新部署不会超过特定频率。
* 磁盘使用率低于特定阈值。
* 创作存储库大小在特定范围内。
* 备份操作已成功完成。
* 监控数据库运行状况和性能。
* AEM云服务的行为符合预期，包括没有阻止的复制队列、一致的数据和性能查询。

为Forms配置的环境中添加了其他检查。 请记住，检查定义不是静态的，可能会发生更改和更新。

## 客户可观察性 {#customer-observability}

客户可以使用 [New Relic应用程序性能监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html) 提供实时性能数据收集和绘制以用于分析和故障诊断的套件。 通过使用监控包，客户可以直接观察各种量度，例如：JVM性能量度、Java的事务时间、后台外部调用和数据库调用。

## 其他资源 {#resources}

* [New Relic应用程序性能监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic.html)
* [记录AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html)
* [监控环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/monitoring-environments.html)
