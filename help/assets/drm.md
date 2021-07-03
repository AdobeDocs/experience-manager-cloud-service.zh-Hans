---
title: Digital Rights Management [!DNL Assets]
description: 了解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]中管理已许可资产的资产到期状态和信息。
contentOwner: AG
feature: 资产管理，DRM
role: Business Practitioner,Administrator
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 7256300afd83434839c21a32682919f80097f376
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 7%

---

# Digital Rights Management资产 {#digital-rights-management-in-assets}

数字资产通常与指定使用条款和持续时间的许可证相关联。 由于[!DNL Adobe Experience Manager Assets]与[!DNL Experience Manager]平台完全集成，因此您可以高效地管理资产到期信息和资产状态。 您还可以将授权信息与资产关联。

## 资产过期 {#asset-expiration}

资产到期是强制执行资产许可证要求的有效方式。 它可确保已发布的资产在过期时取消发布，这样就不会发生任何许可证违规的情况。 没有管理员权限的用户无法编辑、复制、移动、发布和下载已过期的资产。

您可以在以下位置查看资产的到期状态：

* **卡片视图**:对于已过期的资产，卡片上的标记表示该资产已过期。
* **列表视图**:对于已过期的资产，“状 **** 态”列会显示“过 **** 期”横幅。
* **时间轴**:您可以在时间轴中查看资产的到期状态。选择资产，然后选择时间轴。
* **引用边栏**:您还可以在“引用”边栏中查看资产的到期 **** 状态。它可管理复合资产与引用的子资产、收藏集和项目之间的资产到期状态和关系。

1. 导航到要查看其引用网页和复合资产的资产。
1. 选择资产，然后单击[!DNL Experience Manager]徽标。
1. 从菜单中选择&#x200B;**[!UICONTROL 引用]**。
1. 对于已过期的资产，引用边栏会在顶部显示到期状态&#x200B;**[!UICONTROL 资产已过期]**。 如果资产已过期的子资产，引用边栏会显示状态&#x200B;**[!UICONTROL 资产已过期的子资产]**。

### 搜索已过期的资产 {#search-expired-assets}

您可以在“搜索”面板中搜索过期的资产，包括过期的子资产。

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL 搜索]**&#x200B;以显示[!DNL Experience Manager]搜索框。

1. 将光标置于Omnisearch框中，选择`Enter`键以显示搜索结果页面。

1. 单击GlobalNav图标以显示“搜索”面板。

1. 单击/点按&#x200B;**[!UICONTROL 到期状态]**&#x200B;选项以展开。

1. 选择&#x200B;**[!UICONTROL 已过期]**。 过期的资产会显示在搜索结果中。

选择&#x200B;**[!UICONTROL 已过期]**&#x200B;选项时，[!DNL Assets]控制台仅显示复合资产引用的已过期资产和子资产。 在子资产过期后，不会立即显示引用已过期子资产的复合资产。 相反，在[!DNL Experience Manager]检测到它们在下次运行调度程序时引用过期的子资产后，才会显示它们。

如果您将已发布资产的过期日期修改为早于当前计划程序周期的日期，计划仍会在下次运行时将此资产检测为已过期资产，并相应地反映状态。 对于处于不同时区的用户，资产的过期日期会以不同的方式显示。

此外，如果故障或错误阻止调度程序检测当前周期中的过期资产，则调度程序在下一个周期中重新检查这些资产并检测其过期状态。

要启用[!DNL Assets]控制台以显示引用的复合资产以及过期的子资产，请在[!DNL Experience Manager] Configuration Manager中配置&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**&#x200B;工作流。

1. 打开[!DNL Experience Manager]配置管理器。
1. 选择&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**。 默认情况下，会选择&#x200B;**[!UICONTROL 基于时间的计划程序]**，该计划程序会安排作业在特定时间检查资产是否已过期的子资产。 作业完成后，已过期的子资产和引用的资产会在搜索结果中显示为已过期。

