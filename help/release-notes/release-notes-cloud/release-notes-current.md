---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
translation-type: tm+mt
source-git-commit: 429d1710af30f85174f69ed111140b2e4fb5ab0f
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]的一般发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.1.0的发布日期为2021年2月3日。
以下版本(2021.2.0)将于2021年2月25日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

* **[内容片段投放的GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)**:能够使用GraphQL语法查询内容片段，以及基于内容片段模型的模式，以JSON格式输出。

* **[GraphQL API请求的身份验证支持](/help/assets/content-fragments/graphql-authentication-content-fragments.md)**:能够使用服务器端API的访问令牌验证GraphQL API请求。

* GraphQL API的增强JSON输出，包括以JSON格式和区域设置输出富文本的能力。

* 支持嵌套内容片段模型，以允许通过多行文本字段中内联的专用内容片段引用数据类型或内容片段引用创建嵌套内容片段结构。

* 内容片段模型数据类型中提供的其他验证规则，包括“唯一”、“必需”和“可翻译”。

* 能够标记内容片段模型，并允许在文件夹中按标记或路径创建包含策略的内容片段。

* 内容片段编辑器中的可用性增强功能，包括发布操作和片段所基于的模型显示。

* 能够直接在内容片段编辑器中预览JSON输出。


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as扩展 [!DNL Cloud Service] 了智能标记功能以支持在基于文本的资产中识别关键字和实体。文本将被识别、索引，并作为元数据提供，以改进搜索体验，而无需任何配置。 请参阅[智能标记](/help/assets/smart-tags.md)。

* 现在支持MXF文件格式。 请参阅[支持的文件格式](/help/assets/file-format-support.md#video-formats)。

## Adobe Experience Manager商务作为Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：资产和体验片段的新“商务”属性选项卡。 通过此选项卡，您可以将产品/类别关联到资产和体验片段。 该选项卡还显示链接的产品/类别的实时数据，以及在产品控制台中显示详细信息的链接。

* 已发布CIF Venia参考站点- 2021.02.02，其中包括最新的CIF核心组件版本v1.7.0。有关更多详细信息，请参阅[CIF Venia参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02)。

* 已发布CIF核心组件v1.7.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service2021.1.0的发布日期为2021年1月14日。

### 错误修复 {#bug-fixes-cloud-manager}

* 资产生产实例有时可能会将&#x200B;**环境**&#x200B;详细信息页面上的品牌门户状态显示为&#x200B;*挂起*，而不允许用户执行任何操作。

* 从Cloud Manager触发解除休眠时，有时即使成功启动解除休眠，也会显示一条失败消息。

* 已解决在创建或删除环境时遇到的少数故障。

## AEM作为Cloud Service基础{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* 服务器对服务器的身份验证API调用——生成相应的访问令牌，在外部应用程序和AEM之间进行身份验证的服务器对服务器API调用，作为Cloud Service环境。 阅读[文档](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)或查阅[教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication)，了解更多信息。

### SDK Build Analyzers {#sdk-build-analyzers}

AEM作为Cloud ServiceSDK构建分析器主插件可检测主项目中的问题，包括缺少依赖项。 它为开发人员提供了在本地开发过程中发现问题的机会，而且很早之后，您就可以使用Cloud Manager部署到云环境。

为此版本添加了两个新的分析器：

* 重点分析仪
* bundle-nativecode

有关详细信息，请参阅文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)。

## 云过渡工具{#code-transition-tools}

### 发布日期 {#release-date-ctt}

内容传输工具v1.2.2的发布日期为2021年2月1日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}中的新增功能

* 内容传输工具——用户映射工具新增功能和UI。 此功能会将现有用户和用户组自动映射到其AdobeIdentity Management系统ID，作为内容迁移活动的一部分。 有关详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 内容传输工具现在可迁移迁移集中引用的所有组和用户，包括子项。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。
