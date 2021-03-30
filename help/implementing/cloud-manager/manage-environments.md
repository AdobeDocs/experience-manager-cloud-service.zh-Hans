---
title: 管理环境-Cloud Service
description: 管理环境-Cloud Service
translation-type: tm+mt
source-git-commit: 1aca6f0b23aa328ca364f7ab1d4c722bb5cbca9a
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 4%

---


# 管理环境 {#manage-environments}

以下部分介绍用户可以创建的环境类型以及用户可以创建环境的方式。

## 环境类型{#environment-types}

具有必要权限的用户可以创建以下环境类型（在特定租户可用内容的范围内）。

* **生产和阶段环境**:生产和舞台可作为两个组件提供，并用于测试和生产目的。

* **开发**:开发环境可以创建用于开发和测试目的，并且仅与非生产管道相关。

   >[!NOTE]
   >将配置在沙箱项目中自动创建的开发环境，以包括站点和资产解决方案。

   下表总结了环境类型及其属性：

   | 名称 | 创作层 | 发布层 | 用户可以创建 | 用户可以删除 | 可与环境关联的管道 |
   |--- |--- |--- |--- |---|---|
   | 生产 | 是 | 是 如果包含站点 | 是 | 否 | 生产管道 |
   | 暂存 | 是 | 是 如果包含站点 | 是 | 否 | 生产管道 |
   | 开发 | 是 | 是 如果包含站点 | 是 | 是 | 非生产管道 |

   >[!NOTE]
   >生产和舞台可作为两个组件提供，并用于测试和生产目的。  用户将不能仅创建舞台或仅创建生产环境。

## 添加环境{#adding-environments}

1. 单击&#x200B;**添加环境**&#x200B;以添加环境。 此按钮可从&#x200B;**环境**屏幕访问。
   ![](assets/environments-tab.png)

   **添加环境**&#x200B;选项也可用于&#x200B;**环境**&#x200B;卡(当项目中没有环境时)。

   ![](assets/no-environments.png)

   >[!NOTE]
   >将根据缺少权限或可能签订合同禁用&#x200B;**添加环境**&#x200B;选项。

1. 出现 **“添加环境** ”对话框。用户需要提交详细信息，如“环境类型 **”和“环境名称********** ”和“环境描述”（具体取决于用户在特定租户可用的范围内创建环境时的目标）。

   ![](assets/add-environment2.png)

   >[!NOTE]
   >创建环境时，将在Adobe I/O中创建一个或多个&#x200B;*集成*。对于有权访问Adobe I/O Console的客户用户可见，且不得删除。 在“Adobe I/O”控制台的说明中不会声明。

   ![](assets/add-environment-image1.png)

1. 单击&#x200B;**保存**&#x200B;以添加具有已填充条件的环境。  现在，*概述*&#x200B;屏幕显示可从中设置管道的卡。

   >[!NOTE]
   >如果尚未设置非生产管道，则&#x200B;*概述*&#x200B;屏幕将显示卡，您可以从中创建非生产管道。


## 查看环境{#viewing-environment}

“概述”页上的&#x200B;**环境**&#x200B;卡最多列表三个环境。

1. 选择&#x200B;**显示全部**&#x200B;按钮，导航到&#x200B;**环境**&#x200B;摘要页，以用完整的环境列表视图表。

   ![](assets/environment-view-1.png)

1. **环境**&#x200B;页显示所有现有环境的列表。

   ![](assets/environment-view-2.png)

1. 从列表中选择任一环境以视图环境详细信息。

   ![](assets/environment-view-3.png)


## 更新环境{#updating-dev-environment}

舞台和生产环境的更新由Adobe自动管理。

开发环境的更新由项目的用户管理。 当环境未运行最新的公开发行的AEM版本时，主屏幕上的环境卡状态将显示&#x200B;**UPDATE AVAILABLE**。

![](assets/environ-update.png)


**更新**&#x200B;选项可从&#x200B;**环境**卡中访问。
如果单击**环境**&#x200B;卡中的&#x200B;**详细信息**，则此选项也可用。 将打开&#x200B;**环境**&#x200B;页面，选择“开发”环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**更新**，如下图所示：

![](assets/environ-update2.png)

选择此选项将允许部署管理器将与此环境关联的管道更新到最新版本，然后执行该管道。

如果管道已更新，则提示用户执行该管道。

## 删除环境{#deleting-environment}

