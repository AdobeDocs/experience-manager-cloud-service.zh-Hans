---
title: Digital Rights Management [!DNL Assets]
description: 了解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 2%

---

# Digital Rights Management数字资产 {#digital-rights-management-in-assets}

数字资产通常与指定使用条款和持续时间的许可证相关联。 使用 [!DNL Experience Manager] 平台中，您可以高效地管理资产到期信息和许可信息。

## 资产过期 {#asset-expiration}

要对资产强制实施许可证要求，请使用资产到期信息。 到期信息可确保已发布的资产在过期时取消发布，从而防止许可证违规。 没有管理员权限的用户无法编辑、复制、移动、发布和下载已过期的资产。

您可以在以下位置查看资产的到期状态：

* **卡片视图**:对于已过期的资产，卡片上的标记表示该资产已过期。
* **列表视图**:对于已过期的资产， **[!UICONTROL 状态]** 列显示 **[!UICONTROL 过期]** 横幅。
* **时间轴**:您可以在时间轴中查看资产的到期状态。 选择资产，然后选择时间轴。
* **引用边栏**:您还可以在 **[!UICONTROL 引用]** 边栏。 它可管理复合资产与引用的子资产、收藏集和项目之间的资产到期状态和关系。

要查看资产的引用网页和复合资产，请执行以下步骤：

1. 导航到资产，选择资产，然后单击 ![左边栏内容引用图标](assets/do-not-localize/content-rail-icon.png). 左边栏打开。
1. 选择 **[!UICONTROL 引用]** 从左边栏。
1. 对于已过期的资产， [!UICONTROL 引用] 将到期状态显示为 **[!UICONTROL 资产已过期]**. 如果资产已过期，则 [!UICONTROL 引用] 边栏显示状态 **[!UICONTROL 资产已过期子资产]**.

### 搜索已过期的资产 {#search-expired-assets}

要搜索已过期的资产（包括已过期的子资产），请执行以下步骤：

1. 在 [!DNL Assets] 控制台，单击 **[!UICONTROL 搜索]** 在工具栏中，然后按 `Enter`.

1. 单击GlobalNav图标，然后选择 **[!UICONTROL 到期状态]** 选项。

1. 选择 **[!UICONTROL 过期]**. 搜索结果中会显示已过期的资产。

当您选择 **[!UICONTROL 过期]** 选项， [!DNL Assets] 控制台仅显示复合资产引用的已过期资产和子资产。 在子资产过期后，不会立即显示引用已过期子资产的复合资产。 而是会在 [!DNL Experience Manager] 会在下次计划程序执行时检测它们是否引用过期的子资产。

可以将已发布资产的过期日期修改为早于当前计划程序周期的日期。 但是，计划在下次执行时，仍会将此类资产检测为已过期的资产，并且 [!DNL Experience Manager] 反映其报表中的状态。 对于处于不同时区的用户，资产的过期日期会以不同的方式显示。

此外，如果错误导致调度程序无法检测当前周期中的过期资产，则调度程序将在下一个周期中重新检查这些资产，并检测其过期状态。

启用 [!DNL Assets] 控制台以显示引用的复合资产以及过期的子资产，请配置 **[!UICONTROL Adobe CQ DAM到期通知]** 工作流 [!DNL Experience Manager]. 基于时间的计划程序计划作业以在特定时间检查资产是否已过期的子资产。 作业完成后，已过期的子资产和引用的资产会在搜索结果中显示为已过期。

