---
title: AEM as a Cloud Manager版本2021.4.0的发行说明
description: AEM as a Cloud Manager版本2021.4.0的发行说明
feature: Release Information
source-git-commit: a707968483dc1196628b737ad207bfefe63ca94b
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud 2021.4.0版中的Cloud Manager发行说明 {#release-notes}

本页面概述了AEM as a Cloud 2021.4.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud ManagerCloud Service2021.4.0的发布日期是2021年4月8日。
下一版本计划于2021年5月6日发布。

### 新增功能 {#what-is-new-april}

* 更新了添加和编辑程序工作流的UI，使其更加直观。

* 现在，具有必需权限的用户可以通过UI提交商务端点。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管道，**管理Git**&#x200B;按钮也会显示在Pipelines卡上。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 在Adobe I/O开发人员控制台中，由Cloud Manager创建的项目不能再被无意中编辑或删除。

* 当用户添加新环境时，他们将被告知，一旦创建了环境，便无法将其移动到其他区域。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本2021.03.5104.20210328T185548Z或更高版本。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，由Eclipse项目提供的OSGi包已从规则`CQBP-84--dependencies`中排除。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠`( / )`开头的输入路径将不再导致该步骤卡在待处理状态中。

* 创建新生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* `CloudServiceIncompatibleWorkflowProcess`的问题在可下载的问题CSV文件中的严重性不正确。

* `Runmode`检查对非文件夹节点产生误报。
