---
title: 基于角色的权限
description: 基于角色的权限
translation-type: tm+mt
source-git-commit: a1b4feced2dd8becc74383fe8a3b835bde7159d2

---


# 基于角色的权限 {#role-based-permissions}

[!UICONTROL Cloud Manager] 已预配置了具有相应权限的角色。 例如，开发人员开发代码并具有将代码推送到 **Git存储库的权限**。 或者，业务所有者具有不同的权限，允许他们定义关键绩效指标(KPI)并批准部署。

## 用户权限 {#user-permissions}

每个角色都具有与每个角色关联的特定权限、预配置的任务或权限。 下表列出了可用的函数以及可以执行该函数的角色。

| 权限 | 描述 | 企业所有者 | 部署管理器 | 计划经理 | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加计划 | 添加新程序。 | x |  |  |  |
| 创建环境 | 创建Prod+Stage、Dev、Playground环境。 | x | x |  |  |
| 更新环境 | 更新Prod+Stage、Dev、Playground环境。 | x | x |  |  |
| 删除环境 | 删除非生产、开发、运动场环境。 | x | x |  |  |
| 删除环境 | 删除Prod+Stage环境。 |  |  |  |  |
| 计划设置 | 配置计划（包括KPI）。 | x |  |  |  |
| 计划设置 | Git提交访问。 |  | x |  | x |
| 管线设置 | 设置或编辑管道。 |  | x |  |  |
| 管道执行 | 启动管道。 | x | x |  |  |
| 管道执行 | 拒绝／批准重要的3层故障。 | x | x | x |  |
| 管道执行 | 提供GoLive Approval。 | x | x | x |  |
| 管道执行 | 计划生产部署。 | x | x | x |  |
| 管道执行 | 恢复制作管道。 |  |  |  |  |
| 管理环境 | 从“管理环境”屏幕添加Publish-Dispatcher区段。 | x | x |  |  |  |
| 推送更新 | 启动推送更新管道。 |  |  |  |  |
| 生成个人访问令牌 | 访问Git。 |  | x |  | x |

