---
title: 将资产、文件夹和收藏集发布到Brand Portal
description: 将资产、文件夹和收藏集发布到Brand Portal。
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 4677a8771c5891b8c9846e0adb58025304a71bdd

---


# Publish assets to Brand Portal {#publish-assets-to-brand-portal}

作为Adobe Experience Manager(AEM)资产管理员，您可以将资产、文件夹和收藏集发布到AEM Assets Brand Portal实例。 此外，您还可以将资产或文件夹的发布工作流计划到以后的日期或时间。 发布后，Brand Portal用户可以访问资产、文件夹和集合并将其进一步分发给其他用户。

但是，您必须首先使用Brand Portal配置AEM资产。 有关详细信息，请 [参阅配置AEM资产与Brand Portal](configure-aem-assets-with-brand-portal.md)。

如果您随后在AEM资产中对原始资产、文件夹或收藏集进行了修改，则在从AEM资产重新发布之前，这些更改不会反映在Brand Portal中。 此功能可确保在Brand Portal中不提供进行中的更改。 只有管理员发布的已批准更改才可在Brand Portal中使用。

* [将资产发布到Brand Portal](#publish-assets-to-bp)
* [将文件夹发布到Brand Portal](#publish-folders-to-brand-portal)
* [将集合发布到Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe建议交错发布，最好在非高峰时段发布，这样AEM作者就不会占用过多的资源。


## Publish assets to Brand Portal {#publish-assets-to-bp}

以下是将资产从AEM资产发布到Brand Portal的步骤：

1. 从“资产”控制台中，打开父文件夹，选择要发布的所有资产，然后单击工具栏中 **[!UICONTROL 的“快速发布]** ”选项。

   ![publish2bp-2](assets/publish2bp.png)

1. 以下是两种发布资产的方式：
   * [立即发布](#publish-to-bp-now) （立即发布资产）
   * [稍后发布](#publish-to-bp-later) (计划发布资产)

### 立即发布资产 {#publish-to-bp-now}

要将选定资产发布到Brand Portal，请执行以下任一操作：

* 从工具栏中，选择“快 **[!UICONTROL 速发布”]**。 然后，从菜单中，单 **[!UICONTROL 击发布到Brand Portal]**。

* 从工具栏中，选择管 **[!UICONTROL 理发布]**。

   1. 从“操 **[!UICONTROL 作]**”中，选 **[!UICONTROL 择“发布到品牌门户”]**。

      从“计 **[!UICONTROL 划]**”中，选 **[!UICONTROL 择“立即”]**。

      单击&#x200B;**[!UICONTROL 下一步]**。

   2. 在范围中确认您的 **[!UICONTROL 选择]** ，然后单 **[!UICONTROL 击发布到Brand Portal]**。

将显示一条消息，指明资产已排队等候发布到Brand Portal。 登录到Brand Portal界面，查看已发布的资产。

### 稍后发布资产 {#publish-to-bp-later}

要计划将资产发布到Brand Portal以后的日期或时间，请执行以下操作：

1. 选择要计划发布的资产，然后从顶部的工 **[!UICONTROL 具栏中单击]** “管理发布”。

1. 在“管 **[!UICONTROL 理发布]** ”页面上，从“操 **[!UICONTROL 作”中选择]** “发布到品 **[!UICONTROL 牌门户”]**。

   从“计 **[!UICONTROL 划]** ”中 **[!UICONTROL 选择稍后]**。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 选择 **[!UICONTROL 激活日期]** ，并指定时间。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择 **激活日期** ，并指定时间。 单击&#x200B;**下一步**。

1. 在工作流中 **[!UICONTROL 指定工作流]****[!UICONTROL 标题]**。 单击“ **[!UICONTROL 稍后发布]**”。

   ![发布工作流](assets/publishworkflow.png)

登录Brand Portal界面以查看已发布的资产（取决于您的预定日期或时间）。

![bp_landing_page](assets/bp_landing_page.png)


## Publish folders to Brand Portal {#publish-folders-to-brand-portal}

您可以立即发布或取消发布资产文件夹，或计划到以后的日期或时间。

### Publish folders to Brand Portal {#publish-folders-to-bp}

1. 从“资产”控制台中，选择要发布的文件夹，然后单击工 **[!UICONTROL 具栏中的]** “快速发布”选项。

   ![publish2bp](assets/publish2bp.png)

1. **立即发布文件夹**

   要将选定文件夹发布到Brand Portal，请执行以下任一操作：

   * 从工具栏中，选择“快 **[!UICONTROL 速发布”]**。

      从菜单中，选择发 **[!UICONTROL 布到品牌门户]**。

   * 从工具栏中，选择管 **[!UICONTROL 理发布]**。

      1. 从“操 **[!UICONTROL 作]**”中，选 **[!UICONTROL 择“发布到品牌门户”]**。

         从“计 **[!UICONTROL 划]**”中，选 **[!UICONTROL 择“立即”]**。

         Click **Next.**

      1. 在范围中确认您的 **[!UICONTROL 选择]** ，然后单 **[!UICONTROL 击发布到Brand Portal]**。
   将显示一条消息，指明文件夹已排队等候发布到Brand Portal。 登录Brand Portal界面，查看已发布的文件夹。

1. **稍后发布文件夹**

   要将资产文件夹的发布计划到以后的日期或时间，请执行以下操作：

   1. 选择要计划发布的文件夹，从顶部的工具栏中 **[!UICONTROL 选择]** “管理发布”。
   1. 从“操 **[!UICONTROL 作]**”中，选 **[!UICONTROL 择“发布到品牌门户”]**。

      从“计 **[!UICONTROL 划]**”中，选 **[!UICONTROL 择稍后]**。

   1. 选择 **[!UICONTROL 激活日期]** ，并指定时间。 单击&#x200B;**[!UICONTROL 下一步]**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 在范围中确认您 **[!UICONTROL 的选择]**。 单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在工作流下指定工作流 **[!UICONTROL 标题]**。 单击“ **[!UICONTROL 稍后发布]**”。

      ![manageschedulepub](assets/manageschedulepub.png)

### Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

您可以通过从AEM资产实例中取消发布已发布到Brand Portal的任何资产文件夹，来删除该文件夹。 取消发布原始文件夹后，Brand Portal用户将无法再使用其副本。

您可以立即从Brand Portal中取消发布资产文件夹，或计划到以后的日期和时间。

要从Brand Portal取消发布资产文件夹，请执行以下操作：

1. 从“资产”控制台中，选择要取消发布的资产文件夹，然后单击工 **[!UICONTROL 具栏中的]** “管理发布”选项。

   ![publish2bp-1](assets/publish2bp.png)

1. **立即取消发布资产文件夹**

   要立即从Brand Portal中取消发布选定的资产文件夹，请执行以下操作：

   1. 从工具栏中，选择管 **[!UICONTROL 理发布]**。

   1. 从“操 **[!UICONTROL 作]** ”中，选 **[!UICONTROL 择“从Brand Portal取消发布”]**。

      从“计 **[!UICONTROL 划]**”中，选 **[!UICONTROL 择“立即”]**。

      单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在范围中确认您的选 **[!UICONTROL 择]** ，然后单 **[!UICONTROL 击从Brand Portal取消发布]**。

      ![确认——取消发布](assets/confirm-unpublish.png)

1. **稍后取消发布资产文件夹**

   要将资产文件夹的取消发布计划到以后的日期和时间，请执行以下操作：

   1. 从工具栏中，选择管 **[!UICONTROL 理发布]**。

   1. 从“操 **[!UICONTROL 作]**”中，选 **[!UICONTROL 择“从Brand Portal取消发布”]**。

      从“计 **[!UICONTROL 划]**”中，选 **[!UICONTROL 择稍后]**。

   1. 选择 **[!UICONTROL 激活日期]** ，然后指定时间。 单击&#x200B;**[!UICONTROL 下一步]**。

   1. 在范围中确认您的选 **[!UICONTROL 择]** ，然后单击 **[!UICONTROL 下一步]**。

   1. 在工作流中 **[!UICONTROL 指定工作流]****[!UICONTROL 标题]**。 单击“ **[!UICONTROL 稍后取消发布]**”。

      ![取消发布工作流](assets/unpublishworkflows.png)

## Publish collections to Brand Portal {#publish-collections-to-brand-portal}

您可以从AEM Assets云实例中发布或取消发布集合。

>[!NOTE]
>
>内容片段无法发布到Brand Portal。 因此，如果您在AEM资产中选择内容片段，则“发布到 **[!UICONTROL Brand Portal]** ”操作将不可用。
>
>如果包含内容片段的集合从AEM资产发布到Brand Portal，则文件夹中除内容片段外的所有内容将复制到Brand Portal界面。


### 发布集合 {#publish-collections}

以下是将集合从AEM资产发布到Brand Portal的步骤：

1. 在AEM资产UI中，单击AEM徽标。

1. From **Navigation** page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

1. 从“收 **藏集** ”控制台中，选择要发布到Brand Portal的收藏集。

   ![select_collection](assets/select_collection.png)

1. 在工具栏中，单击“ **[!UICONTROL 发布到品牌门户”]**。

1. In the confirmation dialog, click **[!UICONTROL Publish]**.

1. 关闭确认消息。

   以管理员身份登录到Brand Portal。 已发布的集合在“集合”控制台中可用。

   ![已发布集合](assets/published_collection.png)

### 取消发布集合 {#unpublish-collections}

您可以通过从AEM资产实例中取消发布来删除已发布到Brand Portal的任何集合。 在取消发布原始集合后，Brand Portal用户将无法再使用其副本。

以下是取消发布集合的步骤：

1. 从AEM **资产实例的** “收藏集”控制台中，选择要取消发布的收藏集。

   ![select_collection](assets/select_collection-1.png)

1. 在工具栏中，单击“从 **[!UICONTROL Brand Portal中删除]** ”图标。
1. 在对话框中，单击“取 **[!UICONTROL 消发布]**”。
1. 关闭确认消息。 集合将从Brand Portal界面中删除。

除了上述功能，您还可以将元数据模式、图像预设、搜索彩块化和标记从AEM资产发布到Brand Portal。

* [将预设、模式和彩块化发布到Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


有关详细 [信息，请参阅Brand Portal文档](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 。


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
