---
title: AEM 2021.7.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2021.7.0版中Cloud Manageras a Cloud Service的发行说明
feature: Release Information
source-git-commit: 3542d5a6b89b8673444786e3f9062dae0d315946
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud Service 2021.7.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.7.0版中Cloud Manager的发行说明。

>[!NOTE]
>要查看最新的Adobe Experience Manager as a Cloud Service发行说明，请单击[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hans)。

## 发布日期 {#release-date}

AEM 2021.7.0版中Cloud Manager的发布日期是2021年7月15日。


### 新增功能 {#what-is-new}

* 客户现在能够为其Cloud Manager构建过程使用Azul 8和11个JDK，并且可以选择将其中一个JDK用于与工具链兼容的Maven插件&#x200B;*或*&#x200B;整个Maven进程执行。

* 出站出口IP现在将记录在生成步骤日志文件中。

* 现在，运行旧版AEM的暂存环境和生产环境将报告&#x200B;**可用更新**&#x200B;的状态。

* 支持的最大SSL证书数已增加到每个计划20个。

* 每个环境可配置的最大域数已增加到500个。

* **管理Git**&#x200B;按钮已被命名为&#x200B;**访问Git信息**，对话框已被直观地刷新。

* Cloud Manager使用的AEM项目原型版本已更新至版本28。

### 错误修复 {#bug-fixes}

* 在某些情况下，将IP允许列表绑定到环境时，“预览”不是可用选项。

* 手动导航到非现有执行的执行详细信息页面不会显示错误，只是显示无休止的加载屏幕。

* 达到最大数量的SSL证书时显示的错误消息不起作用。

* 在某些情况下， **Overview**&#x200B;页面的管道卡中显示的发行版本可能不一致。

* “添加程序向导”错误地指示创建后无法更改名称。

### 已知问题 {#known-issues}

切换使用Azul JDK的客户应该注意到，并非所有现有应用程序都会在Azul JDK上编译而不出错。 强烈建议在切换前在本地进行测试。

