---
title: 向表单添加版本控制、注释和批注。
description: 使用自适应表单核心组件向自适应表单添加注释、批注和版本控制。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Adaptive Forms, Core Components
hidefromtoc: true
source-git-commit: e71e247f5b6de806b36c5c759b29e7273511f94e
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# 对自适应表单进行版本控制、审核和注释

<!--Before you can use versionings, comments, and annotations in an Adaptive Form, you must ensure you have [enabled Adaptive Form Core Components](
https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).-->

<!--Adaptive Form Core Components facilitates to add versionings, comments, and annotations to a form. These features helps form authors and users to enhance the form development process where they can create multiple versions of a form, collaborate and add their comments to a form, and add annotations to form components.-->

<span class="preview">这是一项预发布功能，可通过我们的[预发布渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>


自适应表单核心组件提供的功能使表单作者能够将版本控制、注释和批注合并到表单中。 这些功能通过允许用户创建和管理表单的多个版本、通过注释参与协作讨论、将注释附加到特定表单组件来简化表单开发过程，从而增强整体表单构建体验。


## 自适应表单版本控制 {#adaptive-form-versioning}

自适应表单版本控制有助于向表单添加版本。 表单作者可以轻松创建表单的多个版本，并最终使用适合业务目标的版本。 此外，表单用户也可以将表单还原到以前的版本。 它还可以帮助作者通过预览表单来比较表单的任意两个版本，使他们能够更好地从UI角度分析表单。 让我们详细了解每个自适应表单版本控制功能：

### 创建表单版本 {#create-a-form-version}

要创建表单的版本，请执行以下步骤：

1. 创建表单或使用现有表单。
1. 在AEM UI上，导航到 **[!UICONTROL 表单]**>>**[!UICONTROL Forms和文档]** 并选择您的 **表单**.
1. 在左侧面板上的选择下拉菜单中，选择 **[!UICONTROL 版本]**.
   ![选择表单](select-a-form.png)
1. 单击 **三点** 位于左下面板上，单击 **[!UICONTROL 另存为版本]**.
1. 现在，为表单版本提供一个标签，您可以通过注释提供有关表单的信息。
   ![创建表单版本](create-a-form-version.png)

### 更新表单版本 {#update-a-form-version}

编辑和更新自适应表单时，会向表单添加新版本。 按照上一节中给出的步骤命名该表单的新版本，如图所示：

![更新表单版本](update-a-form-version.png)

### 还原表单版本 {#revert-a-form-version}

要将表单版本还原到上一个版本，请选择一个表单版本，然后单击 **[!UICONTROL 还原到此版本]**.

![还原表单版本](revert-form-version.png)

### 比较表单版本 {#compare-form-versions}

表单作者可以比较表单的两个不同版本以进行预览。 要比较版本，请选择任意表单版本，然后单击 **[!UICONTROL 与当前比较]**. 它在预览模式下显示两个不同的表单版本。

![比较表单版本](compare-form-versions.png)

## 添加评论 {#add-comments}

审阅是一种允许一个或多个审阅人对表单进行评论的机制。 任何表单用户均可对表单进行注释或通过注释审阅表单。 要在表单上添加评论，请选择 **[!UICONTROL 表单]**，并添加 **[!UICONTROL 注释]** 到窗体。

>[!NOTE]
> 如上所述，在自适应表单核心组件中使用注释时，表单功能 [创建和管理表单审核](/help/forms/create-reviews-forms.md) 已禁用。


![在表单上添加评论](form-comments.png)

## 添加注释 {#adaptive-form-annotations}

在许多情况下，表单组用户需要向表单添加注释以进行审阅，例如在表单的特定选项卡上或表单的组件上。 在这种情况下，作者可以使用注释。 要将注释添加到表单，请执行以下步骤：

1. 在中打开表单 **[!UICONTROL 编辑]** 模式。

1. 单击 **“添加”图标** ，如图所示。
   ![注释](annotation.png)

1. 单击 **“添加”图标** 位于左上边栏的图像，用于添加注释。
   ![添加注释](add-annotation.png)

1. 现在，您可以添加注释，用多种颜色绘制草图以形成组件。

1. 要查看您在表单中添加的所有注释，请选择您的表单，然后您会看到在左侧面板中添加的注释，如图像所示。

   ![查看添加的批注](see-annotations.png)

## 另请参阅 {#see-also}

{{see-also}}
