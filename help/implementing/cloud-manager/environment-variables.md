---
title: Cloud Manager中的环境变量
description: 标准环境变量可以通过Cloud Manager进行配置和管理，并提供给运行时环境，用于OSGi配置。
exl-id: 5cdd5532-11fe-47a3-beb2-21967b0e43c6
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2573eb5f8a8ff21a8e30b94287b554885cd1cd89
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 28%

---


# Cloud Manager中的环境变量 {#environment-variables}

可以通过 Cloud Manager 配置和管理标准环境变量。它们提供给运行时环境，可以在OSGi配置中使用。

根据所更改的内容，环境变量可以是特定于环境的值或环境密钥。

## 关于环境变量 {#overview}

环境变量为AEM as a Cloud Service的用户提供了许多好处，例如：

* 这些变量允许代码和应用程序的行为根据上下文和环境而变化。例如，它们可用于在开发环境中启用与生产或暂存环境不同的配置，以避免代价高昂的错误。
* 它们只需要配置和设置一次，必要时可以更新和删除。
* 它们的值可以在任何时间点更新并立即生效，而无需进行任何代码更改或部署。
* 它们可以将代码与配置分离，并消除在版本控制中包含敏感信息的需要。
* 因其位于代码之外，它们提高了 AEM as a Cloud Service 应用程序的安全性。

使用环境变量的典型用例包括：

* 将 AEM 应用程序与不同的外部端点连接
* 在存储密码时使用引用，而不是直接在代码库中引用
* 当一个程序中存在多个开发环境且某个环境的某些配置不同时

## 添加环境变量 {#add-variables}

如果要添加多个变量，Adobe建议您添加第一个变量，然后在&#x200B;**环境配置**&#x200B;对话框中使用![添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **添加**&#x200B;添加其他变量。 此方法意味着您可以通过一次环境更新来添加这些变量。

要添加、更新或删除环境变量，您必须是&#x200B;[**部署管理员**&#x200B;角色](/help/onboarding/cloud-manager-introduction.md#role-based-premissions)的成员。

**添加环境变量：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要管理的程序。
1. 从侧菜单单击&#x200B;**环境**。
1. 在&#x200B;**环境**&#x200B;页面上，选择表中包含要为其添加环境变量的环境的行。
1. 在环境的详细信息页面上，单击&#x200B;**配置**&#x200B;选项卡。
1. 单击![添加/更新 — 添加圆圈图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **添加/更新**。
如果您是第一次添加环境变量，请单击页面中央的**添加配置**。

   ![配置选项卡](assets/configuration-tab.png)

1. 在&#x200B;**环境配置**&#x200B;对话框中，在表的第一行中输入详细信息。

   | 字段 | 描述 |
   | --- | --- |
   | 名称 | 配置变量的唯一名称。 它标识在环境中使用的特定变量。 它必须遵循以下命名惯例：<ul><li>变量只能包含字母数字字符和下划线(`_`)。</li><li>每个环境最多有200个变量。</li><li>每个名称的长度必须等于或少于100个字符。</li></ul> |
   | 价值 | 变量保存的值。 |
   | 已应用步骤 | 选择变量应用于的服务。 选择&#x200B;**全部**&#x200B;以将变量应用于所有服务。<ul><li>**全部**</li><li>**作者**</li><li>**Publish**</li><li>**预览**</li></ul> |
   | 类型 | 选择变量是普通变量还是密钥。 |

   ![添加变量](assets/add-variable.png)

1. 单击![添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)**添加**。

   根据需要添加其他变量。

1. 单击&#x200B;**保存**。

   状态为&#x200B;**正在更新**&#x200B;的进度环显示在表的右上角。 任何新添加的变量左侧也会显示一个旋转图标。 这些状态表示正在使用配置更新环境。 完成后，新的环境变量会显示在表中。

![更新变量](assets/updating-variables.png)

## 更新环境变量 {#update-variables}

创建环境变量后，可以使用![添加/更新 — 添加圆形图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **添加/更新**&#x200B;来更新环境变量，以打开&#x200B;**环境配置**&#x200B;对话框。

如果要更新多个变量，Adobe建议您在单击&#x200B;**保存**&#x200B;之前使用&#x200B;**环境配置**&#x200B;对话框一次更新所有必需的变量。 这样，您可以通过对环境的一次更新来添加变量。

**要更新环境变量：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要管理的程序。
1. 从侧菜单单击&#x200B;**环境**。
1. 在&#x200B;**环境**&#x200B;页面上，选择表中包含要更新变量的环境的行。
1. 在环境的详细信息页面上，单击&#x200B;**配置**&#x200B;选项卡。
1. 单击![添加/更新 — 添加圆圈图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **添加/更新**。
1. 在&#x200B;**环境配置**&#x200B;对话框中，单击要更改的变量行最后一列中的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 在下拉菜单中，单击&#x200B;**编辑**。

   ![编辑或删除变量](assets/edit-delete-variable.png)

1. 根据需要更新环境变量的值。
编辑密钥时，只能更新值，不能查看。

   ![编辑变量](assets/edit-variable.png)

1. 执行下列操作之一：

   * 单击![应用 — 复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)以应用更改。
   * 单击![撤消图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg)以撤消更改。

1. 单击&#x200B;**保存**。

   状态为&#x200B;**正在更新**&#x200B;的进度环显示在表的右上角。 旋转图标也会出现在任何已更新变量的左侧。 这些状态表示正在使用配置更新环境。 完成后，更新的环境变量将显示在表中。

## 删除环境变量 {#delete-env-variable}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要管理的程序。
1. 从侧菜单单击&#x200B;**环境**。
1. 在&#x200B;**环境**&#x200B;页面上，选择表中包含要更新变量的环境的行。
1. 在环境的详细信息页面上，单击&#x200B;**配置**&#x200B;选项卡。
1. 单击![添加/更新 — 添加圆圈图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **添加/更新**。
1. 在&#x200B;**环境配置**&#x200B;对话框中，单击要更改的变量行最后一列中的![省略号 — 更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
1. 在下拉菜单中，单击&#x200B;**删除**&#x200B;以立即删除变量。
1. 单击&#x200B;**保存**。

## 使用环境变量 {#using}

环境变量可以使您的 `pom.xml` 配置更安全、更灵活。例如，密码不需要硬编码，您的配置可以根据环境变量中的值进行调整。

您可以通过XML访问环境变量和密钥，如下所示：

`${env.VARIABLE_NAME}`

有关如何在`pom.xml`文件中同时使用这两种类型的变量的示例，请参阅[设置项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repository-support-password-protected-maven-repositories)。

有关更多详细信息，另请参阅[官方Maven文档](https://maven.apache.org/settings.html#quick-overview)。

## 环境变量的可用性 {#availability}

环境变量可在多个位置使用，如下所示：

| 可在其中使用环境变量的位置 | 描述 |
| --- | --- |
| “创作”、“预览”和“发布” | 常规环境变量和密钥均可用于创作、预览和发布环境。 |
| Dispatcher | 只有常规环境变量可用于[Dispatcher](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/dispatcher)。<ul><li>无法使用密钥。</li><li>无法在`IfDefine`指令中使用环境变量。</li><li>在部署之前，使用 [Dispatcher 在本地](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools)验证环境变量的使用情况。</li></ul> |
| OSGi 配置 | 可在[OSGi配置](/help/implementing/deploying/configuring-osgi.md)中使用常规环境变量和密钥。 |
| 管道变量 | 除了环境变量，还有在构建阶段公开的管道变量。详细了解[生成环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables)中的管道变量。 |

