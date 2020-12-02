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


[!UICONTROL 云管理器]中的许多功能需要特定权限才能运行。 例如，仅允许特定用户为项目设置关键绩效指标(KPI)。 这些权限在逻辑上分组为角色。

[!UICONTROL Cloud Manager] 当前为用户定义四个角色，这些角色控制特定功能的可用性：

* 企业所有者
* 项目管理器
* 部署管理器
* 开发人员

>[!CAUTION]
>
>要使用[!UICONTROL 云管理器]，您必须具有Adobe ID和Adobe Managed Services产品上下文。

## 角色定义{#role-definitions}

>[!NOTE]
>
>Admin Console中的“开发人员”角色与[!UICONTROL 云管理器]中的“开发人员”角色无关。

下表总结了这些角色：

| [!UICONTROL 云管理] 者角色 | 描述 |
|--- |--- |
| 企业所有者 | 负责定义KPI、批准生产部署和覆盖重要的3层故障。 |
| 项目管理器 | 使用[!UICONTROL 云管理器]执行团队设置、审核状态和视图KPI。 可以批准重要的3层故障。 |
| 部署管理器 | 管理部署操作。 使用[!UICONTROL 云管理器]执行舞台／生产部署。 可以编辑CI/CD管道。 可以批准重要的3层故障。 可以访问Git存储库。 |
| 开发人员 | 开发和测试自定义应用程序代码。 主要使用[!UICONTROL 云管理器]视图状态。 可获取对Git存储库的代码提交访问权限。 |
| 内容作者 | 通常不与[!UICONTROL 云管理器]交互。 可使用[!UICONTROL 云管理器]项目切换器(已从[!UICONTROL Experience Cloud]导航)访问AEM。 |