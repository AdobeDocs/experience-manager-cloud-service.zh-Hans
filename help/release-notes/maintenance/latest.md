---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d73ccc454c89c7e06752de694af97ac26694be17
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 22%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 22450 {#22450}

以下总结了维护版本22450的不断改进，该版本于2025年9月16日公开发布。 上一个维护版本是版本 22171。

激活 2025.9.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新增功能 {#new-features-22450}

* SITES-32595：现在可以识别已完成且已跳过或拒绝片段的工作流。 工作流API响应中提供了新的属性，该属性可列出因无效或引用无效而被排除的片段。
* SITES-33642：现在为修改的内容片段生成和使用了新的API事件。
* SITES-33320：现在可以通过搜索API使用内容片段模型的`technicalName`来搜索该模型。

### 增强功能 {#enhancements-22450}

* SITES-34023：已将`technicalName`字段添加到内容片段模型端点的响应中，以便更好地识别。
* SITES-32766：内容片段模型中的内容资产引用现在支持更广泛的二进制文件类型。
* SITES-33974：改进了OpenAPI文档，使其更加准确且用户友好。
* sites-9173：缓存`ContentPolicyStatus`。
* SITES-9290：改进`TouchEditContext`的缓存。
* SITES-33355：在工作流控制台中的“查看有效负载”上打开新的CF编辑器。
* SITES-33356：在创建CF时打开新的CF编辑器→在触屏UI管理UI中打开。
* SITES-32952：使用投放API时，处理CFM字段的默认值不一致。
* SITES-31539：带有通用编辑器的Edge Delivery：在`head.html`中添加对通用编辑器配置元标记的支持。
* SITES-20672：带有通用编辑器的Edge Delivery：在创作中添加了对其他批量元数据电子表格的支持。
* SITES-32963：使用通用编辑器的Edge Delivery：添加新的试验元数据以优化目标、自动分配和自我学习。
* SITES-30847：发行核心组件2.30.0。
* SITES-29617： referencedBy端点已更新为使用ReferenceSearch类，从而改进了它的性能和可靠性。
* SITES-19308：通过优化参考验证步骤，提高了页面删除过程的性能。
* SITES-34293：对模板化资源实施了延迟加载以提高性能。
* SITES-33892：添加了功能切换，可跳过伪页面的引用检查，这可以提高性能。

### 修复的问题 {#fixed-issues-22450}

* CQ-4360550：修复了AEM Cloud Service中恢复页面移动后语言副本意外消失的问题。
* SITES-25232：设置日期和退出时间扭曲链接没有可见的焦点指示器。
* SITES-25258：焦点不是通过删除注释模式对话框管理的。
* SITES-25305：人口统计工具栏未按逻辑顺序接收焦点。
* SITES-25366：屏幕阅读器不会通知Teaser模式加载状态。
* SITES-34276：使用通用编辑器的Edge Delivery：修复自动创建的CORS策略未应用于发布层。
* SITES-34811：使用通用编辑器的Edge Delivery：修复了hlx选择器未添加到创作时指向电子表格的链接的问题。
* SITES-31669：工具>站点>启动项中的未本地化字符串“此页面重定向到”。
* SITES-30879：站点>页面编辑器>搜索组件中的未本地化字符串。
* SITES-30959：页面编辑器>图像组件中的未本地化字符串。
* SITES-21743：未本地化的“请选择要显示的文档”。 “页面编辑器”>“PDF查看器”中的字符串
* SITES-19785：字符串在核心组件网站>选项卡中未本地化。
* SITES-22059：核心组件站点> PDF查看器中的未本地化的“文件预览不可用”字符串。
* SITES-33360：操作过程中出现未本地化的“错误。 在“启动项”>“编辑”中提供的路径不是“启动项”字符串。
* SITES-32975： “Headless UI”>“启动项”>“将启动项与Source进行比较”中的未本地化日期格式。
* SITES-32973：Headless UI >启动项>重新构建基数中的硬编码字符串。
* SITES-13540：“启动项”>“促销活动”中的未本地化字符串。
* SITES-13085：“站点”>“启动项创建”页面中的未本地化错误字符串。
* SITES-21499：未本地化的字符串是“站点”>“启动项”>“编辑”。
* SITES-14961：截断站点>属性> Blueprint >转出对话框中的日期字段。
* SITES-33764：启动项过滤器(Source路径/工作流创建的启动项)不起作用。
* SITES-33884：“提升当前页面和子页面”会无意中提升超出范围的页面。
* SITES-33611：Live Copy概述不适用于高流量市场。
* SITES-34331：加载非管理员用户的转出覆盖时超时503。
* SITES-34403：关闭期间`NullPointerException`中的`GraphqlClientImpl deactivate()`。
* SITES-33817：解决了UI架构和JCR模型之间的同步问题以确保一致性。
* SITES-31141：现在，API响应中可正确返回未由路径表示的内容引用。
* SITES-34080：内容片段创建过程现在更加稳健，如果没有为请求提供字段，则不会失败。
* SITES-30773：使用“查找和替换”查找单词的正则表达式已得到改进，可正确匹配UTF-8字符。
* SITES-33742：解决了在使用工作流API时阻止成功移动内容片段的错误。

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
