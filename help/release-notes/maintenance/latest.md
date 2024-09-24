---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f728db32f77c58d47f52373987ed9bc83f22fdba
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 17%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17882 {#release-17882}

以下总结了维护版本17882的不断改进，该版本于2024年9月24日公开发布。 上一个维护版本是版本 17689。

2024.10.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17882}

* Assets - 37750： [优先级4] [GraphQL]支持DM scene7 URL：图像智能裁剪。
* CQ - 4354583： [AEMaaCS]通过Adobe管道发送翻译流程事件。
* CQ - 4357642：更新OOTB连接器中的MSFT凭据。
* CQ - 4358217：从请求实体反序列化请求正文。
* CQ - 4358342：仅在一个HTTP方法上注册RequestProcessors。
* Forms - 10781：增强规则编辑器，为面板中的下一个/上一个项目创建规则。
* Forms - 14595：当使用预填充数据计算无浏览器渲染的DoR时，DoR中缺少[无浏览器功能]值。
* Forms - 15619： AEM Forms更新了翻译工具包。
* Forms - 16113： [Adobe Sign]无法由其他用户更新协议状态。
* Forms - 16155： [规则编辑器]实现异步函数。
* GRANITE - 53872：为IMS客户端ID添加新的环境变量。
* SITES - 23738：发行核心组件2.27.0。
* 站点 — 16610：内容片段：获取启动项详细信息端点。
* SITES - 16614：内容片段：重新构建Launch端点。
* 站点 — 16615：内容片段：提升启动项端点。
* 站点 — 24215：内容片段：实施获取启动项源端点。
* 站点 — 20336：内容片段：改进删除内容片段模型时的验证。
* SITES - 21090：内容片段：添加对数字字段的小数最小值/最大值支持
* 站点 — 21658：内容片段：升级以使用UUID引用。
* 站点 — 23054：内容片段：复制内容片段模型。
* 站点 — 23264：内容片段：创建模型的静态架构。
* SITES - 23265：内容片段：通过UI架构GET端点公开模型的静态架构。
* 站点 — 23266：内容片段：能够向内容片段模型添加约束。
* 站点 — 23778：内容片段：搜索内容片段模型应允许搜索从未发布的模型。
* 站点 — 23335：内容片段：添加对外部资产引用的支持。
* 站点 — 24626：内容片段：RTC：UUID迁移的权限：2。
* 站点 — 24786：内容片段： `referencesTree`端点的增强功能。
* 站点 — 24833：内容片段：根据允许的HTML标签列表删除HTML输入的验证。
* 站点 — 23380：GraphQL：使用适当的API读取资源元数据。
* SITES - 22864： [Edge Delivery]通用编辑器与新的AEM内容结构集成H2 2024。
* SITES - 23584：基础组件测试在Java 17上失败。
* SITES - 23662：事件：无法从服务器日志中的JCR日志语句中提取触发发布请求的用户。
* 站点 — 23301：添加对启动新工作流的支持，以便在创建内容片段的翻译时创建文件夹结构。
* SITES - 23336：内容片段：添加对外部资产引用的支持
* 站点 — 24091：MSM内容包拆分：母版。
* SITES - 24114： isSourceRenderCondition：将错误日志消息减少为DEBUG。
* SITES - 24166：触屏UI编辑器的远程资产减轻。
* SITES - 24409：仅在一个HTTP方法上注册所有请求处理器。
* SITES - 25008：改进对PersistenceExceptions和权限问题的处理。
* SITES - 24821： [Xwalk]将aem.page / aem.live设为默认值。

### 修复的问题 {#fixed-issues-17882}

