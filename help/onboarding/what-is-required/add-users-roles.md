---
title: 添加用户和角色 — 必需内容
description: 添加用户和角色 — 必需内容
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%

---


# 添加用户和角色 {#add-users-roles}


[!UICONTROL 云管理器]中的许多功能需要特定权限才能运行。

[!UICONTROL Cloud Manager] 当前为控制特定功能可用性的用户定义四个角色：

* 业务所有者
* 项目 Manager
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用[!UICONTROL 云管理器]，您必须将Adobe ID和Adobe Experience Manager作为Cloud Service产品上下文。

## 角色定义{#role-definitions}

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

## 集成产品用户档案{#integration-product-profile}

除上述功能外，Cloud Manager还将自动创建一个名为“集成 — Cloud Service”的产品用户档案。 此产品用户档案用于Adobe Experience Manager与其他Adobe产品之间的集成。 不能删除此产品用户档案&#x200B;****。 如果意外删除了此用户档案，则需要手动重新创建它。 此用户档案&#x200B;**的显示名称必须**&#x200B;为`CM_CS_DEFAULT`。
