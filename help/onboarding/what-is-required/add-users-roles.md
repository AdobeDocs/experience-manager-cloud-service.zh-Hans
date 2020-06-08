---
title: 添加用户和角色——需要
description: 添加用户和角色——需要
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# 添加用户和角色 {#add-users-roles}


Cloud Manager中的许 [!UICONTROL 多功能] ，都需要特定权限才能运行。 例如，仅允许特定用户为项目设置关键绩效指标(KPI)。 这些权限在逻辑上分组为角色。

[!UICONTROL Cloud Manager当前] 为控制特定功能可用性的用户定义四个角色：

* 企业所有者
* 项目管理器
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使 [!UICONTROL 用Cloud Manager]，您必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义 {#role-definitions}

>[!NOTE]
>
>Admin Console中的开发人员角色与Cloud Manager中的开发人员角 [!UICONTROL 色无关]。

下表总结了这些角色：

| [!UICONTROL 云管理者] 角色 | 描述 |
|--- |--- |
| 企业所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 项目管理器 | 使 [!UICONTROL 用Cloud Manager] ，执行团队设置、审核状态和视图KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使 [!UICONTROL 用Cloud] Manager执行舞台／生产部署。 可以编辑CI/CD管道。 可以批准重要的3层故障。 可以访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使 [!UICONTROL 用Cloud] Manager进行视图。 可获取对Git存储库的代码提交访问权限。 |
| 内容作者 | 通常不与Cloud Manager [!UICONTROL 交互]。 可能使 [!UICONTROL 用Cloud Manager] 项目切换程序(已 [!UICONTROL 从Experience Cloud导航])访问AEM。 |