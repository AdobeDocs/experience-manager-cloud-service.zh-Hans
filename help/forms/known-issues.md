---
title: AEM Formsas a Cloud Service环境的已知问题和限制有哪些？
description: 已知问题和限制  [!DNL AEM Forms] as a Cloud Service的环境。
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 93%

---

# 已知问题和限制 {#known-issues-and-limitations}

开始使用 [!DNL AEM Forms] as a Cloud Service 之前，请查看以下已知问题和限制：

## 已知问题 {#known-issues}

* 请勿添加和运行将自适应表单从发布实例提交到在创作实例上运行的 AEM 工作流的测试，直至另行通知。

* 当您导入使用包含&#x200B;**[!UICONTROL 保存]**&#x200B;按钮的模板的自适应表单时，即使从相应模板中删除&#x200B;**[!UICONTROL 保存]**&#x200B;按钮，该按钮仍会继续出现在自适应表单中。在发布自适应表单之前，请删除其中的&#x200B;**[!UICONTROL 保存]**&#x200B;按钮。请留意发行说明，了解 Forms 门户和“另存为草稿”功能的可用性，以便恢复和使用该按钮。

* AEM 工作流的&#x200B;**[!UICONTROL 设置变量]**&#x200B;步骤不支持数组列表类型的变量。您可以使用流程步骤来设置数组列表类型的变量。

* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的自适应表单时，不会发送文件内容，而在另一端会收到一个 0 字节的文件。该问题间歇性发生，并且仅在使用同步提交时发生。这是 Apple iOS 中的[已知问题。](https://feedbackassistant.apple.com/feedback/9117687)

* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。这是 Apple iOS 中的已知问题。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service 不会为 XDP 和 JSON 架构文件生成缩略图。该服务显示默认图标来代替缩略图。

  ![表单缩略图已知问题](/help/forms/assets/forms-tumbnail-known-issue.png)

* 当您使用具有可重复元素的架构来创建基于核心组件的自适应表单时，从自适应表单编辑器中的数据模型树拖放可重复元素的选项不起作用。

## 限制 {#limitations}

* 对基于 XFA 的自适应表单的支持并非现成可用。如果您需要使用基于 XFA 的自适应表单，请联系 Adobe 支持部门并提供您用例的详细信息和具体要求。

