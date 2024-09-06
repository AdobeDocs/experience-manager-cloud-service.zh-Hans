---
title: Cloud Manager 环境变量
description: 标准环境变量可以通过 Cloud Manager 进行配置和管理，并提供给运行时环境，以便在 OSGi 配置中使用。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 76%

---


# Cloud Manager 环境变量 {#environment-variables}

可以通过 Cloud Manager 配置和管理标准环境变量。这些变量提供给运行时环境，可以在 OSGi 配置中使用。根据所更改的内容，环境变量可以是特定于环境的值或环境密钥。

## 概述 {#overview}

环境变量为 AEM as a Cloud Service 的用户提供了许多好处：

* 这些变量允许代码和应用程序的行为根据上下文和环境而变化。例如，它们可以用于在开发环境中启用与生产或暂存环境不同的配置，以避免代价高昂的错误。
* 它们只需要配置和设置一次，必要时可以更新和删除。
* 它们的值可以在任何时间点更新并立即生效，而无需进行任何代码更改或部署。
* 它们可以将代码与配置分离，并消除在版本控制中包含敏感信息的需要。
* 因其位于代码之外，它们提高了 AEM as a Cloud Service 应用程序的安全性。

使用环境变量的典型用例包括：

* 将 AEM 应用程序与不同的外部端点连接
* 在存储密码时使用引用，而不是直接在代码库中引用
* 当一个程序中存在多个开发环境且某个环境的某些配置不同时

## 添加环境变量 {#add-variables}

>[!NOTE]
>
>您必须是&#x200B;[**部署管理员**&#x200B;角色](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)成员，才能添加或修改环境变量。

1. 登录 Adobe Cloud Manager，网址为 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要管理的程序。
1. 从侧面导航栏中，为所选程序选择&#x200B;**环境**&#x200B;窗口，然后选择要为其创建环境变量的环境。
1. 在环境的详细信息中，选择&#x200B;**配置**&#x200B;选项卡，然后选择&#x200B;**添加**，打开&#x200B;**环境配置**&#x200B;对话框。
   * 如果您是第一次添加环境变量，则可以在页面中央看到&#x200B;**添加配置**&#x200B;按钮。 您可以使用此按钮或&#x200B;**添加**&#x200B;功能，打开&#x200B;**环境配置**&#x200B;对话框。

   ![配置选项卡](assets/configuration-tab.png)

1. 输入变量详细信息。
   * **名称**
   * **值**
   * **已应用服务** — 定义变量适用于哪个服务(作者/Publish/预览)，或者是否适用于所有服务
   * **类型** – 定义变量是普通变量还是密钥

   ![添加变量](assets/add-variable.png)

1. 输入新变量后，必须在包含新变量的行的最后一列中选择&#x200B;**添加**。
   * 通过输入新行并选择&#x200B;**添加**，可以一次输入多个变量。

   ![保存变量](assets/save-variables.png)

1. 选择&#x200B;**保存**&#x200B;来保存变量。

状态为&#x200B;**更新**&#x200B;的指标显示在表的顶部和新添加的变量旁边，表示正在使用配置更新环境。完成后，新的环境变量会显示在表中。

![更新变量](assets/updating-variables.png)

>[!TIP]
>
>如果要添加多个变量，建议添加第一个变量，然后使用&#x200B;**环境配置**&#x200B;对话框中的&#x200B;**添加**&#x200B;按钮添加其他变量。 这样，您可以通过对环境的一次更新来添加变量。

## 更新环境变量 {#update-variables}

创建环境变量后，您可以使用&#x200B;**添加/更新**&#x200B;按钮来更新这些变量，从而启动&#x200B;**环境配置**&#x200B;对话框。

1. 登录 Adobe Cloud Manager，网址为 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。
1. Cloud Manager 列出了可用的各种项目。选择要管理的项目。
1. 在导航面板中，为所选程序选择&#x200B;**环境**&#x200B;窗口，然后选择要为其修改环境变量的环境。
1. 在环境的详细信息中，选择&#x200B;**配置**&#x200B;选项卡，然后在右上方选择&#x200B;**添加/更新**，打开&#x200B;**环境配置**&#x200B;对话框。
1. 使用要修改的变量行最后一列中的省略号按钮，选择&#x200B;**编辑**&#x200B;或&#x200B;**删除**。

   ![编辑或删除变量](assets/edit-delete-variable.png)

1. 根据需要编辑环境变量。
   * 编辑时，省略号按钮将更改为选项，恢复到原始值或确认更改。
   * 编辑密钥时，只能更新值，不能查看。

   ![编辑变量](assets/edit-variable.png)

1. 完成所需的配置更改后，选择&#x200B;**保存**。

[当添加变量时](#add-variables)，状态为&#x200B;**更新**&#x200B;的指标会显示在表的顶部和新更新的变量旁边，表示正在使用该配置更新环境。完成后，更新的环境变量会显示在表中。

>[!TIP]
>
>如果要更新多个变量，建议使用&#x200B;**环境配置**&#x200B;对话框在点击或单击&#x200B;**保存**&#x200B;之前一次更新所有必要的变量。 这样，您可以通过对环境的一次更新来添加变量。

## 使用环境变量 {#using}

环境变量可以使您的 `pom.xml` 配置更安全、更灵活。例如，密码不需要硬编码，您的配置可以根据环境变量中的值进行调整。

您可以通过 XML 访问环境变量和密钥，如下所示。

* `${env.VARIABLE_NAME}`

有关如何在 `pom.xml` 文件中同时使用这两种类型的变量的示例，请参阅文档[设置项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)。

有关更多详细信息，请参阅[Maven 官方文档](https://maven.apache.org/settings.html#quick-overview)。

## 环境变量可用性 {#availability}

可在多个位置使用环境变量。

### “创作”、“预览”和“发布” {#author-preview-publish}

常规环境变量和密钥均可用于创作、预览和发布环境。

### Dispatcher {#dispatcher}

只有常规环境变量可用于[调度程序](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)密钥。

但是，无法在 `IfDefine` 指令中使用环境变量。

>[!TIP]
>
>应验证可将环境变量[在本地用于 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html) 后再部署。

### OSGi 配置 {#osgi}

可在 [OSGi 配置](/help/implementing/deploying/configuring-osgi.md)中使用常规环境变量和密钥。

### 管道变量 {#pipeline}

除了环境变量，还有在构建阶段公开的管道变量。了解有关[生成环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)下的管道变量的更多信息。
