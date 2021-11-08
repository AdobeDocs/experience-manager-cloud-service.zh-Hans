---
title: AEMas a Cloud Service版本2021.10.0中的Cloud Manager发行说明
description: Release Notes for Cloud Manager in AEM as a Cloud Service Release 2021.10.0
feature: Release Information
exl-id: null
source-git-commit: c6c1d3bef85afda0ff86ec073d0ac91ad532c93b
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2021.10.0 {#release-notes}

This page outlines the Release Notes for Cloud Manager in AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans).

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager的发行日期为2021.10.0 2021年10月14日。


### 新增功能 {#what-is-new}

* In preparation for some upcoming changes, existing deployment pipelines will now be referenced and labelled in the user interface as **Full Stack** pipelines.

* Pipeline card has been refreshed to now display a single, integrated face that shows both production and non-production pipelines, and user can select Run/Pause/Resume directly from the action menu associated with each pipeline.

* 具有部署管理器角色的用户现在可以通过UI以自助方式删除生产管道。

* 添加和编辑管道体验已刷新，现在可以使用熟悉的现代模型。

* Users of Cloud Manager can now submit feedback directly from the user interface via the **Feedback** button on top right of the landing page.

* 现在可以从Cloud Manager的用户界面下载每年的SLA图表。

* 现在，代码质量和非生产管道执行将在构建步骤中使用更高效的浅层克隆过程，从而为具有特别大的git存储库的客户缩短构建时间。

* 现在，“添加IP允许列表”向导将通知用户是否已达到允许的最大IP允许列表数。

* Cloud Manager API文档现在包含一个交互式操场，允许已登录的用户从其浏览器中试用该API。 请参阅 [Cloud Manager API操场](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 以了解更多详细信息。

* 如果禁用了“导航到”下的选择选项，则程序卡上的工具提示更具描述性。 此时会显示“生产环境不存在”。

### 错误修复 {#bug-fixes}

* 在极少数情况下，当Adobe员工恢复客户的环境时，在环境完全运行之前，会认为恢复已完成。

* Certain internal requests made during environment creation were not being retried.

* If deployment failed error occurs following domain name verification, the error message has been corrected to request the customer to contact their Adobe representative.

