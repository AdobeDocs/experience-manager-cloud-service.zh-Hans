---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 29%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16145 {#release-16145}

以下总结了维护版本16145的持续改进，该版本于2024年5月1日公开发布。 上一个维护版本是版本 15977。

2024.5.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16145}

* ASSETS-23489：存储库见解改进。
* ASSETS-26926：Dynamic Media上传轮询改进。
* ASSETS-30351：“下载”对话框应异步加载Dynamic Media演绎版大小。
* ASSETS-30379：提高下载中DRM许可证的分辨率。
* ASSETS-31058：在AEM assets UI的“演绎版”选项卡中，显示智能裁剪演绎版，并在用户单击这些演绎版时生成智能裁剪图像。
* ASSETS-31218：在资源投放api中添加对命名smartcrop的支持。
* ASSETS-31979：在异步资产操作期间添加视觉指示器并禁用UI函数。
* ASSETS-32735：改进了资产元数据更新事件。
* ASSETS-34661：AEMaaCS Publish中的DM预览和/或交付URL的API。
* ASSETS-37259：XMP解析改进。
* ASSETS-37263：允许取消失败的资产异步作业。
* CNTBF-114：改进了内容回流。
* CNTBF-148：改进了内容回流。
* CQ-4356992：最新的AEM和Granite翻译。
* SITES-19326：更新 Assets UI 中的链接，即可在新的 CF 编辑器中打开 CF。
* SITES-20686： GraphQL — 通过_dmS7Url公开Dynamic Media URL（对于非图像资源）。
* SKYOPS-68091：更新至Java 11.0.20。

### 修复的问题 {#fixed-issues-16145}

* ASSETS-32321：如果上级文件夹缺少“jcr：content”子节点，则后处理工作流解析失败。
* ASSETS-33856：JPEG图像预设以TXT格式下载文件。
* ASSETS-34096：修复触屏UI视图，以便异步下载报表。
* ASSETS-34493：启用多公司功能切换后，加载下载对话框时失败。
* ASSETS-34824：对于DM禁用的文件夹，复制URL显示为空。
* ASSETS-35226：如果在DAM根上指定，则未解析后处理工作流。
* ASSETS-35559：将DM批量上传失败日志减少为WARN。
* ASSETS-35860：AEM Assets 列视图中的时区转化不正确。
* ASSETS-35935：关闭有效负载审查后不正确的文件夹导航。
* ASSETS-35961：添加裁切按钮在图像配置文件下不起作用。
* ASSETS-36227：在发布时禁用FolderPreviewUpdaterImpl服务。
* ASSETS-36943：在列表视图的文件夹中存在CF和其他非CF项目时，未对齐列。
* ASSETS-36990：导出元数据作业失败/缓慢，并出现大量属性。
* ASSETS-37113：如果查询仅返回CF结果，则重新处理资源作业将立即终止。
* ASSETS-37260：AEM中的元数据导出可能会生成无效的CSV。
* ASSETS-37261：AEM Assets上存在PPTx和PDF注释问题。
* ASSETS-37282：打开大型文件夹的请求速度可能缓慢。
* ASSETS-37330：从OneDrive批量导入会创建错误的AEM文件夹结构。
* ASSETS-37609：删除旧版scene7 conf查找。
* ASSETS-38016：事件中未正确跟踪某些元数据更新。
* CQ-4357161：AEM收件箱有效负载屏幕返回404。
* GRANITE-50041：当下拉菜单中只有“添加演绎版”选项时，如果分辨率大于1440像素宽度，则添加演绎版无法正常工作。
* GRANITE-50279：Coral日期选取器组件中的周名称混乱。
* SCRNS-3949： Screens渠道获取请求时间过长。
* SCRNS-3981： [序列渠道] 当元素加载/卸载事件的顺序被扭曲时，导致出现黑屏。
* SCRNS-4180： [序列渠道] 在从回退缩略图恢复时，对于持续时间为–1的视频，序列将停止并显示一个空白屏幕。
* SCRNS-4245： [序列渠道] 加载视频并从回退缩略图切换视频时，出现空白屏幕的持续时间有限。
* SITES-16055：修复各个属性页面中的Live Copy和Live Copy源链接。
* SCRNS-4243：非管理员用户的内容提供程序中缺少按钮。

### 已知问题 {#known-issues-16145}

无。

### 已弃用的功能和 API {#deprecated-16145}

* [在 Adobe Developer Console 中弃用 JWT 凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* 自 2024 年 5 月 1 日起，Adobe Dynamic Media 将终止对以下内容的支持：

   * SSL（安全套接字层）2.0
   * SSL 3.0
   * TLS（传输层安全性）1.0 和 1.1
   * TLS 1.2 中的以下弱密码：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16145}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.24.6 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
