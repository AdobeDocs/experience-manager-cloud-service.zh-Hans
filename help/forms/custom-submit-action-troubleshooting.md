---
title: 疑难解答自适应Forms的自定义提交操作中的502错误
description: 了解如何识别并解决在自适应Forms（核心组件）中使用自定义提交操作时出现的502错误页面。 本指南介绍常见原因（如未处理的异常），并提供解决步骤。
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="适用于AEM Forms)。"
exl-id: a7469926-7059-4aca-90ff-2554d14c3944
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 2%

---

# 疑难解答：自定义提交操作中的502错误页面

使用自适应Forms（核心组件）时，在提交使用自定义提交操作的表单后，您可能会遇到&#x200B;**502错误页面HTML**。

## 问题

**错误：**&#x200B;自定义提交操作服务失败时显示502错误页HTML。

**原因：**&#x200B;如果自定义提交操作引发未处理的错误（例如，空指针、无效的API响应或运行时失败），就会发生这种情况。

## 解决方法

为了防止502错误页面，请使用try-catch块封装提交逻辑以正常处理错误。

有关详细步骤，请参阅[为自适应Forms（核心组件）创建自定义提交操作](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md)。
