---
title: 为交互式通信启用并配置关联UI
description: 了解如何在交互式通信设置中启用关联视图并配置更新工作流，以便关联者可以使用关联UI。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7c3e8a2b-5f21-4a1e-9e2d-8a4b6c7d8e9f
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 为交互式通信启用并配置关联UI

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

本文介绍了如何为交互式通信(IC)启用关联UI，以及选择性地配置AEM工作流以供提交。 作者在&#x200B;**交互式通信设置**&#x200B;中执行这些步骤。

有关关联UI和用户角色的概述，请参阅[交互式通信编辑器中的关联UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)。

## 先决条件

在启用和配置关联UI之前，请确保您具有：

- **作者访问**&#x200B;交互式通信编辑器。
- 使用所需的布局和数据绑定创建的&#x200B;**交互式通信**。
- 已将&#x200B;**关联用户**&#x200B;添加到&#x200B;**forms-associates**&#x200B;组（关联访问关联UI所必需的）。
- 已将&#x200B;**作者**&#x200B;添加到&#x200B;**forms-associates**&#x200B;组（作者访问关联UI所必需的）。

当您准备好将关联UI与您的应用程序集成并在发布实例上调用它时，您还需要具有已启用弹出窗口支持且已发布IC的浏览器。 有关完整的集成先决条件，请参阅应用程序中的[集成关联UI](/help/forms/interactive-communication/invoke-associate-ui.md)。

## 启用关联视图（关联UI）

在文档级别启用关联UI，以便关联方可以使用交互式通信。

1. 在编辑器中打开交互式通信。
1. 从顶部操作栏或文档选项中，打开&#x200B;**交互式通信设置** （或&#x200B;**设置**）。

   ![交互式通信设置 — 将属性与启用关联视图编辑关联](/help/forms/assets/associate-ui-settings.png)

1. 在左侧面板中，确保选中&#x200B;**关联属性**。
1. 在右侧，选中&#x200B;**启用关联视图编辑**。
1. 单击&#x200B;**应用更改**，然后保存文档。

   ![交互式通信设置 — 将属性与启用关联视图编辑关联](/help/forms/assets/associate-ui-enable-view.png)

消息可能会提醒您应用更改并保存文档以启用“关联视图”。 保存后，该IC可用于关联驱动使用。

### 允许为每个组件编辑关联UI

为IC启用“关联视图”后，必须为关联能够编辑的每个组件打开&#x200B;**允许由关联编辑**。 未启用此设置的组件在关联UI中保持只读状态。

1. 在IC编辑器中，在画布或组件层次结构中选择组件（例如文本字段）。
1. 在右侧&#x200B;**属性**&#x200B;面板中，展开&#x200B;**关联属性**。
1. 将&#x200B;**允许关联编辑** **开启**&#x200B;该组件。
1. 对关联需要编辑的每个组件重复此操作，然后保存文档。

![允许通过关联编辑组件属性](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> **关联属性**&#x200B;还包括诸如&#x200B;**排版规则**（关联UI中字段的字体、大小和样式）、**工具提示**&#x200B;和&#x200B;**模式**（验证）等选项。 使用这些选项控制关联编辑组件时的外观和行为 — 例如，设置验证模式，以便关联以所需格式输入数据。

## 配置关联UI的工作流

要在用户从关联UI提交或更新数据时运行AEM工作流，请配置以下内容：

1. 在&#x200B;**交互式通信设置**&#x200B;中，在左侧面板（在“关联属性”下）中选择&#x200B;**工作流**。
1. 打开&#x200B;**为更新**&#x200B;配置工作流&#x200B;**&#x200B;**。
1. 在&#x200B;**选择工作流模型**&#x200B;中，选择要运行的AEM工作流模型（例如，`conversionWorkflow`或路径，例如`/var/workflow/models/submit-workflow-1`）。
1. （可选）设置&#x200B;**工作流成功消息** （在工作流完成后显示给用户）。
1. 可以选择设置&#x200B;**重定向URL**&#x200B;以在提交后将用户发送到特定页面。
1. 单击&#x200B;**应用更改**&#x200B;并保存文档。

   ![交互式通信设置 — 关联UI的工作流配置](/help/forms/assets/associate-ui-configure-workflow.png)

启用工作流后，每当用户从关联UI提交时，该工作流都会运行。 有关提交和工作流的工作方式（运行位置、使用哪个实例以及关键注意事项），请参阅[关联UI的提交工作流](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior)。 该文章还包含从IC提交内容生成PDF的工作流示例。

## 完成关联UI设置

启用“关联视图”并（可选）配置工作流后：

1. **启用可编辑的字段：**&#x200B;在IC的必需部分中，启用允许关联的字段进行编辑。 根据需要设置验证和强制/只读行为。
1. **发布IC**，使其在关联的发布实例上可用。
1. 与联营公司共享已发布的IC链接。 他们进行身份验证（例如，通过[Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)）并打开关联UI，输入或确认客户数据，然后生成最终通信。 如果已配置工作流，则它会在提交时运行。 有关提交和工作流的工作方式，请参阅[关联UI的提交工作流](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior)。

## 另请参阅

- [在交互式通信编辑器中关联UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [在应用程序中集成关联UI](/help/forms/interactive-communication/invoke-associate-ui.md)
- [关联UI的提交工作流 — IC生成PDF输出](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) — 提交和工作流的工作方式，以及通过IC提交生成PDF的示例工作流。
