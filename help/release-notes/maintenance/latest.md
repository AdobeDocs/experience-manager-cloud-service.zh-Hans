---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1a128e35be06d018ec25fb0e6a479cfd0d242dbd
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 14%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 14227 {#release-14227}

以下总结了维护版本14227的不断改进，该版本于2023年11月9日公开发布。 此维护版本是对上一个维护版本 14029 的更新。维护版本 14227 取代了 14157，并纠正了一个问题。

2023.11.0 功能激活将为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-14227}

<!--* ASSETS-29631: Assets Cloud: Use dam:roles for secure delivery/search.-->
* CQ-4354515：翻译：用于禁止翻译引用的资源的选项。
* Forms-9993：定义将Forms核心组件移入Skyline的步骤。
* Forms-10570：将EC API载入API — 第一台路由器。
* GRANITE-48143：将Sling ResourceMerger升级到1.4.4。
* SITES-14874：事件：展开模型事件的CFM树以包含元数据更改。
* SITES-2719：内容片段：对内容片段变体的标记支持（重新启用）。
* SITES-3619：内容片段：以JSON输出的GraphQL CF变体标记，并按变体标记筛选（重新启用）。
* SITES-13750：内容片段：删除内容片段模型的标记。
* SITES-13920：内容片段：支持为多个字段配置minItems（预发布）。
* SITES-14080：内容片段：删除内容片段变量的标记。
* SITES-14770：内容片段：片段变量应包含fieldTags属性。
* SITES-15356：内容片段：在创建资源时作为响应标头返回etag。
* SITES-15357：内容片段：允许发布不带其引用的片段。
* sites-15938：内容片段：缺少内容引用元数据。
* SITES-16078：内容片段：在获取片段时，填写变量的验证结果属性。
* SITES-16545：内容片段：添加端点以检索内容片段变体的引用。
* SITES-16853：内容片段：删除/adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags端点。

### 修复的问题 {#fixed-issues-14227}

* 修复了各种辅助功能问题
* ASSETS-31015：无法将文件上传到文件扩展名未知的资源。
* ASSETS-24739：在发布时禁用Frame.io自定义操作端点。
* CMGR-49845：内容回流：确定给定检查点的正确根路径时出现问题。
* CMGR-49709：内容回流：更新属性筛选器以忽略其他属性。
* CQ-4354503：随机删除了Adobe IMS配置。
* CQ-4354414： ConfigurationReplicationEventHandler创建大量单独的刷新操作。
* CQ-4354401：翻译：在开始资产处理之前，必须保存由项目创建的资产。
* CQ-4354430：翻译：将不属于语言文件夹结构的资产添加到翻译项目时出错。
* CQ-4354412：翻译：删除翻译作业内容未删除所有引用的内容。
* CQ-4354636：翻译：在语言根级别创建语言副本不会调整页面中的路径。
* CQ-4354700：工作流：工作流有效负载屏幕未加载。
* CQ-4354834：工作流：无法在工作流收件箱任务中添加评论。
* Forms-11302：在RTE中编辑的组件标题在自适应表单编辑器>规则编辑器中显示不正确。
* GRANITE-45706：如果键值具有“Äú)”Äu，则i18n导入失败。
* SITES-14156：事件：并不总是发送发布事件。
* SITES-14520：GraphQL：由于FT_SITES-2719，导致分页的graphql查询性能不佳。
* SITES-16444： GraphQL：GraphQL查询中缺少相同名称字段的DataFetchingException。
* SITES-16225： GraphQL：Java API返回的模型和片段RTE字段的内容类型不正确。
* SITES-15373：内容片段： /adobe/sites/cf/fragments/{fragmentId}/variation/{name}/tags端点未使用正确的资源命名约定。
* SITES-15709：内容片段：创建布尔字段时创建模型端点问题。
* SITES-15727：内容片段：“标记”类型的字段在模型编辑器中只能添加一次。
* SITES-15782：内容片段：枚举类型的字段模型中缺少唯一属性。
* SITES-15786：内容片段：无法在包含&#39;的文件夹中创建内容片段。
* SITES-15790：内容片段：更新版本创建的位置标头。
* SITES-15923：内容片段：CF管理员不显示所有文件夹。
* SITES-15987：内容片段：创建变量时得到500。
* SITES-16067：内容片段：无法修改长文本片段字段的mime类型。
* SITES-16074：内容片段：非字符串的标记字段[]无法从 JCR 进行检索。
* SITES-16079：内容片段： /fragments/{id}/references已开始返回重复项。
* SITES-16118：内容片段：如果修补了片段并且模型中缺少片段字段，则会引发异常。
* SITES-16119：内容片段：如果片段元数据包含无法识别的字段，则会引发异常。
* SITES-16121：内容片段：检索模型日期字段会引发异常。
* SITES-16123：内容片段：如果资源不是内容片段，则获取片段端点会引发异常。
* SITES-16208：内容片段： ContentFragmentModelIdentifier公开误导性的标题属性。
* SITES-16707：内容片段：无法正确读取内容片段模型数据类型。
* SITES-16818：内容片段：仅在存在标记时执行删除。
* SITES-16207：内容片段：POST/adobe/sites/cf/models操作返回两个不同的OK状态代码。
* SITES-15616：内容片段：发布端点有时不发布内容片段的所有引用。
* SITES-16027：内容片段：片段响应中缺少变量引用信息。
* SITES-16243：内容片段：查找和替换不适用于呈现为：多个的字段。
* SITES-16250：内容片段：为CF打补丁有时会返回不正确的etag标头。
* SITES-16686：内容片段：当父引用达到最大深度时，将序列化内容片段非片段引用。
* SITES-12880：快速跟踪：修复“站点”>“设置分析”的本地化。
* SITES-16103：体验片段：由于控制台错误，Target选项不会显示在Cloud Service下方。
* SITES-16001： MSM：可在创建Live Copy时从转出配置中排除多字段组件。
* SITES-16559： MSM：在体验片段的转出过程中删除了转出配置。
* SITES-16797： MSM：修复了在编辑器中重新启用CF字段的继承的问题。
* SITES-16273：页面编辑器：在aem sites页面中从剪贴板复制粘贴出错。
* SITES-16126：站点管理员：在SITES-10288之后，非管理员用户的创作性能缓慢。
* Forms-10534：选择布尔操作数选项时，规则编辑器中出现错误。
* Forms-10248：在自适应表单中，当数据值的类型为Boolean时，规则无法正确设置单选按钮或复选框组件的值。
* Forms-11361：下拉组件自动默认为从列表中选择第一个选项。
* Forms-11413：自适应Forms会触发与Forms Portal预填充服务相关的错误，即使该服务未在使用中也是如此。
* Forms-11433：当自适应表单中包含非表单组件时，提交过程将无法完成。
* Forms-11206：当用户尝试计划自适应表单的发布工作流时，该工作流无法按预期运行。
* Forms-11546： Lighthouse检测到自适应表单中重复面板缺少ARIA标签，影响辅助功能。
* Forms-11095：对电话号码、电子邮件地址和数字字段的ARIA属性定义不正确，导致出现辅助功能问题。

### 已知问题 {#known-issues-14227}

无。

### 嵌套的技术 {#embedded-tech-14227}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
