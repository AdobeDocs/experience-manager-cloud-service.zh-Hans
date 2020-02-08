---
title: 对Adobe Experience Manager(AEM)云服务的显着更改
description: 对Adobe Experience Manager(AEM)云服务的显着更改
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# 对Adobe Experience Manager(AEM)云服务的显着更改 {#notable-changes-aem-cloud}

AEM cloud服务为管理AEM项目提供了许多新功能和可能性。 但是，与AEM云服务相比，AEM Sites内部部署或Adobe Managed service中存在许多差异。 本文档突出强调了重要差异。

>[!NOTE]
>本文档重点介绍了对AEM整体的显着更改。 有关特定于解决方案的更改，请参阅：
>
>* [对AEM cloud服务中的AEM Sites的显着更改](/help/sites-cloud/sites-cloud-changes.md)
>* [对AEM cloud服务中的AEM资产进行的显着更改](/help/assets/assets-cloud-changes.md)


主要区别在以下方面：

* [/apps和/libs在运行时不可更改](#apps-libs-immutable)
* [OSGi捆绑套件和设置必须基于存储库](#osgi)
* [不允许更改发布存储库](#changes-to-publish-repo)
* [不允许自定义运行模式](#custom-runmodes)
* [删除复制代理](#replication-agents)
* [删除经典UI](#classic-ui)
* [发布端交付](#publish-side-delivery)
* [资产处理和交付](#asset-handling)

## /apps和/libs在运行时不可更改 {#apps-libs-immutable}

和中的任何内容和子文 `/apps` 件 `/libs` 夹都是只读的。 任何希望进行更改的功能或自定义代码都将无法进行更改。 将返回一个错误，该错误导致此类内容为只读且写操作无法完成。 这在AEM的许多方面都有影响：

* 完全不允 `/libs` 许更改。
   * 这不是新规则，但是在AEM的先前内部部署版本中未实施。
* 允许覆盖 `/libs` 的区域的叠加仍允许在内 `/apps`。
   * 此类叠加必须通过CI/CD管道从Git获得。
* 无法通过UI编辑存储在中 `/apps` 的静态模板设计信息。
   * 建议您改用“可编辑模板”。
   * 如果仍需要静态模板，配置信息必须通过CI/CD管道从Git获得。
* MSM Blueprint和自定义MSM推出配置必须通过CI/CD管道从Git安装。
* I18n翻译更改需要通过CI/CD管道从Git进行。

## OSGi捆绑套件和设置必须基于存储库 {#osgi}

在AEM的早期版本中用于更改OSGi设置的Web控制台在AEM云服务中不可用。 因此，必须通过CI/CD管道引入对OSGi的更改。

* 对OSGi设置的更改只能通过Git持久性作为基于JCR的OSGi设置进行。
* 新的或更新的OSGi捆绑套件必须通过Git作为CI/CD管道构建流程的一部分引入。

## 不允许更改发布存储库 {#changes-to-publish-repo}

AEM cloud服务不允许直接更改发布存储库。 在AMS上的先前版本内部部署AEM或AEM中，可以直接对发布存储库进行代码更改，例如创建用户、更新用户配置文件和创建节点。 这已不可能，可通过以下方式缓解：

* 对于基于内容和内容的配置：对作者实例进行更改并发布。
* 对于代码和配置：在GIT存储库中进行更改，然后运行CI/CD管道以将其推出。
* 对于与用户相关的数据，如表单提交或配置文件数据：使用Experience Cloud Platform或其他第三方会话感知型商店中的统一配置文件服务。

## 不允许自定义运行模式 {#custom-runmodes}

AEM Cloud service现成可用的运行模式如下：

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

AEM Cloud service中不能使用其他或自定义运行模式。

## 删除复制代理 {#replication-agents}

在AEM cloud服务中，内容使用 [Sling内容分发进行发布](https://sling.apache.org/documentation/bundles/content-distribution.html)。 不再使用或提供在旧版AEM中使用的复制代理，这可能会影响现有AEM项目的以下区域：

* 例如，将内容推送到预览服务器的复制代理的自定义工作流。
* 自定义复制代理以转换内容
* 使用反向复制将内容从发布引回创作

## 删除经典UI {#classic-ui}

经典UI在AEM云服务中不再可用。

## 发布端交付 {#publish-side-delivery}

默认情况下，AEM云服务中提供HTTP加速，包括创作和发布服务的CDN和流量管理。

对于从AMS或内部安装进行项目转换，Adobe强烈建议利用内置CDN，因为AEM Cloud service中的功能已针对提供的CDN进行了优化。

## 资产处理和交付 {#asset-handling}

资产上传、处理和下载已在AEM云服务中进行了优化，以提高效率，从而实现更好的扩展和更快的上传和下载。 但是，这可能会影响一些现有的自定义代码。

* AEM早期版本 **中的默认工作流** DAM资产更新不再可用。
* 提供二进制而无需转换的网站 **组件** ，应使用直接下载。
   * 默认情况下，Sling GET Servlet已更改为执行此操作。
* 提供具有转换的二进制文 **件的网站组件** （例如，通过servlet调整大小）可以继续按原样运行。
* 通过包管理器导入的资产需要使用资产界面中的重新处理 **资产操作** ，手动进行重新处理。
