---
title: 管理环境
description: 了解您可以创建的环境类型以及如何为 Cloud Manager 项目创建环境。
exl-id: 93fb216c-c4a7-481a-bad6-057ab3ef09d3
source-git-commit: 7174b398040acbf9b18b5ac2aa20fdba4f98ca78
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 100%

---

# 管理环境 {#managing-environments}

了解您可以创建的环境类型以及如何为 Cloud Manager 项目创建环境。

## 环境类型 {#environment-types}

具有必要权限的用户可以创建以下环境类型（在特定租户可用的范围内）。

* **生产和暂存** – 生产和暂存环境成对可用，分别用于生产和测试目的。

* **开发** – 开发环境可以创建用于开发和测试目的，并且只能与非生产管道相关联。


单个环境的功能取决于包含[程序中启用的解决方案。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

* [Sites](/help/sites-cloud/home.md)
* [Assets](/help/assets/home.md)
* [表单](/help/forms/home.md)
* [屏幕](/help/screens-cloud/home.md)

>[!NOTE]
>
>生产和暂存环境只能成对创建。 您不能仅创建暂存环境或生产环境。

## 添加环境 {#adding-environments}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要为其添加环境的程序。

1. 从&#x200B;**程序概述**&#x200B;页面，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**添加环境**&#x200B;以添加环境。

   ![环境信息卡](assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

      ![“环境”信息卡](assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 选择&#x200B;**环境类型**。
      * 可用/使用的环境数显示在开发环境类型后面的括号中。
   * 提供&#x200B;**环境名称**。
   * 提供&#x200B;**环境描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](assets/add-environment2.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。 现在可以为新环境设置管道。

## 环境详细信息 {#viewing-environment}

您可以使用概述页面上的&#x200B;**环境**&#x200B;信息卡，以两种方式访问环境详细信息。

1. 在&#x200B;**概述**&#x200B;页面中，单击屏幕顶部的&#x200B;**环境**&#x200B;选项卡。

   ![“环境”信息卡](assets/environments-tab2.png)

   * 或者，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**全部显示**&#x200B;按钮，直接跳转到&#x200B;**环境**&#x200B;选项卡。

      ![显示所有选项](assets/environment-showall.png)

1. **环境**&#x200B;将打开并列出程序的所有环境。

   ![“环境”选项卡](assets/environment-view-2.png)

1. 单击列表中的环境以显示其详细信息。

   ![环境详细信息](assets/environ-preview1.png)

或者，单击所需环境的省略号按钮，然后选择&#x200B;**查看详细信息**。

![查看环境详细信息](assets/view-environment-details.png)

>[!NOTE]
>
>**环境**&#x200B;信息卡仅列出三个新环境。 如前所述，单击&#x200B;**全部显示l**&#x200B;按钮，查看程序的所有环境。

### 访问预览服务 {#access-preview-service}

Cloud Manager 将预览服务（作为附加发布服务提供）提供给每个 AEM as a Cloud Service 环境。

使用该服务，您可以在网站到达实际发布环境并公开使用之前预览网站的最终体验。

创建后，预览服务将应用标记为 `Preview Default [<envId>]` 的默认 IP 允许列表，它会阻止预览服务的所有流量。 要启用访问，必须从预览服务中主动取消应用默认 IP 允许列表。

![预览服务及其允许列表](assets/preview-ip-allow.png)

具有必要权限的用户必须先完成以下选项的步骤，然后才能与您的任何团队共享预览服务 URL，以确保访问预览 URL。

1. 创建适当的 IP 允许列表，将其应用于预览服务，然后立即取消应用 `Preview Default [<envId>]` 允许列表。

   * 有关更多详细信息，请参阅文档[应用和取消应用 IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)。

1. 使用更新 **IP 允许列表**&#x200B;工作流，移除默认 IP 并根据需要添加 IP。 请参阅[管理 IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md)了解详情。

一旦对预览服务的访问被解锁，预览服务名称前面的锁定图标将不再显示。

激活后，您可以使用 AEM 中的管理发布 UI 将内容发布到预览服务。 请参阅[预览内容](/help/sites-cloud/authoring/fundamentals/previewing-content.md)文档，了解更多详细信息。

>[!NOTE]
>
>您的环境必须是 AEM 版本 `2021.05.5368.20210529T101701Z` 或更新版本。 确保更新管道已在您的环境中成功运行以执行此操作。

## 更新环境 {#updating-dev-environment}

作为云本地服务，Adobe 会自动管理生产程序中暂存和生产环境的更新。

然而，对开发环境以及沙盒程序中环境的更新是在程序中管理的。 当此类环境未运行最新的公开可用 AEM 版本时，程序&#x200B;**概述**&#x200B;屏幕上的&#x200B;**环境**&#x200B;信息状态将显示&#x200B;**可用更新**。

![环境更新状态](assets/environ-update.png)

### 更新和管道 {#updates-pipelines}

管道是[将代码部署到 AEM as a Cloud Service 环境的唯一方法。](deploy-code.md)因此，每个管道都与特定的 AEM 版本相关联。

如果 Cloud Manager 检测到有比上次随管道部署的 AEM 更新的版本可用，则会显示环境的&#x200B;**可用更新**&#x200B;状态。

因此，更新过程分为两步：

1. 使用最新 AEM 版本更新管道
1. 运行管道将新版 AEM 部署到环境中

### 更新您的环境 {#updating-your-environments}

单击环境的省略号按钮，可从用于开发环境和沙盒程序环境的&#x200B;**环境**&#x200B;信息卡中获得&#x200B;**更新**&#x200B;选项。

![从“环境”信息卡更新选项](assets/environ-update2.png)

单击程序的&#x200B;**环境**&#x200B;选项卡，然后选择环境的省略号按钮，也可以使用此选项。

![从“环境”选项卡更新选项](assets/environ-update3.png)

具有&#x200B;**部署管理员**&#x200B;角色的用户可以使用此选项将与此环境关联的管道更新为最新的 AEM 版本。

管道版本更新为最新的公开可用 AEM 版本后，系统会提示用户运行关联的管道，将最新版本部署到环境中。

![提示运行管道可更新环境](assets/update-run-pipeline.png)

**更新**&#x200B;选项的行为因程序的配置和当前状态而异。

* 如果管道已经更新，则&#x200B;**更新**&#x200B;选项会提示用户执行管道。
* 如果管道已在更新中，则&#x200B;**更新**&#x200B;选项会通知用户更新已在运行。
* 如果不存在合适的管道，则&#x200B;**更新**&#x200B;选项会提示用户创建一个管道。

## 删除开发环境 {#deleting-environment}

具有必要权限的用户将能够删除开发环境。

在&#x200B;**环境**&#x200B;信息卡的程序&#x200B;**概述**&#x200B;屏幕上，单击要删除的开发环境的省略号按钮。

![删除选项](assets/environ-delete.png)

在程序&#x200B;**概述**&#x200B;窗口的&#x200B;**环境**&#x200B;选项卡上，也可以使用该删除选项。单击环境的省略号按钮，然后选择&#x200B;**删除**。

![“环境”选项卡上的删除选项](assets/environ-delete2.png)

>[!NOTE]
>
>* 无法删除在生产程序中创建的生产和暂存环境。
>* 可以删除沙盒程序中的生产和暂存环境。


## 管理访问权限 {#managing-access}

从&#x200B;**环境**&#x200B;信息卡上环境的省略号菜单中选择&#x200B;**管理访问权限**。 您可以直接导航到作者实例并管理对环境的访问权限。

![管理访问权限选项](assets/environ-access.png)

## 访问开发人员控制台 {#accessing-developer-console}

从&#x200B;**环境**&#x200B;信息卡上环境的省略号菜单中选择&#x200B;**开发人员控制台**。 该操作将在浏览器中打开一个新选项卡，登录页面位于&#x200B;**开发人员控制台**。

![](assets/environ-devconsole.png)

只有具有&#x200B;**开发人员**&#x200B;角色的用户才能访问&#x200B;**开发人员控制台**。 但是，对于沙盒程序来说，任何有权访问沙盒程序的用户都可以访问&#x200B;**开发人员控制台**。

有关详细信息，请参阅文档[使沙盒环境休眠和解除沙盒环境休眠](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction)。

单击单个环境的省略号菜单时，也可以从&#x200B;**概述**&#x200B;窗口的&#x200B;**环境**&#x200B;选项卡中找到此选项。

## 本地登录 {#login-locally}

从&#x200B;**环境**&#x200B;信息卡中的省略号菜单中选择&#x200B;**本地登录** ，可本地登录到 Adobe Experience Manager。

![本地登录](assets/environ-login-locally.png)

此外，您可以从&#x200B;**概述**&#x200B;页面的&#x200B;**环境**&#x200B;选项卡中本地登录。

![从“环境”选项卡本地登录](assets/environ-login-locally-2.png)

## 管理自定义域名 {#manage-cdn}

在 Cloud Manager for Sites 程序中，发布和预览网站服务程序都支持自定义域名。 每个 Cloud Manager 环境最多可以为环境托管 250 个自定义域。

要配置自定义域名，请导航到&#x200B;**环境**&#x200B;选项卡，然后单击环境查看环境详细信息。

![环境详细信息](assets/domain-names.png)

可以对您环境的发布服务执行以下操作。

* [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

* [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)

* [检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的状态或 [SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)。

* [管理 IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)


## 管理 IP 允许列表 {#manage-ip-allow-lists}

Cloud Manager 支持针对 Sites 程序的作者、发布和预览服务的 IP 允许列表。

要管理 IP 允许列表，请导航到程序的&#x200B;**概述**&#x200B;页面的&#x200B;**环境**&#x200B;选项卡。 单击单个环境管理其详细信息。

### 应用 IP 允许列表 {#apply-ip-allow-list}

应用 IP 允许列表将允许列表定义中包含的所有 IP 范围与环境中的作者或发布服务相关联。 必须登录具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户才能应用 IP 允许列表。

IP 允许列表必须存在于 Cloud Manager 中，才能将其应用于环境。 要了解有关 Cloud Manager 中 IP 允许列表的更多信息，请参阅文档 [Cloud Manager 中的 IP 允许列表简介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

按照以下步骤应用 IP 允许列表。

1. 从程序&#x200B;**概述**&#x200B;屏幕的&#x200B;**环境**&#x200B;选项卡中导航到特定环境，然后导航到 **IP 允许列表**&#x200B;表格。
1. 使用 IP 允许列表表顶部的输入字段选择 IP 允许列表以及要应用它的作者或发布服务。
1. 单击&#x200B;**应用**，并确认您的提交。

### 取消应用 IP 允许列表 {#unapply-ip-allow-list}

取消应用 IP 允许列表会将允许列表定义中包含的所有 IP 范围与环境中的作者或发布者服务解除关联。 必须登录具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户才能取消应用 IP 允许列表。

按照以下步骤取消应用 IP 允许列表。

1. 从程序&#x200B;**概述**&#x200B;屏幕的&#x200B;**环境**&#x200B;选项卡中导航到特定环境，然后导航到 **IP 允许列表**&#x200B;表格。
1. 确定列出要取消应用的 IP 允许列表规则的行。
1. 从行末选择省略号按钮。
1. 单击&#x200B;**取消应用**，并确认您的提交。
