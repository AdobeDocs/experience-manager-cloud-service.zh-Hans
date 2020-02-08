---
title: 添加用户和角色——必需内容
description: 添加用户和角色——必需内容
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# 添加用户和角色——必需内容 {#add-users-roles}


Cloud manager中的许多功 [!UICONTROL 能需要特定权限] 才能运行。 例如，仅允许某些用户为程序设置关键绩效指标(KPI)。 这些权限按逻辑分组为角色。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义四个角色：

* 企业所有者
* 计划经理
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用 [!UICONTROL Cloud Manager]，您必须具有Adobe ID和Adobe Managed services产品上下文。

## 角色定义 {#role-definitions}

>[!NOTE]
>
>Admin Console中的“开发人员”角色与 [!UICONTROL Cloud Manager中的“开发人员”角色无关]。

下表总结了这些角色：

| [!UICONTROL Cloud Manager] Roles | 描述 |
|--- |--- |
| 企业所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 计划经理 | 使用 [!UICONTROL Cloud Manager] ，执行团队设置、审核状态和查看KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使用 [!UICONTROL Cloud Manager] 执行舞台／生产部署。 可以编辑CI/CD管道。 可以批准重要的3层故障。 可以访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使 [!UICONTROL 用Cloud Manager] 查看状态。 可以访问Git存储库以进行代码提交。 |
| 内容作者 | 通常不与 [!UICONTROL Cloud Manager交互]。 可能使 [!UICONTROL 用Cloud Manager] Program Switcher(已从 [!UICONTROL Experience Cloud])访问AEM。 |

## 使用Admin Console创建配置文件 {#using-admin-console-to-create-a-profile}

可从Adobe Admin Console [!UICONTROL 为Cloud Manager] 管理角色。 通过将用户添加到Admin console中的 [!UICONTROL Cloud Manager] Product Profile，可提供特定角色成员关系。

您可以通过在 [!UICONTROL Adobe Admin Console中将用户添加到] Cloud Manager **** Product Profile来分配特定角色成员关系，Adobe Admin Console是管理整个组织中Adobe授权的一个中心位置。 要进一步了解Adobe Admin Console，请参阅 [Admin Console文档](https://helpx.adobe.com/enterprise/using/admin-console.html)。

>[!NOTE]
>
>要访问管理控制台并设置您的团队（用户和角色），请打开浏览器并访问 [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise)。

为了向 [!UICONTROL Cloud Manager] （客户组织中的管理员）用户提供相应的基于角色的权限，必须在 **AEM Managed Services** Product Context下创建新的产品配置。

要向 [!UICONTROL Cloud Manager] （云管理器）用户提供相应的基于角色的权限，您必须以管理员身份在与四个Cloud Manager角色中的每个角色对应的 [!UICONTROL AEM Managed Services] Product Context下创建四个新的产品配置文件：

* 企业所有者
* 部署管理器
* 开发人员
* 计划经理

您可以使用 [Admin Console](https://adminconsole.adobe.com/) for Cloud Manager创建用户／用户组或将用户／用户组添加到这些产品配置中，如下图所示：

1. 登录到Admin Console，然后单击“新 **建配置文件** ”以添加新配置文件。

1. 填写字段，为 [!UICONTROL Cloud Manager设置新角色]。

   输入 **配置文件名称**、 **显示名称** ，以创建新配置文件。 此外，您还可以为配置 **文件选择权限组** 。

   单击 **完成** ，以完成配置文件创建步骤。

   >[!NOTE]
   >
   >创建这些产品配置时， **显示名称** ，必须是  Cloud Manager定义的技术值（请参阅下表）。 “配 **置文件名称** ”可以是任何内容，但为避免混淆，建议使用下面“建议的配置文件名称” *列中的值* 。 为此，在创建产品配置时，请取消选中“与配置 **名称相同”** ，并指定相应的值作为“显 **示名称”**。

   | **角色** | **显示名称（必需）** | **推荐的配置文件名称** |
   |---|---|---|
   | 企业所有者 | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 业务所有者角色 |
   | 部署管理器 | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] - Deployment manager角色 |
   | 开发人员 | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 开发人员角色 |
   | 计划经理 | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Cloud Manager] —— 计划经理角色 |

1. 创建产品配置后，您可以将用户（或用户组）添加到产品配置。


