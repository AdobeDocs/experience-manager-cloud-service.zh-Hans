---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: aa9629c3e48ca0bf4654351462a94777af9ed651
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 22%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 14029 {#release-14029}

以下总结了维护版本14029的不断改进，该版本于2023年10月25日公开发布。 此维护版本是对上一个维护版本 13804 的更新。

2023.11.0 功能激活将为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-14029}

* ASSETS-28551：提高“我的链接共享”UI的可扩展性
* ASSETS-28566：添加dam：metadataForm Lucene索引
* ASSETS-29281：更新RAPI以发送v2下载事件

### 修复的问题 {#fixed-issues-14029}

* ASSETS-25199：图像核心组件未显示正确的智能裁剪
* ASSETS-26142：如果发现请求失败或中断，则未设置或重新尝试unified-shell.js customEnvLabel
* ASSETS-26416：在搜索表单中，相对日期谓词始终定义为“1天前”
* ASSETS-27321：在团队成员身份更改时清除组缓存
* ASSETS-27591：修复对旧org.json的依赖关系
* 列入阻止列表 ASSETS-28439：如果未配置全局阻止列表，智能标记将NPE
* ASSETS-28612：“repository-api”中的BlockedTagResolver修复
* ASSETS-28634：Adobe库存中的Omnisearch字段未自动添加资产数据
* ASSETS-28727：处理配置文件配置列表不显示指定的自定义高度和宽度值
* ASSETS-29056：添加转码演绎版AEM标准处理配置文件
* ASSETS-29105：RDE功能模型中SecurityProviderRegistration requiredServicePids中缺少限制提供程序
* ASSETS-29106：在启用Unified Shell的AEM上查看Adobe库存时出现引发错误
* ASSETS-29115：删除限制提供程序路径的配置属性
* ASSETS-29208：在注册CompleteUploadAssetServlet服务之前，由于请求发送到创作面板而导致资源上传出错
* ASSETS-29297：创建带已签出筛选条件的保存搜索选项时出现问题
* ASSETS-29363：元数据配置文件未应用IPTC的默认值
* ASSETS-29404：链接共享报表达到查询限制
* ASSETS-29431：删除旧的功能标记
* ASSETS-29443：当Granite Shell标头模式更改为“选择”时，Unified Shell主页保持可见和可单击状态
* ASSETS-29476： scene7DAMService.getS7FileReference(asset) Api调用未返回预期值。
* ASSETS-29515：具有“jcr：lastModifiedBy”的资源/节点：“workflow-process-service”在列表视图中显示为“外部用户”
* ASSETS-29579：非管理员用户无法创建图像集
* ASSETS-29631：使用dam：roles进行安全交付/搜索
* ASSETS-29689：dc：roles（以及新属性dam：roles）应从AEM端筛选
* ASSETS-29738：资产上传限制失败，出现NullPointerException
* ASSETS-29779：无法将小型资产处理到Web页，因为不在Blob存储中
* ASSETS-29892：对包含大量资产的文件夹导出元数据失败
* ASSETS-29996：仅在PROD实例上间歇性上传资产时，将“外部用户”作为修饰符
* ASSETS-30167：上传资源后，adobe_dam：restrictions的HTML中断
* ASSETS-30276：共享链接UI：无法从资源详细信息共享
* ASSETS-30434：资产处理已完成事件未发送到管道
* ASSETS-30519：将RAPI添加到REDMetricsServletFilter
* CQ-4354413： QueryBuilder：含方括号的查询被错误转换为xpath
* CQ-4354834：无法在收件箱任务中添加评论
* CQ-4354836：无法从项目控制台启动工作流或创建任务
* CQ-4354867： ToggleCondition引用了InstanceActionServlet中不存在的字段
* CQ-4354895：AEM翻译包：10月12日
* GRANITE-45560：事件信封中的通用模式表示形式
* GRANITE-47267：更新至Apache Felix Http Jetty 4.2.18
* GRANITE-47599：内容导入自13323升级以来失败(JCRVLT-721)
* GRANITE-47873：Apache Felix Webconsole 4.9.6的更新

### 已知问题 {#known-issues-14029}

* CQ-4354836：无法从项目控制台启动工作流或创建任务。
* CQ-4354834 ：用户无法在收件箱任务中添加评论。

### 嵌套的技术 {#embedded-tech-14029}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
