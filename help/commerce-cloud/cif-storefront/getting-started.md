---
title: AEM Commerce as a Cloud Service快速入门
description: 了解如何使用Adobe Experience Manager Cloud Manager、CI/CD管道和Venia参考店面部署Adobe (AEM)商务项目。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---


# AEM Commerce as a Cloud Service快速入门 {#start}

要开始使用Adobe Experience Manager (AEM) Commerce as a Cloud Service，您的Experience Manager Cloud Service必须配置Commerce integration framework (CIF)加载项。 CIF加载项是[AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)之上的额外模块。

>[!TIP]
>
>**您是否考虑过Edge Delivery Services？**
>
>Edge Delivery Services是Adobe首选的店面创建解决方案。 有关详细信息，请参阅文档[简介和概述](/help/commerce-cloud/introduction.md)。

## 加入 {#onboarding}

AEM Commerce as a Cloud Service的入门培训分为两步：

1. 启用AEM Commerce as a Cloud Service并配置CIF加载项
1. 将AEM Commerce as a Cloud Service与您的商务解决方案连接

Adobe完成了第一个入门培训步骤。 有关定价和配置的更多详细信息，您必须联系您的销售代表。

配置CIF加载项后，该加载项将应用于任何现有的Cloud Manager项目。 如果您没有Cloud Manager项目，则必须创建一个。 有关更多详细信息，请参阅[设置程序。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html)

第二步是每个AEM as a Cloud Service环境的自助服务。 在CIF加载项初始配置后，您必须执行一些其他配置。

## 将AEM与Commerce解决方案连接 {#solution}

要将CIF加载项和[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)与商业解决方案连接，必须通过Cloud Manager环境变量提供GraphQL端点URL。 变量名称为`COMMERCE_ENDPOINT`。 必须配置通过HTTPS的安全连接。

此环境变量在以下两个位置使用：

* GraphQL从AEM通过某些常见的可共享GraphQl客户端(由AEM CIF核心组件和客户项目组件使用)向commerce后端调用。
* 在每个GraphQL环境中设置一个AEM代理URL，变量设置在`/api/graphql`处可用。 此URL由AEM Commerce创作工具(CIF加载项)和CIF客户端组件使用。

每个GraphQL环境可以使用不同的AEM as a Cloud Service端点URL。 通过这种方法，项目可以将AEM暂存环境与Commerce暂存系统和AEM生产环境连接到一个Commerce生产系统。 GraphQL端点必须可公开使用，不支持专用VPN或本地连接。 或者，可以提供身份验证标头以使用需要身份验证的其他CIF功能。

（可选）并且仅对于Adobe Commerce Enterprise/Cloud，CIF加载项支持为AEM作者使用暂存的目录数据。 此数据要求您配置授权标头。 出于安全原因，此标头仅在AEM Author实例上可用和使用。 AEM发布实例无法显示暂存数据。

可以使用两个选项来配置端点：

### 通过Cloud Manager用户界面（默认） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

可以使用“环境详细信息”页面上的对话框完成此配置。 在查看启用了Commerce的程序的此页时，如果当前未配置端点，则会显示一个按钮：

![CM环境信息](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

单击此按钮将打开一个对话框：

![CM Commerce端点](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png)

设置暂存目录支持的端点和（可选）授权标头后，该端点会显示在详细信息页面上。 单击“编辑”图标可打开同一个对话框，如有必要，可在其中编辑端点。

![CM环境信息](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### 通过Adobe I/O CLI  {#adobe-cli}

要通过AEM CLI将Adobe I/O与商务解决方案连接，请执行以下步骤：

1. 通过Cloud Manager插件获取Adobe I/O CLI。

   * 查看[Adobe Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)，了解如何下载、设置和使用[Adobe I/O CLI](https://github.com/adobe/aio-cli)和[Cloud Manager CLI插件。](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. 使用AEM as a Cloud Service程序验证Adobe I/O CLI。

1. 在Cloud Manager中设置`COMMERCE_ENDPOINT`变量。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * 有关详细信息，请参阅[CLI文档](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   * 商业GraphQL端点URL必须指向商业的GraphQl服务并使用安全的HTTPS连接。 例如：`https://<yourcommercesystem>/graphql`。

1. 启用需要身份验证的暂存目录功能（可选）。

   >[!NOTE]
   >
   >此功能仅在Adobe Commerce Enterprise或Cloud Edition中可用。 有关详细信息，请参阅[基于令牌的身份验证](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。

   * 在Cloud Manager中设置`COMMERCE_AUTH_HEADER`密码变量：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列出所有Cloud Manager变量以进行仔细检查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

您已准备好使用AEM Commerce as a Cloud Service，可以通过Cloud Manager部署您的项目。

## 配置存储和目录 {#catalog}

CIF加载项和[CIF核心组件](https://github.com/adobe/aem-core-cif-components)可用于连接到不同商务商店（或商店视图等）的多个AEM网站结构。 默认情况下，CIF加载项使用默认配置进行部署，该默认配置连接到Adobe Commerce的默认商店和目录。

可以通过执行以下步骤的CIF Cloud Service配置来调整项目的此配置：

1. 在AEM中，转到“工具”>“云服务”>“CIF配置”。

1. 选择要更改的商务配置。

1. 通过操作栏打开配置属性。

![CIF云服务配置](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

可以配置以下属性：

* GraphQL客户端 — 为商务后端通信选择配置的GraphQL客户端。 此客户端通常应保留默认值。
* 存储视图 — 存储视图标识符。 如果为空，则使用默认存储视图。
* GraphQL代理路径 — AEM中的GraphQL代理用于向商务后端GraphQL端点代理请求的URL路径。

  >[!NOTE]
  >
  > 在大多数设置中，不能更改默认值`/api/graphql`。 只有未使用所提供的GraphQL代理的高级设置才应更改此设置。

* 启用目录UID支持 — 在商业后端GraphQL调用中启用对UID而不是ID的支持。

  >[!NOTE]
  >
  > Adobe Commerce 2.4.2中引入了对UID的支持。仅当您的Commerce后端支持2.4.2或更高版本的GraphQL架构时，才启用UID。

* 目录根类别标识符 — 商店目录根的标识符(UID或ID)

  >[!CAUTION]
  >
  > 从CIF核心组件版本2.0.0开始，删除了`id`的支持并将其替换为`uid`。 如果您的项目使用CIF核心组件版本2.0.0，则必须启用目录UID支持，并使用有效类别UID作为“目录根类别标识符”。

以上所示的配置仅供参考。 项目应提供自己的配置。

有关更复杂的设置，请参阅结合使用多个AEM网站结构以及不同的商务目录的[Commerce多商店设置](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)教程。

## 其他资源 {#additional-resources}

* [AEM项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [Commerce多商店设置](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [多个Commerce系统设置](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
