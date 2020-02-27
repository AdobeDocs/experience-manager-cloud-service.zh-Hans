---
title: 添加用户和角色——必需内容
description: 添加用户和角色——必需内容
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f

---


# 添加用户和角色 {#add-users-roles}


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