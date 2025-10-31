---
title: 使用其他数据选项在交互式通信编辑器中预览PDF
description: 在交互式通信编辑器中使用PDF预览功能通过不同的数据选项以三种不同的方式预览交互式通信。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 15%

---


# 交互式通信编辑器中的 PDF 预览

>[!NOTE]
>
> 交互式通信功能在早期采用者计划下提供。 请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期采用者计划期间不断改进，提示词、示例和最佳实践可能会发生变化。

PDF预览功能使用户可以通过三种不同的方式预览交互式通信：不使用数据、使用基于JSON的本地数据或使用来自配置数据模型的示例数据。

## 主要优点

- 使用示例数据预览交互式通信，可视化将实时数据与通信合并时的显示方式。

- 上传本地JSON数据文件以生成数据驱动预览，而无需后端设置。

- 使用连接的表单数据模型(FDM)来模拟设计期间与样本数据的实时数据集成。

- 轻松地在数据选项（无数据、本地数据、FDM）之间切换以验证布局、结构和个性化。

## 使用其他数据选项在交互式通信编辑器中预览PDF

不使用数据、本地数据或配置数据模型中的示例数据预览交互式通信，以实现灵活的测试和验证。

+++1.无数据预览。

1.1.在IC编辑器中打开交互式通信。

1.2.使用“PDF预览”选项并选择&#x200B;**无数据**&#x200B;选项查看无数据的通信。

![查找IC文档](/help/forms/interactive-communication/assets/nodata.png)

+++

+++2.使用本地JSON数据预览

2.1.准备结构化JSON文件。 作为参考，您可以从用于通信的JSON架构[(FDM)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model)中复制示例数据。

2.2.在IC编辑器中，转到&#x200B;**PDF预览** >使用本地数据。

2.3.选择并上传您的JSON文件，使用提供的数据渲染PDF预览。

![查找IC文档](/help/forms/interactive-communication/assets/localdata.png)

+++

+++3.使用数据模型预览 

3.1.选择&#x200B;**使用数据模型**&#x200B;以使用来自IC的已配置表单数据模型(FDM)的示例数据。

3.2.预览会自动填充模型字段中的数据。 确保首次使用时将示例数据保存在FDM中，否则预览可能会显示为“无数据”。

![查找IC文档](/help/forms/interactive-communication/assets/datamodel.png)

+++

