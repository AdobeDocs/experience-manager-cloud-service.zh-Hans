---
title: 管理发布
description: Publish或将资源取消发布到Experience Manager Assets、Dynamic Media和Brand Portal
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 4%

---

# 在Experience Manager Assets中管理发布 {#manage-publication-in-aem}

作为[!DNL Adobe Experience Manager Assets]管理员，您可以将包含资源的资源和文件夹从创作实例发布到[!DNL Experience Manager Assets]、[!DNL Dynamic Media]和[!DNL Brand Portal]。 此外，您还可以计划在稍后的日期或时间发布资产或文件夹。 发布后，用户可以访问资产，并进一步将资产分发给其他用户。 默认情况下，您可以将资源和文件夹发布到[!DNL Experience Manager Assets]。 但是，您可以将[!DNL Experience Manager Assets]配置为启用发布到[[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html)和[[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html)。

您可以使用[!DNL Experience Manager Assets]界面中提供的&#x200B;**[!UICONTROL 快速Publish]**&#x200B;或&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项，在资源或文件夹级别发布或取消发布资源。 如果您对[!DNL Experience Manager Assets]中的原始资源或文件夹进行后续修改，则在从[!DNL Experience Manager Assets]重新发布之前，这些更改不会反映在发布实例中。 它可确保进行中的更改在发布实例中不可用。 发布实例中只有管理员发布的已批准更改可用。

* [使用Quick Publish的Publish资源](#quick-publish)
* 使用“管理发布”的[Publish资源](#manage-publication)
* [稍后Publish资源](#publish-assets-later)
* [Publish资源到Dynamic Media](#publish-assets-to-dynamic-media)
* [Publish资源到Brand Portal](#publish-assets-to-brand-portal)
* [要求发布](#request-publication)
* [限制和提示](#limitations-and-tips)

## 使用Quick Publish的Publish资源 {#quick-publish}

通过快速发布，可立即将内容发布到所选目标。 从[!DNL Experience Manager Assets]控制台中，导航到父文件夹，然后选择要发布的所有资源或文件夹。 在工具栏中单击&#x200B;**[!UICONTROL 快速Publish]**&#x200B;选项，然后从下拉列表中选择要发布资源的目标。

![快速发布](assets/quick-publish-to-aem.png)

## 使用管理发布管理Publish资源 {#manage-publication}

管理发布允许您向所选目标发布内容或从中取消发布内容，[将内容从DAM存储库添加到发布列表，[包含文件夹设置](#include-folder-settings)以发布所选文件夹的内容并应用筛选器，以及[将发布安排](#publish-assets-later)安排在以后的日期或时间。](#add-content)

从[!DNL Experience Manager Assets]控制台中，导航到父文件夹，然后选择要发布的所有资源或文件夹。 单击工具栏中的&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项。 如果您未在您的[!DNL Experience Manager Assets]实例中配置[!DNL Dynamic Media]和[!DNL Brand Portal]，则只能将资源和文件夹发布到[!DNL Experience Manager Assets]。

![管理发布](assets/manage-publication-aem.png)

以下选项在[!UICONTROL 管理发布]界面中可用：

* [!UICONTROL 操作]
   * `Publish`： Publish资源和文件夹到所选目标
   * `Unpublish`：从目标取消发布资源和文件夹

* [!UICONTROL 目标]
   * `Publish`： Publish资源和文件夹到[!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`： Publish资源到[!DNL Dynamic Media]
   * `Brand Portal`：Publish资源和文件夹到[!DNL Brand Portal]

* [!UICONTROL 计划]
   * `Now`：立即Publish资源
   * `Later`：基于`Activation`日期或时间的Publish资源

若要继续，请单击&#x200B;**[!UICONTROL 下一步]**。 根据选择，**[!UICONTROL 范围]**&#x200B;选项卡反映不同的选项。 **[!UICONTROL 添加内容]**&#x200B;和&#x200B;**[!UICONTROL 包含文件夹设置]**&#x200B;的选项仅可用于将资产和文件夹发布到[!DNL Experience Manager Assets] (`Destination: Publish`)。

![管理发布范围](assets/manage-publication-aem-scope.png)

### 添加内容 {#add-content}

发布到[!DNL Experience Manager Assets]允许您进一步向发布列表添加更多内容（资产和文件夹）。 您可以在dam存储库中将更多资源或文件夹添加到列表中。 单击“**[!UICONTROL 添加内容]**”按钮可添加更多内容。

您可以从一个文件夹添加多个资源，也可以一次添加多个文件夹。 但是，您无法一次从多个文件夹添加资源。

![添加内容](assets/manage-publication-add-content.png)

### 包括文件夹设置 {#include-folder-settings}

默认情况下，将文件夹发布到[!DNL Experience Manager Assets]会发布所有资产、子文件夹及其引用。

要筛选要发布的文件夹内容，请单击&#x200B;**[!UICONTROL 包含文件夹设置]**：

* `Include folder contents`

   * 启用：发布选定文件夹的所有资源、子文件夹（包括子文件夹的所有资源）和引用。
   * 已禁用：仅发布选定的文件夹（空）和引用。 所选文件夹的资产未发布。

* `Include folder contents` 和 `Include only immediate folder contents`

  如果同时选择了这两个选项，则会发布选定文件夹、子文件夹（空）和引用的所有资产。 子文件夹的资产未发布。

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![包含文件夹设置](assets/manage-publication-include-folder-settings.png)

应用筛选器后，单击&#x200B;**[!UICONTROL 确定]**，然后单击&#x200B;**[!UICONTROL Publish]**。 单击“发布”按钮时，将显示确认消息`Resource(s) have been scheduled for publication`。 选定的资源和（或）文件夹将发布到基于计划程序（`Now`或`Later`）的已定义目标。 登录到发布实例，验证是否已成功发布资产和（或）文件夹。

![Publish到AEM](assets/manage-publication-publish-aem.png)

在上图中，您可以看到&#x200B;**[!UICONTROL Publish Target]**&#x200B;属性的不同值。 让我们回顾您选择发布到[!DNL Experience Manager Assets] (`Destination: Publish`)的事实。 那么，它为何显示只有一个文件夹和一个资产发布到`AEM`，而另外两个资产同时发布到`AEM`和`Dynamic Media`？

在这里，您必须了解文件夹属性的角色。 文件夹的&#x200B;**[!UICONTROL Dynamic Media发布模式]**&#x200B;属性在发布过程中扮演着重要角色。 要查看文件夹的属性，请选择一个文件夹，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。 有关资产，请参阅其父文件夹的属性。

下表说明发布如何根据定义的&#x200B;**[!UICONTROL 目标]**&#x200B;和&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;进行：

| [!UICONTROL 目标] | [!UICONTROL Dynamic Media Publish模式] | [!UICONTROL Publish Target] | 允许的内容 |
| --- | --- | --- | --- |
| 发布 | 选择性发布 | `AEM` | Assets和（或）文件夹 |
| 发布 | 即时 | `AEM` 和 `Dynamic Media` | Assets和（或）文件夹 |
| 发布 | 激活后 | `AEM` 和 `Dynamic Media` | Assets和（或）文件夹 |
| Dynamic Media | 选择性发布 | `Dynamic Media` | 资源 |
| Dynamic Media | 即时 | `None` | 无法发布资源 |
| Dynamic Media | 激活后 | `None` | 无法发布资源 |

>[!NOTE]
>
>仅将资源发布到[!DNL Dynamic Media]。
>
>不支持将文件夹发布到[!DNL Dynamic Media]。
>
>如果您选择文件夹(`Selective Publish`)并选择[!DNL Dynamic Media]目标，则[!UICONTROL Publish Target]属性将反映`None`。


现在，让我们将上述使用案例中的&#x200B;**[!UICONTROL 目标]**&#x200B;更改为&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;并验证结果。 这样一来，只将`Selective Publish`文件夹的资产发布到[!DNL Dynamic Media]。 `Immediate`和`Upon Activation`文件夹的资产未发布，并反映了`None`。

![Publish到Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>如果未在您的[!DNL Experience Manager Assets]实例上配置[!DNL Dynamic Media]，并且&#x200B;**[!UICONTROL 目标]**&#x200B;是&#x200B;**[!UICONTROL Publish]**，则资源和文件夹始终发布到`AEM`。
>
>发布到[!DNL Brand Portal]与文件夹属性无关。 所有资源、文件夹和收藏集都可以发布到Brand Portal。 请参阅[将资源发布到Brand Portal](#publish-assets-to-brand-portal)。

>[!NOTE]
>
>如果已自定义[!DNL Manage Publication]向导，则自定义将继续使用现有功能。
>
>但是，您可以删除现有的自定义项以使用新的[!DNL Manager Publication]功能。

## 稍后Publish资源 {#publish-assets-later}

要计划在稍后的日期或时间发布资产的工作流，请执行以下操作：

1. 从[!UICONTROL Experience Manager Assets]控制台中，导航到父文件夹，然后选择计划发布的所有资源或文件夹。
1. 单击工具栏中的&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项。
1. 单击&#x200B;**[!UICONTROL 操作]**&#x200B;中的&#x200B;**[!UICONTROL Publish]**，然后选择要发布内容的&#x200B;**[!UICONTROL 目标]**。
1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;中选择&#x200B;**[!UICONTROL 稍后]**。
1. 选择&#x200B;**[!UICONTROL 激活日期]**&#x200B;并指定日期和时间。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![管理发布工作流](assets/manage-publication-workflow.png)

1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;选项卡中，**[!UICONTROL 添加内容]**（如有必要）。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 工作流]**&#x200B;选项卡中，指定工作流标题。 单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![工作流标题](assets/manage-publication-workflow-title.png)

   登录到目标实例以验证已发布的资源（取决于计划的日期或时间）。

## Publish资源到Dynamic Media {#publish-assets-to-dynamic-media}

仅将资源发布到[!DNL Dynamic Media]。 但是，发布行为因文件夹属性而异。 文件夹可以将&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;配置为选择性发布，这可能为以下任一情况：

* `Selective Publish`
* `Immediate`
* `Upon Activation`

**[!UICONTROL Immediate]**&#x200B;和&#x200B;**[!UICONTROL On Activation]**&#x200B;模式的发布过程一致，但&#x200B;**[!UICONTROL 选择性Publish]**&#x200B;有所不同。 请参阅[在Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html)中配置文件夹级别的选择性发布。 在文件夹中配置选择性发布后，可以执行以下任一操作：

* [使用“管理发布”有选择地将资源发布到Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [使用“管理发布”从Dynamic Media或Experience Manager有选择地取消发布资源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Publish资源到Dynamic Media或使用Quick Publish进行Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [通过搜索结果有选择地发布或取消发布资源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Publish资源到Brand Portal {#publish-assets-to-brand-portal}

您可以将资源、文件夹和收藏集发布到[!DNL Experience Manager Assets Brand Portal]实例。

* [将资产发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [将文件夹发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [将收藏集发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## 要求发布 {#request-publication}

`Request Publication`选项有助于先验证Assets的工作流，然后再在[!DNL AEM] Assets环境中发布它们。 [!DNL AEM]为各种用户提供不同级别的权限。 您可能是正在上传资产的&#x200B;*参与者*，但在验证上传之前无法发布这些资产。 此外，作为&#x200B;*管理员*，您可以管理以读取和写入Assets的工作流。

请求发布选项适用于以下用户：

* **参与者：**&#x200B;如果您是可以参与[!DNL AEM] Assets的用户，则您对[!DNL AEM] Assets工作流的访问权限有限。 已为您隐藏`Manage publication`按钮。 作为参与者，您只能通过添加Assets进行投稿，但无法发布它们或拥有工作流的读取访问权限。

* **工作流用户：**&#x200B;此用户无法发布资产，但具有工作流的读取权限。 作为工作流用户，您可以：
   * 请求发布
   * 查看`Manage publication`按钮
   * 计划工作流并查看选项`schedule now`和`schedule later`

* **管理员：**&#x200B;作为管理员类型的用户，您可以管理Assets的整体工作流步骤。 `Manage publication`按钮对您可见。 如果选择目标`publish`，您可以稍后为工作流步骤计划资产。

>[!NOTE]
>
>如果选择[!DNL Dynamic Media]作为目标，则会为&#x200B;**工作流用户**&#x200B;和&#x200B;**管理员**&#x200B;用户禁用工作流步骤。
>

## 限制和提示 {#limitations-and-tips}

* `Manage publication`可供至少具有工作流读取权限的用户使用。
* 未发布空文件夹。
* 如果发布正在处理的资源，则仅发布原始内容。 缺少节目。 等待处理完成，然后在处理完成后发布或重新发布资产。
* 取消发布复杂资产时，请仅取消发布资产。 避免取消发布引用，因为它们可能会被其他已发布的资产引用。
