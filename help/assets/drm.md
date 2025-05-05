---
title: ' [!DNL Assets]中的Digital Rights Management'
description: 了解如何在 [!DNL Experience Manager] as a [!DNL Cloud Service]中管理已授权资产的资产到期状态和信息。
contentOwner: AG
feature: Asset Management,DRM
role: User, Admin
exl-id: fa5f94df-1c15-4593-afcb-1d24508da2bf
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 7%

---

# 适用于数字资源的Digital Rights Management {#digital-rights-management-in-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/drm.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

数字资产通常与指定使用条款和持续时间的许可证相关联。 使用[!DNL Experience Manager]平台，您可以有效地管理资产到期信息和许可信息。

## 资产到期 {#asset-expiration}

要强制实施资产的许可证要求，请使用资产到期信息。 到期信息可确保已发布的资产在过期时取消发布，从而防止出现许可证违规情况。 没有管理员权限的用户无法编辑、复制、移动、发布和下载已过期的资源。

您可以在以下位置查看资源的到期状态：

* **卡片视图**：对于已过期的资产，卡片上的标志表示该资产已过期。
* **列表视图**：对于已过期的资产，**[!UICONTROL 状态]**&#x200B;列显示&#x200B;**[!UICONTROL 已过期]**&#x200B;横幅。
* **时间线**：您可以在时间线中查看资产的到期状态。 选择资产并选择“时间轴”。
* **引用边栏**：您还可以在&#x200B;**[!UICONTROL 引用]**&#x200B;边栏中查看资产的到期状态。 它管理资产过期状态以及复合资产与引用的子资产、收藏集和项目之间的关系。

要查看资源的引用网页和复合资源，请执行以下步骤：

1. 导航到资源，选择该资源，然后单击![左边栏内容引用图标](assets/do-not-localize/content-rail-icon.png)。 左边栏将打开。
1. 从左边栏中选择&#x200B;**[!UICONTROL 引用]**。
1. 对于已过期的资源，[!UICONTROL 引用]显示到期状态，因为&#x200B;**[!UICONTROL 资源已过期]**。 如果资源具有过期的子资源，[!UICONTROL 引用]边栏会显示状态&#x200B;**[!UICONTROL 资源具有过期的子Assets]**。

### 搜索过期的资产 {#search-expired-assets}

要搜索过期的资产（包括过期的子资产），请执行以下步骤：

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL 搜索]**，然后按`Enter`。

1. 单击GlobalNav图标并选择&#x200B;**[!UICONTROL 到期状态]**&#x200B;选项。

1. 选择&#x200B;**[!UICONTROL 已过期]**。 搜索结果将显示已过期的资源。

当您选择&#x200B;**[!UICONTROL 过期]**&#x200B;选项时，[!DNL Assets]控制台仅显示由复合资源引用的过期资源和子资源。 引用过期子资产的复合资产不会在子资产过期后立即显示。 相反，在[!DNL Experience Manager]检测到下次执行计划程序时引用过期的子资产后，将显示这些子资产。

可以将已发布资源的到期日期修改为早于当前计划程序周期的日期。 但是，计划在下次执行时仍会检测到此类资产为已过期的资产，[!DNL Experience Manager]会在报告中反映状态。 对于处于不同时区的用户，资源的到期日期显示方式有所不同。

此外，如果错误阻止调度程序在当前周期中检测过期资产，则调度程序在下一个周期中重新检查这些资产并检测其过期状态。

要启用[!DNL Assets]控制台以显示引用的复合资产以及过期的子资产，请在[!DNL Experience Manager]中配置&#x200B;**[!UICONTROL Adobe CQ DAM到期通知]**&#x200B;工作流。 基于时间的调度程序会调度一个作业，以在特定时间检查资产是否已过期子资产。 作业完成后，具有过期子资产和引用资产的资产会在搜索结果中显示为已过期。

1. 访问与您的环境关联的[!DNL Cloud Manager] Git存储库。
1. 提交存储库中名为`com.day.cq.dam.core.impl.ExpiryNotificationJobImpl.cfg.json`的文件，该文件包含以下内容。

   ```json
   {
      "send_email":"false", "asset_expired_limit":"100", "prior_notification_seconds":"86400", "cq.dam.expiry.notification.url.protocol":"http", "cq.dam.expiry.notification.scheduler.istimebased":"true", "cq.dam.expiry.notification.scheduler.period.rule":"10", "cq.dam.expiry.notification.scheduler.timebased.rule":"0 0 0 * * ?"
   }
   ```

1. 按照[中的说明操作 [!DNL Experience Manager] as a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md)中的OSGi配置。

可以使用以下属性配置调度程序：

* 属性`cq.dam.expiry.notification.scheduler.istimebased`的`true`值将启动调度程序。 *属性`cq.dam.expiry.notification.scheduler.timebased.rule`的值是用于定义时间的正则表达式。 以上示例在00小时启动调度程序作业。
* 如果`send_email`设置为`true`，则资产创建者（将特定资产上传到[!DNL Assets]的人员）将在资产过期时收到电子邮件。
* 计划程序的一个迭代中过期的最大资源数是属性`asset_expired_limit`的值。
* 要定期运行作业，请将属性`cq.dam.expiry.notification.scheduler.istimebased`的值设置为`false`，并将属性`cq.dam.expiry.notification.scheduler.period.rule`的值设置为以秒为单位的时间。

<!-- TBD: Web Console not available in CS.

1. Open [!DNL Experience Manager] Configuration Manager.
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time-based Scheduler]** is selected, which 

1. For example, the example expression '0 0 0 &ast; &ast; ?' triggers the job at 0000 hrs.

