---
title: 如何创建多步骤表单序列？
description: 通过  [!DNL Experience Manager Forms] 可定义一系列表单面板，以供用户从中导航和填写自适应表单。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 95%

---

# 多步骤表单序列简介 {#introduction-to-multi-step-form-sequence}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/introduction-form-sequence.html) |
| AEM as a Cloud Service | 本文 |

利用自适应表单，表单作者可以很轻松地创建多步骤数据捕获体验。它内部支持创建多个面板并将每个面板与不同的导航模式关联。表单作者可以在逻辑部中分对表单字段进行分组，并将一个组表示为一个面板。面板之间的整体导航通过面板布局进行控制。作者可以选择以不同的布局排列面板，例如，使用向导布局按顺序放置，或使用选项卡式布局即兴放置。 有关面板布局的信息，请参阅[自适应表单的布局功能](layout-capabilities-adaptive-forms.md)。

在典型的表单填写体验中，涉及的步骤不只是捕获数据。完整表单提交可以包括其他步骤，例如，对表单进行数字签名、验证表单中填写的信息、处理付款等。具体因情况而异。

如果您的用例要求执行一组数据捕获步骤，或者有要求执行某些步骤的法规，[!DNL Experience Manager Forms] 会提供一种跨表单强制执行该通用结构的方法。表单结构的预先计划的实施定义了表单的步骤序列。![多步骤表单序列的示例](assets/formpipeline.png)

多步骤表单序列的示例

让我们举一个用例，您必须为表单的填写、验证、签名和确认步骤创建序列。创建此类序列的步骤如下所示：

1. 定义表单模板并向其中添加所需的面板。序列中的每个步骤都应有一个面板。但是，您可以在面板中包含子面板。

   在本示例中，我们可以添加以下面板：

   * **[!UICONTROL 填写]**：它包含用于捕获数据的表单字段。在这里，您可以包括嵌套的子面板来为不同类型的信息创建部分，例如个人、家庭、财务等。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 电子签名]**：它包含&#x200B;**[!UICONTROL 签名]**&#x200B;组件，该组件可用于基于 XFA 的自适应表单。它提供以下签名服务：

      * Adobe Document Cloud eSign 服务
      * 连笔签名

   * **[!UICONTROL 确认]**：它包含&#x200B;**[!UICONTROL 摘要]**&#x200B;组件，该组件在用户签署表单并到达序列中的“确认（摘要）”步骤后，显示一条确认表单提交的消息。作者可以配置[!UICONTROL 摘要]组件的文本、显示感谢消息、显示生成的 PDF 的链接等。

1. 选择根面板的布局作为&#x200B;**[!UICONTROL 向导]**。
1. 完成其余步骤以创建表单模板。<!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

在表单模板中定义表单序列后，您可以使用它创建将基本结构定义为序列的表单，但您始终能自定义表单以满足您的要求。


## 另请参阅 {#see-also}

{{see-also}}