1. 要定期运行该作业，请清除&#x200B;**[!UICONTROL 基于时间的计划程序规则]**&#x200B;字段，并在&#x200B;**[!UICONTROL 周期性计划程序]**&#x200B;字段中修改时间（以秒为单位）。例如，示例表达式“0 0 0 &amp;ast; &amp;ast; ?”会在 00 小时开始作业。

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. 在&#x200B;**[!UICONTROL 以秒为单位的先前通知]**&#x200B;字段中，指定要在资产过期之前的时间（以秒为单位），以接收有关过期的通知。 如果您是管理员或资产创建者，则会在资产过期前收到一条消息，通知您资产将在指定的时间后过期。

   资产过期后，您会收到另一则确认到期的通知。 此外，会停用已过期的资产。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 资产状态 {#asset-states}

[!DNL Assets]控制台可以显示资产的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个用于描述其状态的标签，例如已过期、已发布、已批准、已拒绝等。

1. 在[!DNL Assets]用户界面中，选择资产。

1. 单击工具栏中的&#x200B;**[!UICONTROL Publish]** 。 如果工具栏中未显示&#x200B;**Publish** ，请单击工具栏中的&#x200B;**[!UICONTROL 更多]**，然后找到&#x200B;**[!UICONTROL Publish]**&#x200B;选项。

1. 从菜单中选择&#x200B;**[!UICONTROL Publish]**，然后关闭确认对话框。
1. 退出选择模式。 资产的发布状态显示在卡片视图中资产缩略图的底部。 在列表视图中，已发布列显示资产发布的时间。

1. 要显示其资产详细信息页面，请在[!DNL Assets]界面中选择资产，然后单击&#x200B;**[!UICONTROL 属性]**。

1. 在[!UICONTROL Advanced]选项卡中，从&#x200B;**[!UICONTROL Expires]**&#x200B;字段设置资产的过期日期。

1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以显示资产控制台。
1. 资产的发布状态会在卡片视图中资产缩略图的底部显示过期状态。 在列表视图中，资产的状态显示为&#x200B;**[!UICONTROL 已过期]**。

1. 在[!DNL Assets]控制台中，选择一个文件夹并在该文件夹中创建审核任务。
1. 审核和批准/拒绝审核任务中的资产，然后单击&#x200B;**[!UICONTROL 完成]**。
1. 导航到创建审核任务的文件夹。 您批准/拒绝的资产状态将显示在卡片视图的底部。 在列表视图中，批准和到期状态会显示在相应的列中。

1. 要根据资产的状态搜索资产，请单击&#x200B;**[!UICONTROL 搜索]**&#x200B;以显示Omnisearch栏。

1. 选择`Return`并单击[!DNL Experience Manager]以显示搜索面板。
1. 在搜索面板中，单击&#x200B;**[!UICONTROL 发布状态]**&#x200B;并选择&#x200B;**[!UICONTROL 已发布]**&#x200B;以在[!DNL Assets]中搜索已发布的资产。

1. 单击&#x200B;**[!UICONTROL 批准状态]**，然后单击相应的选项以搜索已批准或已拒绝的资产。

1. 要根据资产的到期状态搜索资产，请在“搜索”面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

1. 您还可以根据各种搜索彩块化下的状态组合来搜索资产。 例如，您可以通过在搜索彩块化中选择相应的选项，来搜索已在审核任务中批准且尚未过期的已发布资产。

## Digital Rights Management在[!DNL Assets]中 {#digital-rights-management-in-assets-1}

此功能强制您在从[!DNL Adobe Experience Manager Assets]下载授权资产之前接受许可协议。

如果您选择受保护的资产并单击&#x200B;**[!UICONTROL 下载]**，则会将您重定向到许可页面以接受许可协议。 如果您不接受许可协议，则&#x200B;**[!UICONTROL Download]**&#x200B;选项将不可用。

如果选择的资产包含多个受保护的资产，请一次选择一个资产，接受许可协议，然后继续下载资产。

如果满足以下任一条件，则资产会被视为受保护：

* 资产元数据属性`xmpRights:WebStatement`指向包含资产许可协议的页面路径。
* 资产元数据属性`adobe_dam:restrictions`的值是指定许可协议的原始HTML。

>[!NOTE]
>
>`/etc/dam/drm/licences`位置用于存储[!DNL Experience Manager]早期版本中的许可证，该位置已被弃用。
>
>如果您创建或修改许可证页面，或将许可证页面从以前的[!DNL Experience Manager]版本中导入，则Adobe建议将许可证页面存储在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`下。

### 下载受DRM保护的资产 {#downloading-drm-assets}

1. 在卡片视图中，选择要下载的资产，然后单击&#x200B;**[!UICONTROL 下载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在[!UICONTROL 许可证]窗格中，选择&#x200B;**[!UICONTROL 同意]**。 资产旁边会显示一个复选标记。 单击&#x200B;**[!UICONTROL Download]**&#x200B;选项。

   >[!NOTE]
   >
   >仅当您选择同意受保护资产的许可协议时，才会启用&#x200B;**[!UICONTROL 下载]**&#x200B;选项。 但是，如果您的选择包含受保护和不受保护的资产，则窗格中只会列出受保护的资产，并且会启用&#x200B;**[!UICONTROL Download]**&#x200B;选项来下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 在对话框中，单击&#x200B;**[!UICONTROL 下载]**&#x200B;以下载资产或其演绎版。
