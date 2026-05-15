---
title: 使用通用编辑器创建表单
description: 使用自适应Forms表达式可添加自动验证、计算以及打开或关闭部分的可见性。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 67%

---

# 使用通用编辑器创建表单

使用通用编辑器创建以下表单。 该表单具有3个下拉列表，其值将使用API集成进行填充
![自适应表单](assets/address-form.png)

## 居住国家/地区

在初始化时，将使用 API 调用返回的结果填充居住国家/地区下拉列表。
![initialize-event](assets/initialize-event.png)

## 成功处理程序

成功处理程序被定义为根据地理名称数组，将国家/地区下拉列表的 enum 和 enumNames 设置为相应的取值。 geonames数组在“事件有效负载”选项下可用
![事件有效负载](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## 获取子级值

当用户在“居住国家/地区”下拉列表中做出选择时，将填充“州/省”下拉列表。 与所选国家关联的 geonameId 将作为输入参数传递给 GetChildren API 集成。

![get-children](assets/invoke-service-get-children.png)

已定义序列处理程序来设置StateOrProvidle下拉字段的enum/enumNames
![get-children-success-handler](assets/child-success-handler.png)

当选择了州或省后，可按照上述用于填充“州/省”下拉列表的相同模式来填充“城市”下拉列表。