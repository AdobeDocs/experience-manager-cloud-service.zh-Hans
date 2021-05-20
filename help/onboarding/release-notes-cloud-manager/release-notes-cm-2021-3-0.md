---
title: AEM as a Cloud Manager版本2021.3.0的发行说明
description: AEM as a Cloud Manager版本2021.3.0的发行说明
feature: 发行信息
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 84a97f09402602df33c8f0494feed57fdb510add
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service2021.3.0 {#release-notes}中的Cloud Manager发行说明

本页面概述了AEM as a Cloud 2021.3.0中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM as a Cloud ManagerCloud Service2021.3.0的发布日期是2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 对于为[IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)预先具有自定义域名配置的环境，客户将看到有关其以前现有配置的消息，并能够通过UI自助服务。

* 具有必需权限的用户现在可以编辑程序，允许他们以自助方式执行以下操作：
   * 将站点解决方案添加到包含资产的现有项目中，反之亦然。
   * 从同时具有站点和资产的现有项目中删除站点或资产。
   * 将第二个未使用的解决方案权利添加到现有项目或作为新项目。

* **AEM推送** 更新标签现在将同时显示在“管道执行”和“活动”屏幕中。

* 如果环境已休眠，但也有AEM更新可用，则&#x200B;**已休眠**&#x200B;状态将优先于&#x200B;**更新可用**。

* 现在，用户在导航到Unified Shell的“用户配置文件”图标（右上方）后，通过选择“查看Cloud Manager角色”选项，可以查看其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更加清晰。

* 在“生产管道”执行屏幕中， **版本**&#x200B;标签已重新标记为&#x200B;**Git标记**。

* 重新标记了在重要量度未达到定义的阈值时定义行为的标签，以反映其真实行为：**取消立即**&#x200B;和&#x200B;**立即批准**。

* 类和方法弃用列表已根据AEMCloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

* Cloud Manager生产管道现在将包含[自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 错误修复 {#bug-fixes}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊的情况下，打开“添加程序”对话框时生成的默认程序名称可能与现有程序名称重复。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，指出操作失败，尽管实际开始执行。

* 当客户生成导致无效的包时，不必要地重新启动生成步骤。

* 有时，即使未部署该配置，用户也会在IP旁允许列表看到绿色的“活动”状态。

* 所有现有的生产管道都将通过体验审核步骤自动启用。
