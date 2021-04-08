---
title: AEM中Cloud Manager作为Cloud Service版本2021.4.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2021.4.0的发行说明
feature: 发行信息
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
translation-type: tm+mt
source-git-commit: 69694f2067c53667803d38bbf7bc752f3b3afac6
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Adobe Experience Manager中Cloud Manager作为Cloud Service 2021.4.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2021.4.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2021.4.0的发布日期为2021年4月8日。
下一版本计划于2021年5月06日发布。

### 新增功能 {#what-is-new-april}

* 对“添加”和“编辑”项目工作流的UI更新，使其更直观。

* 具有必需权限的用户现在可以通过UI提交商务端点。

* 环境变量现在可以作用于特定服务（创作或发布）。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管线，**管理Git**&#x200B;按钮也会显示在管线卡上。

* Cloud Manager使用的AEM项目原型版本已更新为版本27。

* 云管理器创建的Adobe I/O开发人员控制台中的项目不再可以无意中编辑或删除。

* 当用户添加新环境时，他们将收到通知，创建环境后，无法将其移动到其他区域。

* 环境变量现在可以作用于特定服务（创作或发布）。 需要AEM 2021.03.5104.20210328T185548Z或更高版本。

* 澄清了删除环境时启动管线时的错误消息。

* 现在，规则`CQBP-84--dependencies`中不包括Eclipse项目提供的OSGi捆绑包。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠`( / )`开头的输入路径将不再导致步骤卡在挂起状态中。

* 创建新的生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* `CloudServiceIncompatibleWorkflowProcess`的问题在可下载的问题CSV文件中严重性不正确。

* `Runmode`检查在非文件夹节点上产生误报。