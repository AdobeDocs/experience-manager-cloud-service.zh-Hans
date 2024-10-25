---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18311 {#18311}

下面总结了针对维护版本 18311 的持续改进，该版本于 2024 年 10 月 22 日公开发布。上一个维护版本是版本 18175。

激活 2024.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18311}

* ASSETS-41820：处理看门狗的索引改进。
* ASSETS-43720：处理看门狗的功能改进。
* ASSETS-42554：大文件夹的性能改进。
* SKYOPS-77603：商业用户管理重定向。

### 修复的问题 {#fixed-issues-18311}

* ASSETS-37534：搜索变更不会暴露用于审批目标的属性。
* ASSETS-38322：删除发布标准提供商配置删除发布事件功能。
* ASSETS-40482：Scene7 视频播放器中的播放/暂停和静音/取消静音按钮存在可访问性问题。
* ASSETS-40593：单击“资产”>“文件”中的”属性“按钮后出现错误页面。
* ASSETS-40598：当未同步的资产移动到启用同步的文件夹时同步智能裁剪。
* ASSETS-40743：当文件名中存在某些字符时触发“替换资产”对话框的问题。
* ASSETS-40825：编辑搜索表单后资产搜索方面消失。
* ASSETS-41007：在 AEM 上进行删除有时会在传递时留下孤立资产。
* ASSETS-41172：动态媒体模板名称中不允许使用特殊字符。
* ASSETS-41896：文件夹中 cq:discarded 属性中提到的资产不应发布到 Brand Portal。
* ASSETS-42067：Dynamic Media 模板 - 下载出现错误。
* ASSETS-42070：Dynamic Media 模板 - 非管理员用户应该具有模板创建/编辑访问权限。
* ASSETS-42344：已连接的资产同步已断开 - 重新连接并为客户提供建议。
* ASSETS-42620：资产版本的预览选项存在问题 - 打开资产时显示空白预览。
* ASSETS-42701：Web 优化图像传递和裁切问题。
* ASSETS-42966：如果多个作业共享相同的路径，则异步路障可能会错误地解除阻塞。
* ASSETS-43072：Dynamic Media 模板 - 模板引用查找因无效引用而中断。
* ASSETS-43212：元数据架构编辑器中的国际化问题。
* ASSETS-43202：修复从时间线选择要打印的注释的问题。
* ASSETS-43502：AEM CS 现有图像预设名称未显示在编辑页面上。
* ASSETS-43538：异步复制资产作业使用了错误的源路径属性。
* ASSETS-43798：复制资产之前先检查目标路径。
* ASSETS-43945：将异步资产作业队列的重试延迟增加至 20 分钟。
* ASSETS-44025：当选择单个资产时，异步删除资产作业失败。
* SITES-26128：CreateLiveCopyStep 中出现类转换异常。
* SCRNS-4551：[SG Pools] 包含视频组件的 Screens 频道在浏览器预览和播放器上显示“常规页面错误”

### 已知问题 {#known-issues-18311}

* FORMS - 15818：组件描述符条目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在服务器日志中未找到语句。这些是无害的日志语句。

### 已弃用的功能和 API {#deprecated-18311}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-18311}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 3 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18311}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
