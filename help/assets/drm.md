---
title: Digital Rights Management [!DNL Adobe Experience Manager Assets] 即云服务。
description: 了解如何在云服务中管理授权资产的资产到期状态 [!DNL Experience Manager] 和信息。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 31b8db4403dff1934033e1ed93651a076dba7a1a
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 7%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

数字资产通常与指定使用条款和持续时间的许可证相关联。 由于 [!DNL Adobe Experience Manager Assets] 与平台完全集成，您 [!DNL Experience Manager] 可以有效地管理资产到期信息和资产状态。 您还可以将许可信息与资产关联。

## 资产过期 {#asset-expiration}

资产到期是实施资产许可要求的有效方式。 它可确保发布的资产在过期后取消发布，这样不会发生任何违反许可的情况。 没有管理员权限的用户无法编辑、复制、移动、发布和下载过期的资产。

您可以在以下位置视图资产的过期状态：

* **卡视图**: 对于过期的资产，卡上会显示一个标志，指示其已过期。
* **列表视图**: 对于过期的资产， **[!UICONTROL 状态]** 列显示 **[!UICONTROL 过期横幅]** 。
* **时间轴**: 您可以视图时间轴中资产的过期状态。 选择资产，然后选择时间轴。
* **引用边栏**: 您还可以在引用边栏中视图资产的 **[!UICONTROL 过期]** 状态。 它管理资产到期状态以及复合资产与引用的子资产、集合和项目之间的关系。

1. 导航到要视图其引用网页和复合资产的资产。
1. 选择资产，然后单击 [!DNL Experience Manager] 徽标。
1. 从菜 **[!UICONTROL 单中选]** 择“引用”。
1. 对于过期的资产，引用边栏的顶部会显 **[!UICONTROL 示资产已过期]** 。 如果资产已过期子资产，引用边栏会显示资产 **[!UICONTROL 已过期子资产的状态]**。

### 搜索过期的资产 {#search-expired-assets}

您可以在“搜索”面板中搜索过期的资产，包括过期的子资产。

1. 在控制 [!DNL Assets] 台中，单击工 **[!UICONTROL 具栏中]** 的“搜索”以显示“全局搜索”框。

1. 将光标置于“全搜索”框中，按Enter键显示搜索结果页面。

1. 单击GlobalNav图标以显示“搜索”面板。

1. 单击/点按&#x200B;**[!UICONTROL 到期状态]**&#x200B;选项以展开。

1. 选择 **[!UICONTROL 过期]**。 过期的资产会显示在搜索结果中。

当您选择过期 **[!UICONTROL 选项]** ，控制台将仅 [!DNL Assets] 显示复合资产引用的过期资产和子资产。 在子资产过期后，不会立即显示引用已过期子资产的复合资产。 相反，在下次运行调度程序时 [!DNL Experience Manager] 检测到它们引用了过期的子资产后，会显示这些子资产。

如果您将已发布资产的过期日期修改为早于当前调度程序周期的日期，计划仍会在下次运行时将此资产检测为过期资产，并相应地反映其状态。

此外，如果故障或错误导致调度程序无法在当前周期中检测过期的资产，调度程序会在下一个周期重新检查这些资产并检测其过期状态。

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. 打开 [!DNL Experience Manager] Configuration Manager。
1. 选 **[!UICONTROL 择Adobe CQ DAM到期通知]**。 默认情况下， **[!UICONTROL 系统会选择]** “基于时间的调度程序”，这将计划作业，以在特定时间检查资产是否已过期子资产。 作业完成后，已过期的子资产和引用的资产会在搜索结果中显示为过期。

1. 要定期运行该作业，请清除&#x200B;**[!UICONTROL 基于时间的计划程序规则]**&#x200B;字段，并在&#x200B;**[!UICONTROL 周期性计划程序]**&#x200B;字段中修改时间（以秒为单位）。例如，示例表达式“0 0 0 &amp;ast; &amp;ast; ?”会在 00 小时开始作业。

<!-- 1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >Only the asset creator (the person who uploads a particular asset to AEM Assets) receives an email when the asset expires. See how to configure email notification for additional details around configuring email notifications at the overall AEM level.
-->

