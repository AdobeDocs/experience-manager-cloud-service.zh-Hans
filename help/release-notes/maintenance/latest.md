---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 24%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 13665 {#release-13665}

以下总结了维护版本13665的不断改进，该版本于2023年9月27日公开发布。 此维护版本取代版本 13420。

2023.10.0功能激活提供了此维护版本的完整功能集。 有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13665}

* 对内容片段API进行了各种改进。
* ASSETS-26713：资产功能板：新的Experience UI功能板现在可以从触屏UI访问。
* SITES-11206：内容片段：搜索API以获取内容片段。
* SITES-11262：内容片段：用于切换到新内容片段编辑器的按钮。
* SITES-15447：核心组件：版本2.23.4的发布。

### 修复的问题 {#fixed-issues-13665}

* 各种与翻译相关的更新。
* CQ-4354428：工作流：无法完成收件箱中的任务。
* SITES-9733：内容片段：内容片段引用面板中的资产引用显示0（零）引用。
* SITES-14561：内容片段：修复并改进了标记到标记转换的HTML。
* SITES-14882：内容片段：编辑内容片段并在未单击保存或关闭按钮的情况下关闭选项卡后，将存储相应的值。
* SITES-15167：内容片段：使用无效有效负载修补变体不会返回400，而会返回500。
* SITES-15514：内容片段：RTE中表的Markdown输出格式不正确。
* SITES-15661：内容片段：请勿在片段API的引用字段中使用唯一约束和重新排序项。
* SITES-15730：屏幕：屏幕渠道预览功能在功能板上不起作用。
* SITES-15995：内容片段：对模型和片段长文本字段的MIME类型进行硬编码。
* SITES-16074：内容片段：非字符串的标记字段[] 无法从JCR检索。
* SITES-16084：内容片段：CFHomeCardModelImpl缺少目标导航器。
* SITES-14773：体验片段：链接引用未在体验片段内更新。
* SITES-14899：体验片段：为Target中的XF变体创建多个选件。
* SITES-8590： GraphQL：持久查询中的变量存在编码问题。
* SITES-9224： GraphQL： GraphQLServlet中出现“Writer halreads honsed”异常。
* SITES-14800： GraphQL：使用变量的持久GraphQL查询中出现异常。
* SITES-15586： GraphQL：使用null值筛选持久查询时出现问题。
* SITES-15622： GraphQL：使用数字和布尔参数的持久查询存在问题。
* SITES-15654： GraphQL：同名的合并和属性存在问题。
* SITES-15267：启动项：促销活动不选取在修改启动项配置之前修改的启动页。
* SITES-15406：启动项：无法添加启动页面。
* SITES-15427：启动项：“提升当前页面和子页面”范围的行为不一致。
* SITES-15429：启动项：创作页面在提升启动项时被删除。
* SITES-15462：启动项：自动提升流程发布提升范围外的页面。
* SITES-15815：启动项：从启动项中删除页面导致启动项无法成功提升。
* SITES-15223：页面编辑器：在平板电脑大小模拟器中无法调整组件大小。
* sites-15463：页面模板：无法发布模板。

### 已知问题 {#known-issues-13665}

无

### 嵌套的技术 {#embedded-tech-13665}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
