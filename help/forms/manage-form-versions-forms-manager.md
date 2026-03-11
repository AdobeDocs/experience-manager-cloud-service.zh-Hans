---
title: 在Forms Manager中管理表单版本
description: 了解如何在Forms Manager UI中创建和管理自适应Forms、表单片段、主题和其他资源的版本。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="适用于AEM Forms)。"
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 5%

---

# 在Forms Manager UI中管理表单Assets版本

<span class="preview">此功能可通过提前访问计划获得。 若要请求访问，请将您的官方地址中的电子邮件发送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。</span>

Forms Manager现在支持对表单资源进行版本控制。 您可以从Forms Manager UI创建版本、查看版本历史记录和恢复资源的早期版本。

## 支持的资源类型 {#supported-asset-types}

您可以创建和管理以下资源类型的版本：

| 资源类型 | 描述 |
|---|---|
| 自适应Forms（核心组件） | 使用核心组件构建的自适应Forms |
| 自适应Forms（基础组件） | 使用基础组件构建的自适应Forms |
| 表单片段 | 在多个表单中共享的可重用表单部分 |
| 主题 | 应用于自适应Forms的可视样式定义 |
| XDP模板 | 基于XFA的表单模板 |
| 二进制资产 | 存储在表单DAM存储库下的其他文件 |

## 创建一个版本 {#create-version-forms-manager}

要创建表单资源的版本，请执行以下操作：

1. 导航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 选择表单或资源。
1. 在左侧面板中，选择&#x200B;**[!UICONTROL 时间轴]**。
1. 单击时间线工具栏中的&#x200B;**[!UICONTROL 另存为版本]**。
   ![另存为版本](/help/forms/assets/create-version.png)
1. 输入&#x200B;**[!UICONTROL 标签]**&#x200B;和可选的&#x200B;**[!UICONTROL 注释]**&#x200B;来说明所做的更改。
1. 单击&#x200B;**[!UICONTROL 创建]**。
   ![另存为版本2](/help/forms/assets/create-version1.png)

时间轴面板中会显示该版本及其标签、注释和时间戳。

## 在上载期间版本化资产 {#version-on-upload}

上传与现有资源同名的资源时，Forms Manager会显示&#x200B;**文件上传**&#x200B;对话框，其中列出了要更新的资源。 该对话框显示资源名称、部分和路径。

如果具有相同名称的资产已存在，则上传操作会替换现有资产并自动创建新版本。 您可以在时间线中查看创建的版本。

![文件上载对话框显示版本化的上载](/help/forms/assets/version-upload.png)

## 查看版本历史记录 {#view-version-history}

要查看资源的版本历史记录，请执行以下操作：

1. 在Forms Manager中选择资源。
1. 在左侧面板中，选择&#x200B;**[!UICONTROL 时间轴]**。
   ![版本历史记录](/help/forms/assets/version-history.png)

时间线显示所有版本条目以及活动事件。 每个条目都会显示标签、注释、作者和时间戳。

## 恢复以前的版本 {#restore-version}

要将资源还原到早期版本，请执行以下操作：

1. 在Forms Manager中选择资源。
1. 在左侧面板中，选择&#x200B;**[!UICONTROL 时间轴]**。
1. 选择要还原的版本。
1. 单击&#x200B;**[!UICONTROL 还原到此版本]**。
   ![还原版本](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>图像无法还原到以前的版本。 所有其他资源类型(包括自适应Forms、表单片段、主题和XDP模板)都支持版本还原。

## 另请参阅 {#see-also}

* [对自适应表单进行版本控制、审核和注释](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [导入和导出表单及相关资产](/help/forms/import-export-forms-templates.md)
* [发布和取消发布表单](/help/forms/publishing-unpublishing-forms.md)
