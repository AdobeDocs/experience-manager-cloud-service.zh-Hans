---
title: 2020.3.0版发行说明
description: 2020.3.0版发行说明
translation-type: tm+mt
source-git-commit: bcbb50f467a0e3b3047e2bb872a8fe39a9f02a1a

---


# Release Notes for AEM as a Cloud Service 2020.3.0 {#release-notes}

以下部分概述了Experience Manager作为云服务2020.3.0的一般发行说明。

## Cloud Manager {#cloud-manager}

Cloud Manager 2020.3.0版本的发布日期为2020年3月5日。

可查看本节以了解Cloud Manager 2020.3.0版的新增功能和更新。

### 新增功能 {#what-is-new}

* 构建步骤运行时，构建步骤的日志现在可用。
* 管道执行详细信息页面上的某些消息已经编辑，以便清晰明了。

### 错误修复 {#bug-fixes}

* 无法通过UI下载自定义和产品功能测试步骤的日志文件。
* 当云服务程序的git存储库创建失败时，具有部署管理器角色的用户有时无法从此故障中恢复。
* 在创建沙箱程序期间的某些用户活动可能导致程序创建在创建非生产管道之前失败。
* 构建步骤中使用的短暂SonarQube实例在配置的超时内偶尔无法启动。
* 在同一云服务程序中并发创建开发环境可能会遇到一个条件，即只能成功创建一个环境。
* Experience Cloud云服务程序通知未得到一致接收。
* 在特定项目中， *应始终关闭ResourceResolver对象* ，将产生空指针异常；然而，这并不影响管道执行。

