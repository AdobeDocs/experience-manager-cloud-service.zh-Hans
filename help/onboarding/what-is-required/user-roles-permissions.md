---
title: Cloud Manager角色
description: 本页介绍用户角色和权限。 可查看本页以了解如何添加用户并将其分配给Cloud Manager角色。
exl-id: d1689134-044a-4d96-97a2-cd09f735a680
source-git-commit: a0edbaf650fdfbc271a000ab4827a4c414321613
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 6%

---

# Cloud Manager角色 {#user-roles-permissions}

## 用户角色 {#user-roles}

Cloud Manager中的许多功能需要特定权限才能运行，并根据分配的角色和权限限制您在用户界面中执行的操作。 在某些情况下，如果您没有执行操作的权限，则界面控件会存在，但会被禁用。

如果您希望执行某项操作，但无法执行，请检查下面的部分[用户角色和权限](#permissions)。 根据您的目标，您可以联系系统管理员并请求所需的角色。

Cloud Manager当前为用户定义了四个角色，这些角色可控制特定功能的可用性：

* 业务所有者
* 部署管理器
* 项目经理
* 开发人员

>[!NOTE]
>Admin Console中的开发人员角色与[!UICONTROL Cloud Manager]中的开发人员角色无关。

## 查看角色 {#view-roles}

要在Cloud Manager中查看您的角色，请登录到Cloud Manager UI，选择右上角的配置文件图标，然后选择&#x200B;**用户角色**，如下图所示。

>[!NOTE]
>请参阅[导航到Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) ，了解有关登录到Cloud Manager的更多信息。

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### 集成产品配置文件 {#integration-product-profile}

除了上述功能之外，Cloud Manager还将自动创建一个名为“集成 — Cloud Service”的产品配置文件。 此产品配置文件用于Adobe Experience Manager与其他Adobe产品之间的集成。 不能删除此产品配置文件&#x200B;****。 如果意外删除了此配置文件，则需要手动重新创建此配置文件。 此配置文件&#x200B;**的“显示名称”必须**&#x200B;为`CM_CS_DEFAULT`。


## 用户角色和权限 {#permissions}

[!UICONTROL Cloud Manager 预配置了一些具有适当权限的角色。]例如，开发人员开发代码，并有权将代码推送到Git存储库。 或者，业务所有者具有不同的权限，可以添加和编辑程序、添加环境以及批准部署。

每个角色都具有与其关联的特定权限。 例如，如果您的角色是：

* ***“业务所有者***”中，您具有“添加新程序”或“编辑程序”权限，可以添加或更新环境，以及运行任何管道。

* ***部署管理器***&#x200B;中，您有权添加或更新环境，并运行任何管道。

* ***开发人员***，您有权生成访问Git的个人访问令牌。

   >[!NOTE]
   > 可以将用户分配到多个角色。 例如，将“业务所有者”和“部署管理者”角色分配给用户时，会向他们提供这些权限的组合或总和。


下表概述了Cloud Manager中的角色及其关联权限。

| 权限 | 描述 | 业务所有者 | 部署管理器 | 项目经理 | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加程序<br>编辑程序 | 添加新程序。<br>编辑程序 — 添加或删除解决方案或加载项 | x |  |  |  |
| 创建环境 | 创建Prod+Stage、Dev、Environments。 | x | x |  |  |
| 更新环境 | 更新Prod+Stage、Dev、Environments。 | x | x |  |  |
| 删除开发环境 | 删除开发环境。 | x | x |  |  |
| 管道设置 | 设置或编辑管道。 |  | x |  |  |
| 管道执行 | 启动管道。 | x | x |  |  |
| 管道执行 | 拒绝/批准3层重要故障。 | x | x | x |  |
| 管道执行 | 提供GoLive批准。 | x | x | x |  |
| 管道执行 | 计划生产部署。 | x | x | x |  |
| 管道删除 | 允许删除管道。 |  | x |  |  |
| 执行取消 | 取消当前执行。 |  | x |  |  |
| 生成个人访问令牌 | 访问Git。 |  | x |  | x |
