---
title: AEMas a Cloud Service版本2021.10.0中的Cloud Manager发行说明
description: AEMas a Cloud Service版本2021.10.0中的Cloud Manager发行说明
feature: Release Information
exl-id: f8a87b00-52ce-42a6-a955-45cb14703b40
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2021.10.0 {#release-notes}

本页概述了AEM as a Cloud Service 2021.10.0中Cloud Manager的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.10.0 2021年10月14日。


### 新增功能 {#what-is-new}

* 为了准备一些即将发生的更改，现在将在用户界面中引用现有部署管道，并将其标记为 **完全堆栈** 管道。

* 管道卡已刷新，现在可显示单个集成的表面，该表面既显示生产管道，也显示非生产管道，用户可以直接从与每个管道关联的操作菜单中选择“运行/暂停/恢复”。

* 具有部署管理器角色的用户现在可以通过UI以自助方式删除生产管道。

* 添加和编辑管道体验已刷新，现在可以使用熟悉的现代模型。

* Cloud Manager的用户现在可以通过 **反馈** 按钮。

* 现在可以从Cloud Manager的用户界面下载每年的SLA图表。

* 现在，代码质量和非生产管道执行将在构建步骤中使用更高效的浅层克隆过程，从而为具有特别大的git存储库的客户缩短构建时间。

* 现在，“添加IP允许列表”向导将通知用户是否已达到允许的最大IP允许列表数。

* Cloud Manager API文档现在包含一个交互式操场，允许已登录的用户从其浏览器中试用该API。 请参阅 [Cloud Manager API操场](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以了解更多详细信息。

* 如果禁用了“导航到”下的选择选项，则程序卡上的工具提示更具描述性。 此时会显示“生产环境不存在”。

### 错误修复 {#bug-fixes}

* 在极少数情况下，当Adobe员工恢复客户的环境时，在环境完全运行之前，会认为恢复已完成。

* 在环境创建期间发出的某些内部请求未重试。

* 如果在域名验证后发生部署失败错误，则错误消息已被更正，以请求客户联系其Adobe代表。
