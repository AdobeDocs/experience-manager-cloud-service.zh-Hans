---
title: AEM Commerce入门as a Cloud Service
description: 了解如何将启用商务的AEM项目部署到运行AEM as a Cloud Service环境。 使用Venia Cloud Manager和CI/CD管道的功能，将Venia引用店面构建到运行的Adobe。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 2%

---

# AEM Commerce入门as a Cloud Service {#start}

要开始使用AEM Commerceas a Cloud Service，您的Experience Manager Cloud Service需要配置商务集成框架(CIF)附加组件。 CIF附加组件是 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## 入门 {#onboarding}

AEM Commerceas a Cloud Service的入门过程分为两步：

1. 启用AEM Commerceas a Cloud Service并配置CIF附加组件
2. 将AEM Commerceas a Cloud Service与您的商务解决方案连接

第一个入门步骤由Adobe完成。 有关定价和配置的更多详细信息，您需要联系您的销售代表。

配置CIF附加组件后，该插件将应用于任何现有的Cloud Manager程序。 如果您没有Cloud Manager程序，则需要创建一个新程序。 有关更多详细信息，请参阅 [设置程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

第二步是为每个AEMas a Cloud Service环境提供自助服务。 在初始配置CIF附加组件后，您还需要执行一些其他配置。

## 将AEM与商务解决方案连接 {#solution}

连接CIF附加组件和 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 通过商务解决方案，您需要通过Cloud Manager环境变量提供GraphQL端点URL。 变量名称为 `COMMERCE_ENDPOINT`. 必须配置通过HTTPS的安全连接。

此环境变量用于以下两个位置：

- 通过AEM CIF核心组件和客户项目组件使用的一些常见可共享的GraphQl客户端，从AEM向商务后端调用GraphQL。
- 在每个AEM环境中设置一个GraphQL代理URL，该变量在 `/api/graphql`. 这由AEM商务创作工具（CIF附加组件）和CIF客户端组件使用。

每个AEMas a Cloud Service环境都可以使用不同的GraphQL端点URL。 这样，项目就可以将AEM暂存环境与商务暂存系统和AEM生产环境连接到商务生产系统。 必须公开提供该GraphQL端点，不支持专用VPN或本地连接。 可选地，可以提供验证标头以使用需要验证的附加CIF功能。

（可选）仅对于Adobe Commerce Enterprise / Cloud，CIF附加组件支持为AEM作者使用分阶段目录数据。 这要求配置授权标头。 出于安全考虑，此标头仅可用，并用于AEM创作实例。 AEM发布实例无法显示暂存数据。

有两个选项可配置端点：

### 通过Cloud Manager UI（默认） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

可以使用“环境详细信息”页面上的对话框来完成此操作。 查看启用了商务的程序的此页面时，如果当前未配置端点，则会显示一个按钮：

![CM环境信息](/help/commerce-cloud/assets/commerce-cmui.png)

单击此按钮将打开一个对话框：

![CM Commerce端点](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

在设置了用于暂存目录支持的端点和授权标头（可选）后，将在详细信息页面上显示该端点。 单击编辑图标将打开相同的对话框，如有必要，可以在该对话框中修改端点。

![CM环境信息](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 通过Adobe I/OCLI  {#adobe-cli}

要通过AEM CLI将Adobe I/O与商务解决方案连接，请执行以下步骤：

1. 使用Cloud Manager插件获取Adobe I/OCLI

   检查 [AdobeCloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hans) 关于如何下载、设置和使用 [Adobe I/OCLI](https://github.com/adobe/aio-cli) 和 [Cloud Manager CLI插件](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. 使用AEMas a Cloud Service程序验证Adobe I/OCLI

3. 设置 `COMMERCE_ENDPOINT` 变量

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   请参阅 [CLI文档](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 以了解详细信息。

   商务GraphQL端点URL必须指向商务的GraphQl服务，并使用安全的HTTPS连接。 例如：`https://<yourcommercesystem>/graphql`。

4. 启用需要身份验证的暂存目录功能（可选）

   >[!NOTE]
   >
   >此功能仅在Adobe Commerce Enterprise或Cloud Edition中可用。 请参阅 [基于令牌的身份验证](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) 以了解详细信息。

   设置 `COMMERCE_AUTH_HEADER` Cloud Manager中的秘密变量：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列出所有Cloud Manager变量，以进行复查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

借助此功能，您可以使用AEM Commerceas a Cloud Service，并可以通过Cloud Manager部署项目。

## 配置存储和目录 {#catalog}

CIF附加组件和 [CIF核心组件](https://github.com/adobe/aem-core-cif-components) 可用于连接到不同商务商店（或商店视图等）的多个AEM站点结构。默认情况下，CIF加载项会部署一个默认配置，该配置连接到Adobe Commerce的默认商店和目录。

可通过CIFCloud Service配置按照以下步骤操作，针对项目调整此配置：

1. 在AEM中，转到“工具” — >“Cloud Services” — > CIF配置

2. 选择要更改的商务配置

3. 通过操作栏打开配置属性

![CIFCloud Services配置](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可以配置以下属性：

- GraphQL客户端 — 为商务后端通信选择已配置的GraphQL客户端。 此设置通常应保持默认状态。
- 存储视图 — 存储视图标识符。 如果为空，则使用默认的存储视图。
- GraphQL代理路径 — AEM中用于将请求代理到商务后端GraphQL端点的URL路径GraphQL代理。
   >[!NOTE]
   >
   > 在大多数设置中，默认值 `/api/graphql` 不得更改。 只有不使用提供的GraphQL代理的高级设置才应更改此设置。
- 启用目录UID支持 — 在商务后端GraphQL调用中启用对UID的支持，而不是ID。
   >[!NOTE]
   >
   > 在Adobe Commerce 2.4.2中引入了对UID的支持。仅当商务后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。
- 目录根类别标识符 — 存储目录根的标识符（UID或ID）
   >[!CAUTION]
   >
   > 从CIF核心组件版本2.0.0开始，支持 `id` 已删除，替换为 `uid`. 如果您的项目使用CIF核心组件版本2.0.0，则必须启用“目录UID支持”，并使用有效的类别UID作为“目录根类别标识符”。

上面显示的配置供参考。 项目应提供自己的配置。

有关使用多个AEM网站结构并结合不同商务目录的更复杂设置，请参阅 [商务多商店设置](configuring/multi-store-setup.md) 教程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商务多商店设置](configuring/multi-store-setup.md)
