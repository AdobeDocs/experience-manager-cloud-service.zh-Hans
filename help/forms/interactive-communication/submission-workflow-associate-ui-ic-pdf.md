---
title: 关联UI的提交工作流 — IC生成PDF输出
description: 了解提交和工作流如何用于关联UI，并遵循一个示例工作流，该工作流从交互式通信(IC) JSON生成PDF。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---

# 关联UI提交工作流

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

本文说明了为关联UI启用工作流时，提交和工作流如何工作。 然后，它会介绍如何配置提交工作流。 演练使用从交互式通信(IC)有效负载生成PDF作为示例；您可以根据其他工作流类型调整步骤。

<!--## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).-->

## 配置提交工作流

以下步骤说明了如何创建在用户从关联UI提交时运行的工作流。 在此我们使用&#x200B;**将IC渲染到PDF**&#x200B;作为示例，并完成现成的&#x200B;**IC渲染PDF输出**&#x200B;步骤。 当用户从关联UI提交时，有效负载会被发送到工作流；此步骤使用有效负载中的&#x200B;**communicationDom** (IC-JSON)生成PDF。

### 有效负荷结构

工作流接收JSON有效负载。 **communicationDom**&#x200B;字段包含用于PDF生成的IC-JSON。 **IC渲染PDF输出**&#x200B;步骤使用它作为模板输入。

| 字段 | 描述 |
|-------|-------------|
| communicationDom | 用于PDF代的IC-JSON |
| auditMetadata | 审核信息 |
| submitData | 已提交的表单数据(JSON) |
| prefillData | 预填充数据(JSON) |
| referer， cookie， queryString， clientIP， userAgent， formSubmitter | 请求元数据 |

### 创建工作流模型

1. **基本：**&#x200B;创建工作流模型（例如，添加工作流作为&#x200B;**pdfrenderworkflow**）。

   ![工作流模型基本选项卡](/help/forms/assets/associate-ui-add-workflow.png)

1. **变量：**&#x200B;添加与有效负载和步骤：**communicationDom** (JSON)、**auditMetadata** (JSON)、**outputDocument** （文档）匹配的变量。

   ![工作流变量](/help/forms/assets/associate-ui-add-variables.png)

1. **步骤：**&#x200B;添加&#x200B;**IC渲染PDF输出**&#x200B;步骤。
   ![添加工作流步骤](/help/forms/assets/associate-ui-add-step.png)

1. 在其&#x200B;**输入**&#x200B;选项卡中，将&#x200B;**选择模板(JsonObject)**&#x200B;设置为&#x200B;**变量** → **communicationDom**。 保存步骤和模型。

   ![IC渲染PDF输出 — 输入选项卡](/help/forms/assets/associate-ui-input-variable.png)

1. 在其&#x200B;**输出**&#x200B;选项卡中，将&#x200B;**选择模板(JsonObject)**&#x200B;设置为&#x200B;**变量** → **communicationDom**。 保存步骤和模型。

   ![工作流变量和画布](/help/forms/assets/assocaite-ui-output-variable.png)

### 连接工作流以关联UI

在[启用并配置关联UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)中，启用关联视图，并在&#x200B;**工作流**&#x200B;中，将&#x200B;**配置更新工作流**&#x200B;设置为开启并选择此工作流模型。 发布IC并[集成关联UI](/help/forms/interactive-communication/invoke-associate-ui.md)，因此提交会触发此工作流。

![交互式通信设置 — 关联UI的工作流配置](/help/forms/assets/associate-ui-configure-workflow.png)

启用&#x200B;**将工作流数据存储外部化**&#x200B;后，请配置外部化器，以便将工作流数据存储到外部存储（例如，Azure）中。 请参阅[将工作流数据外部化](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html?lang=zh-Hans)。

## 另请参阅

- [在交互式通信编辑器中关联UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [为交互式通信启用并配置关联UI](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [在应用程序中集成关联UI](/help/forms/interactive-communication/invoke-associate-ui.md)
- [将工作流数据外部化](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html?lang=zh-Hans)
