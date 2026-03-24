---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 0595cb45f39142e19721abedeedc8525579398a7
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 12%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 24678 {#24678}

以下总结了维护版本24678的持续改进，该版本于2026年3月4日公开发布。 上一个维护版本是版本 24464。

2026.3.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>发行说24893已设为私有。

### 增强功能 {#enhancements-24678}

* Forms-18927：在AEM Forms文件附件组件中添加了对自定义MIME类型和文件扩展名的支持，使用户能够附加更多种类的文档类型。
* Forms-18211、FORMS-22936：用户遇到辅助功能问题，在`<fieldset>`元素中，复选框未正确分组，并且组标签未作为第一个子项嵌套在`<legend>`中。 这会影响依赖屏幕阅读器进行导航的残障用户。 基于核心组件的自适应Forms现在引入了字段集和图例支持，以提供更好的无障碍支持。
在面板中添加了“字段集”选项，通过该选项，用户可在表单中更有效地组织和分组相关字段。
* Forms-23880：在核心组件中添加了主题编辑器支持。 此增强功能使用户能够更有效地自定义和管理核心组件中的主题，从而提高其设计灵活性和工作流程。
* Forms-21772：添加了对Forms管理UI的版本控制支持。 此增强功能使用户能够创建和检索基于核心组件和基于基础组件的自适应Forms、表单片段、主题和二进制Assets的版本，从而改善资源管理和版本控制。
* Forms-23094：为基于基础组件的自适应Forms添加了客户端解析，使企业客户能够将其表单迁移到云。 此增强功能支持代码编辑器规则中的EcmaScript功能（以前不支持这些功能），从而帮助实现更平稳的迁移过程。
* Forms-23853：添加了对覆盖sling组件中的reCAPTCHA的支持。 此增强功能使用户能够自定义reCAPTCHA设置，从而提高企业客户的灵活性和安全性。
* SITES-34936：带有通用编辑器的Edge Delivery：按模型添加筛选内容片段以进行发布。
* SITES-36203：带有通用编辑器的Edge Delivery：添加代码切换开关以启用多字段和复合多字段支持。
* SITES-37037：使用通用编辑器的Edge Delivery：改进电子表格导入以自动检测分隔符。
* SITES-37804：带有通用编辑器的Edge Delivery：添加对封闭用户组创作（提前访问）的支持。
* SITES-38990：带有通用编辑器的Edge Delivery：为路径映射添加对排除项的支持。
* SITES-39171：带有通用编辑器的Edge Delivery：在块和块项中添加对`cq:tags`的支持。
* SITES-40042：使用通用编辑器的Edge Delivery：将配置服务设置为新站点的默认值。
* SITES-37649： GraphQL：支持JCR级别的多行文本字段筛选。
* SITES-37843： GraphQL：JCR级别不支持筛选多值字段（收藏集）。
* SITES-37540：替换和替换CF字段值的所有操作（给定字段名称的查找和替换）。
* SITES-37741：在获取片段变量响应中添加“卡片”属性（管理UI中的卡片视图）。
* SITES-37754：通过API发布文件夹：当`validateReferences`设置为true时，根据需要进行树验证。
* SITES-37756：显示内容片段的签入/签出状态信息。
* SITES-37805：架构更新：无法重命名/移动修改的片段（文档）。
* SITES-37847：提高了借出内容ReferenceProvider SQL-2查询（LentContent检索）的性能。
* SITES-39255：将OpenAPI实施更新为复合字段的最新Java API更改。
* SITES-37096：当存在孤立节点时，删除启动项控制台速度缓慢。
* SITES-38117：找到一种在不影响性能的情况下查询子启动项的方法。
* SITES-38317：将启动工作流的用户添加到元数据（由服务用户运行时，使用实际用户而不是通用用户）。
* SITES-39203：显示启动工作流的用户（而不是服务用户运行时的通用用户）。
* SITES-13083：在站点> Live Copy创建对话框中本地化错误字符串。
* SITES-13389：在站点>时间线中本地化“已创建的版本……在提升启动项之前”字符串。
* SITES-16176：在页面编辑器>图像v3组件配置对话框中本地化字符串。
* SITES-35702：“Live Copy概述”选项卡中的“Live Copy为最新且继承受限”字符串未本地化。
* SITES-35748：“内容片段模型编辑器”中的“启用产品变体选择”复选框标签未本地化。
* SITES-35750：“内容片段模型编辑器”中输入字段中的未本地化的“产品SKU（以`#`字符分隔）”占位符。
* SITES-37113：“CIF配置”选项卡中的“取消继承”对话框未本地化。
* SITES-25240：修复了Teaser模式call to action的辅助功能。
* SITES-25531：修复了搜索模式中颜色对比度的辅助功能。
* SITES-37115：Vienia演示存储中截断的图标。

### 修复的问题 {#fixed-issues-24678}

* CQ-4361552：修复了在导入翻译中保留HTML转义Unicode的i18n JSON词典。
* CQ-4361634：修复的体验片段不可选或添加到翻译项目。
* CQ-4362072：修复了AEMaaCS翻译工作流 — DE > ES步骤无法将页面添加到翻译项目。
* Forms-23741：用户遇到了InvokeDDX和Asset上传步骤未级联运行的问题，需要执行两个单独的工作流。 这影响了将AEM as a Cloud Service与站点和Forms加载项一起使用的生产环境。
* Forms-23877：用户遇到在使用旧版核心组件直接在站点页面中创建表单时自定义函数未在运行时加载的问题。
* Forms-24038：用户在动态添加更多选项卡时遇到了导航按钮问题。
* Forms-23721：修复了在“编辑”对话框中为文本输入配置的验证模式无法持久存在的问题。 以前，模式值会保存下来，但不会被保留或显示在UI中，这会给表单作者带来混淆。
* Forms-23456：在自适应Forms中使用表组件时，移动设备上的屏幕阅读器会出现有关表中隐藏标题行的错误公告。 在上下文中声明了一个隐藏的表标题，这会给依赖于iOS VoiceOver和Android TalkBack的用户带来困惑。
* Forms-23454：用户遇到基于核心组件的自适应Forms的日期选择器问题。 输入无效日期时，系统将自动更正以关闭可能的日期。
* Forms-23117：遇到验证码的用户在基于基础组件的自适应Forms中无法正确翻译。
* Forms-22634：用户遇到了“包含附件”和“使用HTML模板”选项同时使用时未包含电子邮件附件的问题。
* Forms-23288：用户遇到在资产共享共享共享模式中嵌入自适应Forms的问题。 URL在中间路径中包含`.html`时，表单无法正确加载。
* Forms-19198：用户使用Dispatcher规则嵌入表单时遇到404错误。 由于URL重写器无法重写这些URL，导致/etc.clientlibs/toggles.json、rum库和analyticsparserconfigparser.json等URL出现错误。
* SITES-33799：带有通用编辑器的Edge Delivery：修复了未发布的优化视频演绎版。
* SITES-35082：使用通用编辑器的Edge Delivery：从富文本中删除空段落、前导和尾随换行符。
* SITES-35524：使用通用编辑器的Edge Delivery：修复包含非ASCII特殊字符的路径的发布失败。
* SITES-38647：使用通用编辑器的Edge Delivery：修复具有多个站点的环境中的性能瓶颈。
* SITES-40521：使用通用编辑器的Edge Delivery：修复块和块项的重复类名。
* SITES-37887： GraphQL：对大型结果集进行UUID查找可能会导致响应时间增加。
* SITES-38412：当存在唯一字段/概要（唯一约束现在不包括启动项中的CF）时，无法修补启动项中的片段。
* SITES-38606：使用片段引用UUID（变量中的uuid引用的水合物CF）向CF添加变量时出现验证错误。
* SITES-39489：Assets UI显示cq:discarded文件夹中的片段（从管理API响应中删除的软删除CF）。
* SITES-39517：包含包含枚举的复合字段的GET CF失败，出现500错误。
* SITES-40072：带制表符的复合字段返回空占位符值。
* SITES-39575： Live Copy保存将删除`cq:rolloutConfigs` — 转出配置丢失。
* SITES-39694：生产转出因NPE而失败。
* SITES-39761： NavigationItem.getLink()在CIF v2导航组件中返回null。
* SITES-40519：当live-copy目标资源为null时，MSM转出失败并出现NullPointerException。
* SITES-17531：页面编辑器>图像>智能裁剪中的硬编码“智能裁剪预览”字符串。
* SITES-31575：信息工具提示在页面编辑器>轮盘组件>属性中不完全可见。
* SITES-34215：自动完成JS组件在对话框选项卡中的必需pathfield上引发立即验证错误。
* SITES-35218：某些AEM核心组件无法正确呈现空alt标记。
* SITES-37114：“CIF配置”选项卡中的“启用目录UID支持”工具提示被截断。
* SITES-36138：检测到没有索引的查询（事件）。
* SITES-37682： `/libs/cq/Page/Page.css.jsp`和`/libs/cq/Page/Page.js.jsp.`中的内容类型覆盖
* SITES-38709：经典UI文本RTE显示升级到6.5.24后的原始HTML。
* SITES-39630：嵌套的内容片段更新未反映在导出的目标选件中。
* SITES-39696：计划激活/取消激活的打开/关闭时间不起作用。
* SITES-39824：将体验片段导出到Adobe Target时返回500 (NPE)。
* SITES-40253： `/bin/cif/invalidate-cache`上间歇性500错误 — `/var/cif/cacheinvalidation`下的Oak冲突。
* SITES-40341：修复`HtmlToJsonConvertorImpl`中样式标记中的base64内联图像。

### 已知问题 {#known-issues-24678}

无。

### 已弃用的功能和 API {#deprecated-24678}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-24678}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 15 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-24678}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
