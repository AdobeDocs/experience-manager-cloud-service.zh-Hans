---
title: “层叠”下拉列表
description: 使用自适应Forms表达式可添加自动验证、计算以及打开或关闭部分的可见性。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 2%

---

# 用例描述

在构建表单或应用程序时，以结构化方式指导用户完成位置选择通常很有用。 级联下拉列表让这种选择既简单又便于用户使用 — 用户首先选择国家/地区，这将过滤可用州/省列表，然后根据州最终选择城市。 这种方法不仅保持表单的整洁，还防止无效的组合（例如，选择在选定状态下不存在的城市）。

要完成此用例，需要执行以下步骤

- 创建 API 集成
- 创建包含字段的表单，以捕获国家/地区/州/市
- 创建规则以使用API集成填充下拉列表