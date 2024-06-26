---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fd687498a8c72bf5d47b7b97aadf22d7d1e8dd2b
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 96%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16799 {#release-16799}

下面总结了维护版本 16799 的持续改进，该版本已于 2024 年 6 月 18 日公开发行。上一个维护版本是版本 16544。

2024.6.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16799}

* ASSETS-31977：增强资产移动、复制和删除操作。
* ASSETS-33618：Dynamic Media 中视频的自动转录和翻译功能。
* ASSETS-35185：审批 ContentHub 和 DM 的操作并向 damAssetLucene 属性添加属性。
* ASSETS-35533：将 DRM 和 CAI 属性添加到 damAssetLucene 索引。
* ASSETS-37280：当源字幕 (vtt) 仍在处理时，对翻译进行顺序作业处理。
* ASSETS-37559：改进资产删除事件。
* ASSETS-37723：实现资产发布事件。
* ASSETS-37724：实现资产未发布事件。
* ASSETS-38614：共享链接 UI 增强功能。
* ASSETS-39601：将验证正则表达式自动应用于 Asset Livecopy 名称。
* ASSETS-39454：在 Quickstart 中升级到查看器 2024.5.0。
* CNTBF-184：支持内容回流中 `/conf` 下方的路径。

### 修复的问题 {#fixed-issues-16799}

* ASSETS-37335：在过滤器中编辑搜索面板会取消选中所有框。
* ASSETS-38069：AEM DAM PDF 预览时间线过滤器选择问题。
* ASSETS-38215：Adobe Stock 许可证按钮在企业订阅的 AEM as a Cloud Service 中显示为灰色。
* ASSETS-38578：资产链接共享报告中的超链接不正确。
* ASSETS-38678：查看“集合详细信息”中损坏的设置。
* ASSETS-39071：如果原始呈现 mimetype 为空，则 Web 优化传递可能会引发异常。
* ASSETS-39316：在收藏夹中按名称排序不起作用。
* ASSETS-39377：当收到来自远程 API 的背压时，从 OneDrive 批量导入可能会失败。
* ASSETS-39428：版权管理 UI 中的渲染问题。
* CQ-4357150：cq-content-sync 捆绑包中的 Guava。
* GRANITE-52573：包含双斜杠 `//` 的请求将被拒绝，状态代码为 400。
* SCRNS-4194：移除对 Google Guava API 的依赖。
* SCRNS-4360：频道内容提供商中非管理员用户缺少“管理发布”和“快速发布”按钮。
* SCRNS-4323：隐藏/禁用从 screens.html 启动。

### 已知问题 {#known-issues-16799}

>[!NOTE]
> AEM Engineering 已发现启动功能存在回归问题，这会影响从 16461 开始的当前 AEM 版本。由于这种回归，包含非深层页面的新启动项（应用新版本后创建）将由于缺少配置而无法正确推广。
> 如果您的环境受到影响，可以通过客户支持获取用于识别和更新缺失配置的 shell 脚本（内部参考 SITES-22457）。
> 我们将提供长期修复，以确保新的启动项能够以所有正确的配置进行创建。在此之前，还可以根据需求提供内部补丁版本。

#### Forms

1. 如果用户下载的AEM Forms SDK版本高于 `AEM Forms add-on v2024.05.04.00-240400`，批处理文件无法启动Docker服务。 要解决该问题：
   1. 下载[文件夹](/help/forms/assets/sdk_hotfix.zip)。
   1. 从下载的文件夹中提取内容并复制 `sdk.sh` 和 `sdk.bat` 文件。
   1. 用新文件替换 AEM Forms SDK 中现有的 `sdk.sh` 和 `sdk.bat` 文件。

### 更改通知 {#change-notice-16799}

* 此版本包含以下新的产品索引版本：
   * **damAssetLucene-11**
   * **片段 11**

  先前索引版本的自定义版本将自动与新产品索引版本合并。请对合并版本应用进一步的自定义更新。

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-16799}

若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16799}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
