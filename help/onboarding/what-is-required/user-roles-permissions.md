---
title: 用户角色和权限
description: 本页介绍用户角色和权限。 可查看本页以了解如何添加用户并将其分配给Cloud Manager角色。
translation-type: tm+mt
source-git-commit: 4b9476b094438acd08c945f0102b029b6792cb88
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 8%

---


# 用户角色和权限{#user-roles-permissions}

## 用户角色 {#user-roles}

Cloud Manager中的许多功能需要特定权限才能操作，并根据分配的角色和权限限制您在用户界面中执行的操作。 在某些情况下，如果您没有执行操作的权限，则会显示接口控件，但会禁用它。

如果有要执行但无法执行的操作，请检查下面的部分[用户角色和权限](#permissions)。 根据您的目标，您可以联系系统管理员并请求所需的角色。

Cloud Manager当前为控制特定功能可用性的用户定义四个角色：

* 业务所有者
* 部署管理器
* 项目 Manager
* 开发人员

>[!NOTE]
>Admin Console中的“开发人员”角色与[!UICONTROL 云管理器]中的“开发人员”角色无关。

## 查看您的角色{#view-roles}

要视图您在Cloud Manager中的角色，请登录Cloud Manager UI，选择右上角的用户档案图标，然后选择&#x200B;**用户角色**，如下图所示。

>[!NOTE]
>请参阅[导航到Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md)以了解有关登录到Cloud Manager的更多信息。

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### 集成产品用户档案{#integration-product-profile}

除上述功能外，Cloud Manager还将自动创建一个名为“集成 — Cloud Service”的产品用户档案。 此产品用户档案用于Adobe Experience Manager与其他Adobe产品之间的集成。 不能删除此产品用户档案&#x200B;****。 如果意外删除了此用户档案，则需要手动重新创建它。 此用户档案&#x200B;**的显示名称必须**&#x200B;为`CM_CS_DEFAULT`。


## 用户角色和权限{#permissions}

[!UICONTROL Cloud Manager 预配置了一些具有适当权限的角色。]例如，开发人员开发代码并有权将代码推送到&#x200B;**Git存储库**。 或者，业务所有者具有不同的权限，允许他们添加和编辑项目、添加环境和批准部署。

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