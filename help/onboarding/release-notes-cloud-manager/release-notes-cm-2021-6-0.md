---
title: AEM as a Cloud Manager版本2021.5.0的发行说明
description: AEM as a Cloud Manager版本2021.5.0的发行说明
feature: 版本信息
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 673ac234f0e9bfc0f5e6878abf5d01d38cbe918f
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud 2021.6.0版中的Cloud Manager发行说明 {#release-notes}

本页面概述了AEM as a Cloud 2021.6.0中Cloud Manager的发行说明。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的最新发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans)。

## 发布日期 {#release-date}

AEM as a Cloud Service2021.6.0中Cloud Manager的发布日期是2021年6月10日。

### 新增功能 {#what-is-new}

* 预览服务将以滚动方式部署到所有程序。 当客户的计划启用了预览服务后，系统会在产品中通知客户。 有关更多详细信息，请参阅[访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序的名称。

* 在项目创建期间和通过管理git工作流在默认推送命令中使用的默认分支名称已更改为`main`。

* 在UI中编辑项目体验已刷新。

* 质量规则`ImmutableMutableMixCheck`已更新，可将`/oak:index`节点分类为不可变。

* 质量规则`CQBP-84`和`CQBP-84--dependencies`已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 为避免混淆，“环境详细信息”页面上的“发布AEM”和“发布Dispatcher”区段行已进行合并。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 添加了新的代码质量规则来验证`damAssetLucene`索引的结构。 有关更多详细信息，请参阅[自定义DAM资产Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)。

* “环境详细信息”页面现在将显示发布和预览服务的多个域名（如果适用）。 有关更多详细信息，请参阅[环境详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，即使未部署该配置，用户也可能在IP允许列表旁看到绿色的&#x200B;*活动*&#x200B;状态。

* 某些程序编辑序列可能会导致无法创建或编辑生产管道。

* 某些程序编辑序列可能会导致在&#x200B;**概述**&#x200B;页面中显示一条误导性消息，以便重新执行程序设置。
