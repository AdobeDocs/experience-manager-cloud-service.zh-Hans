---
title: 管理环境-Cloud Service
description: 管理环境-Cloud Service
translation-type: tm+mt
source-git-commit: 1304a0cfa67c38943b1a36c105fbd5eafb3f8c4f
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 4%

---


# 管理环境 {#manage-environments}

以下部分介绍用户可以创建的环境类型以及用户可以如何创建环境。

## 环境类型{#environment-types}

具有必需权限的用户可以创建以下环境类型（在特定租户可用的范围内）。

* **生产和阶段环境**:生产和阶段可作为两个对象提供，用于测试和生产目的。

* **开发**:开发环境可以创建用于开发和测试目的，并且仅与非生产管道相关。

   >[!NOTE]
   >在沙箱项目中自动创建的开发环境将配置为包括站点和资产解决方案。

   下表汇总了环境类型及其属性：

   | 名称 | 创作层 | 发布层 | 用户可以创建 | 用户可以删除 | 可与环境关联的管道 |
   |--- |--- |--- |--- |---|---|
   | 生产 | 是 | 是 如果包含站点 | 是 | 否 | 生产管道 |
   | 暂存 | 是 | 是 如果包含站点 | 是 | 否 | 生产管道 |
   | 开发 | 是 | 是 如果包含站点 | 是 | 是 | 非生产管道 |

   >[!NOTE]
   >生产和阶段可作为两个对象提供，用于测试和生产目的。  用户将不能仅创建舞台或仅创建生产环境。

## 添加环境{#adding-environments}

1. 单击&#x200B;**添加环境**&#x200B;以添加环境。 此按钮可从&#x200B;**环境**屏幕访问。
   ![](assets/environments-tab.png)

   **添加环境**&#x200B;选项也可用于&#x200B;**环境**&#x200B;卡，当项目中有零环境时。

   ![](assets/no-environments.png)

   >[!NOTE]
   >将根据缺少权限或合同内容禁用&#x200B;**添加环境**&#x200B;选项。

1. 出现 **“添加环境** ”对话框。用户需要提交详细信息，如“环境类型 **”和“环境名称********** ”和“环境描述”（具体取决于用户在特定租户可用的范围内创建环境时的目标）。

   ![](assets/add-environment2.png)

   >[!NOTE]
   >创建环境时，在Adobe I/O创建一个或多个&#x200B;*集成*。对于有权访问Adobe I/O控制台的客户用户可见，且不得删除这些控制台。 在Adobe I/O控制台的说明中不会声明此问题。

   ![](assets/add-environment-image1.png)

1. 单击&#x200B;**保存**&#x200B;以添加具有已填充条件的环境。  现在，*概述*&#x200B;屏幕显示可从中设置管道的卡。

   >[!NOTE]
   >如果尚未设置非生产管道，*概述*&#x200B;屏幕将显示卡，您可以从中创建非生产管道。


## 查看环境{#viewing-environment}

“概述”页上的&#x200B;**环境**&#x200B;卡最多列表三个环境。

1. 选择&#x200B;**显示全部**&#x200B;按钮，导航至&#x200B;**环境**&#x200B;摘要页，以视图具有完整环境列表的表。

   ![](assets/environment-view-1.png)

1. **环境**&#x200B;页显示所有现有环境的列表。

   ![](assets/environment-view-2.png)

1. 从环境中选择任一列表以视图环境详细信息。

   ![](assets/environment-view-3.png)


## 更新环境{#updating-dev-environment}

舞台和生产环境的更新由Adobe自动管理。

开发环境的更新由项目的用户管理。 当环境未运行最新的公开发行的AEM版本时，主屏幕上的环境卡状态将显示&#x200B;**UPDATE AVAILABLE**。

![](assets/environ-update.png)


**更新**&#x200B;选项可从&#x200B;**环境**卡中访问。
如果单击**环境卡**&#x200B;中的&#x200B;**详细信息**，则此选项也可用。 **环境**&#x200B;页面将打开，选择“开发”环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**更新**，如下图所示：

![](assets/environ-update2.png)

选择此选项将允许部署管理器将与此环境关联的管道更新到最新版本，然后执行该管道。

如果管道已更新，则提示用户执行管道。

## 删除环境{#deleting-environment}

具有必要权限的用户将能够删除开发环境。

