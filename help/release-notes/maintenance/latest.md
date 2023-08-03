---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: acaed9eed20e8134574fd326e23ac68130ac019b
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 14%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 12874 {#release-12874}

以下总结了维护版本12874的不断改进，该版本于2023年8月2日公开发布。 此维护版本是对上一个维护版本 12790 的更新。

激活 2023.8.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

### 增强 {#enhancements-12874}

- 索引定义的新版本： `/oak:index/damAssetLucene-9`
- ASSETS-18351：切换到不安全的Facet — 提高搜索性能
- ASSETS-17896：从索引 — 基于智能标记的相似性搜索中删除特征向量
- ASSETS-8715：为属性“jcr：content/metadata/dam：status”添加null检查/非null检查
- GRANITE-45138：从预测的标记动态提升属性中删除属性索引
- ASSETS-17614：将Scene7 ID添加为索引属性（启用null检查和不启用null检查）
- ASSETS-14516：将“新UI”垃圾桶功能的属性添加到索引中
- ASSETS-16270：将合并的标题属性添加到索引（用于排序）
- ASSETS-24478：从索引中删除5个可能较大的属性（基于对客户索引数据的分析）
- ASSETS-3383：添加了一个额外的标记“assetsOmnisearch”

AEM版本12874及更高版本包含新版本的damAssetLucene索引(damAssetLucene-9)。 为了提供最快速的搜索体验，damAssetLucene-9更改了Oak查询结果彩块化的行为，不再评估对基础搜索索引返回彩块化的访问控制（称为“不安全”模式）。

因此，可能会向用户显示方面计数值，其中包括当前用户无权访问的资产。 这不允许用户访问、下载或读取这些资源，也不允许用户获取有关资源存在的任何进一步信息。

如果需要以前的行为，客户应执行中所述的步骤 [内容搜索和索引](/help/operations/indexing.md) 要使用之前的“统计”彩块化模式创建damAssetLucene-9索引的自定义版本。

### 修复的问题 {#fixed-issues-12874}

- ASSETS-24379：对ReplicateOnModifyListener进行了改进。
- ASSETS-25794：解决了S7ConfigResolverImpl的一个问题，该问题导致它在启动时执行开销巨大的查询。
- ASSETS-25473：修复了没有复制权限的用户能够查看快速发布选项的错误。
- ASSETS-24803：解决了查看器功能中的XSS漏洞。
- ASSETS-25489：更正了下载带有错误后缀的智能裁剪的问题。
- ASSETS-25435：修复了下载动态呈现版本时缺少WidthxHeight字段的错误
- ASSETS-25741：修复了缺少可视星号(`*`)符号，表示“基本”选项卡部分中的必填“宽度”编辑字段。
- ASSETS-25759：提高了高对比度黑白模式下下拉列表元素焦点的可见性。
- ASSETS-25749：修复了在使用键盘选项卡进行导航时，焦点未移动到视频下方的多个控件，从而导致无法访问这些控件的问题。
- ASSETS-26074：恢复了非视频资源名称127个字符的限制。
- ASSETS-21428：修复了元数据架构编辑器中的多行字段与以下字段重叠的问题
- ASSETS-21989：修复了302和401响应上可能覆盖CORS标头，从而阻止远程DAM登录的问题
- ASSETS-22603：修复了在查看资产下载报表时影响列名称和值的问题
- ASSETS-23120：修复了AssetSetLastModifiedProcess中与泄露资源解析程序相关的问题
- ASSETS-24938：修复了导致资产文件夹属性对话框的保存按钮行为类似于保存+关闭的问题
- ASSETS-25456：修复了名称较长的资产导致无法在资产属性编辑器中单击操作的问题
- ASSETS-25832：修复了将完全访问文件夹中的资产关联到只读访问文件夹的问题。
- ASSETS-25397：修复了在新UI中重命名的资产的新名称未反映在搜索结果中的问题
- ASSETS-26102：修复了可能阻止从CI中心连接器上传的问题
- ASSETS-26172：减小保存在持久Sling作业节点中的批量导入进度日志内容的大小
- ASSETS-26292：Java API中已弃用AssetManager createOrUpdateAsset()和createOrReplaceAsset()方法
- ASSETS-26399：修复了阻止将收藏集发布到Brand Portal的问题
- ASSETS-26533：修复了Indesign服务器集成中的一个问题，该问题可能导致长时间处理请求超时
- ASSETS-26549：修复了Assets列表视图中存在的一个问题，该问题会导致“外部用户”显示为所有上传资源的最后一个修改用户
- ASSETS-26551：解决了未在创作实例上删除的资产未取消发布的问题
- ASSETS-26571：修复了Assets Reports页面的一个问题，该问题导致当列表中存在多个失败的报表作业时，页面加载失败
- ASSETS-26147：修复了在设置window.top.opener但未设置window.opener时，Unified Shell会尝试将iframe重定向到/ui的问题
- ASSETS-26576：修复了Dropbox导入的问题，该问题导致创建了错误的文件夹层次结构
- ASSETS-26671：修复了批量导入操作无法包含位于DCIM文件夹中的文件的问题
- ASSETS-26700：修复了在保存公共文件夹的属性页面而不做更改时会创建3个不必要组的问题
- CQ-4353449：修复了允许具有只读标记权限的用户使用标记UI创建标记的问题
- GRANITE-46601：修复了导致快速入门SDK无法在JDK 11.0.20上启动的问题
- SKYOPS-33168：修复了CM开发人员控制台中存在的一个问题，该问题会阻止为不带扩展名的资产名称加载/content/dam
- SKYOPS-61484：修复了RDEProvider服务中允许未替换的${sling.home}令牌在合并的OSGi配置中持续存在的问题
- 各种安全性、可访问性和本地化修复

### 已知问题 {#known-issues-12874}

- GRANITE-46851：内容分发中的测试连接不起作用

### 嵌套的技术 {#embedded-tech-12874}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 版本 2.23.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
