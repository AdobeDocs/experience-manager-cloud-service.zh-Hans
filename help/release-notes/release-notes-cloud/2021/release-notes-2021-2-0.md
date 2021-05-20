---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.2.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 作为Cloud Service2021.2.0发行说明。'
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]作为Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as aCloud Service2021.2.0的发布日期是2021年2月25日。
以下版本(2021.3.0)将于2021年3月25日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### 无头内容管理 {#headless}

* **[用于内容片段交付的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能够使用GraphQL语法和基于内容片段模型的架构查询内容片段，以便以JSON格式输出。

* **[对GraphQL API请求的身份验证支持](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能够使用服务器端API的访问令牌来验证GraphQL API请求。

* **[RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)**:添加了对使用查看和编辑AEM内外部SPA的支持。

* **[在AEM中编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**:添加了将独立单页应用程序上传到AEM实例、添加内容的可编辑部分并启用创作的功能。

* 增强了GraphQL API的JSON输出，包括能够以JSON格式和区域设置输出富文本。

* 支持嵌套内容片段模型，以允许通过多行文本字段中的专用内容片段引用数据类型或内联内容片段引用来创建嵌套的内容片段结构。

* 内容片段模型数据类型中提供的其他验证规则，包括“唯一”、“必需”和“可翻译”。

* 能够标记内容片段模型，并允许在文件夹中按标记或路径创建策略的内容片段。

* 增强了内容片段编辑器中的可用性，包括发布操作和片段所基于模型的显示。

* 能够直接在内容片段编辑器中预览JSON输出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] {#what-is-new-assets}的新增功能

* 资产可使用[!DNL Experience Manager Assets Brand Portal]进行来源补充。 它有助于为新的营销活动、照片和项目从机构用户那里获取资产。

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 有权使用预配置的实 [!DNL Brand Portal] 例。[!DNL Cloud Manager]用户可以在[!DNL Experience Manager Assets]上激活[!DNL Brand Portal]作为[!DNL Cloud Service]。 请参阅[激活Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en)。

* 企业现在可以使用[!DNL Brand Portal]来源资产。 资产源功能利用[!DNL Brand Portal]来帮助客户与代理用户互动，为新的营销活动、照片和项目来源资产。 请参阅 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)中的[资产源。

* [!DNL Brand Portal]使用情况报表现在仅显示活动用户。 此时不会显示不活动的用户。 活动用户是指将其帐户分配给[!DNL Admin Console]中的产品配置文件的用户。 请参阅[[!DNL Brand Portal] 报表](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)。

* 在[!DNL Brand Portal]中，引入了新的下载设置，允许您在下载文件夹、收藏集等内容时为每个资产创建单独的文件夹。 请参阅[下载设置](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

## [!DNL Assets] {#bug-fixes-assets}中的错误修复

* 选择多个资产以更新属性时，有时会发生错误，或更新已取消选择资产的属性。 (CQ-4316532)
* 尝试打开[!UICONTROL 资产管理员搜索边栏]时，页面仍为空白，单击[!UICONTROL 编辑] > [!UICONTROL 设置]会生成错误。 (CQ-4315079)
* 在解决命名冲突后创建现有资产的新版本时，会覆盖原始资产的元数据。 (CQ-4313594)
* 打印具有长注释文本的资产时，即使有空格，注释文本也会被裁剪。 (CQ-4314101)

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：使用体验片段单独丰富产品目录页面。

* 扩展了产品控制台属性，用于显示链接的资产和体验片段，包括快速导航到关联内容的操作。

* 已发布CIF Venia参考网站 — 2021.02.24，其中包含最新的CIF核心组件版本v1.8.0。有关更多详细信息，请参阅[CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)。

* 已发布CIF核心组件v1.8.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service2021.2.0中的Cloud Manager的发布日期是2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets客户现在可以通过Cloud Manager UI以自助方式选择何时何地部署其Brand Portal实例。 对于具有Assets解决方案的常规（非沙盒）计划，现在可以在生产环境中配置Brand Portal。 在生产环境中只能完成一次配置。

* 项目和沙盒创建中使用的AEM项目原型已更新到版本25。

* 代码扫描过程中标识的已弃用API列表已得到细化，以包含最新Cloud ServiceSDK版本中已弃用的其他类和方法。

* 更新了Cloud Manager的SonarQube配置文件，以删除Sonar规则squid:S2142。 这不再与线程中断检查冲突。

* Cloud Manager UI将通知那些暂时无法添加/更新域名的用户，因为关联的环境要么具有附加在其上的正在运行的管道，要么当前正在等待批准步骤。

* 现在，将动态删除客户`pom.xml`文件中设置的带声纳前缀的属性，以避免生成和质量扫描失败。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 已添加其他代码质量规则以解决Cloud Service兼容性问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 将SSL证书与域名匹配不再区分大小写。

* 现在，如果证书私钥不符合2048位限制，Cloud Manager UI将通知用户，并显示相应的错误消息。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能会导致环境删除卡住。

* 某些管道故障被错误地报告为管道错误。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具v1.2.4的发布日期是2021年2月10日。

### 错误修复 {#bug-fixes-ctt}

* 映射多个用户时，某些用户的IMS ID映射不正确。 此问题已修复。

### 发布日期 {#release-date-ctt-feb}

内容传输工具v1.2.2的发布日期是2021年2月1日。

### 内容传输工具{#what-is-new-ctt}的新增功能

* 内容传输工具 — 用户映射工具中新增了功能和用户界面。 此功能会自动将现有用户和组映射到其AdobeIdentity Management系统ID，以将其作为内容迁移活动的一部分。
有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 。
* 内容传输工具现在可迁移迁移集中引用的所有组和用户，包括子项。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的发布日期是2021年2月18日。

### 最佳实践分析器{#what-is-new-bpa}的新增功能

* 能够检测AEM Forms和AEM Forms实施的使用情况，并指示与作为Cloud Service迁移到AEM Forms相关的区域。
* 能够检测并报告自定义组件和模板的使用情况和计数。
* 能够检测所使用的节点存储和数据存储的类型。
* 能够检测Dynamic Media的使用情况。
* 能够检测使用的Java版本。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具{#what-is-new-crt}的新增功能

* 已发布新版AIO-CLI插件。 此插件的最新版本包括针对Repository Modernizer的若干错误修复。
请参阅[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) ，了解有关此插件的更多信息。

### 错误修复 {#bug-fixes-crt}

* 对Repository Modernizer执行了若干错误修复。
请参阅[GitHub资源：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) ，以了解更多详细信息。
