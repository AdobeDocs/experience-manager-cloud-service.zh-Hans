---
title: 基于角色的权限
description: 基于角色的权限
translation-type: tm+mt
source-git-commit: 3c56d94f9922cb65b91912dd96eb8aa60efc2b53
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 21%

---


# 基于角色的权限 {#role-based-permissions}

[!UICONTROL Cloud Manager 预配置了一些具有适当权限的角色。]例如，开发人员开发代码并具有将代码推送到Git存储库 **的权限**。 或者，业务所有者具有不同的权限，允许他们定义关键绩效指标(KPI)并批准部署。

## 用户权限 {#user-permissions}

每个角色都具有与每个角色关联的特定权限、预配置的任务或权限。 此表列表了可用的函数以及可以执行该函数的角色。

| 权限 | 描述 | 企业所有者 | 部署管理器 | 项目管理器 | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加项目 | 添加新项目。 | x |  |  |  |
| 创建环境 | 创建Prod+Stage、Dev、Playmorg环境。 | x | x |  |  |
| 更新环境 | 更新Prod+Stage、Dev、Playmorg环境。 | x | x |  |  |
| 删除环境 | 删除“非生产”、“开发”、“操场”环境。 | x | x |  |  |
| 删除环境 | 删除Prod+Stage环境。 |  |  |  |  |
| 项目设置 | 配置项目（包括KPI）。 | x |  |  |  |
| 项目设置 | Git提交访问。 |  | x |  | x |
| 管线设置 | 设置或编辑管道。 |  | x |  |  |
| 管道执行 | 开始管道。 | x | x |  |  |
| 管道执行 | 拒绝／批准重要的3层故障。 | x | x | x |  |
| 管道执行 | 提供GoLive Approval。 | x | x | x |  |
| 管道执行 | 计划生产部署。 | x | x | x |  |
| 管道执行 | 恢复生产管道。 |  |  |  |  |
| 管道删除 | 允许删除管道。 |  | x |  |  |
| 执行取消 | 取消当前执行。 |  | x |  |  |
| 管理环境 | 从“管理环境屏幕”添加Publish-Dispatcher区段。 | x | x |  |  |  |
| 推送更新 | 开始推送更新管道。 |  |  |  |  |
| 生成个人访问令牌 | 访问Git。 |  | x |  | x |

