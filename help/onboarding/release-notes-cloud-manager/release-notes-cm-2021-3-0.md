---
title: AEM中Cloud Manager作为Cloud Service版本2021.3.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2021.3.0的发行说明
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4,feb7592e-7b41-43d0-84a1-e92d76a049b3
translation-type: tm+mt
source-git-commit: 388a21f7740a3a598f905fc433f54e37df799e6d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Adobe Experience Manager中Cloud Manager作为Cloud Service 2021.3.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2021.3.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2021.3.0的发布日期为2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 拥有[IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)预存自定义域名配置的环境的客户将看到有关其先前现有配置的消息，并将能够通过UI自助服务。

* 具有必需权限的用户现在可以编辑项目，允许他们以自助方式执行以下操作：
   * 将站点解决方案添加到包含资产的现有项目，反之亦然。
   * 将站点或资产从包含站点和资产的现有项目中删除。
   * 将第二个未使用的解决方案授权添加到现有项目或作为新项目。

* **AEM推** 送更新标签现在将同时显示在“管线执行”和“活动”屏幕中。

* 如果环境已休眠，但也有可用的AEM更新，则&#x200B;**已休眠**&#x200B;状态将优先于&#x200B;**可用更新**。

* 现在，用户在导航至Unified Shell的“用户用户档案”图标（右上方）后，通过选择“视图 Cloud Manager角色”选项，即可查看其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更清晰。

* **版本**&#x200B;标签已重新标记到“生产”管线执行屏幕中的&#x200B;**Git标签**。

* 当重要量度未达到定义的阈值时定义行为的标签已重新标记，以反映其真实行为：**取消立即**&#x200B;和&#x200B;**立即批准**。

* 类和方法弃用列表已根据AEM Cloud Service SDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

* Cloud Manager生产管道现在将包含[自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 错误修复 {#bug-fixes}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 在将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊情况下，打开“添加项目”对话框时生成的默认项目名称可能是现有项目名称的重复。

* 有时，如果用户在启动管道后立即从管道执行页面导航离开，将显示一条错误消息，指出操作失败，尽管实际执行会开始。

* 当客户生成导致包无效时，不必要地重新启动生成步骤。

* 有时，即使未部署IP，用户也会在IP旁看到允许列表绿色的“活动”状态。

* 所有现有生产管道将通过体验审核步骤自动启用。
