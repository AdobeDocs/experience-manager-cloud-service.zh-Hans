---
title: AEM as a Cloud Service 2022.4.0版中的迁移工具发行说明
description: AEM as a Cloud Service 2022.4.0版中的迁移工具发行说明
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# AEM as a Cloud Service 2022.4.0版中的迁移工具发行说明 {#release-notes}

此页概述了AEM as a Cloud Service 2022.4.0中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.28的发布日期是2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告不受支持的Asset Manager API的使用情况。 AEM as a Cloud Service不再支持四个API。 客户应确保不再使用这些API，而应使用新的资产上传方法。

* 能够检测内容片段模板的使用情况。 在AEM as a Cloud Service上创建新内容片段模板不再支持内容片段模板。 客户需要创建内容片段模型以替换内容片段模板。

* 能够在存储库中资产的元数据节点下检测具有100多个子体的资产。 建议删除在加载包含此类资源的文件夹时不需要用来提高性能的元数据节点。

* 能够检测和报告所使用的数据存储类型。

* 更新了AEM表单门户的模式。

### 错误修复 {#bug-fixes-bpa}

* BPA报告核心组件的调查结果，而不是仅报告客户组件的调查结果。 此问题已得到修复。
