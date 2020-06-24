---
title: 管理受众
description: 受众控制台使您能够创建、组织和管理Adobe Target帐户的受众，或管理ContextHub的区段
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 57%

---


# 管理受众{#managing-audiences}

受众控制台允许您为Adobe Target帐户创建、组织和管理受众，或管理ContextHub的区段：

* 添加受众 - Adobe Target 受众或 ContextHub 区段。
* 管理受众。

An Audience, called *segment* in ContextHub, is a class of visitors defined by specific criteria, which then determines who sees a targeted activity. 定位活动时，您可以直接在“定位”过程中选择受众，也可以在“受众”控制台中创建新受众。

在“受众”控制台中，各受众按品牌进行组织。

Audiences are available in Targeting mode for [authoring targeted content](/help/sites-cloud/authoring/personalization/targeted-content.md), where you can also create audiences (but you need to create Adobe Target audiences in the Audiences console). 在“定位”模式下创建的受众会显示在“受众”控制台中。

受众显示有相应的标签，用于说明定义的受众类型：

* CH - ContextHub 区段
* AT - Adobe Target 受众

## 在“受众”控制台中创建 ContextHub 区段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在“受众”控制台中或在定位过程中创建 ContextHub 区段。

要在“受众”控制台中创建 ContextHub 区段，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.
1. 单击或点按&#x200B;**创建 ContextHub 区段**。

   ![创建区段](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. 在&#x200B;**新 ContextHub 区段**&#x200B;对话框中，输入标题并调整提升，然后单击&#x200B;**创建**。您的新ContextHub区段将显示在受众列表中。

   >[!NOTE]
   >
   >您可以通过点按或单击“已修改”来对修改列 **表进行排序** ，按降序排序，以查看任何新创建的受众。

For further detail about creating segments using ContextHub, please see the Configuring Segmentation with ContextHub documentation. <!--For further detail about creating segments using ContextHub, please see the [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) documentation.-->

## 使用“受众”控制台创建 Adobe Target 受众 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以直接在 AEM 中使用“受众”控制台创建 Adobe Target 受众。

受众由确定目标活动中包含哪些人的规则进行定义。受众定义可以包含多个规则，每个规则可以包含多个参数。

使用多个规则时，这些规则会通过布尔运算符 AND 进行组合，这意味着任何潜在的受众成员必须满足所有定义的条件才能包含在活动中。例如，如果您定义了操作系统规则和浏览器规则，则只有同时使用定义的操作系统和定义的浏览器的访客才会包含在活动中。

>[!NOTE]
>
>如果“创建”菜 **单中未显示** “创建 **** 目标受众”，则您没有创建受众的必要权限。 您需要下面的写 `/etc/segmentation` 入权限才能创建受众。 默认情况下，组内容作者具有写权限。

要创建 Adobe Target 受众，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.

   ![导航到受众](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. In the Audiences console, tap or click **Create** and then** Create Target Audience**.

   ![创建目标受众](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. 在 **Adobe Target 配置**&#x200B;对话框中，选择目标配置，然后单击或点按&#x200B;**确定**。
1. 在“规则#1”区域中，单击或点按属性类型并在可用字段中输入任何属性信息。完成后，选中该属性右侧的复选标记以保存该属性。有关所有属性的信息，请参阅[属性及其选项](#attributes-and-their-options)。
1. 单击 **添加规则** ，以添加其他规则。 根据需要输入任意数量的规则。 规则与布尔运算符AND相结合，这意味着受众必须满足每个规则的所有要求才能符合活动条件。
1. 单击或点按&#x200B;**下一步**。
1. 为受众输入一个名称，然后单击或点按&#x200B;**保存**。
1. Tap or click **Save**. 受众随即会列在“受众”列表中。

### 属性及其选项 {#attributes-and-their-options}

您可以为以下每个属性创建定位规则。

| **属性** | **描述** | **有关更多信息** |
|---|---|---|
| **移动设备** | 根据移动设备、设备类型、设备供应商、屏幕尺寸（按像素）等参数目标移动设备。 | 请参 [阅移动文档](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/mobile.html) (Adobe Target)。 |
| **自定义** | 自定义参数是mbox参数。 如果您将任何 mbox 参数传递给 mbox，或者使用 targetPageParams 函数，这些参数将会显示在此处以供在受众中使用。 | 请参 [阅自定义参数](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) (Adobe Target)。 |
| **操作系统** | 您可以目标使用特定操作系统的访客。 | 目标使用Linux、Macintosh或Windows的用户。 |
| **站点页面** | 目标访客，他们位于特定页面或具有特定mbox参数。 | 请参 [阅站点页面文档](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/site-pages.html) (Adobe Target)。 |
| **浏览器** | 您可以目标在用户访问您的页面时使用特定浏览器或特定浏览器选项的用户。 | 请参 [阅浏览器选项文档](https://docs.adobe.com/help/en/target/using/audiences/create-audiences/categories-audiences/browser.html) (Adobe Target)。 |
| **访客配置文件** | 目标访客符合特定用户档案参数。 | 请参阅 [访客用户档案文档](https://docs.adobe.com/content/help/en/target/using/audiences/visitor-profiles/visitor-profile.html) (位于Adobe Target)。 |
| **流量源** | 目标访客基于搜索引擎或将其引用到您网站的登陆页。 | 请参 [阅Adobe Target的](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) “流量源”文档。 |

## 在“受众”控制台中修改受众 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能编辑在当前所编辑的相同 AEM 实例中创建的 Adobe Target 受众。无法编辑在不同的 AEM 环境中创建的目标受众。

您可以从“受众”控制台编辑任何ContextHub受众。 您还可以编辑Adobe Target受众，但只能编辑在AEM中创建的：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。Click or tap **Audiences**.
1. Tap or click the icon next to the ContextHub segment you want to edit, and tap or click **Edit**.
1. 在区段编辑器中进行任何编辑。有关详细信息，请参阅ContextHub文档。 <!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
