---
title: 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改
description: 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 81%

---

# 对 Adobe Experience Manager (AEM) as a Cloud Service 的显著更改 {#notable-changes-aem-cloud}

AEM 云服务为管理 AEM 项目提供了许多新功能和可能性。但是，与 AEM 云服务相比，On-Premise 版或 Adobe Managed Service 中的 AEM Sites 存在很大差异。本文档重点介绍了这些重要差异。

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="对AEM作为Cloud Service的显着更改"
>abstract="在此选项卡中，您可以查看有助于您了解内部部署版AEM之间或与Adobe Managed Services中的AEM as a Cloud Service相比有何差异的内容。"
>additional-url="https://video.tv.adobe.com/v/330543" text="AEM作为Cloud Service的演变"


>[!NOTE]
>本文档重点介绍了对 AEM 整体的显著更改。有关更多信息和特定于解决方案的更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* 与先前版本相比，Adobe Experience Manager as a Cloud Service 具有的[新增功能和不同之处](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service[架构](/help/overview/architecture.md)
>* [对 AEM Sites as a Cloud Service 的显著更改](/help/sites-cloud/sites-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)


主要区别包括以下方面：

* [/apps 和 /libs 在运行时不可更改](#apps-libs-immutable)

* [OSGi 包和设置必须基于存储库](#osgi)

* [不允许更改发布存储库](#changes-to-publish-repo)

* [不允许自定义运行模式](#custom-runmodes)

* [删除了复制代理](#replication-agents)

* [删除了经典 UI](#classic-ui)

* [发布端交付](#publish-side-delivery)

* [资产处理和交付](#asset-handling)

## /apps 和 /libs 在运行时不可更改 {#apps-libs-immutable}

`/apps` 和 `/libs` 中的所有内容和子文件夹均为只读。任何希望在这两处做出更改的功能或自定义代码都将无法进行。将返回一个错误，指出此类内容为只读，无法完成写入操作。这对 AEM 的许多方面都有影响：

* `/libs` 中不允许进行任何更改。
   * 这不是新规则，只是在先前的 AEM On-Premise 版本中未强制执行。
* 对于 `/libs` 中允许覆盖的区域，`/apps` 中仍允许覆盖。
   * 必须通过 CI/CD 管道从 Git 实现此类覆盖。
* 无法通过 UI 编辑存储在 `/apps` 中的静态模板设计信息。
   * 建议您改用可编辑的模板。
   * 如果仍需使用静态模板，必须通过 CI/CD 管道从 Git 获得配置信息。
* 必须通过 CI/CD 管道从 Git 安装 MSM Blueprint 和自定义 MSM 转出配置。
* 必须通过 CI/CD 管道从 Git 更改 I18n 翻译。

## OSGi 包和设置必须基于存储库 {#osgi}

在 AEM 的早期版本中用于更改 OSGi 设置的 Web 控制台在 AEM 云服务中不可用。因此，必须通过 CI/CD 管道引入对 OSGi 的更改。

* 与基于 JCR 的 OSGi 设置一样，对 OSGi 设置的更改只能通过 Git 持久性来实现。
* 在 CI/CD 管道构建的过程中，必须通过 Git 引入新的或更新的 OSGi 包。

## 不允许更改发布存储库 {#changes-to-publish-repo}

除了发布层`/home`文件夹下的更改之外，还不允许在AEMCloud Service上直接更改发布存储库。 在On-Premise AEM或AEM on AMS的先前版本中，可以直接对发布存储库进行代码更改。 可通过以下方式缓解某些限制：

* 对于内容和基于内容的配置：对创作实例进行更改并将其发布。
* 对于代码和配置：在 GIT 存储库中进行更改，然后运行 CI/CD 管道以将其推出。

## 不允许自定义运行模式 {#custom-runmodes}

为 AEM 云服务提供的现成可用的运行模式如下：

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

AEM 云服务中不能使用其他运行模式或自定义运行模式。

## 删除了复制代理 {#replication-agents}

在 AEM 云服务中，使用 [Sling 内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)发布内容。不再使用或提供在以前版本的 AEM 中使用的复制代理，这可能会影响现有 AEM 项目的以下方面：

* 例如，将内容推送到预览服务器的复制代理的自定义工作流。
* 自定义复制代理以转换内容
* 使用反向复制将内容从发布层引回创作层

## 删除了经典 UI {#classic-ui}

经典 UI 在 AEM 云服务中不再可用。

## 发布端交付 {#publish-side-delivery}

默认情况下，AEM 云服务中提供 HTTP 加速，包括创作和发布服务的 CDN 和流量管理。

要通过 AMS 或 On-Premise 安装进行项目转换，Adobe 强烈建议利用内置 CDN，因为 AEM 云服务中的功能已针对提供的 CDN 进行了优化。

## 资产处理和交付 {#asset-handling}

在[!DNL Experience Manager Assets]中，资产上传、处理和下载已优化为[!DNL Cloud Service]。 [!DNL Assets] 现在更高效，可进行更大的扩展，并且允许您以更快的速度上传和下载。此外，它还会影响现有的自定义代码和某些操作。 有关更改列表以及与[!DNL Experience Manager] 6.5功能对等的信息，请参阅[对 [!DNL Assets]](/help/assets/assets-cloud-changes.md)的更改。
