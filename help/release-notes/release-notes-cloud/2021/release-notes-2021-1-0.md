---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.1.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 作为Cloud Service2021.1.0发行说明。'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]作为Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.1.0的发布日期是2021年2月3日。
以下版本(2021.2.0)将于2021年2月25日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

* **[内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加/更新和删除内容片段变量的功能。

* **[用于内容片段交付的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能够使用GraphQL语法和基于内容片段模型的架构查询内容片段，以便以JSON格式输出。

* **[对GraphQL API请求的身份验证支持](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能够使用服务器端API的访问令牌来验证GraphQL API请求。

* 增强了GraphQL API的JSON输出，包括能够以JSON格式和区域设置输出富文本。

* 支持嵌套内容片段模型，以允许通过多行文本字段中的专用内容片段引用数据类型或内联内容片段引用来创建嵌套的内容片段结构。

* 内容片段模型数据类型中提供的其他验证规则，包括“唯一”、“必需”和“可翻译”。

* 能够标记内容片段模型，并允许在文件夹中按标记或路径创建策略的内容片段。

* 增强了内容片段编辑器中的可用性，包括发布操作和片段所基于模型的显示。

* 能够直接在内容片段编辑器中预览JSON输出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a扩 [!DNL Cloud Service] 展了智能标记功能，以支持基于文本的资产中的关键词和实体的识别。文本将被标识、编入索引，并作为元数据提供，以改进搜索体验，而无需进行任何配置。 请参阅[智能标记](/help/assets/smart-tags.md)。

* 现在支持MXF文件格式。 请参阅[支持的文件格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：资产和体验片段新增了“商务”属性选项卡。 利用此选项卡，可将产品/类别关联到资产和体验片段。 选项卡还显示链接的产品/类别的实时数据，以及在产品控制台中显示详细信息的链接。

* 已发布CIF Venia参考网站 — 2021.02.02，其中包含最新的CIF核心组件版本v1.7.0。有关更多详细信息，请参阅[CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* 已发布CIF核心组件v1.7.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service2021.1.0中的Cloud Manager的发布日期是2021年1月14日。

### 错误修复 {#bug-fixes-cloud-manager}

* 资产生产实例有时可能会在&#x200B;**Environments**&#x200B;详细信息页面上将Brand Portal状态显示为&#x200B;*Pending*，而不允许用户执行任何操作。

* 从Cloud Manager触发解除休眠时，有时即使成功启动解除休眠，也会显示失败消息。

* 解决了在环境创建或删除中遇到的极少数失败案例。

## 代码重构工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}的新增功能

* 已发布新版AIO-CLI插件。 此插件的最新版本包括针对AEM Dispatcher Converter和Repository Modernizer的错误修复，并且还支持新的实用程序 — 索引转换器。 请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以了解有关此插件的更多信息。

* 索引转换器是一个实用程序，可用于将客户的自定义OAK索引定义转换为AEM作为与Cloud Service兼容的OAK索引定义。 有关更多详细信息，请参阅[索引转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 向[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)添加的新功能，该功能可创建单独的包`ui.config`以包含所有OSGi配置。

### 错误修复 {#crt-bug-fixes}

* 对AEM Dispatcher Converter和Repository Modernizer工具进行了若干错误修复。 请参阅[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

## AEM as a A Foundation {#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 服务器到服务器经过身份验证的API调用 — 生成相应的访问令牌，以在外部应用程序和AEM(作为Cloud Service环境)之间进行经过身份验证的服务器到服务器API调用。 通过阅读[文档](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或咨询[tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)了解更多信息。

### SDK内部版本分析程序{#sdk-build-analyzers}

AEM as a Maven SDK Build Analyzer Maven插件可检测Maven项目中的问题，包括缺少依赖项。 它使开发人员有机会在本地开发过程中发现问题，而且在使用Cloud Manager部署到云环境之前就已经很早。

为此版本添加了两个新分析程序：

* 重点分析仪
* 束 — nativecode

有关更多信息，请参阅此文档[](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 云过渡工具{#code-transition-tools}

### 发布日期 {#release-date-ctt}

内容传输工具v1.2.2的发布日期是2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}的新增功能

* 内容传输工具 — 用户映射工具中新增了功能和用户界面。 此功能会自动将现有用户和组映射到其AdobeIdentity Management系统ID，以将其作为内容迁移活动的一部分。 有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) 。
* 内容传输工具现在可迁移迁移集中引用的所有组和用户，包括子项。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。
