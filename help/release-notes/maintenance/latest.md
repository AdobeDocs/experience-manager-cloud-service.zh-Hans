---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 53b692b9f668387c889c28498bb20c67149e36be
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 28%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16799 {#release-16799}

以下总结了维护版本16799的不断改进，该版本于2024年6月18日公开发布。 上一个维护版本是版本 16544。

2024.6.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16799}

* ASSETS-31977：增强了资产移动、复制和删除操作。
* ASSETS-33618：Dynamic Media中视频的自动转录和翻译功能。
* ASSETS-35185：ContentHub和DM的审批操作，并向damAssetLucene属性添加属性。
* ASSETS-35533：将DRM和CAI属性添加到damAssetLucene索引。
* ASSETS-37280：当源子标题(vtt)仍在处理时，翻译的连续作业处理。
* ASSETS-37559：改进了已删除资源的事件。
* ASSETS-37723：实施资产发布事件。
* ASSETS-37724：实施资产未发布事件。
* ASSETS-38614：共享链接UI增强功能。
* ASSETS-39601：自动将验证正则表达式应用于资产Livecopy名称。
* ASSETS-39454：在快速入门中升级到查看器2024.5.0。
* CNTBF-184：下面的支持路径 `/conf` 在内容倒流中。

### 修复的问题 {#fixed-issues-16799}

* ASSETS-37335：在筛选器中编辑搜索面板会取消选中所有框。
* ASSETS-38069：时间轴筛选器选择中的AEM DAMPDF预览问题。
* ASSETS-38215：适用于企业的AEMas a Cloud Service订阅中，Adobe Stock的“许可证”按钮显示为灰色。
* ASSETS-38578：资产链接共享报表中的超链接不正确。
* ASSETS-38678：查看收藏集详细信息中损坏的设置。
* ASSETS-39071：如果原始演绎版mimetype为null，则Web优化投放可能会引发异常。
* ASSETS-39316：按名称排序在收藏集中不起作用。
* ASSETS-39377：从远程API接收背压时，从OneDrive批量导入可能会失败。
* ASSETS-39428：版权管理UI中的呈现问题。
* CQ-4357150：cq-content-sync捆绑包中的Guava。
* GRANITE-52573：包含双斜杠的请求 `//` 已拒绝，状态代码为400。
* SCRNS-4194：删除对Google Guava API的依赖关系。
* SCRNS-4360：渠道的内容提供程序中缺少非管理员用户的“管理发布和快速发布”按钮。
* SCRNS-4323：隐藏/禁用screens.html中的启动项。

### 已知问题 {#known-issues-16799}

>[!NOTE]
> AEM Engineering已确定Launches功能的回归，该回归将影响以16461开始的当前AEM版本。 由于此回归，包含非深层页面的新启动项（在应用新版本后创建）因缺少配置而无法正常提升。
> 如果您的环境受到影响，可通过客户支持使用一个shell脚本来识别和更新缺失的配置(内部参考SITES-22457)。
> 将提供更长期的修复，以确保使用所有正确的配置创建新启动项。 在此之前，还可根据需要提供内部补丁发行版本。

#### Forms

1. 如果用户下载最新的AEM Forms SDK (`AEM Forms add-on v2024.05.04.00-240400`)，批处理文件无法启动Docker服务。 要解决此问题：
   1. 下载 [文件夹](/help/forms/assets/sdk_hotfix.zip).
   1. 从下载的文件夹中提取内容并复制 `sdk.sh` 和 `sdk.bat` 文件。
   1. 替换现有 `sdk.sh` 和 `sdk.bat` AEM Forms SDK中包含新文件的文件。

### 更改通知 {#change-notice-16799}

* 此发行版本包含以下新产品索引版本：
   * **damAssetLucene-11**
   * **fragments-11**

  以前的索引版本的自定义版本将自动与新的产品索引版本合并。 请对合并的版本应用进一步的自定义更新。

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
