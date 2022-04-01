---
title: 配置翻译集成框架
description: 了解如何配置翻译集成框架以与第三方翻译服务相集成。
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 5ef9ac087ec3feab9c68935b81882451c308daed
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 2%

---

# 配置翻译集成框架 {#configuring-the-translation-integration-framework}

翻译集成框架与第三方翻译服务集成以编排AEM内容的翻译。 这涉及到三个基本步骤。

1. [连接到翻译服务提供商。](#connecting-to-a-translation-service-provider)
1. [创建翻译集成框架配置。](#creating-a-translation-integration-configuration)
1. [将云配置与您的页面关联。](#configuring-pages-for-translation)

有关AEM中的内容翻译功能的概述，请参阅 [翻译多语言站点的内容](overview.md).

>[!TIP]
>
>如果您是翻译内容的新用户，请参阅 [站点翻译历程、](/help/journey-sites/translation/overview.md) 这是使用AEM强大的翻译工具翻译AEM Sites内容的指导路径，非常适合那些没有AEM或翻译经验的用户。

## 连接到翻译服务提供商 {#connecting-to-a-translation-service-provider}

创建将AEM连接到翻译服务提供商的云配置。 AEM包含 [连接到Microsoft Translator](connect-ms-translator.md) 默认情况下。

以下翻译供应商为翻译项目提供了AEM API的实施。

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (AdobeExchange Premier合作伙伴)
* [粘土片技术](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Cloudwords](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM云](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [林戈特克](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [智能玲](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

安装连接器包后，可以为连接器创建云配置。 通常，您需要提供凭据以通过翻译服务进行身份验证。 有关为Microsoft Translator连接器添加云配置的信息，请参阅 [与Microsoft Translator集成](connect-ms-translator.md).

您可以根据需要为同一连接器创建多个云配置。 例如，为您与同一供应商拥有的每个帐户或项目创建一个配置。

配置连接后，您可以创建使用该连接的翻译集成框架配置。

## 创建翻译集成配置 {#creating-a-translation-integration-configuration}

创建翻译集成框架配置以指定如何翻译内容。 配置包括以下信息：

* 要使用的翻译服务提供商
* 是否执行人或机器翻译
* 是否翻译与页面或资产关联的其他内容，如标记

在创建框架配置后，您可以根据配置将云配置与要翻译的页面相关联。 启动翻译过程后，翻译工作流会根据关联的框架配置进行。

当网站的不同部分具有不同的翻译要求时，请相应地创建多个框架配置。 例如，多语言网站可能包含英语、西班牙语和日语副本。 网站所有者使用两个不同的翻译服务提供商进行西班牙语和日语的翻译。 因此，框架的两个配置已配置。 每个配置都使用不同的翻译服务提供程序。

配置翻译集成框架后，您可以 [将其与页面关联](preparation.md) 用它。

>[!TIP]
>
>有关AEM中的内容翻译功能的概述，请参阅 [翻译多语言站点的内容](overview.md).

框架的单个配置可控制页面内容和资产的翻译方式。 要创建新的翻译配置，请执行以下操作：

1. 在 [全局导航菜单，](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) 单击或点按 **工具 — >Cloud Services — 和翻译Cloud Services**.
1. 导航到要在内容结构中创建配置的位置。 这通常基于特定网站，也可以是全局网站。
1. 在字段中提供以下信息，然后单击或点按 **创建**.:
   1. 选择 **配置类型** 中。
   1. 输入 **标题** 的URL。 的 **标题** 在 **Cloud Services** 控制台以及页面属性下拉列表中。
   1. （可选）键入 **名称** 用于存储配置的存储库节点。
1. 在 **编辑配置** ，请在 **站点** 和 **资产** 选项卡，然后单击或点按 **保存并关闭**.

### 站点配置属性 {#sites-configuration-properties}

的 **站点** 选项卡可控制页面内容翻译的执行方式。

![站点的翻译配置](../assets/translation-configuration.png)

| 属性 | 描述 |
|---|---|
| 翻译方法 | 此属性定义框架对网站内容执行的翻译方法：<br> — 机器翻译：翻译提供者使用机器翻译实时执行翻译。<br> — 人文翻译：内容将发送给翻译提供商，由翻译人员翻译。<br> — 请勿翻译：内容不会发送以进行翻译。 这将跳过某些内容分支，这些内容分支虽未翻译，但可使用最新内容进行更新。 |
| 翻译提供商 | 此属性定义要执行翻译的翻译提供程序。 安装相应的连接器后，提供程序即会显示在列表中。 |
| 内容目录 | （仅限机器翻译）此属性是描述正在翻译的内容的类别。 在翻译内容时，类别会影响术语和措辞的选择。 |
| 翻译标记 | 此选项允许翻译与页面关联的标记。 |
| 翻译页面资产 | 此属性定义如何转换从文件系统添加到组件或从资产引用的资产：<br> — 请勿翻译：页面资产未进行折算。<br> — 使用站点翻译工作流：资产将根据 **站点** 选项卡。<br> — 使用资产翻译工作流：资产将根据 **资产** 选项卡。 |
| 自动执行翻译 | 启用此属性可在创建翻译项目后自动执行翻译作业。 选择此选项时，您没有机会复查和调整翻译作业的范围。 |
| 禁用仅更新翻译 | 选中此选项后，更新翻译项目将提交所有可翻译的字段进行翻译，而不只是上次翻译后更改的字段。 |

### 资产配置属性 {#assets-configuration-properties}

资产属性可控制如何配置资产。 有关翻译资产的更多信息，请参阅 [为资产创建语言副本](/help/assets/translate-assets.md).

![站点的翻译配置](../assets/translation-configuration-assets.png)

| 属性 | 描述 |
|---|---|
| 翻译方法 | 此属性将选择框架为资产执行的翻译类型：<br> — 机器翻译：翻译提供程序使用机器翻译立即执行翻译。<br> — 人文翻译：内容会自动发送到翻译提供商以进行手动翻译。<br> — 请勿翻译：不会发送资产进行翻译。 |
| 翻译提供商 | 此属性定义要执行翻译的翻译提供程序。 安装相应的连接器后，提供程序即会显示在列表中。 |
| 内容目录 | （仅限机器翻译）此属性描述要翻译的内容。 在翻译内容时，类别会影响术语和措辞的选择。 |
| 翻译资产 | 激活此资产以在翻译项目中包含资产。 |
| 翻译元数据 | 激活此属性可转换资产元数据。 |
| 翻译标记 | 激活此属性可翻译与资产关联的标记。 |
| 自动执行翻译 | 选择此属性可在创建翻译项目后自动执行翻译作业。 选择此选项时，您没有机会复查或调整翻译作业的范围。 |
| 禁用仅更新翻译 | 选中此选项后，更新翻译项目将提交所有可翻译的字段进行翻译，而不只是上次翻译后更改的字段。 |
| 为翻译启用内容模型字段* | 启用此选项将使用 **可翻译** 字段 [内容片段模型](/help/assets/content-fragments/content-fragments-models.md#properties) 以确定字段是否已翻译。 在这种情况下， [翻译规则](rules.md) 被取代。 |

>[!NOTE]
>
>*此功能在预发行渠道中提供。
> 
>请参阅 [预发行渠道文档](/help/release-notes/prerelease.md#enable-prerelease) 以了解有关如何为环境启用该功能的信息。

## 配置翻译页面 {#configuring-pages-for-translation}

要配置将源页面翻译成其他语言，请将这些页面与以下云配置关联：

* 将AEM连接到翻译提供商的云配置。
* 用于配置翻译详细信息的翻译集成框架。

请注意，翻译集成框架云配置标识了用于连接到服务提供商的云配置。 将源页面与框架云配置关联时，该页面必须与框架云配置所使用的服务提供商云配置关联。

将页面与云配置关联后，页面的子项将继承该关联。 例如，如果您将 `/content/wknd/language-masters/en/magazine` 页面， `magazine` 页面下的子页面将根据框架进行翻译。

如果需要，您可以覆盖子代页面上的关联。 例如，网站的内容主要与旅行和生活方式有关。 但是，页面的一个分支描述了公司。 在这种情况下，站点的根页面可能与翻译集成框架相关联，该框架指定使用“生活方式”类别进行机器翻译，而描述公司的分支将使用使用“常规”类别执行机器翻译的框架。

### 将页面与翻译提供程序关联 {#associating-a-page-with-a-translation-provider}

将页面与您用来翻译页面和子代页面的翻译提供程序关联。

1. 在站点控制台中，选择要配置的页面，然后单击或点按 **查看属性**.
1. 单击或点按 **Cloud Services** 选项卡。
1. 在 **添加配置** 下拉列表中，选择配置。
1. 单击或点按 **保存并关闭**.

### 将页面与翻译集成框架关联 {#associating-pages-with-a-translation-integration-framework}

将页面与翻译集成框架关联，该框架定义您希望如何翻译页面和子页面。

1. 在站点控制台中，选择要配置的页面，然后单击或点按 **查看属性**.
1. 单击或点按 **Cloud Services** 选项卡。
1. 在 **添加配置** 下拉列表中，选择配置。
1. 单击或点按 **保存并关闭**.
