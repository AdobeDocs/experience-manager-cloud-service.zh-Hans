---
title: 级联下拉列表
description: 使用自适应Forms表达式可添加自动验证、计算以及打开或关闭部分的可见性。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 86%

---

# 用例说明

在构建表单或应用程序时，引导用户以结构化方式选择位置通常非常有用。 级联下拉列表让这一过程更简单、更友好——用户先选择国家/地区，系统会筛选出可用的州/省列表，然后再根据所选州/省选择最终的城市。 这种方式不仅使表单更加简洁，还能避免无效组合（例如在所选州中选择一个不存在的城市）。

要实现此用例，需要执行以下步骤：

- 创建 API 集成
- 创建包含国家或地区/州或省/城市字段的表单
- 创建规则，通过 API 集成来填充下拉列表