1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

1. In the **[!UICONTROL Prior notification in seconds]** field, specify the time in seconds before the asset expiry when you want to receive a notification. If you are an administrator or the asset creator, you receive a message before the expiration of the asset. After the asset expiry, you receive another notification that confirms the expiration. In addition, the expired asset is deactivated.

1. Select **[!UICONTROL Save]**.
-->

## 资产状态 {#asset-states}

[!DNL Assets]控制台可以显示资源的各种状态。 根据特定资产的当前状态，其卡片视图会显示一个描述其状态的标签，例如，已过期、已发布、已批准、已拒绝等。

1. 在[!DNL Assets]用户界面中，选择一个资产。

1. 从工具栏中选择&#x200B;**[!UICONTROL 发布]**。 如果在工具栏中未看到[!UICONTROL 发布]选项，请单击工具栏上的&#x200B;**[!UICONTROL 更多]**，然后找到&#x200B;**[!UICONTROL 发布]**&#x200B;选项。

1. 从菜单中选择&#x200B;**[!UICONTROL 发布]**，然后关闭确认对话框。

1. 退出选择模式。 资源的发布状态显示在卡片视图的资源缩略图底部。 在列表视图中，已发布列显示资产的发布时间。

1. 要显示其资源详细信息页面，请在[!DNL Assets]界面中选择一个资源，然后单击&#x200B;**[!UICONTROL 属性]**。

1. 在[!UICONTROL 高级]选项卡中，通过&#x200B;**[!UICONTROL 过期]**&#x200B;字段设置资源的过期日期。

1. 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 关闭]**&#x200B;以显示资产控制台。

1. 资源的发布状态表示卡片视图中资源缩略图底部的已过期状态。 在列表视图中，资产的状态显示为&#x200B;**[!UICONTROL 已过期]**。

1. 在[!DNL Assets]控制台中，选择一个文件夹，然后在该文件夹上创建审核任务。

1. 审阅并批准/拒绝审阅任务中的资产，然后单击&#x200B;**[!UICONTROL 完成]**。

1. 导航到您为其创建审阅任务的文件夹。 您批准/拒绝的资产状态将显示在卡片视图的底部。 在列表视图中，审批和到期状态显示在相应的列中。

1. 要根据资产的状态搜索资产，请单击&#x200B;**[!UICONTROL 搜索]**&#x200B;以显示搜索栏。

1. 选择`Return`并单击[!DNL Experience Manager]。

1. 在搜索面板中，单击&#x200B;**[!UICONTROL 发布状态]**&#x200B;并选择&#x200B;**[!UICONTROL 已发布]**&#x200B;以在[!DNL Assets]中搜索已发布的资源。

1. 要搜索已批准或已拒绝的资产，请选择&#x200B;**[!UICONTROL 批准状态]**&#x200B;并选择适当的选项。

1. 要根据资产的到期状态搜索资产，请在搜索面板中选择&#x200B;**[!UICONTROL 到期状态]**，然后选择相应的选项。

1. 您还可以根据各种搜索彩块化下的状态组合搜索资源。 例如，您可以搜索在审核任务中批准且未过期的已发布资产。 要搜索此类资源，请在搜索彩块化中选择相应的选项。

## [!DNL Assets]中的Digital Rights Management {#digital-rights-management-in-assets-1}

DRM功能强制接受许可协议，然后才能从[!DNL Assets]下载许可资产。

如果您选择受保护的资产并单击&#x200B;**[!UICONTROL 下载]**，则会将您重定向到许可证页面以接受许可协议。 如果不接受许可协议，**[!UICONTROL 下载]**&#x200B;选项将不可用。

如果所选内容包含多个受保护资产，则一次选择一个资产，接受许可协议，然后继续下载资产。

如果满足以下任一条件，则资产被视为受保护：

* 资源元数据属性`xmpRights:WebStatement`指向包含资源的许可协议的页面的路径。
* 资源元数据属性`adobe_dam:restrictions`的值是指定许可协议的原始HTML。

>[!NOTE]
>
>位置`/etc/dam/drm/licences`用于存储早期版本的[!DNL Experience Manager]中的许可证。 该位置现已弃用。 如果您创建或修改许可证页面，或者从以前的[!DNL Experience Manager]版本移植页面，Adobe建议您将此类资源存储在`/apps/settings/dam/drm/licenses`或`/conf/*/settings/dam/drm/licenses`位置。

### 下载受DRM保护的资产 {#downloading-drm-assets}

1. 在卡片视图中，选择要下载的资源并选择&#x200B;**[!UICONTROL 下载]**。
1. 在&#x200B;**[!UICONTROL 版权管理]**&#x200B;页面，从列表中选择要下载的资产。
1. 在[!UICONTROL 许可证]窗格中，选择&#x200B;**[!UICONTROL 同意]**。 资产旁边会显示一个复选标记。 选择&#x200B;**[!UICONTROL 下载]**&#x200B;选项。

   >[!NOTE]
   >
   >仅当您选择同意受保护资产的许可协议时，才会启用&#x200B;**[!UICONTROL 下载]**&#x200B;选项。 但是，如果您的选择包含受保护和不受保护的资产，则窗格中仅列出受保护的资产，并且&#x200B;**[!UICONTROL 下载]**&#x200B;选项可用于下载不受保护的资产。 要同时接受多个受保护资产的许可协议，请从列表中选择资产，然后选择“同 **[!UICONTROL 意”]**。

1. 要下载资源或其演绎版，请在对话框中选择&#x200B;**[!UICONTROL 下载]**。

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
