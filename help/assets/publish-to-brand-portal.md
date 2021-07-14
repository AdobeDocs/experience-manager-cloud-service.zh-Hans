---
title: 将资产、文件夹和收藏集发布到 Brand Portal
description: 将资产、文件夹和收藏集发布到 Brand Portal。
contentOwner: Vishabh Gupta
feature: Brand Portal,Asset Distribution，配置
role: User
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 13ea0161771776f23d3789adfb8487df06a7e4b1
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 97%

---

# 将资产发布到 Brand Portal {#publish-assets-to-brand-portal}

作为 Adobe Experience Manager (AEM) Assets 管理员，您可以将资产、文件夹和收藏集发布到 AEM Assets Brand Portal 实例。此外，您还可以安排在稍后的日期或时间执行资产或文件夹的发布工作流。发布后，Brand Portal 用户可以访问资产、文件夹和收藏集，并将其进一步分发给其他用户。

但是，您必须首先使用 Brand Portal 配置 AEM Assets。有关详细信息，请参阅[使用 Brand Portal 配置 AEM Assets](configure-aem-assets-with-brand-portal.md)。

如果您随后在 AEM Assets 中对原始资产、文件夹或收藏集进行了修改，则在从 AEM Assets 重新发布之前，这些更改不会反映在 Brand Portal 中。此功能可确保在 Brand Portal 中不会出现进行中的更改。只有管理员发布的已批准更改才会出现在 Brand Portal 中。

