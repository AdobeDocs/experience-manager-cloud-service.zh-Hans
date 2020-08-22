---
title: AEM Commerce作为Cloud Service入门
description: AEM Commerce作为Cloud Service入门
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 2%

---


# AEM Commerce作为Cloud Service入门 {#start}

要开始将AEM Commerce作为Cloud Service，您的Experience Manager Cloud Service需要配置商务集成框架(CIF)加载项。 CIF附加组件是AEM Sites上的一个额外模块， [作为Cloud Service](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/sites/home.html)。

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## 入门 {#onboarding}

AEM Commerce as a saCloud Service的入门过程分为两步：

1. 启用AEM Commerce作为Cloud Service并设置CIF加载项
2. 将AEM Commerce作为Cloud Service与您的Magento环境

第一步是Adobe。 您需要提供诸如IMS组织、Magento环境的GraphQL端点URL等信息。 作为配置过程的一部分。 有关定价和供应的更多详细信息，您需要联系销售代表。

一旦您配置了CIF加载项，该加载项将应用于任何现有Cloud Manager项目。 如果您没有Cloud Manager项目，则需要创建新的Cloud Manager。 有关详细信息，请参阅 [设置项目](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二步是作为Cloud Service环境为每个AEM提供自助服务。 在CIF加载项的初始配置之后，您还需要进行一些其他配置。

## 将AEM Commerce与Magento连接 {#magento}

要将CIF附加组件和AEM CIF核 [心组件与您的Magento](https://github.com/adobe/aem-core-cif-components) 环境连接，您需要通过云管理器环境变量提供Magento图QL端点URL。 变量名称为 `COMMERCE_ENDPOINT`。 必须配置通过HTTPS的安全连接。
每个AEM都可以使用不同的Magento图形QL端点URL作为Cloud Service环境。 这样，项目可以将AEM分阶段环境与Magento分阶段系统和AEM生产环境连接到Magento生产系统。 该MagentoGraphQL端点必须是公开可用的，不支持专用VPN或本地连接。

要将AEM Commerce与Magento连接，请执行以下步骤：

1. 使用Cloud Manager插件获取AdobeI/O CLI

   查看 [Cloud Manager的文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) ，了解如何下载、设置 [和使用Cloud Manager CLI插](https://github.com/adobe/aio-cli) 件中的I/O [](https://github.com/adobe/aio-cli-plugin-cloudmanager)CLIAdobe。

2. 将CLI验证为AEMCloud Service项目

3. 在云管 `COMMERCE_ENDPOINT` 理器中设置变量

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有关详 [细信息](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) ，请参阅CLI文档。

   MagentoGraphQL端点URL必须指向Magento的GraphQl服务，并使用安全HTTPS连接。 For example: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>您可以使用以下命令列表所有Cloud Manager变量，以进行多次检查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>您也可以使 [用Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) API配置Cloud Manager变量。

有了这一功能，您就可以将AEM Commerce用作Cloud Service，并可以通过云管理器部署您的项目。

## 第三方商务集成 {#integrations}

对于第三方商务集成，需 [要一个API映射层](architecture/third-party.md) ，才能将AEM Commerce作为Cloud Service和CIF核心组件与您的商务系统连接。 此API映射层通常部署在Adobe I/O Runtime。 有关可用集成和访问Adobe I/O Runtime的信息，请与销售代表联系。
