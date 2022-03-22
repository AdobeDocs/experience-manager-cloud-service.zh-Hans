---
title: AEM 2021.6.0版中Cloud Manager的发行说明
description: AEM 2021.5.0版中Cloud Manager的发行说明
feature: Release Information
exl-id: 9a0a53d3-31d4-493d-ba2e-b4bb22f60351
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service 2021.6.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.6.0版中Cloud Manager的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans).

## 发布日期 {#release-date}

AEM 2021.6.0版中Cloud Manager的发布日期是2021年6月10日。

### 新增功能 {#what-is-new}

* 预览服务将以滚动方式部署到所有程序。 当客户的计划启用了预览服务后，系统会在产品中通知客户。 请参阅 [访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 以了解更多详细信息。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序的名称。

* 在项目创建期间和在通过管理Git工作流的默认推送命令中使用的默认分支名称已更改为 `main`.

* 在UI中编辑项目体验已刷新。

* 质量规则 `ImmutableMutableMixCheck` 已更新以进行分类 `/oak:index` 节点不可变。

* 质量规则 `CQBP-84` 和 `CQBP-84--dependencies` 已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 为避免混淆，“环境详细信息”页面上的“发布AEM”和“发布Dispatcher”区段行已进行合并。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 添加了新代码质量规则以验证 `damAssetLucene` 索引。 请参阅 [自定义DAM资产Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 以了解更多详细信息。

* “环境详细信息”页面现在将显示发布和预览服务的多个域名（如果适用）。 请参阅 [环境详细信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#viewing-environment) 以了解更多详细信息。

### 错误修复 {#bug-fixes}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，用户可能会看到绿色 *活动* IP允许列表旁边的状态，即使未部署该配置也是如此。

* 某些程序编辑序列可能会导致无法创建或编辑生产管道。

* 某些程序编辑序列可能会导致 **概述** 页面显示一条误导性消息以重新执行程序设置。
