---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: ht
source-wordcount: '902'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 22450 {#22450}

以下为维护版本 22450 的持续改进内容，该版本已于 2025 年 9 月 16 日正式发布。上一个维护版本是版本 22171。

激活 2025.9.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新增功能 {#new-features-22450}

* SITES-32595：现在可以识别包含被跳过或拒绝片段的已完成的工作流。工作流 API 响应中新增了一个属性，用于列出因无效或引用无效而排除的片段。
* SITES-33642：新增 API 事件，用于生成和处理已修改的内容片段。
* SITES-33320：现在可以通过搜索 API 使用 `technicalName` 搜索内容片段模型。

### 增强功能 {#enhancements-22450}

* SITES-34023：在内容片段模型端点的响应中新增了 `technicalName` 字段，以便更好地进行识别。
* SITES-32766：内容片段模型中的内容资产引用现已支持更广泛的二进制文件类型。
* SITES-33974：改进了 OpenAPI 文档，使其更准确且更易于使用。
* SITES-9173：缓存 `ContentPolicyStatus`。
* SITES-9290：改进了 `TouchEditContext` 的缓存机制。
* SITES-33355：在工作流控制台中点击“查看负载”时，会打开新的内容片段编辑器。
* SITES-33356：在“创建内容片段 → 在 TouchUI 管理用户界面中打开”时，将会打开新的内容片段编辑器。
* SITES-32952：使用投放 API 时，对内容片段模型字段默认值的处理不一致。
* SITES-31539：使用通用编辑器的 Edge Delivery：在 `head.html` 中新增对通用编辑器配置元标记的支持。
* SITES-20672：使用通用编辑器的 Edge Delivery：在创作中新增对额外批量元数据表格的支持。
* SITES-32963：使用通用编辑器的 Edge Delivery：新增实验性元数据，用于优化目标、自动分配和自我学习。
* SITES-30847：发布核心组件 2.30.0。
* SITES-29617：更新了 referencedBy 端点，以使用 ReferenceSearch 类，从而提升性能和可靠性。
* SITES-19308：通过优化引用验证步骤，提高了页面删除流程的性能。
* SITES-34293：为模板化资源实施了延迟加载，以提升性能。
* SITES-33892：新增功能开关，可跳过伪页面的引用检查，从而提升性能。

### 修复的问题 {#fixed-issues-22450}

* CQ-4360550：修复了在 AEM Cloud Service 中还原页面移动操作后语言副本意外消失的问题。
* SITES-25232：“设置日期”和“退出时间扭曲”链接缺少可见的焦点指示器。
* SITES-25258：“删除注释”模式对话框中未正确管理焦点。
* SITES-25305：人口统计工具栏未按逻辑顺序获得焦点。
* SITES-25366：屏幕阅读器未提示 Teaser 模态框的加载状态。
* SITES-34276：使用通用编辑器的 Edge Delivery：修复自动创建的 CORS 策略未在发布层生效的问题。
* SITES-34811：使用通用编辑器的 Edge Delivery：修复在创作过程中未向电子表格链接添加 hlx 选择器的问题。
* SITES-31669：在工具 > 网站 > 启动中，“此页面重定向到”字符串未本地化。
* SITES-30879：网站 > 页面编辑器 > 搜索组件中的字符串未本地化。
* SITES-30959：页面编辑器 > 图像组件中的字符串未本地化。
* SITES-21743：页面编辑器 > PDF 查看器中的“请选择要显示的文档。”字符串未本地化。
* SITES-19785：核心组件网站 > 选项卡中的字符串未本地化。
* SITES-22059：核心组件网站 > PDF 查看器中的“文件预览不可用”字符串未本地化。
* SITES-33360：发布项 > 编辑中的“操作过程中出现错误。提供的路径不是发布项”字符串未本地化。
* SITES-32975：Headless UI > 发布项 > 将发布项与源比较中的日期格式未本地化。
* SITES-32973：Headless UI > 发布项 > 重新设定基准中存在硬编码字符串。
* SITES-13540：发布项 > 推广中的字符串未本地化。
* SITES-13085：网站 > 发布项创建页面中的错误字符串未本地化。
* SITES-21499：网站 > 发布项 > 编辑中的字符串未本地化。
* SITES-14961：网站 > 属性 > Blueprint > 转出对话框中的日期字段被截断。
* SITES-33764：发布项筛选条件（源路径/由工作流创建的发布项）无效。
* SITES-33884：“提升当前页面及其子页面”会意外提升超出范围的页面。
* SITES-33611：在高容量市场中，Live Copy 概览无法正常工作。
* SITES-34331：为非管理员用户加载转出叠加层时出现 503 超时。
* SITES-34403：关闭过程中，在 `GraphqlClientImpl deactivate()` 中发生 `NullPointerException`。
* SITES-33817：已解决 UI 架构与 JCR 模型之间的同步问题，以确保一致性。
* SITES-31141：在 API 响应中，现已正确返回未通过路径表示的内容引用。
* SITES-34080：内容片段创建过程现更加稳健，即使请求未提供任何字段也不会失败。
* SITES-30773：“查找和替换”功能的正则表达式已优化，可正确匹配 UTF-8 字符。
* SITES-33742：已修复使用工作流 API 时阻止内容片段成功移动的错误。

### 已知问题 {#known-issues-22450}

无。

### 已弃用的功能和 API {#deprecated-22450}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-22450}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 18 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-22450}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
