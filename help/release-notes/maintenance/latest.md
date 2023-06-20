---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 26178edc3308801e0273aca67b7cd82180131483
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 37%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 12255 {#release-12255}

以下是维护版本12255的持续改进，该版本于2023年6月13日公开发布。 此维护版本是对上一个维护版本 12142 的更新。

此维护版本的功能支持将为您提供完整功能集。有关完整详细信息，请参阅[最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 增强 {#enhancements-12255}

无。

### 已知问题 {#known-issues-12255}

- ASSETS-25729 — 视图切换器菜单被切断
- ASSETS-25728 — 重新处理资产选项在搜索视图中不可用
- ASSETS-22603 — 某些下载类型的资产报表列在UI中显示“null”值。 可下载的CSV不受影响。

### 修复的问题 {#fixed-issues-12255}

- 各种与辅助功能相关的更新
- ASSETS-15116 — “资产”搜索视图中提供的“转到位置”选项
- ASSETS-17453 - (Dynamic Media)无法为视频选择自定义缩略图
- ASSETS-19279 — 大型文件的资产下载存档
- ASSETS-19544 — 用户上次修改以获取资源更新
- ASSETS-20146 — （触屏UI）资产下载报表由于验证错误而失败的报表始终显示在报表列表页面的顶部
- ASSETS-21056 — 优化资产引用性能以最大限度地减少写入
- ASSETS-21909 — 当vtt下载失败时，无法查看智能裁剪视频
- ASSETS-22261 — 链接共享下载文件夹结构与资产UI下载不一致
- ASSETS-22550 — 默认情况下搜索筛选器面板现在打开
- ASSETS-22920 — 从Brand Portal中取消发布文件夹不会将中的资产标记为未发布
- ASSETS-22922 — 禁用的查看器预设显示在Dynamic Media组件中
- ASSETS-23461 — 从“资源”搜索视图中快速发布Brand Portal
- ASSETS-23466 -InDesign Server无法访问链接处理无法解析包含空格的AAL链接
- ASSETS-23469 — 默认资源筛选器与自定义筛选器冲突
- ASSETS-23981 — 标题排序功能在收藏集链接中不起作用
- ASSETS-24723 — 再次重新处理已发布的资产，无需用户干预
- GRANITE-45385 — 迁移树激活以使用sling作业而不是工作流

### 嵌套的技术 {#embedded-tech-12255}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
