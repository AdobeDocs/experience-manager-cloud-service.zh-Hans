---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e8ea040ba3f8c73d7ed64c9669ac1d0a22d3a3c8
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 23%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 12441 {#release-12441}

下面总结了维护版本 12441 的持续改进，该版本已于 2023 年 6 月 27 日公开发布。此维护版本是对上一个维护版本 12255 的更新。

2023.7.0功能激活将提供此维护版本的完整功能集。 请参阅 [Experience Manager版本路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 了解更多信息。

### 增强 {#enhancements-12441}

- SITES-8769：改进ResponsiveGrid中的StyleImpl调用
- Forms-5054：增加了对所有 [雕像](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) 受Adobe Sign支持。

### 修复的问题 {#fixed-issues-12441}

- 各种与辅助功能相关的更新
- SITES-12688：页面编辑器：逻辑运算符或无法在资产查找器搜索中正常工作
- SITES-4951：页面编辑器：页面编辑器中的标记搜索未找到子标记
- SITES-12465：体验片段：箭头键在体验片段组件对话框中不起作用
- SITES-12893：体验片段：对体验片段应用循环引用验证
- SITES-12715：体验片段：应用于体验片段文件夹的云服务配置不持久
- SITES-13097：体验片段：无法将体验片段添加到翻译项目
- SITES-13165： GraphQL：恢复用于筛选空值的默认行为
- SITES-12577：链接检查器：转换器不会间歇性地重写链接
- SITES-13559：转出组件时引发“不可修改”异常
- SITES-11757： MSM：从父项继承转出配置不会为子页面恢复配置
- SITES-14073：站点管理员：选择要导出的属性时，CSV报表失败，返回500
- Forms-7648：无法验证数字框组件中的最大位数。 验证脚本不起作用。
- Forms-8177：当Forms服务处于活动状态时， `com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Failed to retrieve asset dependencies` 遇到错误。
- Forms-8300：当用户尝试在打开任务后委派任务时，委派响应会重新加载任务，而不是打开用户的AEM收件箱UI。
- Forms-8500：在启用了IE模式选项的Microsoft® Edge浏览器上，HTML5 Forms无法打开。
- Forms-8541：渲染自适应Forms时，发生空指针异常。
- Forms-8964：在Google Chrome或Mozilla Firefox的Android™设备上打开表单时，无法删除在文本框组件中输入的文本。
- Forms-9026：当用户基于复杂且有效的JSON架构创建自适应表单时，将相关的JSON架构字段拖到自适应Forms编辑器以创建自适应Forms字段，并刷新自适应Forms编辑器窗口，所有字段都将被删除并且自适应Forms编辑器显示为空白。
- Forms-9263：当复选框选项的显示文本包含特殊字符时，用户无法选中此类复选框。
- Forms-8668：呈现表单的“PDF预览”时，错误日志中会显示一些不需要的Java™栈栈转储。 但是，渲染表单时没有问题。
- Forms-8116：将规则应用于自适应Forms容器组件时，未保存应用的规则。
- Forms-7906：将自适应表单添加到AEM Sites容器组件时，无法打开规则编辑器。
- Forms-8846： Bind引用属性不适用于自适应Forms附件组件。
- Forms-9072：在创建表单片段时搜索方案时，搜索结果不会返回任何方案以供选择。
- Forms：修复了多个与辅助功能相关的错误，以提高AEM Forms功能的辅助功能。

### 已知问题 {#known-issues-12441}

无。

### 嵌套的技术 {#embedded-tech-12441}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
