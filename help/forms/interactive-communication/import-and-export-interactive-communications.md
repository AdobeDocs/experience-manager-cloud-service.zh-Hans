---
title: 导入和导出交互式通信
description: 通过导入和导出交互式通信，用户可以无缝地跨环境迁移、重用和管理通信。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 14%

---


# 导入和导出交互式通信

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期采用者计划期间不断改进，提示词、示例和最佳实践可能会发生变化。

交互式通信(IC)中的导入和导出功能使用户能够跨环境无缝地迁移、重用和管理通信。 它允许您从一个环境导出交互式通信(IC)及其关联的片段和数据模型，并将其导入另一个环境，从而确保一致性并减少部署期间的重复工作。

## 主要优点

- 简化跨环境的IC迁移。
- 保留片段、数据模型和依赖项。
- 减少跨项目重新创建IC的工作。

## 导入和导出交互式通信

在一个环境中创建交互式通信(IC)，并通过以下步骤导出和导入该交互式通信(IC)而在另一个环境中重复使用：

+++1.如何导出交互式通信

1.1.选择[创建的交互式通信](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) (IC)。
1.2.单击**下载**选项以将其导出为ZIP文件。
1.3.下载的ZIP文件包含IC及其选定的**模板**、**片段**&#x200B;和&#x200B;**数据模型**。

![查找IC文档](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++2.如何导入交互式通信

2.1.转到目标环境。
2.2.导航到**Forms > Forms和文档>创建>文件上传**。
2.3.将ZIP文件上传到**导入** IC。

![查找IC文档](/help/forms/interactive-communication/assets/uploadfile.png)

2.4.上载后，交互式通信连同其关联片段和数据模型一起出现。

![查找IC文档](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++3.导入和导出片段

3.1.要导出，请从&#x200B;**Forms > Forms和文档**&#x200B;中选择所需的片段，然后单击&#x200B;**下载**&#x200B;以将其导出为ZIP文件。

3.2.要导入，请转到目标环境，导航到Forms > Forms和文档>创建> **文件上传**，然后上传导出的ZIP文件。

这允许跨不同环境轻松重用片段，确保设计的一致性并减少重复工作。
+++
