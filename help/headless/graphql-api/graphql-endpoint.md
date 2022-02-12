---
title: 在AEM中管理GraphQL端点
description: 了解如何在Adobe Experience Manager as a Cloud Service中管理GraphQL端点以进行无头内容交付。
feature: Content Fragments,GraphQL API
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---


# 在AEM中管理GraphQL端点 {#graphql-aem-endpoint}

端点是用于访问GraphQL for AEM的路径。 使用此路径，您（或您的应用程序）可以：

* 访问GraphQL模式，
* 发送GraphQL查询，
* 接收响应（对您的GraphQL查询）。

AEM中有两种类型的端点：

* 全局
   * 可供所有站点使用。
   * 此端点可以使用所有站点配置(在 [配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser))。
   * 如果有任何内容片段模型应在站点配置之间共享，则应在全局站点配置下创建这些模型。
* 站点配置：
   * 对应于站点配置，如 [配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * 特定于指定的站点/项目。
   * 特定于站点配置的端点将使用该特定站点配置中的内容片段模型以及全局站点配置中的内容片段模型。

>[!CAUTION]
>
>内容片段编辑器允许一个站点配置的内容片段引用另一个站点配置的内容片段（通过策略）。
>
>在这种情况下，并非所有内容都可以使用特定于Sites配置的端点进行检索。
>
>内容作者应控制此情景；例如，考虑将共享的内容片段模型置于全局站点配置下可能会非常有用。

用于AEM全局端点的GraphQL的存储库路径是：

`/content/cq:graphql/global/endpoint`

您的应用程序可以在请求URL中对其使用以下路径：

`/content/_cq_graphql/global/endpoint.json`

要为AEM启用GraphQL的端点，您需要：

* [启用GraphQL端点](#enabling-graphql-endpoint)
* [发布GraphQL端点](#publishing-graphql-endpoint)

## 启用GraphQL端点 {#enabling-graphql-endpoint}

要启用GraphQL端点，您首先需要具有适当的配置。 请参阅 [内容片段 — 配置浏览器](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>如果 [尚未启用内容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md), **创建** 选项将不可用。

要启用相应的端点，请执行以下操作：

1. 导航到 **工具**, **资产**，然后选择 **GraphQL**.
1. 选择&#x200B;**创建**。
1. 的 **创建新GraphQL端点** 对话框。 您可以在此指定：
   * **名称**:端点名称；您可以输入任何文本。
   * **使用由提供的GraphQL模式**:使用下拉菜单选择所需的站点/项目。

   >[!NOTE]
   >
   >对话框中显示以下警告：
   >
   >* *如果不对 GraphQL 端点仔细管理，则可能会带来数据安全和性能问题。请确保在创建端点后设置适当的权限。*


1. 使用确认 **创建**.
1. 的 **后续步骤** 对话框将提供指向安全控制台的直接链接，以便您能够确保新创建的端点具有适当的权限。

   >[!CAUTION]
   >
   >每个人都可以访问该端点。 这可能会（尤其是在发布实例上）带来安全问题，因为GraphQL查询可能会给服务器带来沉重的负载。
   >
   >您可以在端点上设置与用例相应的ACL。

## 发布GraphQL端点 {#publishing-graphql-endpoint}

选择新端点并 **发布** 以使其在所有环境中完全可用。

>[!CAUTION]
>
>每个人都可以访问该端点。
>
>在发布实例上，这可能会引起安全问题，因为GraphQL查询可能会给服务器带来沉重的负载。
>
>您必须设置 [适合您的用例的ACL](/help/headless/security/permissions.md) 在端点上。