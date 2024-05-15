---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 100%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16145 {#release-16145}

下面总结的是维护版本 16145 的持续改进内容，该版本于 2024 年 5 月 1 日公开发布。上一个维护版本是版本 15977。

2024.5.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16145}

* ASSETS-23489：存储库洞察方面的增强功能。
* ASSETS-26926：对 Dynamic Media 上传轮询进行了改进。
* ASSETS-30351：下载对话框应异步加载 Dynamic Media 演绎版大小。
* ASSETS-30379：提高下载功能中 DRM 许可证的分辨率。
* ASSETS-31058：在“演绎版”选项卡中的 AEM 资产 UI 中显示智能裁切演绎版，并在用户单击这些演绎版时生成智能裁切图像。
* ASSETS-31218：在资产投放 API 中添加对命名智能裁切内容的支持。
* ASSETS-31979：在进行异步资产操作期间添加视觉指示器并禁用 UI 功能。
* ASSETS-32735：改进资产元数据更新事件。
* ASSETS-34661：用于 DM 预览和/或 AEMaaCS Publish 提供的投放 URL 的 API。
* ASSETS-37259：对 XMP 解析进行了改进。
* ASSETS-37263：允许取消失败的 Assets 异步作业。
* CNTBF-114：对内容回流进行了改进。
* CNTBF-148：对内容回流进行了改进。
* CQ-4356992：最新的 AEM 和 Granite 翻译。
* SITES-19326：更新 Assets UI 中的链接，即可在新的 CF 编辑器中打开 CF。
* SITES-20686：GraphQL - 通过 _dmS7Url 公开 Dynamic Media URL（适用于非图像资产）。
* SKYOPS-68091：更新至 Java 11.0.20。

### 修复的问题 {#fixed-issues-16145}

* ASSETS-32321：如果祖先文件夹缺少“jcr：content”子节点，则后处理工作流程会解析失败。
* ASSETS-33856：JPEG 图像预设以 TXT 格式下载文件。
* ASSETS-34096：修复异步下载报告的 Touch UI 视图。
* ASSETS-34493：启用多公司功能切换后加载下载对话框时失败。
* ASSETS-34824：对于 DM 禁用文件夹，复制 URL 显示为空。
* ASSETS-35226：如果在 DAM 根上进行指定，则后处理工作流程无法得到解决。
* ASSETS-35559：将 DM 批量上传失败日志减少为 WARN。
* ASSETS-35860：AEM Assets 列视图中的时区转化不正确。
* ASSETS-35935：关闭负载审查后文件夹导航出错。
* ASSETS-35961：在图像配置文件下添加裁切按钮不起作用。
* ASSETS-36227：发布时禁用 FolderPreviewUpdaterImpl 服务。
* ASSETS-36943：当列表视图中的文件夹中存在 CF 和其他非 CF 项目时，列无法对齐。
* ASSETS-36990：导出元数据作业因属性过多而失败/放缓。
* ASSETS-37113：如果查询仅返回 CF 结果，则重新处理资产作业将会立即终止。
* ASSETS-37260：在 AEM 中导出元数据时可能会产生无效的 CSV。
* ASSETS-37261：AEM Assets 上的 PPTx 和 PDF 注释问题。
* ASSETS-37282：打开大型文件夹的请求可能会很慢。
* ASSETS-37330：从 OneDrive 批量导入时会创建错误的 AEM 文件夹结构。
* ASSETS-37609：删除旧版 scene7 conf 查找功能。
* ASSETS-38016：某些元数据更新未在事件中正确跟踪。
* CQ-4357161：AEM 收件箱负载屏幕返回 404。
* GRANITE-50041：当下拉选项中只有“添加渲染”选项，并且分辨率宽度超过 1440px 时，“添加渲染”不起作用。
* GRANITE-50279：Coral Datepicker 组件中的星期名称混乱。
* SCRNS-3949：Screens 频道获取请求时间过长。
* SCRNS-3981：[序列频道]当元素加载/卸载事件的序列失真时会导致黑屏。
* SCRNS-4180：[序列频道]从后备缩略图恢复后，对于视频时长为 -1 的频道，序列停止并显示空白屏幕。
* SCRNS-4245：[序列频道]加载视频并从后备缩略图切换时，空白屏幕的持续时间有限。
* SITES-16055：修复相应属性页面中的 Live Copy 和 Live Copy Source 链接。
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