具有必要权限的用户将能够删除开发环境。

**删除**&#x200B;选项可从&#x200B;**环境**&#x200B;卡的下拉菜单中访问。 单击&#x200B;**...**，用于要删除的开发环境。

![](assets/environ-delete.png)

如果单击&#x200B;**环境**&#x200B;卡中的&#x200B;**详细信息**，则也可以使用删除选项。 将打开&#x200B;**环境**&#x200B;页面，选择“开发”环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**删除**，如下图所示：

![](assets/environ-delete2.png)


>[!NOTE]
>
>此功能不适用于为生产目的而设置的生产项目中的生产/阶段环境集。 但是，此功能可用于沙箱项目中的生产/舞台环境。

## 管理访问{#managing-access}

从&#x200B;**环境**&#x200B;卡的下拉菜单中选择&#x200B;**管理访问**。 您可以直接导航到创作实例并管理环境的访问权限。

有关详细信息，请参阅[管理对作者实例的访问](/help/onboarding/what-is-required/accessing-aem-instance.md)。

![](assets/environ-access.png)


## 访问开发人员控制台{#accessing-developer-console}

从&#x200B;**环境卡**&#x200B;的下拉菜单中选择&#x200B;**开发人员控制台**。 这将在您的浏览器中打开一个新选项卡，登录页指向&#x200B;**开发人员控制台**。

只有“开发人员”角色的用户才有权访问&#x200B;**“开发人员控制台”**。 沙箱项目的例外情况，在沙箱项目中，有权访问Cloud Manager Sandbox的任何用户都将有权访问&#x200B;**开发人员控制台**。

有关详细信息，请参阅[冬眠和脱冬沙箱环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction)。


![](assets/environ-devconsole.png)

如果单击&#x200B;**环境**&#x200B;卡中的&#x200B;**详细信息**，则此选项也可用。 将打开&#x200B;**环境**&#x200B;页面，选择环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**开发人员控制台**。

## 本地登录{#login-locally}

从&#x200B;**环境**&#x200B;卡片的下拉菜单中选择&#x200B;**本地登录**&#x200B;以本地登录Adobe Experience Manager。

![](assets/environ-login-locally.png)

此外，您还可以从&#x200B;**环境**&#x200B;摘要页本地登录。

![](assets/environ-login-locally-2.png)

## 管理自定义域名{#manage-cdn}

从“环境摘要”页面导航到&#x200B;**环境**&#x200B;详细信息页面。

可以对环境的发布服务执行以下操作，如下所述：

1. [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [查看和更新自定义域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

1. [正在检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 或SSL证 [书的状态](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)。

1. [检查IP允许列表的状态](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)

## 管理IP允许列表{#manage-ip-allow-lists}

从“环境摘要”页面导航到环境详细信息页面。 您可以在此处对您的环境的发布和/或作者服务执行以下操作。

### 应用IP允许列表{#apply-ip-allow-list}

应用IP允许列表是将允许列表定义中的所有IP范围与环境中的作者或发布服务关联的过程。 必须登录业务所有者或部署管理者角色中的用户才能应用IP允许列表。

>[!NOTE]
>IP允许列表必须存在于云管理器中，才能将其应用于环境服务。 要进一步了解Cloud Manager中的IP允许列表，请导航至[ Cloud Manager中的IP允许列表简介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

请按照以下步骤应用IP允许列表:

1. 从&#x200B;**环境**&#x200B;详细信息页导航到特定环境，然后导航到&#x200B;**IP允许列表**&#x200B;表。
1. 使用IP允许列表表顶部的输入字段选择IP允许列表以及要应用它的作者或发布服务。
1. 单击&#x200B;**应用**&#x200B;并确认您的提交。

### 取消应用IP允许列表{#unapply-ip-allow-list}

取消应用IP允许列表是将允许列表定义中包含的所有IP范围与环境中的作者或发布者服务取消关联的过程。 必须登录业务所有者或部署管理器角色中的用户，才能取消应用IP允许列表。

请按照以下步骤取消应用IP允许列表:

1. 从“环境”屏幕导航到特定的&#x200B;**环境**&#x200B;详细信息页，然后导航到&#x200B;**IP允许列表**&#x200B;表。
1. 确定要取消应用的IP允许列表规则所在的行。
1. 选择&#x200B;**...**&#x200B;菜单。
1. 选择&#x200B;**取消应用**&#x200B;选项并确认您的提交。


