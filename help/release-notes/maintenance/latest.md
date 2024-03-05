---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 77a4b445d9117959ed8855aef445c02529178800
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 11%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15262 {#release-15262}

以下总结了维护版本15262的持续改进，该版本于2024年3月5日公开发布。 上一个维护版本是版本 14697。

2024.3.0 功能激活将为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-15262}

* ASSETS-30632：在列表视图中添加了单独的Brand Portal发布状态列。
* ASSETS-30934：添加了对 `Iptc4xmpCore:AltTextAccessibility` 和 `Iptc4xmpCore:ExtDescrAccessibility` 属性到资产元数据编辑器中。
* ASSETS-31297：改进检查以防止从Dynamic Media中删除复制的资产。
* ASSETS-33246：发布索引定义 `damAssetLucene-10`.
* ASSETS-33590：在处理配置文件中添加了对视频的Web呈现版本的支持。
* GRANITE-36205：将Oak版本更新为1.60-T20240131102219-0cde853。
* SITES-19326：更新资产UI中的链接以在新的CF编辑器中打开CF。
* GUIDES-12945：AI支持的智能建议，用于在创作内容时添加内容引用
* GUIDES-12706：Web编辑器中版本历史记录功能的改版
* GUIDES-14948：改善了翻译面板中的用户体验
* GUIDES-8782：改进了“插入元素”对话框中的搜索逻辑
* GUIDES-14681：能够使用动态基线发布多个输出预设
* 有关AEM Guides中增强功能的完整列表，请参阅： [AEM Guides的新增功能](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### 修复的问题 {#fixed-issues-15262}

* ASSETS-15977：删除已弃用的v1搜索事件和管道生成器。
* ASSETS-18088：将batik库依赖项升级到1.17。
* ASSETS-21965：元数据写回工作流必须仅在资产元数据更改时启动。
* ASSETS-26368：如果作业配置不存在，则未删除计划的批量导入作业。
* ASSETS-26549：具有“jcr：lastModifiedBy”的资源/节点：“workflow-process-service”在列表视图中显示为“外部用户”。
* ASSETS-26842：在处理配置文件中将“Firefly”文本更新为“App Builder”。
* ASSETS-28708：某些IMS令牌请求的响应非常慢。
* ASSETS-28767：如果文件夹包含大号，则资产的发布状态不一致。 已发布的资源。
* ASSETS-29011：智能裁剪对只读用户可见。
* ASSETS-29348： AssetMoveEventHandler可能会占用太多内存。
* ASSETS-29738：对于wff文件，资源上传限制失败并出现NullPointerException。
* ASSETS-30068：批量导入Asset Essentials以包含“作业已完成，但出现错误”的状态COMPLETED_WITH_ERROR。
* ASSETS-30261：发送到管道的资源事件的imsUserId不正确。
* ASSETS-30538：移动PDF文件后缺少查看页面选项。
* ASSETS-30626：无法创建为assetId为空的资产报告的投放请求。
* ASSETS-30756：当文件夹名称以“html”结尾时，移动资产向导操作失败。
* ASSETS-30810：在呈现旧版Youtube配置之前清理标记。
* ASSETS-31015：无法上传文件扩展名为.msg的资源。
* ASSETS-31038：未处理通知服务收到的任务事件。
* ASSETS-31097：禁用WCM内容的异步复制，以避免遍历查询警告。
* ASSETS-31256：具有“jcr：lastModifiedBy”的资源/节点：“workflow-process-service”在列表视图中显示为“外部用户”。
* ASSETS-31260：当下拉列表JSON包含大列表时，资产元数据表单下拉字段无法正常工作。
* ASSETS-31280：在将资源添加到收藏集时，使其以拼合的结构下载。
* ASSETS-31301： `dynamicmedia_sly.js` 无法通过Use API正确实例化。
* ASSETS-31330：ko_KR：字幕和音轨中的未本地化字符串。
* ASSETS-31405：对大型InDesign布局进行InDesign服务器处理失败。
* ASSETS-31570：Unified Shell — 需要多次按资产详细信息“保存并关闭”、“取消”按钮才能正常工作。
* ASSETS-31673：大型Dropbox文件的批量导入失败。
* ASSETS-32108： AEM Assets未在“视图”设置中保存用户定义的卡片大小。
* ASSETS-32230：升级com.adobe.aem.repoapi包的最低运行时版本。
* ASSETS-32544：元数据导出作业间歇性失败。
* ASSETS-32679：资源(PDF)预览存在缓存问题。
* ASSETS-32754：任务无法分配给之前未登录的用户。
* ASSETS-32755：配置com/adobe/cq/dam/assetmove作业主题以使用有序队列。
* ASSETS-32899：在收藏集中搜索非常慢。
* ASSETS-33098：AEM Assets搜索Facet“标记谓词”无法按预期使用。
* ASSETS-33454：审阅任务活动和时间轴中未显示的注释。
* ASSETS-34088：PDF预览在AEM Assets上不起作用。
* ASSETS-34155： Dynamic Media — 更新了AEM查看器/2024.1.0。
* ASSETS-34684：在内容树中处理多值dc：title。
* ASSETS-34789：修复文件名冲突检查中的规范化问题。
* DXML-13276： AEM Guides — 集成GraniteContent中的索引并将其从库中移除。
* GRANITE-47995：由于与“cq：isDelivered”属性冲突，删除操作可能会失败。
* GRANITE-48079：为OAuth联机令牌验证启用POST请求。
* GRANITE-48143：将org.apache.sling.resourcemerger升级到1.4.4 。
* GRANITE-49031：更新到Jackson 2.16.1。
* SCRNS-3961： Screens — 序列渠道：渐隐过渡中使用的Jquery动画可导致黑屏。
* SITES-15868：提高列表片段的性能。
* SITES-16079： `/fragments/{id}/references` 已开始返回重复项。
* SITES-16118：如果修补了片段并且模型中缺少片段字段，则会引发异常。
* SITES-16121：检索模型日期字段会引发异常。
* SITES-16207：POST/adobe/sites/cf/models操作返回两个不同的OK状态代码。
* SITES-17361：将Jsoup重新嵌入到sites-headless包中。
* SITES-17768：GraphQL可输出内容片段中引用资源的Dynamic Media URL。
* SKYOPS-66622：运行启用了buildTransform的管道后，创作部署崩溃循环。
* SKYOPS-69977：自适应图像Servlet在最新更新后不加载图像。
* GUIDES-15045：编辑器中的拼写检查不允许选择建议。
* GUIDES-14968：全局导航按钮不起作用，无法加载仪表板。
* GUIDES-14943：在本机PDF发布中，条件预设中的自定义属性不适用于本机PDF发布。
* GUIDES-15085：在本机PDF发布中，无法解析2023年12月版的Adobe Experience Manager Guides的关键参考。
* GUIDES-13486： **基线筛选器** 文件无法在Web编辑器中使用文件名。
* 有关AEM Guides中修复的问题的完整列表，请参阅： [AEM Guides已修复问题](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### 已知问题 {#known-issues-15262}

无。

### 变更通知 {#change-notice-15262}

**需要操作**

即将进行的更改需要库 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 用于自定义功能测试，将至少更新为版本 **1.2.1**

确保您在中依赖项 `it.tests/pom.xml` 已更新。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

2024年4月6日之后需要此更改。

如果未更新依赖关系库，将导致“自定义功能测试”步骤中的管道失败。

### 嵌套的技术 {#embedded-tech-15262}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
