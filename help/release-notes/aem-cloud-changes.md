---
title: 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改
description: 对Adobe Experience Manager (AEM)as a Cloud Service的重要更改。
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 97%

---

# 对 Adobe Experience Manager as a Cloud Service 的显著更改 {#notable-changes-aem-cloud}

Adobe Experience Manager (AEM) Cloud Service 对于管理 AEM 项目带来许多新功能和可能性。但是，内部部署版或 Adobe Managed Service 中的 AEM Sites 与 AEM Cloud Service 有一些区别。本文档重点介绍这些重大区别。

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="AEM as a Cloud Service 中的重大更改"
>abstract="在此选项卡中，可查看帮助您了解内部或 Adobe Managed Services 中的 AEM 与 AEM as a Cloud Service 之间区别的内容。"
>additional-url="https://video.tv.adobe.com/v/330543" text="AEM as a Cloud Service 的演变"


>[!NOTE]
>本文档重点介绍了对 AEM 整体的重大更改。有关更多信息和特定于解决方案的更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* 与先前版本相比，Adobe Experience Manager as a Cloud Service 具有的[新增功能和不同之处](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service 的[架构](/help/overview/architecture.md)
>* [对 AEM Sites as a Cloud Service 的显著更改](/help/sites-cloud/sites-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)

主要区别包括以下方面：

* [/apps 和 /libs 在运行时不可更改](#apps-libs-immutable)

* [必须当作代码一样对待 OSGi 捆绑包和配置](#osgi)

* [不允许更改发布存储库](#changes-to-publish-repo)

* [不允许使用自定义运行模式](#custom-runmodes)

* [删除了复制代理和相关更改](#replication-agents)

* [删除了经典 UI](#classic-ui)

* [发布端投放](#publish-side-delivery)

* [资源处理和投放](#asset-handling)

## /apps 和 /libs 在运行时不可更改 {#apps-libs-immutable}

`/apps` 和 `/libs` 中的任何内容和子文件夹均为只读。预计在这两处作出更改的任何功能或自定义代码都无法这样做。其中返回一个错误，表示此类内容为只读，未能完成写入操作。这种情况影响 AEM 的若干方面：

* 完全不允许在 `/libs` 中作出更改。
   * 这并非新规则，但并未在以前的 AEM 内部部署版本中强制执行。
* 仍允许在 `/apps` 内使用 `/libs` 中可叠加的区域的叠加。
   * 必须通过 CI/CD 管道从 Git 获得此类叠加。
* 无法通过 UI 编辑存储在 `/apps` 中的静态模板设计信息。
   * 建议您改用可编辑的模板。
   * 如果仍需使用静态模板，则必须通过 CI/CD 管道从 Git 获得配置信息。
* 必须通过 CI/CD 管道从 Git 安装 MSM Blueprint 和自定义 MSM 转出配置。
* 必须通过 CI/CD 管道从 Git 获得 I18n 翻译变更。

## 必须当作代码一样对待 OSGi 捆绑包和配置 {#osgi}

必须通过 CI/CD 管道引入对 OSGi 捆绑包和配置的更改。

* 必须通过 CI/CD 管道通过 Git 引入新的或更新的 OSGi 捆绑包。
* 只能通过 CI/CD 管道从 Git 获得对 OSGi 配置的更改。

在 AEM Cloud Service 的早期版本中用于更改 OSGi 包和配置的 Web 控制台不可用。

## 不允许更改发布存储库 {#changes-to-publish-repo}

除了发布层上的 `/home` 文件夹下的更改外，不允许在 AEM Cloud Service 上直接更改发布存储库。在内部部署 AEM 或 AEM on AMS 的早期版本中，可以直接对发布存储库进行代码更改。可以通过以下方式减少一些限制：

* 对于内容和基于内容的配置：在“创作”实例上作出您的更改，然后发布这些更改。
* 对于代码和配置：在 GIT 存储库中作出您的更改，然后运行 CI/CD 管道以转出这些更改。

## 不允许使用自定义运行模式 {#custom-runmodes}

AEM Cloud Service 中不能使用其他运行模式或自定义运行模式。有关为 AEM Cloud Service 提供的开箱即用的运行模式列表，请参阅[部署到 AEM as a Cloud Service](/help/implementing/deploying/overview.md#runmodes)。

## 删除了复制代理和相关更改 {#replication-agents}

在 AEM Cloud Service 中，使用 [Sling 内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)发布内容。不再使用或提供在以前 AEM 版本中使用的复制代理，而这可能会影响现有 AEM 项目的以下方面：

* 例如，将内容推送到预览服务器的复制代理的自定义工作流。
* 自定义复制代理以转换内容。
* 使用反向复制将内容从“发布”恢复为“创作”。

此外，从复制代理管理控制台中删除了“暂停”和“禁用”按钮。

## 删除了经典 UI {#classic-ui}

经典 UI 在 AEM Cloud Service 中不再可用。

## 发布端投放 {#publish-side-delivery}

默认情况下在 AEM Cloud Service 中提供“创作”和“发布”服务的 HTTP 加速，其中包括 CDN 和流量管理。

对于从 AMS 或内部部署安装过渡而来的项目，由于为所提供的 CDN 优化了 AEM Cloud Service 中的功能，因此 Adobe 强烈建议使用内置的 CDN。

## 资源处理和投放 {#asset-handling}

[!DNL Experience Manager Assets] as a [!DNL Cloud Service] 中已优化资源上传、处理和下载。 AEM [!DNL Assets] 现在更高效，可进行更大规模的伸缩，并使您可更快地上传和下载。此外，它会影响现有的自定义代码和一些操作。有关更改列表以及与 [!DNL Experience Manager] 6.5 功能的等同性，请参阅[更改 [!DNL Assets]](/help/assets/assets-cloud-changes.md)。
