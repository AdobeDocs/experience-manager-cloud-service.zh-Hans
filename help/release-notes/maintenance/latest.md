---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 6b4fa2802b860c938f5085f047cc880f29698f3e
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 81%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 13206 {#release-13206}

下面总结了维护版本 13206 的持续改进，该版本已于 2023 年 8 月 21 日公开发布。此维护版本取代了版本13173和13099，以修复影响收件箱功能的问题。

激活 2023.8.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13206}

- SITES-13906：GraphQL - 升级到 graphql-java 20.1。
- SITES-8972：GraphQL - 在 JSON 中为枚举数据类型添加选项标签。
- SITES-9689：GraphQL - 在 JSON 中添加内容引用数据类型的标题和描述。
- SITES-13052：内容片段 - 将内容片段导出到 Adobe Target。

### 修复的问题 {#fixed-issues-13206}

- SITES-14937：MSM - 在实时副本上点击“保存并关闭”时，会切换“从父值继承转出配置“。
- SITES-14847：内容片段 - 内容片段链接未突出显示。
- SITES-11620：内容片段 - UI 中的参考路径略有删减。
- SITES-14171：GraphQL - 在某些情况下，缓存数据的循环引用不会被破坏。
- SITES-14577：体验片段 - 批量发布不适用于实时副本。
- SITES-14341：管理员UI — 删除删除权限时，“属性”按钮的行为不一致。
- SITES-11000：管理 UI - 参考：某些页面中缺少传入链接。
- SITES-11559：管理 UI - 参考：传入链接显示错误页面。
- SITES-14337：管理 UI - 在特定情况下打开编辑器页面会产生错误。
- SITES-13425：ContextHub - 单击 ContextHub 按钮时不显示菜单栏。
- CQ-4354266：无法打开收件箱项目。
- CQ-4354279：在“个性化”选项卡下看不到活动报表。
- FORMS-9971：当在不同的区域设置中呈现自适应表单时，组件的可见性会被错误地解释和应用。
- FORMS-9888：当自适应表单设置为在表单提交时重定向到外部 URL（感谢页面）时，它无法重定向到外部 URL。
- FORMS-9845：使用规则编辑器清除下拉列表后，尽管假定已清除，但先前提供的值仍然存在。
- FORMS-9263：当复选框的标签包含特殊字符并且用户单击该复选框时，不会选择相应的复选框。
- FORMS-9254：当用户滚动浏览条款和条件组件的文本时，即使在用户滚动浏览整个文本之前，组件内的复选框也会自动启用。
- FORMS-9045：脚本标签无法解析 BASE XDP 中的外部片段引用。
- FORMS-9026：尝试使用 JSON 架构创建自适应表单（该架构具有带有空字符串的枚举并且验证没有错误）时，该过程会导致失败。接下来，刷新页面后，表单无法正确加载，显示空白表单并在日志中显示错误。
- FORMS-8964：在 Android™ Chrome/Firefox 中，如果达到最大字符数限制，文本框组件中的文本将变得不可编辑。
- FORMS-8668：尽管功能表单呈现，但错误日志中的 Java™ 堆栈转储过多，导致日志文件膨胀。
- FORMS-8554：启用延迟加载的自适应表单在作者实例的预览模式下不起作用。
- FORMS-8177：当表单服务处于活动状态时，出现异常“com.adobe.aem.formsndocuments.publish.AssetReferenceProvider 无法检索资产依赖项。”。禁用表单服务后该错误消失。
- FORMS-3691：某些对象缺少 IIFE（立即调用函数表达式）作用域。使用 IIFE 的主要目的是为函数内的变量创建一个作用域，防止这些变量污染全局作用域。
- sites-15463：站点模板 — 无法发布模板。

### 已知问题 {#known-issues-13206}

- SITES-15359：内容片段 — 变量名称模式无法正确匹配具有以下特征的变量 ```'_'``` 在资源名称中。
- Forms-10444：自适应Forms模板 — 无法发布模板（解决方法：使用分发控制台）。
- CQ-4354191：工作流 — 由于nt：unstructured节点上存在复制元数据，自定义启动器可能会触发许多次（解决方法：更新启动器以排除复制元数据属性以避免重叠）。
- SITES-15622： GraphQL — 使用数字和布尔参数的持久查询存在问题。
- SITES-15654： GraphQL — 同名的合并和属性存在问题。

### 嵌套的技术 {#embedded-tech-13206}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.2 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
