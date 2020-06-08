---
title: 对 Adobe Experience Manager (AEM) 云服务的显著更改
description: 对 Adobe Experience Manager (AEM) 云服务的显著更改
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 100%

---


# 对 Adobe Experience Manager (AEM) 云服务的显著更改 {#notable-changes-aem-cloud}

AEM 云服务为管理 AEM 项目提供了许多新功能和可能性。但是，与 AEM 云服务相比，On-Premise 版或 Adobe Managed Service 中的 AEM Sites 存在很大差异。本文档重点介绍了这些重要差异。

>[!NOTE]
>本文档重点介绍了对 AEM 整体的显著更改。有关特定于解决方案的更改，请参阅：
>
>* [对 AEM 云服务中的 AEM Sites 的显著更改](/help/sites-cloud/sites-cloud-changes.md)
>* [对 AEM 云服务中的 AEM Assets 的显著更改](/help/assets/assets-cloud-changes.md)


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

AEM 云服务不允许直接更改发布存储库。在 On-Premise AEM 或 AMS 上 AEM 的先前版本中，可以直接对发布存储库进行代码更改以执行一些操作，例如创建用户、更新用户配置文件和创建节点。现在不能这样做，但可通过以下方式进行缓解：

* 对于内容和基于内容的配置：对创作实例进行更改并将其发布。
* 对于代码和配置：在 GIT 存储库中进行更改，然后运行 CI/CD 管道以将其推出。
* 对于与用户相关的数据（如表单提交或配置文件数据）：使用 Experience Cloud 平台或其他第三方会话感知型存储中的统一配置文件服务。

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

AEM 云服务中的资产上传、处理和下载操作已进行优化以提高效率，从而实现缩放自如，并加快上传和下载速度。但是，这可能会影响一些现有的自定义代码。

* AEM 早期版本中的默认工作流程 **DAM 资产更新**&#x200B;不再可用。
* **不进行转换**&#x200B;直接交付二进制文件的网站组件应使用直接下载。
   * Sling GET Servlet 已更改为默认执行此操作。
* **转换后**&#x200B;交付二进制文件的网站组件（例如，通过 servlet 调整大小）可以继续按原样操作。
* 通过包管理器输入的资产需要使用“资产”界面中的&#x200B;**重新处理资产**&#x200B;操作执行手动重新处理。
