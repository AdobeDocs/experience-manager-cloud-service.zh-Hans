---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cb963a233b5afd4497704233db7f51c37563d0f9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 22%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 13099 {#release-13099}

以下总结了维护版本13099的不断改进，该版本于2023年8月15日公开发布。 此维护版本是对上一个维护版本 12874 的更新。

激活 2023.8.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13099}

- SITES-13906： GraphQL — 升级到graphql-java 20.1。
- SITES-8972： GraphQL — 在JSON中为枚举数据类型添加选项标签。
- SITES-9689： GraphQL — 在JSON中为内容引用数据类型添加标题和描述。
- SITES-13052：内容片段 — 将内容片段导出到Adobe Target

### 修复的问题 {#fixed-issues-13099}

- SITES-14937： MSM — 从父项继承转出配置值在点击活动副本上的保存并关闭时切换。
- SITES-14847：内容片段 — 内容片段链接未高亮显示。
- SITES-11620：内容片段 — 在UI中稍微剪切引用路径。
- SITES-14171： GraphQL — 在某些情况下，不会破坏缓存数据的循环引用。
- SITES-14577：体验片段 — 批量发布不适用于活动副本。
- SITES-14341：管理员UI — 删除删除权限时，“属性”按钮的行为不一致。
- SITES-11000：管理员UI — 引用：某些页面中缺少传入链接。
- SITES-11559：管理员UI — 引用：传入链接显示错误的页面。
- SITES-14337：管理员UI — 在特定情况下，打开编辑器页面会生成错误。
- SITES-13425：ContextHub — 单击ContextHub按钮时菜单栏不显示。
- Forms-9971：在其他区域设置中呈现自适应表单时，组件的可见性会得到不准确的解释和应用。
- Forms-9888：如果将自适应表单设置为在提交表单时重定向到外部URL（感谢页面），则自适应表单将无法重定向到外部URL。
- Forms-9845：使用规则编辑器清除下拉列表后，尽管假定存在清除，但之前提供的值仍将保留。
- Forms-9263：如果复选框的标签包含特殊字符，并且用户单击了该复选框，则相应的复选框未选中。
- Forms-9254：当用户滚动条款与条件组件的文本时，组件中的复选框会在用户滚动整个文本之前自动启用。
- Forms-9045：脚本标记不会解析基本XDP中的外部片段引用。
- Forms-9026：尝试使用JSON架构创建自适应表单时，如果该JSON架构的枚举包含空字符串并且验证无错误，则该过程会导致失败。 接下来，在刷新页面时，表单无法正确加载，显示空白表单并在日志中显示错误。
- Forms-8964：在Android™ Chrome/Firefox中，如果达到最大字符限制，则文本在文本框组件中将变为不可编辑。
- Forms-8668：尽管呈现了功能表单，错误日志中仍存在过多的Java™栈栈转储，从而导致日志文件膨胀。
- Forms-8554：启用了延迟加载的自适应Forms在创作实例的预览模式下不起作用。
- Forms-8177：当表单服务处于活动状态时，出现“com.adobe.aem.formsndocuments.publish.AssetReferenceProvider无法检索资源依赖关系”异常。 发生。 禁用表单服务时，该错误消失。
- Forms-3691：某些对象缺少IIFE（立即调用函数表达式）作用域。 使用IIFE的主要目的是在函数中为变量创建一个范围，以防止这些变量污染全局范围。


### 已知问题 {#known-issues-13099}

- SITES-15359：变量名称模式无法正确匹配具有以下特征的变量 ```'_'``` 在资源名称中。

### 嵌套的技术 {#embedded-tech-13099}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.2 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
