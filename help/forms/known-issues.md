---
title: 已知问题和限制
description: 已知问题和限制  [!DNL AEM Forms] as a Cloud Service环境
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 94825e3b60d970fec5bf696d932ca66bb83fd2f3
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 11%

---

# 已知问题和限制 {#known-issues-and-limitations}

开始使用之前 [!DNL AEM Forms] as a Cloud Service，请查看以下已知问题和限制：

## 已知问题 {#known-issues}

* 在进一步通知之前，请勿添加和运行将自适应表单从发布实例提交到在创作实例上运行的AEM Workflow的测试。

* 导入自适应表单时，使用的模板包含 **[!UICONTROL 保存]** 按钮， **[!UICONTROL 保存]** 即使按钮从相应的模板中移除，它也会继续在自适应表单中显示。 删除 **[!UICONTROL 保存]** 按钮(在发布之前从自适应Forms中删除)。 留意发行说明，了解Forms门户的可用性，并留意另存为草稿功能以恢复和使用按钮。

* 此 **[!UICONTROL 设置变量]** AEM Workflows中的步骤不支持数组列表类型的变量。 您可以使用流程步骤来设置数组列表类型的变量。

* 从Apple iOS设备提交包含标准HTML上传字段的自适应表单时，不会发送文件内容，并在另一端收到0字节的文件。 此问题间歇性地出现，并且仅在使用同步提交时出现。 这是 [已知问题](https://feedbackassistant.apple.com/feedback/9117687) 在Apple iOS中。

* 从Apple iOS设备提交包含标准HTML上传字段的表单时，有时不会发送文件内容，而在另一端会收到0字节的文件。 这是Apple iOS中的一个已知问题。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Formsas a Cloud Service不会为XDP和JSON架构文件生成缩略图。 该服务显示默认图标来代替缩略图。

   ![Forms缩略图已知问题](/help/forms/assets/forms-tumbnail-known-issue.png)


## 限制 {#limitations}

* 对基于 XFA 的自适应表单的支持并非现成可用。如果您需要使用基于 XFA 的自适应表单，请联系 Adobe 支持部门并提供您用例的详细信息和具体要求。

