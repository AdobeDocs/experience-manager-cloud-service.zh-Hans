---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b0198fee3fb8c2f02f50819bea5757e5b8373ac1
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 99%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15262 {#release-15262}

下面总结了维护版本 15262 的持续改进情况，该版本于 2024 年 3 月 6 日公开发布。上一个维护版本是版本 14697。

2024.3.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-15262}

* ASSETS-30632：在列表视图中添加了单独的 Brand Portal 发布状态列。
* ASSETS-30934：在资源元数据编辑器中添加了对 `Iptc4xmpCore:AltTextAccessibility` 和 `Iptc4xmpCore:ExtDescrAccessibility` 属性的支持。
* ASSETS-31297：改进检查，防止从动态媒体中删除复制的资源。
* ASSETS-33246：发布索引定义 `damAssetLucene-10`。
* ASSETS-33590：在处理配置文件中添加对视频的 webm 演绎版的支持。
* GRANITE-36205：将 oak 版本更新到 1.60-T20240131102219-0cde853。
* SITES-19326：更新 Assets UI 中的链接，即可在新的 CF 编辑器中打开 CF。
* GUIDES-12945：人工智能驱动的智能建议，可在创作内容时添加内容引用
* GUIDES-12706：改进了 Web 编辑器中的版本历史记录功能
* GUIDES-14948：改进了平移面板中的用户体验
* GUIDES-8782：改进了“插入元素”对话框中的搜索逻辑
* GUIDES-14681：能够发布具有动态基线的多个输出预设
* 有关 AEM Guides 增强功能的完整列表，请参阅：[AEM Guides 中的新增功能](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=zh-Hans#release-info)

### 修复的问题 {#fixed-issues-15262}

* ASSETS-15977：删除已弃用的 v1 搜索事件和管道生成器。
* ASSETS-18088：将 batik 库依赖项升级到 1.17。
* ASSETS-21965：元数据写回工作流必须仅在资源元数据更改时启动。
* ASSETS-26368：如果作业配置不存在，则不会移除计划的批量导入作业。
* ASSETS-26549：具有 &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; 的资源/节点在列表视图中显示为“外部用户”。
* ASSETS-26842：更新“Firefly”文本以在处理配置文件中读取“应用程序生成器”。
* ASSETS-28708：某些 IMS 标记请求的响应非常缓慢。
* ASSETS-28767：如果文件夹包含大量已发布的资源，则资源的发布状态不一致。
* ASSETS-29011：智能裁切对只读用户可见。
* ASSETS-29348：AssetMoveEventHandler 可能会消耗过多内存。
* ASSETS-29738：资源上传限制失败，woff 文件出现 NullPointerException。
* ASSETS-30068：批量导入资源要素，以包括“作业已完成，但存在错误”的状态 COMPLETED_WITH_ERROR。
* ASSETS-30261：发送到管道的资源事件的 imsUserId 不正确。
* ASSETS-30538：移动 PDF 文件后，“查看页面”选项丢失。
* ASSETS-30626：无法为 assetId 为空的资源创建投放请求。
* ASSETS-30756：当文件夹名称以“html”结尾时，移动资源向导操作失败。
* ASSETS-30810：在渲染旧版 YouTube 配置之前清理标记。
* ASSETS-31015：无法上传文件扩展名为 .msg 的资源。
* ASSETS-31038：通知服务接收到的任务事件未得到处理。
* ASSETS-31097：禁用 WCM 内容的异步复制以避免出现遍历查询警告。
* ASSETS-31256：具有 &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; 的资源/节点在列表视图中显示为“外部用户”。
* ASSETS-31260：当下拉 JSON 具有较大的列表时，资源元数据表单下拉字段无法正常工作。
* ASSETS-31280：将资源添加到收藏集时以扁平结构下载。
* ASSETS-31301：无法通过 Use API 以正确的方式对 `dynamicmedia_sly.js` 进行实例化。
* ASSETS-31330：ko_KR：字幕和音频轨道中存在未本地化的字符串。
* ASSETS-31405：对于大型 InDesign 版面，InDesign Server 处理失败。
* ASSETS-31570：Unified Shell - 资源详细信息“保存并关闭”、“取消”按钮需要按多次才起作用。
* ASSETS-31673：对大型 Dropbox 文件的批量导入失败。
* ASSETS-32108：AEM Assets 未在视图设置中保存用户定义的信息卡大小。
* ASSETS-32230：升级 com.adobe.aem.repoapi 捆绑包的最低运行时版本。
* ASSETS-32544：元数据导出作业间歇性失败。
* ASSETS-32679：资源 (PDF) 预览的缓存问题。
* ASSETS-32754：无法将任务分配给之前未登录的用户。
* ASSETS-32755：配置 com/adobe/cq/dam/assetmove 作业主题，以使用有序队列。
* ASSETS-32899：在收藏集中搜索时非常缓慢。
* ASSETS-33098：AEM Assets 搜索方面“标记谓词”无法按预期工作。
* ASSETS-33454：时间线中未出现查看任务活动和评论。
* ASSETS-34088：无法在 AEM Assets 中使用 PDF 预览功能。
* ASSETS-34155：动态媒体 - 更新了 AEM 查看器/2024.1.0。
* ASSETS-34684：处理内容树中的多值 dc:title。
* ASSETS-34789：修复文件名冲突检查中的标准化问题。
* DXML-13276：AEM Guides - 将索引集成到 GraniteContent 中并将其从库中移除。
* GRANITE-47995：由于与“cq:isDelivered”属性冲突，删除操作可能会失败。
* GRANITE-48079：启用 OAuth 在线标记验证的 POST 请求。
* GRANITE-48143：将 org.apache.sling.resourcemerger 升级到 1.4.4。
* GRANITE-49031：更新至 Jackson 2.16.1。
* SCRNS-3961：Screens - 序列渠道：淡入淡出过渡中使用的 Jquery 动画会导致黑屏。
* SITES-15868：提高列出片段的性能。
* SITES-16079： `/fragments/{id}/references` 开始返回重复项。
* SITES-16118：如果修补片段并且模型中缺少片段字段，则会引发异常。
* SITES-16121：检索模型日期字段会引发异常。
* SITES-16207：POST /adobe/sites/cf/models 操作返回两个不同的 OK 状态代码。
* SITES-17361：将 Jsoup 重新嵌入 sites-headless 捆绑包中。
* SITES-17768：GraphQL 为内容片段中引用的资源输出动态媒体 URL。
* SKYOPS-66622：运行启用 buildTransform 的管道后，作者部署崩溃循环。
* SKYOPS-69977：自适应图像 Servlet 在最新更新后不会加载图像。
* GUIDES-15045：编辑器中的拼写检查不允许选择建议。
* GUIDES-14968：全局导航按钮不起作用，仪表板无法加载。
* GUIDES-14943：在原生 PDF 发布中，条件预设中的自定义属性不适用于原生 PDF 发布。
* GUIDES-15085：在原生 PDF 发布中，未解决 2023 年 12 月版 Adobe Experience Manager Guides 的关键引用内容。
* GUIDES-13486：**基准筛选条件**&#x200B;文件无法在 Web 编辑器中使用“文件名”。
* 有关 AEM Guides 中已修复问题的完整列表，请参阅：[AEM Guides 修复的问题](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=zh-Hans#release-info)

### 已知问题 {#known-issues-15262}

* ASSETS-35923：将 `aem-sdk-api` 版本升级到 `2024.2.15262.20240224T002940Z-231200` 后 CM 管道生成步骤中出现 `UnsupportedClassVersionError`。**需要客户采取行动将 CM Java 版本设置为 11**，请参阅 [生成环境/设置 Maven JDK 版本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=zh-Hans#alternate-maven-jdk-version)
* ASSETS-35860：AEM Assets 列视图中的时区转化不正确。
* SCRNS-4171：升级到 15262 并发布渠道时，Windows Screens 变为空白并停止工作。
* GRANITE-50774：GraniteContent 应在初始化时使用属性值的确定性顺序。

### 更改通知 {#change-notice-15262}

**必需执行的操作**

#### 将 CM Java 版本设置为 11 {#set-java-version-11}

新版本的 aem-sdk-api 包含使用 Java 11 目标编译的类，该目标与 Cloud Manager 生成环境默认 JDK 版本 1.8 不兼容。此更新要求使用 JDK 11 执行 Maven。

建议客户将 `.cloudmanager/java-version` 文件添加到其 git 存储库的根目录中，其中的内容为：`11`。[生成环境/设置 Maven JDK 版本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=zh-Hans#alternate-maven-jdk-version)

#### 将 aem-cloud-testing-clients 更新到 1.2.1 {#update-aem-cloud-testing-clients}

即将发生的更改需要将您在自定义功能测试中使用的库 [aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients) 更新到至少 **1.2.1** 版本

确保您在 `it.tests/pom.xml` 中的依赖项已经升级。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

此更改需要在2024年4月6日之前执行。

如果未更新依赖项库，则会导致“自定义功能测试”步骤中的管道失败。

### 嵌套的技术 {#embedded-tech-15262}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
