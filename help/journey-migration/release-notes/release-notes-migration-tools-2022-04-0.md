---
title: AEMas a Cloud Service版本2022.4.0中迁移工具的发行说明
description: AEMas a Cloud Service版本2022.4.0中迁移工具的发行说明
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
source-git-commit: 717b2c851a18ef5171d64a462509ce08fb87a59c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 5%

---

# AEMas a Cloud Service版本2022.4.0中迁移工具的发行说明 {#release-notes}

本页概述了AEM 2022.4.0as a Cloud Service中迁移工具的发行说明。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.28的发布日期是2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告不受支持的Asset Manager API的使用情况。 有四个API在AEMas a Cloud Service中不再受支持。 客户应确保不再使用这些API，并且应使用新的资产上传方法。

* 能够检测内容片段模板的使用情况。 不再支持在AEMas a Cloud Service上创建新内容片段模板。 客户将需要创建内容片段模型来替换内容片段模板。

* 能够检测存储库中资产元数据节点下具有100个以上子项的资产。 建议删除在加载包含此类资产的文件夹时不需要的元数据节点，以提高性能。

* 能够检测和报告所使用的数据存储类型。

* 更新了AEM表单门户的模式。

### 错误修复 {#bug-fixes-bpa}

* BPA报告的是核心组件的发现结果，而不是仅报告客户组件。 此问题已得到修复。
