---
title: AEM Commerce入门Cloud Service
description: 了解如何将支持商务的AEM项目部署到正在运行的AEM作为云服务环境。 使用Adobe Cloud Manager和CI/CD管道的功能，为正在运行的环境构建Venia参考店面。
topics: Commerce
feature: Commerce Integration Framework， Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 05242f0ca4168e220a4b83436da4daa0013edfaf
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 2%

---


# AEM Commerce入门，作为Cloud Service{#start}

要开始将AEM Commerce作为Cloud Service，您的Experience Manager Cloud Service需要配置Commerce Integration Framework(CIF)Add-on。 CIF附加模块位于[AEM Sites上，作为Cloud Service](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/sites/home.html)。

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## 入门 {#onboarding}

AEM Commerce as a Cloud Service的入门是一个分两步的过程：

1. 启用AEM Commerce作为Cloud Service并设置CIF加载项
2. 将AEM Commerce作为Cloud Service与您的Magento环境

第一个入门步骤由Adobe完成。 有关定价和供应的更多详细信息，您需要联系销售代表。

一旦您配置了CIF加载项，它将应用于任何现有Cloud Manager项目。 如果您没有Cloud Manager项目，则需要创建新Cloud Manager管理器。 有关详细信息，请参阅[设置项目](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二步是作为Cloud Service环境，为每个AEM提供自助服务。 在CIF加载项的初始配置之后，您还需要进行一些其他配置。

## 使用Magento {#magento}连接AEM Commerce

要将CIF加载项和[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)与您的Magento环境连接，您需要通过Cloud Manager环境变量提供MagentoGraphQL端点URL。 变量名为`COMMERCE_ENDPOINT`。 必须配置通过HTTPS的安全连接。
每个AEM都可以使用不同的MagentoGraphQL端点URL作为Cloud Service环境。 这样，项目可以将AEM暂存环境与Magento暂存系统和AEM生产环境连接到Magento生产系统。 该MagentoGraphQL端点必须是公开可用的，不支持专用VPN或本地连接。

要将AEM Commerce与Magento连接，请执行以下步骤：

1. 使用Cloud Manager插件获取Adobe I/O CLI

   请查看[Adobe Cloud Manager文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)，了解如何下载、设置和使用[Adobe I/OCLI](https://github.com/adobe/aio-cli)和[Cloud Manager CLI plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 将CLI验证为AEM项目

3. 在云管理器中设置`COMMERCE_ENDPOINT`变量

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有关详细信息，请参见[CLI docs](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   Magento GraphQL端点URL必须指向Magento的GraphQl服务，并使用安全的HTTPS连接。 例如：`https://demo.magentosite.cloud/graphql`。

>[!TIP]
>
>您可以使用以下命令列表所有Cloud Manager变量以进行多次检查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>或者，您也可以使用[Cloud Manger API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)配置Cloud Manager变量。

借助此功能，您可以将AEM Commerce用作Cloud Service，并可以通过云管理器部署您的项目。

## 启用分阶段目录功能（可选）{#staging}

>[!NOTE]
>
>此功能仅在Magento Enterprise Edition或Magento Cloud中提供。

1. 登录Magento并创建集成令牌。 有关详细信息，请参阅[基于令牌的身份验证](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。 确保集成令牌仅具有&#x200B;*对`Content -> Staging`资源的*&#x200B;访问权限。 复制`Access Token`值。

1. 在云管理器中设置`COMMERCE_AUTH_HEADER`机密变量：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization Bearer: <Access Token>"
   ```

   请参阅[将AEM Commerce与Magento](#magento)连接，了解如何配置Adobe I/O CLI for Cloud Manager。

## 第三方商务集成{#integrations}

对于第三方商务集成，需要[API映射层](architecture/third-party.md)才能将AEM Commerce作为Cloud Service和CIF核心组件与您的商务系统连接。 此API映射层通常部署在Adobe I/O Runtime上。 有关可用集成和访问Adobe I/O Runtime的信息，请与销售代表联系。
