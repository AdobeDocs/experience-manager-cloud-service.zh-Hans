---
title: 下载资源
description: 从以下位置下载资源 [!DNL Adobe Experience Manager Assets] 和启用或禁用下载功能。
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 4%

---

# 从以下位置下载资源 [!DNL Adobe Experience Manager] {#download-assets-from-aem}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=en) |
| AEM as a Cloud Service | 本文 |

您可以下载资源，包括静态和动态演绎版。 或者，您可以直接发送带有资产链接的电子邮件，链接指向 [!DNL Adobe Experience Manager Assets]. 下载的资源捆绑在一个ZIP文件中。 <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

无法下载以下资源类型：图像集、旋转集、混合媒体集和轮播集。

您可以使用以下方法从Experience Manager下载资源：

<!-- * [Link Share](#link-share-download) -->

* [Experience Manager用户界面](#download-assets)
* [资产共享公用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用下载资源 [!DNL Experience Manager] 界面 {#download-assets}

Experience Manager根据资源数量和大小优化下载体验。 从用户界面实时下载较小的文件。 [!DNL Experience Manager] 直接下载原始文件的单个资产请求，而不是将单个资产放在ZIP存档中，这样可以加快下载速度。 Experience Manager支持通过异步请求进行大型下载。 大于100 GB的下载请求将拆分为多个ZIP存档，每个存档的最大大小为100 MB。

默认情况下， [!DNL Experience Manager] 在中触发通知 [[!DNL Experience Manager] 收件箱](/help/sites-cloud/authoring/getting-started/inbox.md) 生成下载存档时。

![收件箱通知](assets/inbox-notification-for-large-downloads.png)


### 为大型下载启用电子邮件通知 {#enable-emails-for-large-downloads}

在以下任意情况下都会触发异步下载：

* 如果有十个以上的资产
* 如果下载大小大于100 MB
* 如果下载准备时间超过30秒

在后端运行异步下载时，用户可以继续探索并进一步在Experience Manager中工作。 除了Experience Manager收件箱通知之外，Experience Manager还可以发送电子邮件，以在下载过程完成后通知User。 要启用此功能，管理员可以通过以下方式配置电子邮件服务 [配置SMTP服务器连接](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

配置电子邮件服务后，管理员和用户可以从Experience Manager界面启用电子邮件通知。

要启用电子邮件通知，请执行以下操作：

1. 登录 [!DNL Experience Manager Assets].
1. 单击右上角的用户图标，然后单击 **[!UICONTROL 我的首选项]** 打开“用户首选项”窗口。
1. 选择 **[!UICONTROL 资产下载电子邮件通知]** 复选框，然后单击 **[!UICONTROL Accept]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


要下载资产，请执行以下步骤：

1. 在 [!DNL Experience Manager] 用户界面，单击 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**.
1. 导航到要下载的资源。 选择文件夹或文件夹中的一个或多个资源。 在工具栏上，单击 **[!UICONTROL 下载]**.

   ![从下载资源时可用的选项 [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. 在下载对话框中，选择所需的下载选项。

   | 下载选项 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资源创建单独的文件夹]** | 选择此选项可为每个资源创建一个文件夹，其中包含资源的所有已下载演绎版。 如果未选定该属性，则每个资产（以及所选的下载资产演绎版）都会包含在生成的存档的父文件夹中。 |
   | **[!UICONTROL 电子邮件]** | 选择此选项可向其他用户发送电子邮件通知（包含下载链接）。 收件人用户必须是 `dam-users` 组。 标准电子邮件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您可以在以下位置找到部署期间自定义的模板： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在以下位置存储特定于租户的自定义模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资产]** | 选择此选项可下载原始格式的资源。<br>如果原始资产具有子资产，则子资产选项可用。 |
   | **[!UICONTROL 节目]** | 演绎版是资产的二进制表示形式。 资产具有主要表示形式 — 即上传文件的表示形式。 它们可以有任意数量的呈现。 <br> 使用此选项，您可以选择想要下载的演绎版。 可用的演绎版取决于您选择的资源。 |
   | **[!UICONTROL 智能裁剪]** | 选择此选项可从下载所选资源的所有智能裁剪演绎版 [!DNL Experience Manager]. 将创建包含智能裁剪呈现的zip文件并下载到本地计算机。 |
   | **[!UICONTROL 动态演绎版]** | 选择此选项可实时生成一系列替代演绎版。 选择此选项时，您还可以通过从以下各项中选择要动态创建的演绎版 [图像预设](/help/assets/dynamic-media/image-presets.md) 列表。 <br>此外，您还可以选择大小和测量单位、格式、颜色空间、分辨率以及任何可选的图像修饰符（如反转图像）。 仅当满足以下条件时，选项才可用 [!DNL Dynamic Media] 已启用。 |

1. 在对话框中，单击 **[!UICONTROL 下载]**.

   如果为大型下载启用了电子邮件通知，则收件箱中会显示一封包含已存档zip文件夹的下载URL的电子邮件。 单击电子邮件中的下载链接以下载zip存档。

   ![适用于大型下载的电子邮件通知](/help/assets/assets/email-for-large-notification.png)

   您还可以在以下位置查看通知 [!DNL Experience Manager] 收件箱。

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## 下载使用链接共享功能共享的资源 {#link-share-download}

使用链接共享资源是一种方便的方法，让感兴趣的人无需登录到即可访问它 [!DNL Assets]. 请参阅 [链接共享功能](/help/assets/share-assets.md#sharelink).

当用户从共享链接下载资产时， [!DNL Assets] 使用异步服务，提供更快且无中断的下载。 要下载的资产将在收件箱中的后台排入可管理文件大小的ZIP存档中。 对于较大的下载，下载将分块为100 GB的文件。

此 [!UICONTROL 下载收件箱] 显示每个存档的处理状态。 处理完成后，您可以从收件箱中下载存档。

![下载收件箱](assets/link-sharing-download-inbox.png)

## 启用资源下载servlet {#enable-asset-download-servlet}

中的默认servlet [!DNL Experience Manager] 允许经过身份验证的用户发出任意大型的并发下载请求，以创建资产的ZIP文件。 下载准备工作可能会影响性能，甚至可能导致服务器和网络过载。 要减少此功能引起的此类类似DoS的潜在风险， `AssetDownloadServlet` 发布实例已禁用OSGi组件。 如果在创作实例上不需要下载功能，请在创作实例上禁用servlet。

要允许从DAM下载资产，例如在使用Asset Share Commons或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议将允许的下载大小设置得尽可能小，而不影响日常下载要求。 高值可能会影响性能。

1. 创建具有针对发布运行模式的命名约定的文件夹，即， `config.publish`：

   `/apps/<your-app-name>/config.publish`

1. 在config文件夹中，创建一个文件类型 `nt:file` 已命名 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. 填充 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` ，如下所示。 将下载的最大大小（以字节为单位）设置为的值 `asset.download.prezip.maxcontentsize`. 下面的示例将ZIP下载的最大大小配置为不超过100 KB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用资源下载servlet {#disable-asset-download-servlet}

如果您不需要下载功能，请禁用Servlet以防止任何类似DoS的风险。 此 `Asset Download Servlet` 可以在上禁用 [!DNL Experience Manager] 通过更新Dispatcher配置来阻止任何资产下载请求，从而创作和发布实例。 也可以直接通过OSGi控制台手动禁用servlet。

1. 要通过Dispatcher配置阻止资源下载请求，请编辑 `dispatcher.any` 配置并将新规则添加到 [过滤区域](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## OnTime或OffTime呈现版本 {#on-off-time-rendition}

要启用 `OnOffTimeAssetAccessFilter` 服务，您需要创建OSGi配置。 根据开启/结束时间设置，此服务允许除了资源本身之外，还阻止对演绎版和元数据的访问。 OSGi配置应为 `com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`. 应遵循以下步骤：

1. 在Git的项目代码中，创建配置文件，位于 `/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`. 文件应包含 `{}` 作为其内容，表示相应的OSGi组件的OSGi配置为空。 此操作将启用该服务。
1. 通过以下方式部署您的代码，包括此新配置 [!DNL Cloud Manager].
1. 部署后，即可根据资源的开启/结束时间设置访问演绎版和元数据。 如果当前日期或时间早于开启时间或晚于关闭时间，则会显示错误消息。
有关添加空OSGi配置的更多详细信息，请参阅此 [指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en).

## 提示和限制 {#tips-limitations}

* 如果下载空文件夹， [!DNL Experience Manager] 传达有关创建ZIP存档的成功消息，但并未创建该存档。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资产](drm.md)
>* [在Win或Mac桌面上使用Experience Manager桌面应用程序下载资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [使用受支持的Adobe Creative Cloud应用程序中的Adobe资源链接下载资源](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
