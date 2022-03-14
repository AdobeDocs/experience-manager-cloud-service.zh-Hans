---
title: AEM 2021.4.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2021.4.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
exl-id: a11ebe0e-2872-4fde-acc0-5babc6b01e1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2021.4.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.4.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2021.4.0版中Cloud Manager的发布日期是2021年4月8日。
下一版本计划于2021年5月6日发布。

### 新增功能 {#what-is-new-april}

* 更新了添加和编辑程序工作流的UI，使其更加直观。

* 现在，具有必需权限的用户可以通过UI提交商务端点。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本 `2021.03.5104.20210328T185548Z` 或更高版本。

* 的 **管理Git** 按钮，即使尚未配置管道，该按钮也会显示在管道卡上。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 在Adobe I/O开发人员控制台中，由Cloud Manager创建的项目不能再被无意中编辑或删除。

* 当用户添加新环境时，他们将被告知，一旦创建了环境，便无法将其移动到其他区域。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本2021.03.5104.20210328T185548Z或更高版本。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，Eclipse项目提供的OSGi包已从规则中排除 `CQBP-84--dependencies`.

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，输入路径以斜杠开头 `( / )` 将不再导致步骤卡在“待定”状态中。

* 创建新生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* 的问题 `CloudServiceIncompatibleWorkflowProcess` 的可下载问题CSV文件中的严重性不正确。

* 的 `Runmode` 检查在非文件夹节点上产生误报。