* [将资产发布到 Brand Portal](#publish-assets-to-bp)
* [将文件夹发布到 Brand Portal](#publish-folders-to-brand-portal)
* [将收藏集发布到 Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe 建议实施错峰发布，最好在非高峰时段发布，这样 AEM 作者就不会占用过多的资源。

## 将资产发布到 Brand Portal {#publish-assets-to-bp}

以下是将资产从 AEM Assets 发布到 Brand Portal 的步骤：

1. 在 Assets 控制台中，打开父文件夹，选择要发布的所有资产，然后单击工具栏中的&#x200B;**[!UICONTROL 快速发布]**&#x200B;选项。

   ![publish2bp-2](assets/publish2bp.png)

1. 以下是发布资产的两种方式：
   * [立即发布](#publish-to-bp-now)（立即发布资产）
   * [稍后发布](#publish-to-bp-later)（计划发布资产）

### 立即发布资产 {#publish-to-bp-now}

要将选定资产发布到 Brand Portal，请执行以下任一操作：

* 在工具栏中，选择&#x200B;**[!UICONTROL 快速发布]**。然后，在菜单中，单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

* 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

   1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;中，选择&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

      在&#x200B;**[!UICONTROL 计划]**&#x200B;中，选择&#x200B;**[!UICONTROL 立即]**。

      单击&#x200B;**[!UICONTROL 下一步]**。

   2. 在&#x200B;**[!UICONTROL 范围]**&#x200B;中确认您的选择，然后单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

此时将显示一条消息，表明资产已排队等候发布到 Brand Portal。登录到 Brand Portal 界面可查看已发布的资产。

### 稍后发布资产 {#publish-to-bp-later}

要计划在稍后的日期或时间将资产发布到 Brand Portal，请执行以下操作：

1. 选择计划发布的资产，然后单击顶部工具栏中的&#x200B;**[!UICONTROL 管理发布]**。

1. 在&#x200B;**[!UICONTROL 管理发布]**&#x200B;页面上，从&#x200B;**[!UICONTROL 操作]**&#x200B;中选择&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

   在&#x200B;**[!UICONTROL 计划]**&#x200B;中选择&#x200B;**[!UICONTROL 稍后]**。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 选择&#x200B;**[!UICONTROL 激活日期]**，并指定时间。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择&#x200B;**激活日期**，并指定时间。单击&#x200B;**下一步**。

1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流标题]**。单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![publishworkflow](assets/publishworkflow.png)

登录 Brand Portal 界面可查看已发布的资产（取决于您的计划日期或时间）。

![bp_landingpage](assets/bp_landingpage.png)


## 将文件夹发布到 Brand Portal {#publish-folders-to-brand-portal}

您可以立即发布或取消发布资产文件夹，或安排在稍后的日期或时间执行操作。

### 将文件夹发布到 Brand Portal {#publish-folders-to-bp}

1. 在 Assets 控制台中，选择要发布的文件夹，然后单击工具栏中的&#x200B;**[!UICONTROL 快速发布]**&#x200B;选项。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到 Brand Portal，请执行以下任一操作：

   * 在工具栏中，选择&#x200B;**[!UICONTROL 快速发布]**。

      在菜单中，选择&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

   * 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

      1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;中，选择&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

         在&#x200B;**[!UICONTROL 计划]**&#x200B;中，选择&#x200B;**[!UICONTROL 立即]**。

         单击&#x200B;**下一步**。

      1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;中确认您的选择，然后单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

   此时将显示一条消息，表明文件夹已排队等候发布到 Brand Portal。登录到 Brand Portal 界面可查看已发布的文件夹。

1. **稍后发布文件夹**

   要计划在稍后的日期或时间发布资产文件夹，请执行以下操作：

   1. 选择计划发布的文件夹，然后单击顶部工具栏中的&#x200B;**[!UICONTROL 管理发布]**。
   1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;中，选择&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

      在&#x200B;**[!UICONTROL 计划]**&#x200B;中，选择&#x200B;**[!UICONTROL 稍后]**。

   1. 选择&#x200B;**[!UICONTROL 激活日期]**，并指定时间。单击&#x200B;**[!UICONTROL 下一步]**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;中确认您的选择。单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;下指定工作流标题。单击&#x200B;**[!UICONTROL 稍后发布]**。

      ![manageschedulepub](assets/manageschedulepub.png)

### 从 Brand Portal 取消发布文件夹 {#unpublish-folders-from-brand-portal}

您可以通过从 AEM Assets 实例中取消发布已发布到 Brand Portal 的任何资产文件夹，来删除该文件夹。取消发布原始文件夹后，Brand Portal 用户将无法再使用其副本。

您可以立即从 Brand Portal 中取消发布资产文件夹，或安排在稍后的日期和时间取消发布。

要从 Brand Portal 取消发布资产文件夹，请执行以下操作：

1. 在 Assets 控制台中，选择要取消发布的资产文件夹，然后单击工具栏中的&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项。

   ![publish2bp-1](assets/publish2bp.png)

1. **立即取消发布资产文件夹**

   要立即从 Brand Portal 中取消发布选定的资产文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

   1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;中，选择&#x200B;**[!UICONTROL 从 Brand Portal 取消发布]**。

      在&#x200B;**[!UICONTROL 计划]**&#x200B;中，选择&#x200B;**[!UICONTROL 立即]**。

      单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;中确认您的选择，然后单击&#x200B;**[!UICONTROL 从 Brand Portal 取消发布]**。

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **稍后取消发布资产文件夹**

   要计划在稍后的日期和时间取消发布资产文件夹，请执行以下操作：

   1. 在工具栏中，选择&#x200B;**[!UICONTROL 管理发布]**。

   1. 在&#x200B;**[!UICONTROL 操作]**&#x200B;中，选择&#x200B;**[!UICONTROL 从 Brand Portal 取消发布]**。

      在&#x200B;**[!UICONTROL 计划]**&#x200B;中，选择&#x200B;**[!UICONTROL 稍后]**。

   1. 选择&#x200B;**[!UICONTROL 激活日期]**，并指定时间。单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;中确认您的选择，然后单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流标题]**。单击&#x200B;**[!UICONTROL 稍后取消发布]**。

      ![unpublishworkflows](assets/unpublishworkflows.png)

## 将收藏集发布到 Brand Portal {#publish-collections-to-brand-portal}

您可以从 AEM Assets 云实例中发布或取消发布收藏集。

>[!NOTE]
>
>无法将内容片段发布到 Brand Portal。因此，如果您在 AEM Assets 中选择内容片段，则&#x200B;**[!UICONTROL 发布到 Brand Portal]** 操作将不可用。
>
>如果将包含内容片段的收藏集从 AEM Assets 发布到 Brand Portal，则文件夹中除内容片段外的所有内容将复制到 Brand Portal 界面。

### 发布收藏集 {#publish-collections}

以下是将收藏集从 AEM Assets 发布到 Brand Portal 的步骤：

1. 在 AEM Assets UI 中，单击 AEM 徽标。

1. 在&#x200B;**导航**&#x200B;页面中，转到 **[!UICONTROL Assets]** > **[!UICONTROL 收藏集]**。

1. 在&#x200B;**收藏集**&#x200B;控制台中，选择要发布到 Brand Portal 的收藏集。

   ![select_collection](assets/select_collection.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 发布到 Brand Portal]**。

1. 在确认对话框中，单击&#x200B;**[!UICONTROL 发布]**。

1. 关闭确认消息。

   以管理员身份登录到 Brand Portal。已发布的收藏集将显示在“收藏集”控制台中。

   ![已发布的收藏集](assets/published_collection.png)

### 取消发布收藏集 {#unpublish-collections}

您可以通过从 AEM Assets 实例中取消发布已发布到 Brand Portal 的任何收藏集，来删除该收藏集。取消发布原始收藏集后，Brand Portal 用户将无法再使用其副本。

以下是取消发布收藏集的步骤：

1. 从 AEM Assets 实例的&#x200B;**收藏集**&#x200B;控制台中，选择要取消发布的收藏集。

   ![select_collection](assets/select_collection-1.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 从 Brand Portal 中删除]**&#x200B;图标。
1. 在对话框中，单击&#x200B;**[!UICONTROL 取消发布]**。
1. 关闭确认消息。收藏集将从 Brand Portal 界面中删除。

除了上述功能，您还可以将元数据架构、图像预设、搜索 Facet 和标记从 AEM Assets 发布到 Brand Portal。

* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


有关详细信息，请参阅 [Brand Portal 文档](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)。


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
