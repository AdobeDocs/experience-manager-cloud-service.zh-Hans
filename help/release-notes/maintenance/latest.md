---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d2c26a122bd2a0a970af7578932d88e6f93487d5
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 12%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 25194 {#25194}

以下总结了维护版本25194的持续改进，该版本于2026年4月1日公开发布。 上一个维护版本是版本 24678。

2026.4.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>发行说24893已设为私有。

### 增强功能 {#enhancements-25194}

* Assets-65127：事件自定义元数据：改进了元数据名称的处理。
* Assets-63313：根据C2PA清单为导出的资源和父项自动创建相关链接。
* Assets-10995：限制下载zip文件中的资源数。
* Forms-24388：为交互式通信(IC)编辑器添加了一个本地开发环境，通过该环境，开发人员可以构建和测试配置，而无需依赖共享服务器。 此增强功能可帮助企业客户更快地迭代，减少环境依赖项，并提高整体开发效率。
* Forms-24014：增强了文件附件组件的规则编辑器，以支持使用“AND”逻辑组合条件，例如，允许诸如“如果文件附件已更改并且面板有效，则执行此操作”之类的规则。 以前，无法对文件附件使用其他条件；此更新使更复杂的规则定义能够支持高级工作流。
* Forms-23571：除了自定义事件之外，还通过添加对开箱即用(OOTB)事件的支持，增强了用于触发器事件规则的现有简化语法视图。 以前，用户只能将简化的语法用于自定义事件，并且必须在“WHEN”和“ON TRIGGER EVENT”规则之间切换以分别配置OOTB和自定义事件。 通过此更新，OOTB和自定义事件均可在相同的简化语法中使用，从而简化规则配置并减少切换上下文的需求。
* Forms-24462：在React Vanilla组件中添加了对涂写签名组件的支持，以用于Headless自适应Forms (AF)。 此增强功能使用户能够直接在基于React的表单中捕获手写签名，支持企业客户的数字签名工作流和计划的上线时间表。
* Forms-24343：在表单模型JavaScript对象表示法(JSON)中添加了`custom:setProperty`的优化处理，从而加快动态属性更新的处理。 此增强功能提高了依赖频繁运行时更改的复杂自适应Forms (AF)的性能，从而使用户交互更顺畅，缩短了加载时间。
* Forms-24358：添加了对在模型JavaScript对象表示法(JSON)结构中使用`items`属性而非`:items`和`:itemsOrder`的支持。 此增强功能使开发人员可以使用更清晰、更直观的数据模型，该模型与常用JSON约定更好地保持一致，并简化了与外部系统的集成。
* Forms-24087：新增支持在自适应Forms (AF)中直接在片段容器上定义规则和事件。 此增强功能使作者能够在容器级别应用条件逻辑和交互，从而提高重复使用率并减少跨单个片段字段重复规则的需求。
* Forms-24440：在交互式通信编辑器的规则编辑器的THEN下拉列表中添加了一个新的“删除字段”操作，该操作允许用户在满足规则条件时从表单中完全删除选定的组件。 此增强功能支持需要动态重构表单的工作流，而不是仅隐藏字段，同时仍会触发适当的`forms_ready`脚本以实现一致行为。
* Forms-23898：增加了对在交互式通信(IC)编辑器中使用`@`表示法定义变量的支持，使用户能够更直观地配置动态表。 此增强功能简化了变量驱动表内容的设置，并提高了在创作体验中管理动态数据时的清晰度。
* Forms-23702：为SharePoint List (SPList)连接添加了基于证书的身份验证，从而支持对SharePoint数据的更安全、基于证书的访问。 此增强功能可帮助企业客户满足更严格的安全性和法规遵从性要求，同时减少对基于密码的身份验证的依赖。
* Forms-23800：增加了对覆盖sling配置中的reCAPTCHA密钥的支持，使企业客户能够符合其自身的安全和合规要求。 此增强功能允许对特定于环境的密钥进行管理，以便管理员能够安全地集成reCAPTCHA而无需更改代码。

### 修复的问题 {#fixed-issues-25194}

* Assets-62882：管理员视图：上传多个无效文件名时信息工具提示中断。
* Assets-63642：共享链接无法在某些开发环境中呈现资产(SLA3)。
* Assets-59267：为投放有效负载加载应用程序元数据时出现NPE。
* Assets-59227：元数据导出：由于正则表达式匹配，不再包含未选择的属性。
* Assets-65187：列数据包含转义逗号时，在云中进行CSV预览。
* Assets-63441：确保所有用户都有权读取Assets Omnisearch配置。
* SITES-40095：元数据编辑器：本地内容片段引用超过10个条目。
* Forms-24811：用户在管理表单逻辑规则时遇到问题。 当他们尝试修改之前创建的规则时，规则编辑器不允许进行更改，从而强制用户从头开始重新创建规则，并减慢表单维护速度。
* Forms-24720：用户在自适应Forms (AF)中配置新创建的变量时遇到问题。 当他们将规则添加到数据绑定或未绑定的变量时，规则无法按预期保存，从而强制用户重新创建其逻辑并减慢创作工作流的速度。
* Forms-24195：用户在重置自适应Forms (AF)中的下拉字段时遇到不一致行为。 当下拉列表配置了占位符并且表单或组件重置时，字段变为空白而不是返回到占位符值，导致对所需选择的混淆。
* Forms-24718：用户在选择“主页”按钮时，在交互式通信(IC)编辑器中遇到导航问题。 该按钮未返回主Adobe Experience Manager (AEM)界面，而是未按预期重定向，在IC编辑和AEM主屏幕之间移动时会中断用户的工作流程。
* Forms-24810：用户在首次尝试加载表单的自适应用户界面(AUI)时遇到间歇性故障。 在某些会话中，初始页面无法正确呈现，强制用户刷新或重试，然后才能开始填写表单。
* Forms-24520：用户在使用自适应用户界面(AUI)的代理用户界面(UI)打印预览中遇到缺少页码的问题。 当代理打开打印预览时，页码字段有时显示为空，使得在查看或共享打印的副本时更难以引用特定页面。
* Forms-24532：用户使用带有SharePoint `/teams`列表配置的表单数据模型(FDM)预填充时遇到失败。 依赖这些列表的政府组织发现，表单加载时没有预期的预填充数据，从而中断了数据收集工作流，并增加了手动输入的工作量。
* Forms-24516：在AEM Forms as a Cloud Service中升级SDK后，用户遇到记录文档(DoR)中缺少涂写签名数据的问题。 使用涂写选项签署表单时，生成的DoR不显示捕获的签名，导致企业客户混淆和不完整记录。
* Forms-18631：用户遇到桌面、响应式Web设计(RWD)平板电脑和RWD移动设备视图上的网格布局无障碍问题。 在将Windows 11上的Chrome与NVDA（非可视化桌面访问）屏幕阅读器结合使用时，网格缺少相应的角色和属性，使得辅助型技术难以正确解释和导航内容。
* Forms-24798：用户在AEM Forms用户界面(UI)中的自适应Forms (AF)规则中使用`else`条件时遇到了不一致行为。 当不符合主规则条件时，关联的`else`操作未运行，导致表单逻辑和字段可见性的行为与作者配置的行为不同。
* Forms-24334：在JavaScript (AEM) Forms as a Cloud Service中使用嵌入的自适应表单(AF)时，用户遇到预填充失败和Adobe Experience Manager对象表示法(JSON)合并问题。 加载已迁移的表单时，预期的预填充数据未显示，并且合并的JSON内容不完整或不正确。 这会阻止从内部部署AEM 6.5迁移到受影响环境的AEM Forms as a Cloud Service。
* Forms-24441：用户在Adobe Experience Manager (AEM) Forms as a Cloud Service中遇到记录文档(DoR)模板配置问题。 当他们在快速开发环境中保存自定义DoR模板时，该模板将恢复到默认版本，阻止他们保留其预期布局和设置。
* Forms-24393：当旧模板继续显示为“无标题”而非显示有意义的名称时，用户会遇到困惑。 这使得在日常创作工作中难以区分和重用现有模板。
* Forms-24163：用户在预览包含片段的版本2表单时遇到问题。 在预览模式下，表单内容未按预期呈现，导致用户无法在发布之前验证布局和行为。
* Forms-24328：在将不可见reCAPTCHA v2与“在用户操作中验证CAPTCHA”选项结合使用时，用户遇到表单提交未完成的情况。 企业客户发现，受影响环境中的表单未按预期提交，从而中断了联系和征求建议书工作流。

#### AEM Guides {#guides-25194}

* GUIDES-38412 ：在编辑Schematron `(*.sch)`文件并使用查找和替换功能时，“查找和替换”面板在底部部分显示在屏幕外，阻止访问其输入字段和控件。
* GUIDES-37806：如果在具有不同条件预设的多个映射中重用同一主题，则发布最新映射到Salesforce时会覆盖主题内容，从而导致向以前发布映射的用户显示的数据不正确。
* GUIDES-39394：在将最初作为具有特定版本（例如，在`/en/`下）的语言特定资产管理的图像移动到全局文件夹并执行更新版本基线导出时，新基线将继续引用该图像的过时语言特定版本，从而导致基线导出失败。
* GUIDES-39054：创建动态基线时，编辑器有时会因多个并发API请求而变得无响应，导致所有其他操作暂停。
* GUIDES-37781：将用户分配给审核任务时，下拉列表会列出所有用户，而非仅列出与所选项目关联的用户，从而导致用户选项无效。
* GUIDES-39385：打开地图的报表时，“筛选器”面板的加载存在延迟。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-25194}

无。

### 已弃用的功能和 API {#deprecated-25194}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-25194}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 9 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-25194}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
