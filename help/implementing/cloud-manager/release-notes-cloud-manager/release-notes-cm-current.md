---
title: AEMas a Cloud Service版本2021.12.0中的Cloud Manager发行说明
description: 以下是AEMas a Cloud Service版本2021.12.0中Cloud Manager的发行说明。
feature: Release Information
source-git-commit: 6389dfaf1e4569a0e7bf2c6dbfa30bb003c4db5b
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service中的Cloud Manager发行说明2021.12.0 {#release-notes}

本页面概述了AEMas a Cloud Service中Cloud Manager的发行说明2021.12.0。

>[!NOTE]
>
>请参阅 [本页](/help/release-notes/release-notes-cloud/release-notes-current.md) ，以了解最新的Adobe Experience Manager as a Cloud Service发行说明。

## 发布日期 {#release-date}

AEM Manager在as a Cloud Service中的发布日期为2021.12.0 2021年12月16日。 下一版本计划于2022年1月发布。

### 新增功能 {#what-is-new}

* 提交哈希（已在UI中可见）现在也在API中提供。
* “活动”页面现在包含一个用于运行管道的弹出窗口，该弹出窗口提供了管道详细信息概览摘要。
* 添加了更新，以包含“活动”页面中显示的其他详细信息。
* Cloud Manager中的“学习”选项卡现在包含对API指南和相关资源的快速访问。
* 现在，具有部署管理器角色的用户可以从“存储库”页面的“操作”菜单中为没有分支的存储库启动项目/分支创建向导。
* 现在，将通知处于添加或编辑管道工作流中的部署管理器在选定的存储库没有分支时如何创建分支或项目。
* 新增了Cloud Manager自助服务功能，允许 [在环境级别添加自由格式变量和密钥。](/help/implementing/cloud-manager/environment-variables.md)
* 使用 [参考演示附加组件](/help/journey-sites/demos-add-on/overview.md) （于2021年12月17日提供），可安装AEM产品的最新演示代码库，并准备通过 [快速网站创建工具](/help/journey-sites/quick-site/overview.md) 中。
* 前端管道现在支持管道变量。
* 现在，可以在“程序编辑”对话框中为所有沙箱启用屏幕。
* 概述页面中由行动动员卡提供的指南已刷新，以准确反映它与生产完整堆栈管道的关联。
* 添加了“活动”页面的增强功能，以显示适用于管道的其他详细信息，包括源代码、提交ID等。
* 在复制TXT条目（“TXT值”而不是“TXT记录”）时，对UI进行了次要更新，以删除潜在的混淆。
* [与证书错误相关的文档](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) 更新了，以涵盖其他示例以及故障排除步骤。
* 前端管道执行中现在有一个选项，可在部署到生产之前拒绝或批准。
* Cloud Manager使用的AEM项目原型版本已更新至版本32。


### 错误修复 {#bug-fixes}

* 构建步骤日志中未包含功能和UI测试对象。
* 无法通过公共API访问产品、功能和UI测试步骤的日志。
* 在极少数情况下，从环境详细信息页面到发布或预览服务的链接将无法正常工作。
* 即使用户在名称字段中输入不同的名称，完整堆栈生产管道仍将保留为“生产管道”。
