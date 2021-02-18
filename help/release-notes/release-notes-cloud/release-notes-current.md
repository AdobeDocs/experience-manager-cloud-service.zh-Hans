---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
translation-type: tm+mt
source-git-commit: 6f48b5daa5b47ad19db8b3431350111364f962fc
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]的一般发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.1.0的发布日期为2021年2月3日。
以下版本(2021.2.0)将于2021年2月25日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

### 无头内容管理 {#headless}

* **[内容片段投放的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能够使用GraphQL语法查询内容片段，并基于内容片段模型的模式，以JSON格式输出。

* **[GraphQL API请求的身份验证支持](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能够使用服务器端API的访问令牌验证GraphQL API请求。

* **[RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)**:增加了在AEM中使用查看和编辑外部SPA的支持。

* **[在AEM中编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**:添加了将独立单页应用程序上传到AEM实例、添加内容的可编辑部分以及启用创作的功能。

* GraphQL API的增强JSON输出，包括以JSON格式和区域设置输出富文本的功能。

* 支持嵌套内容片段模型，以允许通过多行文本字段中内嵌的专用内容片段引用数据类型或内容片段引用创建嵌套内容片段结构。

* 内容片段模型数据类型中提供的其他验证规则，包括“唯一”、“必需”和“可翻译”。

* 可标记内容片段模型，并允许在文件夹中按标记或路径创建包含策略的内容片段。

* 内容片段编辑器中的可用性增强功能，包括发布操作和片段所基于的模型的显示。

* 能够直接在内容片段编辑器中预览JSON输出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] 作为对智 [!DNL Cloud Service] 能标记功能的扩展，以支持在基于文本的资产中识别关键字和实体。文本将被识别、索引，并作为元数据提供，以改进搜索体验，而无需任何配置。 请参阅[智能标签](/help/assets/smart-tags.md)。

* 现在支持MXF文件格式。 请参阅[支持的文件格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：资产和体验片段的新“商务”属性选项卡。 通过此选项卡，您可以将产品/类别关联到资产和体验片段。 该选项卡还显示链接的产品/类别的实时数据，以及在产品控制台中显示详细信息的链接。

* 已发布CIF委内瑞拉参考站点 — 2021.02.02，其中包括最新的CIF核心组件版本v1.7.0。有关更多详细信息，请参阅[CIF委内瑞拉参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* 已发布CIF核心组件v1.7.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service 2021.2.0的发布日期为2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets客户现在可以通过Cloud Manager UI以自助方式选择何时何地部署其Brand Portal实例。 对于具有资产解决方案的常规（非沙箱）项目，现在可以在生产环境上设置Brand Portal。 在生产环境上只能执行一次设置。

* 在“项目”和“沙箱创建”中使用的AEM Project原型已更新为版本25。

* 在代码扫描过程中识别的已弃用API的列表已得到改进，以包括最新Cloud Service SDK版本中已弃用的其他类和方法。

* SonarQube 用户档案 for Cloud Manager已更新以删除Sonar规则squid:S2142。 这不再与“线程中断检查”冲突。

* Cloud Manager UI将通知暂时无法添加/更新域名的用户，因为关联的环境已连接正在运行的管道，或者当前正在等待批准步骤。

* 现在，将动态删除客户`pom.xml`文件中设置的属性，以避免生成和质量扫描失败。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则该用户可能暂时无法选择该证书。

* 已添加其他代码质量规则，以解决Cloud Service兼容性问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 与域名匹配的SSL证书不再区分大小写。

* 现在，如果证书私钥不符合2048位限制，Cloud Manager用户界面将通知用户，并显示相应的错误消息。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能导致环境删除卡住。

* 某些管线故障被错误地报告为管线错误。

## AEM as a Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 服务器对服务器的身份验证API调用 — 生成相应的访问令牌，以便在外部应用程序和AEM之间进行身份验证的服务器对服务器API调用，作为Cloud Service环境。 阅读[文档](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或查阅[教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)，了解更多信息。

### SDK Build Analyzers {#sdk-build-analyzers}

AEM作为Cloud Service SDK Build Analyzer Maven Plugin可检测特定项目中的问题，包括缺少依赖项。 它为开发人员提供了在本地开发过程中发现问题的机会，而远在使用Cloud Manager部署到云环境之前。

为此版本添加了两个新分析器：

* 重点分析器
* bundle-nativecode

有关详细信息，请参阅文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具v1.2.4的发布日期为2021年2月10日。

### 错误修复 {#bug-fixes-ctt}

* 映射多个用户时，某些用户的IMS ID映射不正确。 此问题已解决。

### 发布日期 {#release-date-ctt-feb}

内容传输工具v1.2.2的发布日期为2021年2月01日。

### 内容传输工具{#what-is-new-ctt}的新增功能

* 内容传输工具 — 用户映射工具新增功能和UI。 此功能会自动将现有用户和用户组映射到其AdobeIdentity Management系统ID，作为内容迁移活动的一部分。
有关详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 内容传输工具现在可迁移迁移集中引用的所有组和用户，包括子项。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的发布日期为2021年2月18日。

### 最佳实践分析器{#what-is-new-bpa}的新增功能

* 能够检测AEM Forms和AEM Forms实施的使用情况并指示与作为Cloud Service迁移到AEM Forms相关的领域。
* 能够检测并报告自定义组件和模板的使用情况和计数。
* 能够检测使用的节点存储和数据存储的类型。
* 能够检测Dynamic Media的使用情况。
* 能够检测使用的Java版本。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具{#what-is-new-crt}的新增功能

* 已发布AIO-CLI插件的新版本。 此插件的最新版本包括存储库Modernizer的多个错误修复。
请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以了解有关此插件的更多信息。

### 错误修复 {#bug-fixes-crt}

* 在Repository Modernizer上完成了多个错误修复。
请参阅[GitHub资源：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)以了解更多详细信息。








