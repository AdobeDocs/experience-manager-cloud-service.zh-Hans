---
title: 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改
description: 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改。
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 49%

---

# 对Adobe Experience Manager as a Cloud Service的重要更改 {#notable-changes-aem-cloud}

Adobe Experience Manager (AEM)Cloud Service为管理AEM项目提供了许多新功能和可能性。 但是，与AEM Cloud Service相比，内部部署版或Adobe托管服务中的AEM Sites存在一些差异。 本文档重点介绍了这些重要差异。

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

* [OSGi 捆绑包和配置必须视为代码](#osgi)

* [不允许更改发布存储库](#changes-to-publish-repo)

* [不允许自定义运行模式](#custom-runmodes)

* [删除了复制代理和相关更改](#replication-agents)

* [删除了经典 UI](#classic-ui)

* [发布端投放](#publish-side-delivery)

* [资源处理和投放](#asset-handling)

## /apps 和 /libs 在运行时不可更改 {#apps-libs-immutable}

中的任何内容和子文件夹 `/apps` 和 `/libs` 是只读的。 任何希望在这两处做出更改的功能或自定义代码都将无法做出更改。 返回一个错误，指出此类内容为只读，无法完成写入操作。这对AEM的多个领域产生了影响：

* `/libs` 中不允许进行任何更改。
   * 这不是新规则，只是在先前的AEM内部部署版本中未强制执行。
* 中的区域叠加 `/libs` 可以覆盖的仍然允许在 `/apps`.
   * 必须通过CI/CD管道从Git实现此类叠加。
* 存储在中的静态模板设计信息 `/apps` 无法通过UI进行编辑。
   * 建议您改用可编辑的模板。
   * 如果仍需要静态模板，必须通过CI/CD管道从Git获取配置信息。
* 必须通过CI/CD管道从Git安装MSM Blueprint和自定义MSM转出配置。
* 必须通过CI/CD管道从Git更改I18n翻译。

## OSGi 捆绑包和配置必须视为代码 {#osgi}

必须通过CI/CD管道引入对OSGi捆绑包和配置的更改。

* 新的或更新的OSGi捆绑包必须通过CI/CD管道通过Git引入。
* 只能通过CI/CD管道从Git更改OSGi配置。

在 AEM Cloud Service 的早期版本中用于更改 OSGi 包和配置的 Web 控制台不可用。

## 不允许更改发布存储库 {#changes-to-publish-repo}

除了发布层上的 `/home` 文件夹下的更改外，不允许在 AEM Cloud Service 上直接更改发布存储库。在内部部署 AEM 或 AEM on AMS 的早期版本中，可以直接对发布存储库进行代码更改。可以通过以下方式减少一些限制：

* 对于内容和基于内容的配置：对创作实例进行更改并将其发布。
* 对于代码和配置：在GIT存储库中进行更改，然后运行CI/CD管道以转出这些更改。

## 不允许自定义运行模式 {#custom-runmodes}

为AEM Cloud Service提供了以下现成运行模式：

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

AEM Cloud Service 中不能使用其他运行模式或自定义运行模式。

## 删除了复制代理 和相关更改 {#replication-agents}

在 AEM Cloud Service 中，使用 [Sling 内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)发布内容。不再使用或提供在以前版本的AEM中使用的复制代理，这可能会影响现有AEM项目的以下方面：

* 例如，将内容推送到预览服务器的复制代理的自定义工作流。
* 自定义复制代理以转换内容。
* 使用“反向复制”将内容从“发布”带回“创作”。

此外，暂停和禁用按钮也会从复制代理管理控制台中删除。

## 删除了经典 UI {#classic-ui}

经典 UI 在 AEM Cloud Service 中不再可用。

## 发布端投放 {#publish-side-delivery}

默认情况下，AEM Cloud Service中提供HTTP加速，包括创作和发布服务的CDN和流量管理。

对于从AMS或内部部署转换的项目，Adobe强烈建议使用内置CDN，因为AEM Cloud Service中的功能已针对提供的CDN进行了优化。

## 资源处理和投放 {#asset-handling}

[!DNL Experience Manager Assets] as a [!DNL Cloud Service] 中已优化资源上传、处理和下载。 AEM [!DNL Assets] 现在更高效，支持更多扩展，并可让您以更快的速度上传和下载。 此外，它会影响现有的自定义代码和一些操作。有关更改列表以及与 [!DNL Experience Manager] 6.5 功能的等同性，请参阅[更改 [!DNL Assets]](/help/assets/assets-cloud-changes.md)。
