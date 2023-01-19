---
title: Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2023.1.0 发行说明
description: 这些是 AEM as a Cloud Service 中的 Cloud Manager 2024.1.0 发行说明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 33%

---


# Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2023.1.0 发行说明 {#release-notes}

本页记录了AEM as a Cloud Service中Cloud Manager 2023.1.0版的发行说明。

>[!NOTE]
>
>请参阅[本页](/help/release-notes/release-notes-cloud/release-notes-current.md)，了解 Adobe Experience Manager as a Cloud Service 的当前发行说明。

## 发布日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2023.1.0版的发布日期是2023年1月19日。 下一个版本计划于 2023 年 2 月 16 日发布。

## 新增功能 {#what-is-new}

* 可用性增强是通过更新光标样式来区分用户在何处可以执行操作还是默认指针来实现的。

* 在环境和管道执行的列表中，您现在可以通过单击单个行来访问详细信息。

* 自定义UI测试报表现在会复制到Cloud Manager存储，并且可以通过Cloud Manager API调用访问。

* 用户现在可以使用左 — 右箭头在上线小组件状态之间进行转换。

   ![上线小组件过渡](assets/go-live-transitions.gif)

* 自助服务 [创建支持HIPAA的计划](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 现在，当相应的权限和权限可用时，即可使用。

## 错误修复 {#bug-fixes}

* Cloud Manager将防止两个管道执行同时（或几乎同时）开始，从而避免管道故障。
