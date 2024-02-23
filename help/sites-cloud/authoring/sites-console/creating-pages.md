---
title: 创建页面
description: 了解如何使用站点控制台为您的网站创建新页面。
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 64%

---


# 创建页面 {#creating-pages}

了解如何使用为您的网站创建新页面 **站点** 控制台。

>[!TIP]
>
>在开始创建新页面之前，请熟悉 [如何在AEM中组织页面。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## 访问权限 {#access-privileges}

您的帐户需要拥有适当的访问权限和权限才能创建页面。

如果您遇到任何问题，我们建议您与系统管理员联系。

## 创建新页面 {#creating-a-new-page}

除非提前为您创建了所有页面，否则必须先创建页面，然后才能开始创建内容：

1. 打开 [该 **站点** 控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航到要创建新页面的位置。
1. 使用工具栏中的&#x200B;**创建**&#x200B;打开下拉选择器，然后从列表中选择&#x200B;**页**：

   ![创建页面](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. 在向导的第一步中，您可以执行以下操作之一：

   * 选择要用于创建新页面的模板，然后选择 **下一个** 以继续。

   * 单击/点按&#x200B;**取消**&#x200B;可中止该过程。

   ![为新页面选择模板](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. 在向导的最后一步中，您可以执行以下操作之一：

   * 使用三个选项卡输入 [页面属性](/help/sites-cloud/authoring/sites-console/page-properties.md) 您希望指派给新页面，然后选择 **创建** 以实际创建页面。

   * 使用&#x200B;**返回**，可返回到模板选择步骤。

   关键字段为：

   * **标题**：

      * 此字段将显示给用户，是必填字段。

   * **名称**：

      * 用于生成 URI。如果未指定，名称会从标题派生。
      * 如果您提供页面 **名称** 创建页面时，AEM [按照约定验证名称](/help/implementing/developing/introduction/naming-conventions.md) 由AEM和JCR强制实施。
      * 您在&#x200B;**名称**&#x200B;字段中&#x200B;**无法提交无效的字符**。当 AEM 检测到无效字符时，此字段会突出显示，并出现一条说明性消息以指示需要删除/替换的字符。

   >[!TIP]
   >
   >请参阅[页面命名惯例](#page-naming-conventions)。

   创建页面所需的最少信息是 **标题**.

   ![提供页面标题](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 使用&#x200B;**创建**&#x200B;完成此过程并创建新页面。确认对话框将询问您是要立即&#x200B;**打开**&#x200B;该页面，还是返回控制台（**完成**）：

   ![页面创建成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >如果您在创建页面时使用的名称在该位置已经存在，则系统将通过附加一个编号来自动生成该名称的变体。例如，如果 `beach` 已经存在，则新页面会变为 `beach1`。

1. 如果返回控制台，则可以看到新页面：

   ![生成的新页面](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>创建页面后，无法更改其模板 - 除非[使用新模板创建启动项](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)，不过这样会丢失任何现有的内容。
