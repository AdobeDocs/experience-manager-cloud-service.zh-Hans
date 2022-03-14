---
title: AEM 2020.4.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2020.4.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
exl-id: 15665fb5-9444-416b-938a-45c31fdce5cf
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 77%

---

# Adobe Experience Manager as a Cloud Service 2020.4.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2020.4.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2020.4.0版中Cloud Manager的发布日期是2020年4月9日。

## 新增功能 {#whats-new-cloud-manager}

* 现在，可以从 Cloud Manager UI 的环境页面访问发布者 URL。
* 导航更改让用户能够从 Cloud Manager 概述页面编辑、切换或添加项目。
* 更改让用户能够从 Cloud Manager 登陆页面上的项目卡片编辑项目。
* 根据与管道关联的环境，会显示新的管道状态&#x200B;**管道正在运行**。
* 改进了管道执行页面的可理解性。这包括显示管道名称（仅限非生产管道）和类型，以及指示管道状态是否为“进行中/已取消/失败”的徽章。
* 添加了用于改善用户体验和增进了解为何禁用“添加项目/环境”按钮的工具提示。
* 现在，可以通过 UI 和 API 删除失败的环境。
* 提高了用于生成 Git 密码的进程弹性，以应对基础服务层中的问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 管道执行详细信息页面上指向暂存环境的链接不是总能导航到正确的位置。
* 环境创建进程中的各个步骤超时时间提前，从而导致进程失败。
* 更新了生成容器中使用的 Maven 配置，以避免下载伪像元数据时出现死锁。
* 在某些情况下，生成图像步骤可能无法成功下载客户包。
* 某些偶然发生的情况可能会阻止删除环境。
* 不能终如收到 Experience Cloud 通知。