1. 在先 **[!UICONTROL 前通知(秒]** )字段中，指定资产在您希望收到有关到期的通知时在过期时间之前的秒数。 如果您是管理员或资产创建者，您会在资产到期前收到一条消息，通知您资产将在指定时间后过期。

   资产到期后，您会收到另一则通知，确认到期。 此外，过期的资产也会停用。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 资产状态 {#asset-states}

控制 [!DNL Assets] 台可以显示资产的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个标签，用于描述其状态，例如“已过期”、“已发布”、“已批准”、“被拒绝”等。

1. 在用户 [!DNL Assets] 界面中，选择一个资产。

1. 单击 **[!UICONTROL 工具栏]** 中的发布。 如果工具栏上未显示 **发布** ，请单击工 **[!UICONTROL 具栏上的]** 更多 **[!UICONTROL ，然后找到]** 发布选项。

1. 从菜 **[!UICONTROL 单中选择]** “发布”，然后关闭确认对话框。
1. 退出选择模式。 资产的发布状态会显示在卡片视图中资产缩略图的底部。 在列表视图中，已发布列显示资产发布的时间。

1. 要显示其资产详细信息页面，请在界 [!DNL Assets] 面中选择资产，然后单击 **[!UICONTROL 属性]**。

1. 在高级 [!UICONTROL 选项卡中] ，从过期字段中设置资产的过 **[!UICONTROL 期日]** 期。

1. 单击 **[!UICONTROL 保存]** ，然后单 **[!UICONTROL 击关闭]** ，以显示资产控制台。
1. 资产的发布状态会在卡片视图中资产缩略图的底部指示过期状态。 在列表视图中，资产的状态显示为已过 **[!UICONTROL 期]**。

1. 在控制台 [!DNL Assets] 中，选择一个文件夹，然后在该文件夹上创建一个审核任务。
1. 在审核任务中审核和批准／拒绝资产，然后单击完 **[!UICONTROL 成]**。
1. 导航到创建审核任务的文件夹。 您批准／拒绝的资产的状态显示在卡视图的底部。 在列表视图中，批准和到期状态显示在相应的列中。

1. 要根据资产的状态搜索资产，请单 **[!UICONTROL 击]** “搜索”以显示搜索栏。

1. 按回车键并单击 [!DNL Experience Manager] 以显示搜索面板。
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

1. 要根据资产的到期状态搜索资产，请在“搜索”面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

1. 您还可以根据各种搜索彩块化下的状态组合来搜索资产。 例如，您可以通过在搜索彩块化中选择相应的选项，来搜索在审核任务中已批准但尚未过期的已发布资产。

## Adobe Cloud中的数字版权管理 [!DNL Assets] {#digital-rights-management-in-assets-1}

此功能强制您接受许可协议，然后您才能从下载许可资产 [!DNL Adobe Experience Manager Assets]。

如果您选择受保护的资产并单击 **[!UICONTROL 下载]**，则会将您重定向到许可页面以接受该许可协议。 如果您不接受许可协议，则“ **[!UICONTROL 下载]** ”选项不可用。

如果选择的内容包含多个受保护的资产，则一次选择一个资产，接受许可协议，然后继续下载该资产。

如果满足以下任一条件，资产将被视为受保护：

* 资产元数据属 `xmpRights:WebStatement` 性指向包含资产许可协议的页面的路径。
* 资产元数据属性的值 `adobe_dam:restrictions` 是一个原始HTML，它指定许可协议。

>[!NOTE]
>
>已弃用 `/etc/dam/drm/licences` 用于在早期版本中存储许可证 [!DNL Experience Manager] 的位置。
>
>如果您创建或修改许可证页面，或从以前的版本移植 [!DNL Experience Manager] 这些页面，Adobe建议您将它们存储在或 `/apps/settings/dam/drm/licenses` 下面 `/conf/*/settings/dam/drm/licenses`。

### 下载受DRM保护的资源 {#downloading-drm-assets}

1. 在卡视图中，选择要下载的资产，然后单击下 **[!UICONTROL 载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在“许可 [!UICONTROL 证] ”窗格中，选 **[!UICONTROL 择“同意”]**。 资产旁边会显示一个勾形。 单击“下 **[!UICONTROL 载]** ”选项。

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 在对话框中，单击 **[!UICONTROL 下载]** ，以下载资产或其演绎版。
