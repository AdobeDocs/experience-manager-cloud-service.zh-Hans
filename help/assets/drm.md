---
title: Digital Rights Management位置 [!DNL Assets]
description: 了解如何在中管理资源到期状态和已许可资源的信息 [!DNL Experience Manager] as a [!DNL Cloud Service].
contentOwner: AG
feature: Asset Management,DRM
role: User,Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 6%

---

# Digital Rights Management数字资源 {#digital-rights-management-in-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=en) |
| AEM as a Cloud Service | 本文 |

数字资产通常与指定使用条款和持续时间的许可证相关联。 使用 [!DNL Experience Manager] 平台，您可以高效地管理资产到期信息和许可信息。

## 资产到期 {#asset-expiration}

要强制实施资产的许可证要求，请使用资产到期信息。 到期信息可确保已发布的资产在过期时取消发布，从而防止出现许可证违规情况。 没有管理员权限的用户无法编辑、复制、移动、发布和下载已过期的资源。

您可以在以下位置查看资源的到期状态：

* **卡片视图**：对于已过期的资源，信息卡上有一个标记指示该资源已过期。
* **列表视图**：对于过期的资产，为其 **[!UICONTROL 状态]** 列显示 **[!UICONTROL 已过期]** 横幅。
* **时间线**：您可以在时间轴中查看资源的到期状态。 选择资产并选择“时间轴”。
* **引用边栏**：您还可以在中查看资源的到期状态 **[!UICONTROL 引用]** 边栏。 它管理资产过期状态以及复合资产与引用的子资产、收藏集和项目之间的关系。

要查看资源的引用网页和复合资源，请执行以下步骤：

1. 导航到资源，选择资源，然后单击 ![左边栏内容引用图标](assets/do-not-localize/content-rail-icon.png). 左边栏将打开。
1. 选择 **[!UICONTROL 引用]** 从左边栏开始。
1. 对于已过期的资产， [!UICONTROL 引用] 将到期状态显示为 **[!UICONTROL 资产已过期]**. 如果资产已过期的子资产，则 [!UICONTROL 引用] 边栏显示状态 **[!UICONTROL 资产已过期子资产]**.

### 搜索过期的资产 {#search-expired-assets}

要搜索过期的资产（包括过期的子资产），请执行以下步骤：

1. 在 [!DNL Assets] 控制台，单击 **[!UICONTROL Search]** 工具栏中，然后按 `Enter`.

1. 单击GlobalNav图标并选择 **[!UICONTROL 到期状态]** 选项。

1. 选择 **[!UICONTROL 已过期]**. 搜索结果将显示已过期的资源。

当您选择 **[!UICONTROL 已过期]** 选项，则 [!DNL Assets] 控制台仅显示由复合资源引用的已过期资源和子资源。 引用过期子资产的复合资产不会在子资产过期后立即显示。 相反，它们会在以下时间后显示 [!DNL Experience Manager] 检测在下次执行调度程序时它们引用过期的子资源。

可以将已发布资源的到期日期修改为早于当前计划程序周期的日期。 但是，时间表在下次执行时仍会检测到此类资产为已过期的资产，并且 [!DNL Experience Manager] 会在报表中反映状态。 对于处于不同时区的用户，资源的到期日期显示方式有所不同。

此外，如果错误阻止调度程序在当前周期中检测过期资产，则调度程序在下一个周期中重新检查这些资产并检测其过期状态。

要启用 [!DNL Assets] 控制台要显示引用的复合资源以及过期的子资源，请配置 **[!UICONTROL Adobe CQ DAM到期通知]** 中的工作流 [!DNL Experience Manager]. 基于时间的调度程序会调度一个作业，以在特定时间检查资产是否已过期子资产。 作业完成后，具有过期子资产和引用资产的资产会在搜索结果中显示为已过期。

