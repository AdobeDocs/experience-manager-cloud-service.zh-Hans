---
title: AEM as a Cloud Manager版本2021.8.0的发行说明
description: AEM as a Cloud Manager版本2021.8.0的发行说明
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 07a80076493070cb5e754a4cfbafe51cfcd6442e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud 2021.8.0版中的Cloud Manager发行说明 {#release-notes}

本页面概述了AEM as a Cloud 2021.8.0中的Cloud Manager发行说明。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的最新发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans)。

## 发布日期 {#release-date}

AEM as a Cloud Service2021.8.0中的Cloud Manager的发布日期是2021年8月12日。
下一版本计划于2021年9月9日发布。

### 新增功能 {#what-is-new}

* Cloud Service客户现在可以在Cloud Manager中查看服务级别协议(SLA)报表。 这将在今后几个月逐步提供。
请参阅[SLA报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html)以了解更多信息。

* IndexType和`IndexDamAssetLucene`质量规则的类型和严重性已更改。 这两个错误现在都是阻止程序&#x200B;*serverity*&#x200B;的错误。

* 新的Oak索引质量规则已引入，以涵盖异步和tika配置。

* 将每个程序的最大SSL证书数增加到50个。

* 允许用户通过Cloud Manager UI创建和管理多个存储库的自助服务功能。

* SonarQube不必要地读取Git历史数据。 在大型代码库中，这可能会导致不必要的内部版本性能损失。

* 现在有一个API可用于使每个管道的Maven依赖关系缓存失效。

* Cloud Manager使用的AEM项目原型版本已更新至版本29。

### 错误修复 {#bug-fixes}

* 当最新版本小于当前版本时，不应显示“更新可用”状态。

* 对于名称很长的新组织，初始载入失败。

* 有时，当管道因某些原因触发两次时，会导致其中一次执行失败，并出现&#x200B;*无法更新管道执行状态*&#x200B;错误。


