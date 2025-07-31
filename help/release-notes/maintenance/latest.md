---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3686697c85273ccc13e80b8d7f4ad1ff3c79845d
workflow-type: ht
source-wordcount: '632'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21706 {#21706}

以下是 2025 年 7 月 24 日正式发布的维护版本 21706 的持续改进摘要。上一个维护版本是版本 21570。

>[!NOTE]
>
>版本 21644 已设为专用，被版本 21706 取代。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21706}

* ASSETS-39377：改进资产批量导入器中远程存储的 429 的处理。
* ASSETS-46026：元数据导出器的可配置最大深度。
* ASSETS-49172：动态媒体模板资产应从文件夹继承元数据。
* ASSETS-50209：支持 DM 模板中的子字符串。
* ASSETS-52326：AEM Assets 配置页面用于设置 Assets 的标题显示偏好。
* ASSETS-52805：添加批量操作任务的 CSV 输出/下载支持。
* ASSETS-52873：在文件夹属性中添加一个新配置，以禁用该文件夹的 AI 处理。
* ASSETS-53535：改进了 YouTube 视频上传性能。
* ASSETS-53612：控制 Assets 全方位搜索中的混合搜索。
* GRANITE-60183：将 commons-fileupload 依赖项更新至 1.6.0。
* GRANITE-60287：将 QS 更新到 Jackrabbit 2.22.1。
* SITES-30452：带有 ASO 的内容 API - 标题和描述建议。
* SITES-31677：自定义工作区现已支持将 AEM 内容片段导出至 Target。
* SKYOPS-112741：从 AEM-CS SDK 中移除 `com.adobe.granite.product.support` 捆绑包。

### 修复的问题 {#fixed-issues-21706}

* ASSETS-12882：打开查看器预设后出现 UI 对齐问题。
* ASSETS-48958：资产同步问题导致 Sites 本地 AEM 中的已发布状态发生变化。
* ASSETS-50856：`dam:processingAttempts` 在 completeUpload 上未重置。
* ASSETS-51604：链接共享报告的 CSV 文件缺少 “共享对象” 数据。
* ASSETS-51783：如果使用搜索查询未找到配置，则回退到 `/conf/global` 中的 DM 配置。
* ASSETS-51857：资产表项目不可重新排序。
* ASSETS-52169：资产下载中错误包含了新的 BAT 机器演绎版。
* ASSETS-52229：在 AEM as a Cloud Service 中未收到资产报告的收件箱通知。
* ASSETS-52399：com.day.cq.dam.api 中的版本提升可能会破坏客户代码。
* ASSETS-52780：即使未启用切换选项，资产仍可被标记为预览。
* ASSETS-52866：迁移后的 DM 视频在禁用 DM 同步的文件夹中仍处于正在处理的状态。
* ASSETS-53237：图像预设编辑器中的颜色轮廓下拉菜单为空白。
* ASSETS-53240：资产报告 - 从 Dynamic Media 获取资产演绎版大小时，磁盘使用情况报告失败。
* ASSETS-53446：NPE 导致 YouTube 身份验证令牌刷新间歇性失败。
* ASSETS-53827：ACL 验证阻止了混合媒体集的保存。
* ASSETS-5403：发布实例上使用的 Dynamic Media 客户端库应该具有 `allowProxy=true`。
* ASSETS-54261：如果文件下载失败，元数据导入将导致连接泄漏并最终被阻塞。
* CQ-4359863：内容片段编辑器/资产编辑器中，标记搜索因关键词顺序错误而中断。
* CQ-4359958：使 openapi-support 与 AEM 6.5.22.0 及更高版本兼容。
* CQ-4360256：对于通过 `/adobe` servlet 上下文处理的 HTTP 请求，在请求路径中包含 servlet 上下文路径。
* CQ-4360317：添加在构建响应时设置 Sunset 日期标头的方法。
* GRANITE-60311：AEM SDK 快速启动 — “OSGi Installer Configuration Printer” 出现空指针异常（NPE）。
* GS-15285：用户显示为已被停用。

### 已知问题 {#known-issues-21706}

无。

### 已弃用的功能和 API {#deprecated-21706}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21706}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21706}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