**删除**&#x200B;选项可从&#x200B;**环境卡**&#x200B;的下拉菜单中访问。 单击&#x200B;**...**，用于要删除的开发环境。

![](assets/environ-delete.png)

如果单击&#x200B;**环境卡**&#x200B;中的&#x200B;**详细信息**，则删除选项也可用。 **环境**&#x200B;页面将打开，选择“开发”环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**删除**，如下图所示：

![](assets/environ-delete2.png)


>[!NOTE]
>
>此功能不适用于为生产目的而设置的常规环境中的生产／阶段项目集。 但是，该功能可用于沙箱环境中的生产／阶段项目。

## 管理访问{#managing-access}

从&#x200B;**环境卡**&#x200B;的下拉菜单中选择&#x200B;**管理访问**。 您可以直接导航到作者实例并管理环境的访问权限。

请参阅[管理对作者实例的访问权](/help/onboarding/getting-access-to-aem-in-cloud/navigation.md#manage-access-aem)以了解更多。

![](assets/environ-access.png)


## 访问开发人员控制台{#accessing-developer-console}

从&#x200B;**环境卡**&#x200B;的下拉菜单中选择&#x200B;**开发人员控制台**。 这将在您的浏览器中打开一个新选项卡，登录页面指向&#x200B;**开发人员控制台**。

只有具有“开发人员”角色的用户才能访问&#x200B;**“开发人员控制台”**。 沙箱项目例外，在沙箱项目中，有权访问Cloud Manager Sandbox的任何用户都将有权访问&#x200B;**开发人员控制台**。

有关详细信息，请参阅[冬眠和脱冬眠沙箱环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/sandbox-programs.html#hibernating-introduction)。


![](assets/environ-devconsole.png)

如果单击&#x200B;**环境卡**&#x200B;中的&#x200B;**详细信息**，则此选项也可用。 将打开&#x200B;**环境**&#x200B;页，选择环境后，单击&#x200B;**...**&#x200B;并选择&#x200B;**开发人员控制台**。

## 本地登录{#login-locally}

从&#x200B;**环境卡**&#x200B;的下拉菜单中选择&#x200B;**本地登录**&#x200B;以本地登录到Adobe Experience Manager。

![](assets/environ-login-locally.png)

此外，您还可以从&#x200B;**环境**&#x200B;摘要页面本地登录。

![](assets/environ-login-locally-2.png)

## 管理自定义域名{#manage-cdn}

从“环境摘要”页面导航到&#x200B;**环境**&#x200B;详细信息页面。

可以对环境的发布服务执行以下操作，如下所述：

1. [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. [查看和更新自定义域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)

1. [删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md)

## 管理IP允许列表{#manage-ip-allow-lists}

从“环境摘要”页面导航到环境详细信息页面。 您可以在此处对您的环境的发布和／或作者服务执行以下操作。

### 应用IP允许列表{#apply-ip-allow-list}

应用IP允许列表是将“允许列表”定义中包含的所有IP范围与环境中的作者或发布服务相关联的过程。 必须登录“业务所有者”或“部署管理者”角色的用户，才能应用IP允许列表。

>[!NOTE]
>IP允许列表必须存在于云管理器中，才能将其应用于环境服务。 要进一步了解Cloud Manager中的IP允许列表，请导航至Cloud Manager中的[IP允许列表简介](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

请按照以下步骤应用IP允许列表:

1. 从&#x200B;**环境**&#x200B;详细信息页面导航到特定环境，然后导航到&#x200B;**IP允许列表**&#x200B;表。
1. 使用IP允许列表表顶部的输入字段选择IP允许列表以及要将其应用到的创作或发布服务。
1. 单击&#x200B;**应用**&#x200B;并确认您的提交。

### 取消应用IP允许列表{#unapply-ip-allow-list}

取消应用IP允许列表是将允许列表定义中包含的所有IP范围与环境中的作者或发布者服务取消关联的过程。 必须登录“业务所有者”或“部署管理者”角色的用户，才能取消应用IP允许列表。

请按照以下步骤取消应用IP允许列表:

1. 从“环境”屏幕导航到特定的&#x200B;**环境**&#x200B;详细信息页面，然后导航到&#x200B;**IP允许列表**&#x200B;表。
1. 确定要取消应用的IP允许列表规则所在的行。
1. 选择&#x200B;**...**&#x200B;菜单。
1. 选择&#x200B;**取消应用**&#x200B;选项并确认您的提交。


