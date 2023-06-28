---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 47%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 12441 {#release-12441}

下面总结了维护版本 12441 的持续改进，该版本已于 2023 年 6 月 27 日公开发布。此维护版本是对上一个维护版本 12255 的更新。

2023.7.0功能激活将提供此维护版本的完整功能集。 请参阅 [Experience Manager版本路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) 了解更多信息。

### 增强 {#enhancements-12441}

- SITES-8769：改进ResponsiveGrid中的StyleImpl调用

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

### 已知问题 {#known-issues-12441}

无。

### 嵌套的技术 {#embedded-tech-12441}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [Oak API 1.50.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| AEM SLING API | 版本 2.27.0 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