1. 访问 [!DNL Cloud Manager] 与您的环境关联的Git存储库。
1. 提交名为的文件 `com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json` 存储库中的以下内容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 按照的说明操作 [如何在中配置OSGi [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

可以使用以下属性配置调度程序：

* A `true` 属性的值 `cq.dam.expiry.notification.scheduler.istimebased` 启动计划程序。 *属性的值 `cq.dam.expiry.notification.scheduler.timebased.rule` 是用于定义时间的正则表达式。 以上示例在00小时启动调度程序作业。
* 如果 `send_email` 设置为 `true`，资产创建者（将特定资产上传到的人员） [!DNL Assets])会在资产过期时收到电子邮件。
* 计划程序的一次迭代中过期的最大资源数是属性的值 `asset_expired_limit`.
* 要定期运行作业，请设置属性的值 `cq.dam.expiry.notification.scheduler.istimebased` 作为 `false` 并设置属性的值 `cq.dam.expiry.notification.scheduler.period.rule` 时间（秒）。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 资产状态 {#asset-states}

此 [!DNL Assets] 控制台可显示资源的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个描述其状态的标签，例如，已过期、已发布、已批准、已拒绝等。

1. 在 [!DNL Assets] 用户界面中，选择一个资产。

1. 选择 **[!UICONTROL Publish]** 工具栏中。 如果您没有看到 [!UICONTROL Publish] 选项，单击 **[!UICONTROL 更多]** 在工具栏上找到 **[!UICONTROL Publish]** 选项。

1. 选择 **[!UICONTROL Publish]** ，然后关闭确认对话框。

1. 退出选择模式。 资源的发布状态显示在卡片视图的资源缩略图底部。 在列表视图中，已发布列显示资产的发布时间。

1. 要显示其资源详细信息页面，请在 [!DNL Assets] 界面中，选择资产并单击 **[!UICONTROL 属性]**.

1. 在 [!UICONTROL 高级] 选项卡中，设置资源的到期日期 **[!UICONTROL 过期]** 字段。

1. 单击 **[!UICONTROL 保存]** 然后单击 **[!UICONTROL 关闭]** 以显示“资产”控制台。

1. 资源的发布状态表示卡片视图中资源缩略图底部的已过期状态。 在列表视图中，资源的状态显示为 **[!UICONTROL 已过期]**.

1. 在 [!DNL Assets] 控制台，选择一个文件夹，并在该文件夹上创建审阅任务。

1. 审核和批准/拒绝审核任务中的资产，然后单击 **[!UICONTROL 完成]**.

1. 导航到您为其创建审阅任务的文件夹。 您批准/拒绝的资产状态将显示在卡片视图的底部。 在列表视图中，审批和到期状态显示在相应的列中。

1. 要根据资产的状态搜索资产，请单击 **[!UICONTROL Search]** 以显示搜索栏。

1. 选择 `Return` 并单击 [!DNL Experience Manager].

1. 在搜索面板中，单击 **[!UICONTROL 发布状态]** 并选择 **[!UICONTROL 已发布]** 在中搜索已发布的资产 [!DNL Assets].

1. 要搜索已批准或已拒绝的资产，请选择 **[!UICONTROL 审批状态]** 并选择相应的选项。

1. 要根据资产的到期状态搜索资产，请选择 **[!UICONTROL 到期状态]** 在搜索面板中，选择相应的选项。

1. 您还可以根据各种搜索彩块化下的状态组合搜索资源。 例如，您可以搜索在审核任务中批准且未过期的已发布资产。 要搜索此类资源，请在搜索彩块化中选择相应的选项。

## Digital Rights Management位置 [!DNL Assets] {#digital-rights-management-in-assets-1}

DRM功能强制接受许可协议，然后才能从下载许可资产 [!DNL Assets].

如果您选择受保护的资产并单击 **[!UICONTROL 下载]**，您将被重定向到许可页面以接受许可协议。 如果您不接受许可协议， **[!UICONTROL 下载]** 选项不可用。

如果所选内容包含多个受保护资产，则一次选择一个资产，接受许可协议，然后继续下载资产。

如果满足以下任一条件，则资产被视为受保护：

* 资源元数据属性 `xmpRights:WebStatement` 指向包含资产的许可协议的页面的路径。
* 资源元数据属性的值 `adobe_dam:restrictions` 是指定许可协议的原始HTML。

>[!NOTE]
>
>位置 `/etc/dam/drm/licences` 以前版本中用于存储许可证 [!DNL Experience Manager]. 该位置现已弃用。 如果您创建或修改许可证页面，或者从上一页移植页面 [!DNL Experience Manager] 对于版本，Adobe建议将此类资源存储在 `/apps/settings/dam/drm/licenses` 或 `/conf/*/settings/dam/drm/licenses` 位置。

### 下载受DRM保护的资产 {#downloading-drm-assets}

1. 在信息卡视图中，选择要下载的资源并选择 **[!UICONTROL 下载]**.
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在 [!UICONTROL 许可证] 窗格，选择 **[!UICONTROL 同意]**. 资产旁边会显示一个复选标记。 选择 **[!UICONTROL 下载]** 选项。

   >[!NOTE]
   >
   >此 **[!UICONTROL 下载]** 仅当您选择同意受保护资产的许可协议时，才会启用选项。 但是，如果您的选择包含受保护和不受保护的资产，则只有受保护的资产会列在窗格和 **[!UICONTROL 下载]** 选项可用于下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 要下载资源或其演绎版，请选择 **[!UICONTROL 下载]** 在对话框中。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
