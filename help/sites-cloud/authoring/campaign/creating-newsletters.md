---
title: 使用AEM创建Campaign新闻稿
description: 了解如何使用AEMas a Cloud Service创建可随Adobe Campaign Classic一起发送的新闻稿。
feature: Authoring
role: User
exl-id: 60a6a9d0-f5e6-424f-b320-dd4943c55d45
source-git-commit: 6196f3fc67dbcfe03a71bb6a0796dd5d1d0f8546
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 1%

---


# 使用AEM创建Campaign新闻稿 {#creating-newsletters}

在本文档中，您将了解如何使用AEMas a Cloud Service创建可随Adobe Campaign Classic一起发送的新闻稿。

利用AEMas a Cloud Service与Adobe Campaign Classic之间的集成，您可以使用AEM功能强大的创作工具创建新闻稿。 然后，当您准备好发送新闻稿时，可以使用Campaign的收件人管理和分发功能发送新闻稿。

## 前提条件 {#prerequisites}

在使用AEM创建新闻稿并通过Campaign发送之前，您必须先 [集成Adobe Campaign Classic和AEMas a Cloud Service。](/help/sites-cloud/integrating/integrating-campaign-classic.md)

## 创建新闻稿结构 {#create-structure}

新闻稿内容在AEM中的管理方式与管理网站内容非常类似。 首先，创建一个“站点”来保存您的内容。 在此“站点”中，您可以按品牌收集新闻稿。

1. 登录您的AEM创作实例。

1. 在主导航页面中，打开 **站点** 控制台。

1. 在AEM的标准安装中，现有 **Campaign** 文件夹。 选择它并单击 **创建** 按钮，然后 **页面**.

   ![创建页面](assets/create-page.png)

1. 选择 **品牌** 作为您的网站模板，单击 **下一个**.

   ![创建品牌](assets/create-brand.png)

1. 输入 **标题** 单击 **创建** 然后 **完成**.

   ![提供品牌详细信息](assets/create-brand-page.png)

现在，您可以使用基本的内容结构来创建营销活动。

![内容结构](assets/content-structure.png)

## 创建营销活动 {#create-campaign}

现在，您已为营销活动设置了基本的内容结构，接下来可以创建营销活动本身。 营销活动将用于组织可能多个新闻稿。

