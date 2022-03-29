---
title: AEM 2021.3.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2021.3.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 95539851590456b6b5ecbfeb0df8fc7bc7dde74b
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2021.3.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.3.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2021.3.0版中Cloud Manager的发布日期是2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 具有以下客户： [IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) 和 [自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 将看到有关其以前现有配置的消息，并能够通过UI自助服务。

* 具有必需权限的用户现在可以编辑程序，允许他们以自助方式执行以下操作：
   * 将站点解决方案添加到包含资产的现有项目中，反之亦然。
   * 从同时具有站点和资产的现有项目中删除站点或资产。
   * 将第二个未使用的解决方案权利添加到现有项目或作为新项目。

* **AEM推送更新** 现在将同时为“管道执行”和“活动”屏幕显示标签。

* 如果某个环境已休眠，但同时也有一个AEM更新可用，则 **冬眠** 状态将优先于 **更新可用**.

* 现在，用户在导航到Unified Shell的“用户配置文件”图标（右上方）后，通过选择“查看Cloud Manager角色”选项，可以查看其Cloud Manager角色。

* 标签 **申请批准** 已重新标记为 **生产审批** 更清楚。

* 的 **版本** 标签已重新标记为 **Git标记** 在生产管道执行屏幕中。

* 重新标记了在重要量度未达到定义的阈值时定义行为的标签，以反映其真实行为： **立即取消** 和 **立即批准**.

* 类和方法弃用列表已根据版本进行了更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID。

* Cloud Manager生产管道现在将包括 [自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 错误修复  {#bug-fixes}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊的情况下，打开“添加程序”对话框时生成的默认程序名称可能与现有程序名称重复。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，指出操作失败，尽管实际开始执行。

* 当客户生成导致无效的包时，不必要地重新启动生成步骤。

* 有时，即使未部署该配置，用户也会在IP旁允许列表看到绿色的“活动”状态。

* 所有现有的生产管道都将通过体验审核步骤自动启用。
