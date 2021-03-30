---
title: '添加用户和分配云管理器角色 '
description: 可查看本页以了解如何添加用户并将其分配给Cloud Manager角色
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 4%

---


# 添加用户和分配Cloud Manager角色{#add-users-assign}

Adobe将在Adobe Identity Management系统(IMS)中为您的公司创建&#x200B;**组织**&#x200B;标识符，可以在其中管理您的所有用户及其权限。 每个用户(需要是此组织的成员，并将获得对任何[!UICONTROL Experience Cloud]服务的访问权)都需要拥有自己的&#x200B;**Adobe ID**。

## 了解用户角色{#user-roles}

Cloud Manager中的许多功能需要特定权限才能运行。

Cloud Manager当前为控制特定功能可用性的用户定义四个角色：

* 业务所有者
* 部署管理器
* 项目 Manager
* 开发人员

>[!NOTE]
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


## 与角色定义{#permissions}关联的权限

[!UICONTROL Cloud Manager 预配置了一些具有适当权限的角色。]例如，开发人员开发代码并有权将代码推送到&#x200B;**Git存储库**。 或者，业务所有者具有不同的权限，允许他们定义关键绩效指标(KPI)和批准部署。

每个角色都具有与每个角色关联的特定权限。 下表总结了角色、列表可用的函数以及可以执行该函数的角色。

| 权限 | 描述 | 业务所有者 | 部署管理器 | 项目 Manager | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加项目 | 添加新项目。 | x |  |  |  |
| 创建环境 | 创建Prod+Stage、Dev、环境。 | x | x |  |  |
| 更新环境 | 更新Prod+Stage、Dev、环境。 | x | x |  |  |
| 删除环境 | 删除非生产、开发、环境。 | x | x |  |  |
| 管线设置 | 设置或编辑管道。 |  | x |  |  |
| 管道执行 | 开始管道。 | x | x |  |  |
| 管道执行 | 拒绝/批准重要的3层故障。 | x | x | x |  |
| 管道执行 | 提供GoLive批准。 | x | x | x |  |
| 管道执行 | 计划生产部署。 | x | x | x |  |
| 管道删除 | 允许删除管线。 |  | x |  |  |
| 执行取消 | 取消当前执行。 |  | x |  |  |
| 生成个人访问令牌 | 访问Git。 |  | x |  | x |

## 添加用户{#add-users}

>[!NOTE]
>您必须是系统管理员才能添加用户。

1. 如果您是系统管理员，请导航到[Admin Console](https://adminconsole.adobe.com)。 或者，您也可以导航到Cloud Manager，在Cloud Manager中，您会看到&#x200B;**管理访问**&#x200B;按钮，如下所述。

1. 单击位于Cloud Manager登陆页右上角的&#x200B;**管理访问**&#x200B;按钮，在新选项卡中打开Admin Console。

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   在&#x200B;**Admin Console**&#x200B;中，您可以将用户添加到云管理器，并将其分配到角色，即Admin Console中的产品用户档案。

1. 从&#x200B;**产品和服务**&#x200B;卡中选择&#x200B;**Adobe Experience Manager作为Cloud Service**，如下所示。

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. 从操作栏中选择&#x200B;**Users**&#x200B;选项卡，然后选择&#x200B;**Add User**。

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. 选择用户，然后为用户分配适当的云管理者角色或产品用户档案，如下所示。

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >请参阅前几节[“用户角色和权限](#user-roles)”和与角色定义](#permissions)关联的[权限，以确保在&#x200B;**Admin Console**&#x200B;中为正确的用户分配了正确的角色。

   现在，您已将用户添加到Adobe Experience Manager作为Cloud Service产品上下文，并且设置了正确的角色或产品用户档案。

   例如，如果您是以下人员：

   * ***业务所有者***，您具有添加新项目或编辑项目、添加或更新环境、添加/编辑/删除管道和运行任何管道以及将代码部署到AEM环境或代码质量的权限。

   * ***Deployment Manager***，您拥有添加或更新环境、运行任何管道以及将代码部署到AEM 环境或代码质量的权限。

   * ***开发人员***，您有权生成个人访问令牌以访问Git。

      >[!NOTE]
      > 可以将用户分配给多个角色。 例如，将业务所有者和部署管理器角色分配给用户可向他们提供这些权限的组合或总和。