1. 使用 [列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在站点控制台中，选择您之前创建的品牌(在本例中， **WKND转义**)，然后选择 **主控区**，此代码将自动为您创建，然后单击 **创建** 按钮，然后 **页面**.

   ![创建营销活动页面](assets/create-campaign-page.png)

1. 选择 **Campaign** 作为模板，然后单击 **下一个** 和 **完成**.

   ![选择营销活动模板](assets/select-campaign-template.png)

1. 输入 **标题** ，然后单击 **创建** 和 **完成**.

   ![营销活动标题](assets/campaign-title.png)

现在，您有一个营销活动，您可以在其中创建新闻稿。

![活动结构](assets/campaign-structure.png)

## 选择营销活动配置 {#campaign-configuration}

AEM可支持多个集成配置。 对于新营销活动，您必须定义用于发送新闻稿内容的配置。

1. 使用 [列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在站点控制台中，找到您之前创建的营销活动(在本例中， **WKND逃生夏季活动**)，然后使用复选框将其选中，然后单击 **属性** 按钮。

   ![选择营销活动](assets/select-campaign.png)

1. 在 **属性** 窗口，选择 **Cloud Service** 选项卡，以定义要与此营销活动一起使用的集成。

   * 选择 **Adobe Campaign** 从 **Cloud Service配置** 下拉列表。
   * 从 **Adobe Campaign** 下拉列表。
   * 单击&#x200B;**保存并关闭**。

   ![Campaign配置属性](assets/campaign-configuration-properties.png)

您的营销活动现已链接到Adobe Campaign集成。 您可以在AEM中创建新闻稿，然后随Adobe Campaign一起发送。

## 创建新闻稿 {#create-newsletter}

您可以在已创建和配置的营销活动内容结构下创建和管理新闻稿。

1. 使用 [列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在站点控制台中，找到您之前配置的营销活动(在本例中， **WKND逃生夏季活动**)，选择它，然后单击 **创建** 按钮，然后 **页面**.

   ![创建新闻稿](assets/create-newsletter.png)

1. 在创建页面向导中，选择 **Adobe Campaign电子邮件(AC 6.1)** 模板，单击 **下一个**.

   ![选择营销活动电子邮件模板](assets/adobe-campaign-email-template.png)

1. 对于 **属性** 在向导的步骤中，输入 **标题** 对于新闻稿，单击 **创建** 和 **打开**.

   ![新闻稿的标题](assets/create-newsletter-wizard-properties.png)

1. 与编辑任何其他AEM内容页面一样，编辑新闻稿页面以满足您的要求。

您现在已准备好随Adobe Campaign一起发送新闻稿。

## 发布新闻稿 {#publishing-newsletter}

您必须发布新闻稿，才能将新闻稿提供给Adobe Campaign发送。

1. 使用 [列视图](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 在站点控制台中，找到您之前创建的新闻稿(在本例中为 **WKND逃生夏季促销活动的首份新闻稿**)，选择它，然后单击 **页面信息** 按钮，单击 **发布页面**.

1. 选择应为其发布页面的配置，然后单击 **发布**.

   ![发布页面](assets/publish.png)

新闻稿页面现已发布到AEM发布实例，并在Adobe Campaign Classic中可见。 要在Adobe Campaign中选择它，必须获得批准。

1. 单击 **页面信息** 按钮，然后选择 **启动工作流**.

1. 选择 **批准Adobe Campaign** 作为工作流模型（可选地提供描述），然后单击 **启动工作流** 按钮。

   ![启动工作流](assets/start-workflow.png)

1. 新闻稿页面编辑器的顶部会显示一个横幅，提供批准流程中的后续步骤。 单击 **完成**.

   ![批准工作流](assets/approve-workflow.png)

1. 在 **完成工作项** 对话框，选择 **新闻稿审核（管理员）** 在 **下一步** 下拉列表中，然后单击 **确定** 按钮。

   ![新闻稿审阅](assets/newsletter-review.png)

1. 在新闻稿页面编辑器顶部显示的横幅中，再次单击 **完成**.

1. 在 **完成工作项** 对话框，选择 **新闻稿批准** 在 **下一步** 下拉列表中，然后单击 **确定** 按钮。

   ![新闻稿批准](assets/newsletter-approval.png)

1. 当对话框关闭时，在新闻稿页面编辑器顶部显示的横幅会消失，因为审批工作流程已完成。

新闻稿现已在AEM中发布，并且已获准在Adobe Campaign中使用。

>[!TIP]
>
>此处简化了描述的工作流步骤，以说明该过程。 在正常工作流程中，创建新闻稿并批准其工作通常是不同的角色
>
>查看文档 [使用工作流](/help/sites-cloud/authoring/workflows/overview.md) 有关使用工作流的更多详细信息。

## 创建收件人 {#creating-recipient}

要发送您在AEM中创建的新闻稿，您必须先在Adobe Campaign Classic中定义收件人。

1. 使用客户端控制台登录Adobe Campaign Classic。

1. 选择 **工具** -> **资源管理器** 菜单栏。

1. 在资源管理器中，导航到 **用户档案和目标** -> **收件人** 节点。

   ![收件人](assets/recipients.png)

1. 单击 **新建** ，并提供收件人的详细信息。

   * 名字
   * 姓氏
   * 电子邮件地址

1. 单击&#x200B;**保存**。

现在，您有一个收件人，您可以使用Adobe Campaign Classic将新闻稿发送给该收件人。

## 创建电子邮件投放 {#create-delivery}

最后一步是将您在AEM中创建的Newsletter发送给您在Adobe Campaign Classic中添加的收件人。

1. 使用客户端控制台登录Adobe Campaign Classic。

1. 选择 **工具** -> **资源管理器** 菜单栏。

1. 在资源管理器中，导航到 **Campaign Management** -> **投放** 节点，单击 **新建**.

   ![AEM内容交付](assets/delivery-aem-content.png)

1. 在 **投放** 对话框，选择 **包含AEM内容的电子邮件投放** 作为 **投放模板** 从下拉列表中，单击 **继续**.

   ![AEM内容交付](assets/aem-content-delivery.png)

1. 在 **电子邮件参数** ，单击 **从** 链接并输入发件人的信息，然后单击 **确定**.

   * 发件人地址
   * 从字段

   ![从字段定义](assets/delivery-from.png)

1. 在 **电子邮件参数** ，单击 **至** 用于打开的链接 **选择目标** 对话框，然后单击 **添加**.

   ![选择目标](assets/select-target.png)

1. 在 **选择目标元素** 对话框，选择 **收件人** 单击 **下一个**.

   ![选择目标元素](assets/select-target-element.png)

1. 使用过滤器，选择您的收件人 [创建之前](#creating-recipient) 单击 **完成**.

   ![选择收件人](assets/select-target-element-recipient.png)

1. 返回 **选择目标** 对话框，单击 **确定**.

1. 在投放窗口中，单击 **同步**.

   ![同步](assets/synchronize.png)

1. 在 **与AEM内容同步** 对话框中，从列表中选择您之前创建的新闻稿，单击 **确定**.

1. Adobe Campaign的电子邮件内容将与您在AEM中创建的新闻稿内容同步。

   * 单击 **刷新内容** 如果内容未自动加载。

1. 单击 **发送** 来发送电子邮件。

1. 在 **发送到主投放目标** 对话框，选择 **尽快交货** 然后单击 **分析**.

   ![投放分析](assets/delivery-analysis.png)

1. 分析步骤可构建投放，将内容与收件人结合在一起。 创建投放后，单击 **确认投放** 发送电子邮件。 单击&#x200B;**“是”**&#x200B;以确认。

1. 投放已开始。 单击&#x200B;**关闭**。

   ![交付](assets/delivering.png)

1. 单击 **保存** 以保存投放。

您的新闻稿已发送！

>[!TIP]
>
>此示例显示了向单个收件人发送新闻稿的简化交付过程。 当然，正常投放中会包含许多不同的收件人，而Adobe Campaign可以轻松管理这些收件人。 请参阅 [Adobe Campaign Classic文档](https://experienceleague.adobe.com/docs/campaign-classic.html) 有关投放和收件人管理的更多详细信息。
