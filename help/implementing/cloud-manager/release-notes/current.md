---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.3.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2025.3.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 5983c8579dd8606bc8bedfe6fa2a3838493452cd
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 25%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.3.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.3.0 版本。


另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.3.0的发布日期是2025年3月13日星期四。

下一个计划发布于2025年4月10日星期四。

## 新增功能 {#what-is-new}

* **运行多个管道**

  在管道页面上引入了同时运行多个管道的功能。 用户必须至少选择一个管道，但不能超过十个。 在管道页面的右上角附近，单击&#x200B;**运行选定项(x)**。 此时将显示一个模式对话框，其中列出了任何无法启动的管道。 单击&#x200B;**运行**&#x200B;以启动所有有效的管道。

  ![运行选定的管道对话框](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

* **支持扩展到Node.js版本**

  前端构建环境现在支持以下`Node.js`版本：

   * 23
   * 22
   * 20

  另请参阅[使用前端管道](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions)开发站点。<!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## 错误修复

* 修复了Cloud Manager **中的“高级网络配置”更新的**(UI)

  解决了当存在“可用更新”通知时阻止更新&#x200B;**高级网络配置**&#x200B;的罕见问题。 以前，Cloud Manager会锁定配置修改，包括高级联网设置，以防止在更新期间发生冲突。 客户现在可以手动触发待处理更新，以不受限制地应用必要的更改。<!-- CMGR-65913 and CMGR-65788 -->

* **(UI)修复了IP允许列表更新卡在“正在更新”状态**

  解决了由于允许列表的活动域配置重复而导致Cloud Manager中的IP环境更新停留在“正在更新”状态的罕见问题。 以前，客户在更新IP允许列表时会遇到无限的处理延迟，从而无法进行必要的网络访问调整。 此修复确保IP允许列表更新现在可以成功完成而不会卡住。<!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
