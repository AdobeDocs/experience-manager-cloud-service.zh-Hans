---
title: Screens中的Screens Notification Serviceas a Cloud Service
description: 本页介绍如何在Screensas a Cloud Service中配置Notification Service。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

# Screens 通知服务 {#notification-service}

## 简介 {#introduction}

### 概述

AEM Screens通知服务允许管理员接收包含所有AEM Screens播放器列表的报告，这些播放器未在电子邮件的可配置时间段内ping通。

### 如何配置

在AEM Screens Cloud上，客户可以通过创建支持票证来请求报告设备非活动状态，该票证包含以下信息：

* 客户名称
* IMS OrgID
* 计划频率：以小时为单位指定此监视器应发送电子邮件的时间或频率（例如，1）。
* Ping超时：以分钟为单位指定间隔，在此间隔后设备应被视为不可访问。
* 电子邮件ID ：将向其发送报告的电子邮件ID

>[!NOTE]
>仅当在生成电子邮件时设备在给定的ping超时时间内未执行ping操作时，才会向电子邮件播放器报告。

### 示例用例

如果将报表时间设置为5am，并将ping超时设置为1小时，则如果Screens设备在凌晨4:00到凌晨5:00之间未执行ping操作，则会收到一封电子邮件通知，确认设备处于非活动状态。