1. 访问 [!DNL Cloud Manager] 与您的环境关联的Git存储库。
1. 提交名为的文件 `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` 库中，其中包含以下内容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 按照 [如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

您可以使用以下属性配置调度程序：

* A `true` 属性的值 `cq.dam.expiry.notification.scheduler.istimebased` 启动调度程序。 *资产的值 `cq.dam.expiry.notification.scheduler.timebased.rule` 是用于定义时间的正则表达式。 上例在00小时启动调度程序作业。
* 如果 `send_email` 设置为 `true`，资产创建者（将特定资产上传到的人员） [!DNL Assets])会在资产过期时收到一封电子邮件。
* 计划程序的一个迭代中过期的资产的最大数量是属性的值 `asset_expired_limit`.
* 要定期运行作业，请设置属性的值 `cq.dam.expiry.notification.scheduler.istimebased` as `false` 和设置属性的值 `cq.dam.expiry.notification.scheduler.period.rule` 以秒为单位显示时间。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 资产状态 {#asset-states}

的 [!DNL Assets] 控制台可以显示资产的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个用于描述其状态的标签，例如已过期、已发布、已批准、已拒绝等。

1. 在 [!DNL Assets] 用户界面中，选择一个资产。

1. 选择 **[!UICONTROL 发布]** 中。 如果您没有看到 [!UICONTROL 发布] 选项，单击 **[!UICONTROL 更多]** 在工具栏上并找到 **[!UICONTROL 发布]** 选项。

1. 选择 **[!UICONTROL 发布]** ，然后关闭确认对话框。

1. 退出选择模式。 资产的发布状态显示在卡片视图中资产缩略图的底部。 在列表视图中，已发布列显示资产发布的时间。

1. 要显示其资产详细信息页面，请在 [!DNL Assets] 界面，选择资产并单击 **[!UICONTROL 属性]**.

1. 在 [!UICONTROL 高级] 选项卡，从 **[!UICONTROL 过期]** 字段。

1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 关闭]** 以显示资产控制台。

1. 资产的发布状态会在卡片视图中资产缩略图的底部显示过期状态。 在列表视图中，资产的状态显示为 **[!UICONTROL 过期]**.

1. 在 [!DNL Assets] 控制台中，选择文件夹并在文件夹上创建审核任务。

1. 审核和批准/拒绝审核任务中的资产，然后单击 **[!UICONTROL 完成]**.

1. 导航到创建审核任务的文件夹。 您批准/拒绝的资产状态将显示在卡片视图的底部。 在列表视图中，批准和到期状态会显示在相应的列中。

1. 要根据资产的状态搜索资产，请单击 **[!UICONTROL 搜索]** 以显示搜索栏。

1. 选择 `Return` 单击 [!DNL Experience Manager].

1. 在搜索面板中，单击 **[!UICONTROL 发布状态]** 选择 **[!UICONTROL 已发布]** 要在 [!DNL Assets].

1. 要搜索已批准或已拒绝的资产，请选择 **[!UICONTROL 批准状态]** 并选择相应的选项。

1. 要根据资产的到期状态搜索资产，请选择 **[!UICONTROL 到期状态]** 在“搜索”面板中，选择相应的选项。

1. 您还可以根据各种搜索彩块化下的状态组合来搜索资产。 例如，您可以搜索在审核任务中已批准且未过期的已发布资产。 要搜索此类资产，请在搜索彩块化中选择相应的选项。

## Digital Rights Management [!DNL Assets] {#digital-rights-management-in-assets-1}

DRM功能强制您在从下载授权资产之前接受许可协议 [!DNL Assets].

如果您选择受保护的资产，并单击 **[!UICONTROL 下载]**&#x200B;时，系统会将您重定向到许可页面以接受许可协议。 如果您不接受许可协议， **[!UICONTROL 下载]** 选项不可用。

如果选择的资产包含多个受保护的资产，请一次选择一个资产，接受许可协议，然后继续下载资产。

如果满足以下任一条件，则资产会被视为受保护：

* 资产元数据属性 `xmpRights:WebStatement` 指向包含资产许可协议的页面路径。
* 资产元数据属性的值 `adobe_dam:restrictions` 是指定许可协议的原始HTML。

>[!NOTE]
>
>位置 `/etc/dam/drm/licences` 用于在早期版本的 [!DNL Experience Manager]. 位置现已弃用。 如果您创建或修改许可证页面，或将之前的页面导入 [!DNL Experience Manager] 发行版，Adobe建议您将此类资产存储在 `/apps/settings/dam/drm/licenses` 或 `/conf/*/settings/dam/drm/licenses` 位置。

### 下载受DRM保护的资产 {#downloading-drm-assets}

1. 在卡片视图中，选择要下载的资产，然后选择 **[!UICONTROL 下载]**.
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在 [!UICONTROL 许可证] 窗格，选择 **[!UICONTROL 同意]**. 资产旁边会显示一个复选标记。 选择 **[!UICONTROL 下载]** 选项。

   >[!NOTE]
   >
   >的 **[!UICONTROL 下载]** 仅当您选择同意受保护资产的许可协议时，才会启用选项。 但是，如果您的选择包含受保护和不受保护的资产，则只有受保护的资产会列在窗格中，并且 **[!UICONTROL 下载]** 选项，可下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 要下载资产或其演绎版，请选择 **[!UICONTROL 下载]** 中。
