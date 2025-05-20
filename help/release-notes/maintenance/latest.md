---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 859af15f4038b28e6e1398e5168dc008d22985e9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 96%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

>[!NOTE]
>
> 版本20936和20783已设为私有。

## 版本 20626 {#20626}

下面总结了维护版本 20626 的持续改进，该版本于 2025 年 4 月 29 日公开发布。上一个维护版本是版本 20476。

2025.5.0功能激活提供了此维护版本的完整功能集。 有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20626}

* ASSETS-46413、ASSETS-46580：添加了新的审核状态“预览”。
* ASSETS-49542：扩展视频和音频转录和翻译的受支持语言。
* ASSETS-48264：扩展对演绎版的 PNG 质量支持。

### 修复的问题 {#fixed-issues-20626}

* ASSETS-50387：更正内容片段默认缩略图，以便在 GenStudio 中使用。
* ASSETS-49006：当用户没有写入权限时显示视频属性。
* ASSETS-46757、ASSETS-46997：提高智能裁剪编辑器的无障碍可访问性。
* ASSETS-48018：改进资产发布报告中的资产引用跟踪。
* ASSETS-35846：提高创作层与投放层之间的访问权限一致性。
* ASSETS-48171：提高动态媒体模板与画布的一致性。
* ASSETS-49813：改进过期通知。
* ASSETS-47768、ASSETS-49825、ASSETS-49008、ASSETS-48287：提高批量操作的管理和可见性。
* ASSETS-50003、ASSETS-50004：改进对资产下载中包含的演绎版的命名和控制。
* ASSETS-47939：改进 Content Hub 的响应的组织方式。
* ASSETS-46738：提高巨大收藏集的性能。
* ASSETS-50121：提高资产发布事件的可靠性。
* ASSETS-48490：提高图像摄取过程中自动处理的弹性。
* ASSETS-28106、ASSETS-49404：提高全文搜索的稳健性。
* ASSETS-50006、ASSETS-50423：提高在大文件夹中搜索和遍历的性能。
* ASSETS-46021：改进 Safari 和移动浏览器的视频显示。
* ASSETS-49002：改进编辑动态媒体模板的处理方式。
* ASSETS-48376：Content Hub 用户界面中的其他改进。
* ASSETS-48504、ASSETS-49378：对用户界面行为进行的其他改进。
* ASSETS-49540：将资产关系 OpenAPI 移出实验阶段。
* ASSETS-40284：更新有关 Adobe Stock 集成的文档。
* ASSETS-49739：从 Asset 选择器集成 Figma。

#### AEM 指南 {#guides}

* GUIDES-21734：当通过代码片段添加元素或通过模板创建元素时，即使在 XMLEditorConfig 中启用了自动生成 ID 选项，也无法为这些元素生成新的 ID。
* GUIDES-25969：如果一个 DITA 主题中的外部链接缺少 `scope=external` 属性，HTML5 发布就会失败，并且错误日志中不会说明缺少此属性的文件，尤其是在启用微服务的情况下。
* GUIDES-27288：无法将元数据属性传递给使用新 AEM Sites 发布生成的地图登陆页面。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-20626}

无。

### 已弃用的功能和 API {#deprecated-20626}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-20626}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 11 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-20626}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
