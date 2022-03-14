---
title: AEM 2021.5.0版中Cloud Manager的发行说明
description: AEM 2021.5.0版中Cloud Manager的发行说明
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service 2021.5.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.5.0版中Cloud Manager的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 发布日期 {#release-date}

AEM 2021.5.0版中Cloud Manager的发布日期是2021年5月6日。

### 新增功能 {#what-is-new}

* PackageOverlaps质量规则现在会检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入位置中部署同一包的情况。

* 现在，公共API中的存储库端点包含Git URL。

* Cloud Manager用户下载的部署日志将更有洞察力，现在将包含有关失败和成功方案的详细信息。

* 现在，已解决将代码推送到AdobeGit时遇到的间歇性故障。

* 现在，可以在编辑项目工作流期间将商务加载项应用于沙盒项目。

* 的 *编辑程序* 体验已刷新。

* “环境详细信息”页面中的“域名”表将通过分页显示多达250个域名。

* 的 **解决方案和附加组件** 选项卡 **添加程序** 和 **编辑程序** 工作流将显示解决方案，即使只有一个解决方案可供计划使用。

* 生成步骤日志中未生成任何已部署的内容包时的错误消息不明确。

### 错误修复 {#bug-fixes}

* 有时，即使未部署该配置，用户也可能会在IP允许列表旁边看到绿色的“活动”状态。

* 管道变量API将只用状态标记它们，而不删除“已删除”变量 **已删除**.

* 某些代码气味类型的质量问题错误地影响了可靠性评级。

* 由于不支持通配符域，因此UI将禁止用户提交通配符域。

* 当从午夜UTC到凌晨1点之间开始管道执行时，Cloud Manager生成的对象版本不保证大于前一天创建的版本。

* 在沙盒项目设置过程中，成功创建包含示例代码的项目后，“概述”页面中的“管理Git”将显示为主页卡中的链接。
