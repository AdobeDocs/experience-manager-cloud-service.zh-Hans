---
title: 授予的访问权限 — 必需
description: 授予的访问权限 — 必需
translation-type: tm+mt
source-git-commit: 4b62401fd1d0654cf758092176bd815a7fa56159
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 9%

---


# 已授予的访问权限 {#access-rights-granted}

Adobe将在Adobe Identity Management系统(IMS)中为您的公司创建&#x200B;**组织**&#x200B;标识符，可以在其中管理您的所有用户及其权限。 每个用户(需要是此组织的成员，并将获得对任何[!UICONTROL Experience Cloud]服务的访问权)都需要拥有自己的&#x200B;**Adobe ID**。

## 用户标识类型{#user-identity-types}

要开始使用Adobe ID，请访问[管理Adobe身份类型](https://helpx.adobe.com/enterprise/using/identity.html)，了解有关如何使用可用身份类型之一获取Adobe ID的详细说明。

## 用户和角色{#users-and-roles}

Adobe为您的公司创建了组织后，您指定的管理员将作为该组织的第一个成员添加。 默认情况下，管理员将获得管理员权限，并分配 [!UICONTROL AEM 托管服务]、**产品**&#x200B;以及一个或多个 [!UICONTROL Cloud Manager] **产品配置文件**。

1. 当您的系统管理员授予您对Cloud Manager的访问权限后，您将收到一封电子邮件，将带您进入Cloud Manager登录页面，也可通过[Adobe Experience Cloud](https://my.cloudmanager.adobe.com/)访问该页面。

1. 在云管理器的登陆页中，单击&#x200B;**管理访问**。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. 单击&#x200B;**管理访问**&#x200B;后，您将导航到&#x200B;**Admin Console**，从中可以管理用户角色或对云管理器的权限。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   在Admin Console中，您可以执行SysAdmin任务，例如：
   * [管理角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [管理对作者实例的访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

      >[!NOTE]
      >请访问[用户和角色](#users-roles)部分，进一步了解Cloud Manager中的用户和角色定义。

授予这些权限后，管理员现在可通过单一登录(使用Adobe ID)设置以访问[!UICONTROL Experience Cloud]服务、登录AEM云环境并使用[!UICONTROL 云管理器]。

## 用户和角色{#users-roles}

[!UICONTROL 云管理器]中的许多功能需要特定权限才能运行。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义四个角色：

* 业务所有者
* 项目 Manager
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用[!UICONTROL 云管理器]，您必须将Adobe ID和Adobe Experience Manager作为Cloud Service产品上下文。

### 角色定义{#role-definitions}

>[!NOTE]
>
>Admin Console中的“开发人员”角色与[!UICONTROL 云管理器]中的“开发人员”角色无关。

下表总结了这些角色：

| [!UICONTROL Cloud ] Manager角色 | 描述 |
|--- |--- |
| 业务所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 项目 Manager | 使用[!UICONTROL Cloud Manager]执行团队设置、审核状态和视图KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使用[!UICONTROL Cloud Manager]执行舞台/生产部署。 可以编辑CI/CD管道。 可以批准重要的3层故障。 可获取对Git存储库的访问权限。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使用[!UICONTROL 云管理器]来视图状态。 可获取对Git存储库的代码提交访问权限。 |
| 内容作者 | 通常不与[!UICONTROL 云管理器]交互。 可以使用[!UICONTROL 云管理器]项目切换器(已从[!UICONTROL Experience Cloud]导航)访问AEM。 |

### 集成产品用户档案{#integration-product-profile}

除上述功能外，Cloud Manager还将自动创建一个名为“集成 — Cloud Service”的产品用户档案。 此产品用户档案用于Adobe Experience Manager与其他Adobe产品之间的集成。 不能删除此产品用户档案&#x200B;****。 如果意外删除了此用户档案，则需要手动重新创建它。 此用户档案&#x200B;**的显示名称必须**&#x200B;为`CM_CS_DEFAULT`。