* CQ - 4356887：Akamai Technologies Inc.的翻译项目状态不一致
* CQ - 4357878：翻译框架在供应商失败翻译时未设置错误状态。
* CQ - 4358028：如果上传了缩略图，则无法创建项目。
* CQ - 4358290：目标设置不适用于已发布的页面。
* Forms - 13173：自适应表单>规则编辑器>放置对象字段中的下拉列表未对齐。
* Forms - 13873：组件名称中的AFv2： (“ — ”)导致规则失败。
* Forms - 14340：实例化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter时出错。
* Forms - 15363：规则编辑器中的显示名称。
* Forms - 15381：对授权范围消息进行UI增强。
* Forms - 15595： AEM表单TnC组件同意文本换行符问题。
* Forms - 15623： AEMaaCS Forms — 使用一个POST更新Dynamics中的多个表的替代方法。
* Forms - 15682： AEM Forms — 无法将DOR绑定到Dynamics FDM。
* Forms - 15799： Adobe Sign GovCloud签名页面不会在iframe中渲染。
* Forms - 15835：提交表单后URL重写问题。
* Forms - 16091：使用重新构建的Binary.java。
* Forms - 16096： Forms用户无权访问restendpoint对话框。
* Forms - 16139：在核心组件表单中为DoR添加所需的日志记录。
* Forms - 6935：活动组件的状态缺少3对1的对比度。
* Forms - 7018：空元素接收焦点。
* GRANITE - 53028： ExternalProcessPollingHandler中的NPE。
* GRANITE - 53907：无法将服务用户标识为工作流超级用户。
* 站点 — 24405：内容片段：枚举的扩展信息应更具弹性
* 站点 — 23024：内容片段：枚举未返回locked： true (在GET片段中)。
* 站点 — 23269：内容片段：创建内容片段允许设置锁定字段。
* SITES - 23337：内容片段：具有`body`的批处理终结点失败，并出现铸造异常。
* 站点 — 23474：内容片段：分页应在搜索内容片段中排除损坏的资源。
* 站点 — 23615：内容片段：内容片段副本AuthoringInfo未更新
* SITES - 23668：内容片段：修补包含多字段的Live Copy失败，返回400
* 站点 — 23695：内容片段：选项卡描述在UiSchema中不可用
* SITES - 23704：内容片段： _extendedInfo不支持多值枚举
* SITES - 23781：内容片段：枚举字段中不允许存在重复值
* 站点 — 24150：内容片段：缺少有关创建的内容片段版本创作数据
* SITES - 24230：内容片段：修复了搜索内容片段模型中`modified`复制状态后的筛选问题
* 站点 — 24233：内容片段：按`publishedBy`筛选可在搜索内容片段模型中包含未发布的资源
* SITES - 24355：内容片段：未对创建的内容片段的文件夹应用实时关系
* SITES - 24816：内容片段：ValidationStatus消息顺序不一致。
* SITES - 23896：事件：更多事件与“页面移动”事件相关联
* SITES - 23899：事件：页面事件延迟或根本未生成
* SITES - 23961：事件：当存在配置文件夹时，创建包含引用的内容片段模型失败
* SITES - 23963：事件：删除页面的事件有时不会出现
* SITES - 23443： GraphQL： GraphQL光标查询不一致行为。
* SITES - 10994：键盘焦点顺序不符合逻辑。
* SITES - 16357：在“站点”菜单的“设置Analytics”选项卡中，AEM：按钮被截断。
* SITES - 19836：容器中的Ghost组件显示在发布和预览实例上。
* 站点 — 22348：如果某个项目的活动副本超过100个，则Live Copy概述页面加载失败。
* SITES - 22960： ContentFragmentModelOmniSearchHandler中的资源解析程序未关闭。
* SITES - 23284：URL编码导致空白路径浏览器对话框。
* 站点 — 23505：将页面移动到其他位置时，组件显示错误的URL。
* 站点 — 23574：无法预览/比较许多页面的当前版本
* SITES - 23585：恢复具有cq：responsive节点的组件的继承时出现问题
* SITES - 23650：AEM创作环境中传入链接计数的差异
* SITES - 23659：切换导致的内容语言Servlet回归FT_* SITES - 9757
* 站点 — 23759：在体验片段中添加的Assets未随启动项一起发布
* SITES - 24025：AEM中的302重定向返回使用内部DNS而不是公共DNS的位置标头
* SITES - 24036：调查ASCII格式的AEM RTE持久字符
* SITES - 24317：代理配置不适用于基本身份验证
* SITES - 24918： [Xwalk]修复了在使用专用ip出口时偶尔返回的504错误。
* SITES - 2864：辅助功能 — 无法使用键盘拖放功能。

### 已知问题 {#known-issues-17882}

* Forms - 15818：在服务器日志中未找到组件描述符条目`OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml`的语句。 这些是无害的日志语句。

### 已弃用的功能和 API {#deprecated-17882}

请注意，我们正在更新 `com.day.cq.wcm.api`，并且在当前版本中，我们已将其中的一些方法和类标记为 `@Deprecated`。这些将在未来的版本中删除，所以如果您正在使用其中任何一个，请考虑切换到其建议的替代方案。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-17882}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 16 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-17882}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
