---
title: 创建页面
description: 了解如何使用站点控制台为您的网站创建新页面。
exl-id: 77264562-e76a-40c8-9878-847a8878fb8e
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 6e13244d7ba7bb6e7a51525b66274427fe21d664
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 27%

---


# 创建页面 {#creating-pages}

了解如何使用&#x200B;**站点**&#x200B;控制台为您的网站创建新页面。

>[!TIP]
>
>在开始创建新页面之前，请熟悉[AEM中页面的组织方式。](/help/sites-cloud/authoring/sites-console/organizing-pages.md)

## 访问权限 {#access-privileges}

您的帐户需要拥有适当的访问权限和权限才能创建页面。

如果您遇到任何问题，请联系您的系统管理员。

## 创建新页面 {#creating-a-new-page}

除非提前为您创建了所有页面，否则必须先创建页面，然后才能开始创建内容：

1. 打开[站点&#x200B;****&#x200B;控制台。](/help/sites-cloud/authoring/sites-console/introduction.md)
1. 导航到要创建新页面的位置。
1. 使用工具栏中的&#x200B;**创建**&#x200B;打开下拉选择器，然后从列表中选择&#x200B;**页**：

   ![创建页面](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. 在向导的第一步中，您可以：

   * 选择要用于创建新页面的模板，然后选择&#x200B;**下一步**&#x200B;以继续或&#x200B;**取消**&#x200B;以中止进程。
   * [页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)和[通用编辑器](/help/edge/wysiwyg-authoring/templates.md)都支持模板。

   ![为新页面选择模板](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. 在向导的最后一步中，您可以：

   * 使用三个选项卡输入您要分配给新页面的[页面属性](/help/sites-cloud/authoring/sites-console/page-properties.md)，然后选择&#x200B;**创建**&#x200B;以实际创建页面。

   * 使用&#x200B;**返回**，可返回到模板选择步骤。

   关键字段为：

   * **标题**：

      * 此字段将显示给用户，是必填字段。

   * **名称**：

      * 用于生成 URI。如果未指定，名称会从标题派生。
      * 如果您在创建页面时提供页面&#x200B;**Name**，AEM [将依据AEM和JCR实行的约定](/help/implementing/developing/introduction/naming-conventions.md)验证此名称。
      * 您在&#x200B;**名称**&#x200B;字段中&#x200B;**无法提交无效的字符**。当AEM检测到无效字符时，该字段会突出显示，并显示说明性消息以指示需要删除/替换的字符。

   >[!TIP]
   >
   >请参阅[页面命名惯例](#page-naming-conventions)。

   创建页面所需的最少信息是&#x200B;**标题**。

   ![提供页面标题](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. 点按或单击&#x200B;**创建**&#x200B;以完成此过程并创建新页面。 确认对话框询问您是要&#x200B;**立即**&#x200B;打开页面，还是返回控制台（**完成**）。 选择一个以结束页面创建过程。

   ![页面创建成功](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   * 如果选择&#x200B;**打开**，**站点**&#x200B;控制台将基于新页面的模板打开相应的编辑器：
      * [页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)
      * [通用编辑器](/help/sites-cloud/authoring/universal-editor/authoring.md)

如果返回控制台，则可以看到新页面：

![生成的新页面](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!NOTE]
>
>如果使用相同位置已存在的名称创建页面，则AEM会使用通过附加一个编号而指定的名称的变体来创建该页面。 例如，如果`beach`已存在，则新页面将变为`beach1`。

>[!CAUTION]
>
>创建页面后，无法更改其模板，除非您[使用新模板](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template)创建启动项，不过这样会丢失任何现有内容。
