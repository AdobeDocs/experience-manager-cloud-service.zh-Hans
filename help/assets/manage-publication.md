---
title: 管理发布
description: 将资源发布或取消发布到Experience Manager Assets、Dynamic Media和Brand Portal
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 6%

---

# 在Experience Manager Assets中管理发布 {#manage-publication-in-aem}

作为 [!DNL Adobe Experience Manager Assets] 管理员，您可以将资源和包含资源的文件夹从创作实例发布到 [!DNL Experience Manager Assets]， [!DNL Dynamic Media]、和 [!DNL Brand Portal]. 此外，您还可以计划在稍后的日期或时间发布资产或文件夹。 发布后，用户可以访问资产，并进一步将资产分发给其他用户。 默认情况下，您可以将资源和文件夹发布到 [!DNL Experience Manager Assets]. 但是，您可以配置 [!DNL Experience Manager Assets] 启用发布到 [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) 和 [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

您可以使用任意一项在资源或文件夹级别发布或取消发布资源 **[!UICONTROL 快速发布]** 或 **[!UICONTROL 管理发布]** 中提供的选项 [!DNL Experience Manager Assets] 界面。 如果您对中的原始资源或文件夹进行后续修改 [!DNL Experience Manager Assets]，则在您从重新发布之前，更改不会反映在发布实例中 [!DNL Experience Manager Assets]. 它可确保进行中的更改在发布实例中不可用。 发布实例中只有管理员发布的已批准更改可用。

* [使用快速发布发布功能发布资源](#quick-publish)
* [使用“管理发布”发布资源](#manage-publication)
* [稍后发布资产](#publish-assets-later)
* [将资源发布到Dynamic Media](#publish-assets-to-dynamic-media)
* [将资产发布到 Brand Portal](#publish-assets-to-brand-portal)
* [请求发布](#request-publication)
* [限制和提示](#limitations-and-tips)

## 使用快速发布发布功能发布资源 {#quick-publish}

通过快速发布，可立即将内容发布到所选目标。 从 [!DNL Experience Manager Assets] 导航到父文件夹，然后选择要发布的所有资源或文件夹。 单击 **[!UICONTROL 快速发布]** 选项，然后从要发布资产的下拉列表中选择目标。

![快速发布](assets/quick-publish-to-aem.png)

## 使用“管理发布”发布资源 {#manage-publication}

管理发布允许您将内容发布到所选目标或从所选目标取消发布内容， [添加内容](#add-content) 从DAM存储库发布列表， [包括文件夹设置](#include-folder-settings) 发布选定文件夹的内容并应用过滤器，以及 [计划发布](#publish-assets-later) 到以后的日期或时间。

从 [!DNL Experience Manager Assets] 导航到父文件夹，然后选择要发布的所有资源或文件夹。 单击 **[!UICONTROL 管理发布]** 工具栏中的选项。 如果您没有 [!DNL Dynamic Media] 和 [!DNL Brand Portal] 在中配置 [!DNL Experience Manager Assets] 实例时，您只能将资源和文件夹发布到 [!DNL Experience Manager Assets].

![管理发布](assets/manage-publication-aem.png)

以下选项位于 [!UICONTROL 管理发布] 界面：

* [!UICONTROL 操作]
   * `Publish`：将资源和文件夹发布到所选目标
   * `Unpublish`：从目标取消发布资源和文件夹

* [!UICONTROL 目标]
   * `Publish`：将资源和文件夹发布到 [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: 将资源发布到 [!DNL Dynamic Media]
   * `Brand Portal`：将资源和文件夹发布到 [!DNL Brand Portal]

* [!UICONTROL 计划]
   * `Now`：立即发布资源
   * `Later`：发布资源时基于 `Activation` 日期或时间

要继续，请单击 **[!UICONTROL 下一个]**. 根据选择， **[!UICONTROL 范围]** 选项卡反映不同的选项。 的选项 **[!UICONTROL 添加内容]** 和 **[!UICONTROL 包括文件夹设置]** 仅可用于将资产和文件夹发布到 [!DNL Experience Manager Assets] (`Destination: Publish`)。

![管理发布范围](assets/manage-publication-aem-scope.png)

### 添加内容 {#add-content}

发布到 [!DNL Experience Manager Assets] 允许您进一步向发布列表添加更多内容（资产和文件夹）。 您可以在dam存储库中将更多资源或文件夹添加到列表中。 单击 **[!UICONTROL 添加内容]** 按钮以添加更多内容。

您可以从一个文件夹添加多个资源，也可以一次添加多个文件夹。 但是，您无法一次从多个文件夹添加资源。

![添加内容](assets/manage-publication-add-content.png)

### 包括文件夹设置 {#include-folder-settings}

默认情况下，将文件夹发布到 [!DNL Experience Manager Assets] 发布所有资源、子文件夹及其引用。

要筛选要发布的文件夹内容，请单击 **[!UICONTROL 包括文件夹设置]**：

* `Include folder contents`

   * 启用：发布选定文件夹的所有资源、子文件夹（包括子文件夹的所有资源）和引用。
   * 已禁用：仅发布选定的文件夹（空）和引用。 所选文件夹的资产未发布。

* `Include folder contents` 和 `Include only immediate folder contents`

  如果同时选择了这两个选项，则会发布选定文件夹、子文件夹（空）和引用的所有资产。 子文件夹的资产未发布。

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![包括文件夹设置](assets/manage-publication-include-folder-settings.png)

应用过滤器后，单击 **[!UICONTROL 确定]**，然后单击 **[!UICONTROL Publish]**. 单击“发布”按钮时，会显示一条确认消息 `Resource(s) have been scheduled for publication` 显示。 选定的资源和（或）文件夹将根据调度程序(`Now` 或 `Later`)。 登录到发布实例，验证是否已成功发布资产和（或）文件夹。

![发布到 AEM](assets/manage-publication-publish-aem.png)

在上图中，您可以看到 **[!UICONTROL 发布目标]** 属性。 让我们回顾一下，您已选择发布到 [!DNL Experience Manager Assets] (`Destination: Publish`)。 那么，它为何仅显示文件夹和资产发布到 `AEM`，而其他两个资产将发布到两者 `AEM` 和 `Dynamic Media`？

在这里，您必须了解文件夹属性的角色。 文件夹的 **[!UICONTROL Dynamic Media发布模式]** 属性在发布过程中扮演着重要角色。 要查看文件夹的属性，请选择一个文件夹，然后单击 **[!UICONTROL 属性]** 工具栏中。 有关资产，请参阅其父文件夹的属性。

下表说明发布如何根据定义的 **[!UICONTROL 目标]** 和 **[!UICONTROL Dynamic Media发布模式]**：

| [!UICONTROL 目标] | [!UICONTROL Dynamic Media 发布模式] | [!UICONTROL 发布目标] | 允许的内容 |
| --- | --- | --- | --- |
| 发布 | 选择性发布 | `AEM` | 资源和（或）文件夹 |
| 发布 | 即时 | `AEM` 和 `Dynamic Media` | 资源和（或）文件夹 |
| 发布 | 激活后 | `AEM` 和 `Dynamic Media` | 资源和（或）文件夹 |
| Dynamic Media | 选择性发布 | `Dynamic Media` | 资源 |
| Dynamic Media | 即时 | `None` | 无法发布资源 |
| Dynamic Media | 激活后 | `None` | 无法发布资源 |

>[!NOTE]
>
>仅资产发布到 [!DNL Dynamic Media].
>
>将文件夹发布到 [!DNL Dynamic Media] 不受支持。
>
>如果您选择文件夹(`Selective Publish`)，然后选择 [!DNL Dynamic Media] 目标， [!UICONTROL 发布目标] 属性反映 `None`.


现在，让我们更改 **[!UICONTROL 目标]** 在上述用例中， **[!UICONTROL Dynamic Media]** 并验证结果。 这样，只有的资产 `Selective Publish` 文件夹已发布到 [!DNL Dynamic Media]. 的资产 `Immediate` 和 `Upon Activation` 文件夹未发布，并反映 `None`.

![发布到 Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>如果 [!DNL Dynamic Media] 未在您的上配置 [!DNL Experience Manager Assets] 实例和 **[!UICONTROL 目标]** 是 **[!UICONTROL Publish]**，则资源和文件夹始终发布到 `AEM`.
>
>发布到 [!DNL Brand Portal] 与文件夹属性无关。 所有资源、文件夹和收藏集都可以发布到Brand Portal。 请参阅 [将资源发布到Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>如果您已自定义 [!DNL Manage Publication] 向导中，您的自定义设置将继续用于现有功能。
>
>但是，您可以删除现有自定义项以使用新的 [!DNL Manager Publication] 功能。

## 稍后发布资产 {#publish-assets-later}

要计划在稍后的日期或时间发布资产的工作流，请执行以下操作：

1. 从 [!UICONTROL Experience Manager Assets] 导航到父文件夹，然后选择要计划发布的所有资源或文件夹。
1. 单击 **[!UICONTROL 管理发布]** 工具栏中的选项。
1. 单击 **[!UICONTROL Publish]** 从 **[!UICONTROL 操作]**，然后选择 **[!UICONTROL 目标]** 要发布内容的位置。
1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;中选择&#x200B;**[!UICONTROL 稍后]**。
1. 选择 **[!UICONTROL 激活日期]** 并指定日期和时间。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![管理发布工作流程](assets/manage-publication-workflow.png)

1. 在 **[!UICONTROL 范围]** 选项卡， **[!UICONTROL 添加内容]** （如有必要）。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在 **[!UICONTROL 工作流]** 选项卡，指定工作流标题。 单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![工作流标题](assets/manage-publication-workflow-title.png)

   登录到目标实例以验证已发布的资源（取决于计划的日期或时间）。

## 将资源发布到Dynamic Media {#publish-assets-to-dynamic-media}

仅资产发布到 [!DNL Dynamic Media]. 但是，发布行为因文件夹属性而异。 文件夹可以具有 **[!UICONTROL Dynamic Media发布模式]** 配置为进行选择性发布，这可能为以下任一情况：

* `Selective Publish`
* `Immediate`
* `Upon Activation`

的发布流程 **[!UICONTROL 立即]** 和 **[!UICONTROL 激活时]** 模式是一致的，但不同于 **[!UICONTROL 选择性发布]**. 请参阅 [在Dynamic Media中配置文件夹级别的选择性发布](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). 在文件夹中配置选择性发布后，可以执行以下任一操作：

* [使用“管理发布”有选择地将资源发布到Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [使用管理发布从Dynamic Media或Experience Manager有选择地取消发布资源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [使用快速发布将资源发布到Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [通过搜索结果有选择地发布或取消发布资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## 将资产发布到 Brand Portal {#publish-assets-to-brand-portal}

您可以将资源、文件夹和收藏集发布到 [!DNL Experience Manager Assets Brand Portal] 实例。

* [将资产发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [将文件夹发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [将收藏集发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## 请求发布 {#request-publication}

此 `Request Publication` 选项有助于在发布资产之前验证资产的工作流 [!DNL AEM] 资源环境。 [!DNL AEM] 为不同用户提供不同级别的权限。 您可以是 *参与者* 这些用户正在上传资产，但在验证上传后才能发布这些资产。 此外，作为一名 *管理员* 您可以管理资产的读取和写入工作流。

请求发布选项适用于以下用户：

* **投稿人：** 如果您是可以对下列内容做出贡献的用户 [!DNL AEM] Assets，则您对的访问权限有限 [!DNL AEM] 资产工作流程。 `Manage publication` 按钮对您而言是隐藏的。 作为投稿人，您只能通过添加资产进行投稿，但无法发布它们或拥有工作流的读取访问权限。

* **工作流用户：** 此用户无法发布资产，但具有工作流的读取权限。 作为工作流用户，您可以：
   * 请求发布
   * 视图 `Manage publication` 按钮
   * 安排工作流并查看选项 `schedule now` 和 `schedule later`

* **管理员：** 作为管理员类型的用户，您可以管理资产的整个工作流步骤。 `Manage publication` 按钮对您可见。 如果目标 `publish` 之后，您可以为工作流步骤计划资产。

>[!NOTE]
>
>如果 [!DNL Dynamic Media] 已选择作为目标，已为禁用工作流步骤 **工作流用户** 和 **管理员** 用户。
>

## 限制和提示 {#limitations-and-tips}

* `Manage publication` 至少具有工作流读取权限的用户可以使用。
* 未发布空文件夹。
* 如果发布正在处理的资源，则仅发布原始内容。 缺少节目。 等待处理完成，然后在处理完成后发布或重新发布资产。
* 取消发布复杂资产时，请仅取消发布资产。 避免取消发布引用，因为它们可能会被其他已发布的资产引用。
