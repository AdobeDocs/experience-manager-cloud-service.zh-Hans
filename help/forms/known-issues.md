---
title: 已知问题和限制
description: 的已知问题和限制  [!DNL AEM Forms] as a Cloud Service环境
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

开始使用之前 [!DNL AEM Forms] as a Cloud Service地，请查看以下已知问题和限制：

## 已知问题 {#known-issues}

* 在收到进一步通知之前，请不要添加并运行将自适应表单从发布实例提交到在创作实例上运行的AEM工作流的测试。

* 在导入使用包含 **[!UICONTROL 保存]** 按钮 **[!UICONTROL 保存]** 按钮即使从相应的模板中删除，也会继续显示在自适应表单中。 删除 **[!UICONTROL 保存]** 自适应Forms中的“隐藏主体”和“显示主体”。 请留意发行说明，了解Forms Portal的可用情况，并将另存为草稿功能以恢复和使用按钮。

* 的 **[!UICONTROL 设置变量]** AEM工作流的步骤不支持数组列表类型的变量。 您可以使用流程步骤来设置数组列表类型的变量。

* 当您从Apple iOS设备提交包含标准HTML上传字段的自适应表单时，不会发送文件内容，而在另一端接收0字节文件。 此问题间歇性发生，且仅在使用同步提交时发生。 这是 [已知问题](https://feedbackassistant.apple.com/feedback/9117687) 在AppleiOS。

* 当您从Apple iOS设备提交包含标准HTML上载字段的表单时，有时不会发送文件内容，而在另一端会收到0字节文件。 这是Apple iOS中的已知问题。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service不会为XDP和JSON架构文件生成缩略图。 该服务显示默认图标代替缩略图。

   ![Forms缩略图已知问题](/help/forms/assets/forms-tumbnail-known-issue.png)


## 限制 {#limitations}

* 对基于 XFA 的自适应表单的支持并非现成可用。如果您需要使用基于 XFA 的自适应表单，请联系 Adobe 支持部门并提供您用例的详细信息和具体要求。

