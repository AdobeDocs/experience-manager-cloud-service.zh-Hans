---
title: 2020.3.0 版发行说明
description: 2020.3.0 版发行说明
translation-type: tm+mt
source-git-commit: 27225bf4b918f39892ac9ab6f46deb97479f08e8

---


# AEM 云服务 2020.3.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.3.0 的常规发行说明。


## Release Date {#release-date}

Experience Manager作为云服务2020.3.0的发布日期为2020年3月5日。

## Cloud Manager {#cloud-manager}

可查看本节以了解AEM中Cloud Manager的新增功能和2020.3.0版的更新。

### 新增功能 {#what-is-new}

* 现在，在构建步骤运行时，会提供构建步骤的日志。
* 为清楚起见，管道执行详细信息页面上的某些消息进行了编辑。

### 错误修复 {#bug-fixes}

* 无法通过 UI 下载自定义和产品功能测试步骤的日志文件。
* 当云服务程序的 git 存储库创建失败时，处于部署管理员角色的用户有时无法从此种故障中恢复。
* 创建沙盒程序期间的某些用户活动，可能会导致在创建非生产管道之前，程序创建失败。
* 偶尔，构建步骤中使用的临时 SonarQube 实例无法在配置的超时时间内启动。
* 在同一个云服务程序中并发创建开发环境时，可能会遇到这种情况：只能成功创建一个环境。
* 无法持续收到云服务程序的 Experience Cloud 通知。
* 在特定项目中，应始终关闭 *ResourceResolver对象*，这将产生空指针异常；不过，这并不影响管道执行。

