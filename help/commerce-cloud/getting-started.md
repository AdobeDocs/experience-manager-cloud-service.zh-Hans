---
title: AEM Commerce入门Cloud Service
description: 了解如何将支持商务的AEM项目部署到正在运行的AEM作为云服务环境。 使用Adobe Cloud Manager和CI/CD管道的功能，为正在运行的环境构建Venia参考店面。
topics: Commerce
feature: Commerce Integration Framework， Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
translation-type: tm+mt
source-git-commit: 08e258d4e9cd67de3da2aa57c058036bd104472d
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 2%

---

# AEM Commerce入门，作为Cloud Service{#start}

要开始将AEM Commerce作为Cloud Service，您的Experience Manager Cloud Service需要配置Commerce Integration Framework(CIF)Add-on。 CIF附加模块位于[AEM Sites上，作为Cloud Service](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/sites/home.html)。

## 入门 {#onboarding}

AEM Commerce as a Cloud Service的入门是一个分两步的过程：

1. 启用AEM Commerce作为Cloud Service并设置CIF加载项
2. 将AEM Commerce作为Cloud Service与您的商务解决方案

第一个入门步骤由Adobe完成。 有关定价和供应的更多详细信息，您需要联系销售代表。

一旦您配置了CIF加载项，它将应用于任何现有Cloud Manager项目。 如果您没有Cloud Manager项目，则需要创建新Cloud Manager管理器。 有关详细信息，请参阅[设置项目](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二步是作为Cloud Service环境，为每个AEM提供自助服务。 在CIF加载项的初始配置之后，您还需要进行一些其他配置。

## 将AEM与Commerce Solution {#magento}连接

要将CIF加载项和[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)与商务解决方案连接，您需要通过Cloud Manager环境变量提供GraphQL终结点URL。 变量名为`COMMERCE_ENDPOINT`。 必须配置通过HTTPS的安全连接。

此环境变量用于以下两个位置：

- 从AEM到商务后端的GraphQL调用，通过AEM CIF核心组件和客户项目组件使用的一些通用可共享的GraphQl客户端。
- 在每个AEM环境上设置一个GraphQL代理URL，变量设置为`/api/graphql`。 这由AEM商务创作工具(CIF Add-on)和CIF客户端组件使用。

每个AEM都可以使用不同的GraphQL端点URL作为Cloud Service环境。 这样，项目可以将AEM暂存环境与商务暂存系统和AEM生产环境连接到商务生产系统。 该GraphQL端点必须是公开可用的，不支持专用VPN或本地连接。 可选地，可以提供认证头以便使用需要认证的附加CIF功能。

CIF加载项支持为AEM作者使用分阶段目录数据，但仅对Adobe Commerce Enterprise / Cloud可选。 这要求配置授权令牌。 配置的授权令牌仅可用，并且出于安全原因在AEM作者实例上使用。 AEM发布实例无法显示分阶段数据。

配置端点有两个选项：

### 通过Cloud Manager UI（默认）{#cm-ui}

可以使用“环境详细信息”页面上的对话框完成此操作。 查看启用商务的项目的此页时，如果当前未配置终结点，则将显示一个按钮：

![CM环境信息](/help/commerce-cloud/assets/commerce-cmui.png)

单击此按钮将打开一个对话框：

![CM Commerce Endpoint](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

在设置终结点（可选地为分阶段目录支持设置身份验证令牌）后，将在详细信息页上显示该终结点。 单击“编辑”图标将打开相同的对话框，如有必要，可在其中修改端点。

![CM环境信息](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 通过Adobe I/O CLI {#adobe-cli}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

要通过Adobe I/O CLI将AEM与商务解决方案连接，请执行以下步骤：

1. 使用Cloud Manager插件获取Adobe I/O CLI

   请查看[Adobe Cloud Manager文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)，了解如何下载、设置和使用[Adobe I/O CLI](https://github.com/adobe/aio-cli)和[ Cloud Manager CLI插件](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 将Adobe I/O CLI与AEM验证为Cloud Service项目

3. 在云管理器中设置`COMMERCE_ENDPOINT`变量

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有关详细信息，请参见[CLI docs](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   商务GraphQL端点URL必须指向商务的GraphQl服务，并使用安全HTTPS连接。 例如：`https://demo.magentosite.cloud/graphql`。

4. 启用需要身份验证的分阶段目录功能（可选）

   >[!NOTE]
   >
   >此功能仅在Adobe Commerce Enterprise或Cloud Edition中可用。 有关详细信息，请参阅[基于令牌的身份验证](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。

   在云管理器中设置`COMMERCE_AUTH_HEADER`机密变量：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列表所有Cloud Manager变量以进行多次检查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

借助此功能，您可以将AEM Commerce用作Cloud Service，并可以通过云管理器部署您的项目。

## 配置商店和目录{#catalog}

CIF加载项和[CIF核心组件](https://github.com/adobe/aem-core-cif-components)可用于连接到不同商店(或商店视图等)的多个AEM站点结构。默认情况下，CIF加载项部署时会配置一个默认配置，该配置连接到Adobe Commerce的默认存储和目录(Magento)。

此配置可通过CIFCloud Service配置按以下步骤调整：

1. 在AEM中，转到工具 — >Cloud Services-> CIF配置

2. 选择要更改的商务配置

3. 通过操作栏打开配置属性

![CIFCloud Services配置](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可以配置以下属性：

- GraphQL客户端 — 为商务后端通信选择已配置的GraphQL客户端。 这通常应保持为默认值。
- 存储视图-(Magento)存储视图标识符。 如果为空，则使用默认存储视图。
- GraphQL代理路径 — AEM中用于代理向商务后端GraphQL端点的请求的URL路径GraphQL代理。
   >[!NOTE]
   >
   > 在大多数设置中，默认值`/api/graphql`不得更改。 只有不使用提供的GraphQL代理的高级设置才应更改此设置。
- 启用目录UID支持 — 在商务后端GraphQL调用中启用UID而非ID支持。
   >[!NOTE]
   >
   > Adobe Commerce(Magento)2.4.2中引入了对UID的支持。仅当您的商务后端支持版本2.4.2或更高版本的GraphQL模式时，才启用此功能。
- 目录根类别标识符 — 存储目录根的标识符（UID或ID）

上面所示的配置供参考。 项目应提供自己的配置。

有关使用多个AEM站点结构并结合不同商务目录的更复杂设置，请参阅[商务多商店设置](configuring/multi-store-setup.md)教程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商务多商店设置](configuring/multi-store-setup.md)
