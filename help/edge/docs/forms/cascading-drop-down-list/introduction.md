---
title: 级联下拉列表
description: 使用 API 集成动态填充下拉列表
feature: Edge Delivery Services
role: User,Developer
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '125'
ht-degree: 100%

---

# 用例说明

在构建表单或应用程序时，引导用户以结构化方式选择位置通常非常有用。级联下拉列表让这一过程更简单、更友好——用户先选择国家/地区，系统会筛选出可用的州/省列表，然后再根据所选州/省选择最终的城市。这种方式不仅使表单更加简洁，还能避免无效组合（例如在所选州中选择一个不存在的城市）。

要实现此用例，需要执行以下步骤：

- 创建 API 集成
- 创建包含国家或地区/州或省/城市字段的表单
- 创建规则，通过 API 集成来填充下拉列表