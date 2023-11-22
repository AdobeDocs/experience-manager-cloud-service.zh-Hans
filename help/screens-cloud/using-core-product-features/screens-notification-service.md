---
title: Screensas a Cloud Service中的Screens通知服务
description: 本页介绍如何在Screensas a Cloud Service中配置“通知服务”。
index: true
exl-id: 74215a70-45c8-4b7f-ba30-60c332de07e9
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# Screens 通知服务 {#notification-service}

## 简介 {#introduction}

### 概述

通过AEM Screens Notifications Service，如果AEM Screens播放器未在可配置的时间段ping通，管理员将收到电子邮件。

### 如何配置

在AEM Screens Cloud上，客户可以通过创建支持票证来请求关于设备非活动状态的警报，该票证包含以下信息：

* 客户名称
* IMS OrgID
* 计划频率：以小时为单位指定此监视器应发送电子邮件的时间或频率（例如，1）。
* Ping超时：以分钟为单位指定间隔，在此间隔后设备应被视为不可访问。
* 电子邮件ID ：将向其发送报告的电子邮件ID
