---
title: 从 AEM 下载资产
description: 了解如何从AEM下载资产以及启用或禁用下载功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6998ee5f3c1c1563427e8739998effe0eba867fc

---


# 从 AEM 下载资产 {#download-assets-from-aem}

您可以下载包括静态和动态演绎版在内的资产。下载的资产将打包在ZIP文件中。 对于导出作业，压缩的 ZIP 文件大小最大为 1 GB。每个导出作业最多允许处理的资产总数为 500 个。

>[!NOTE]
>
>要能够下载资产，成员必须具有启动触发资产下载的工作流的权限。

要下载资产，请导航到资产，选择资产，然后点按／单击工具栏中 **[!UICONTROL 的下载]** 图标。 在显示的对话框中，指定下载选项。

无法下载图像集、旋转集、混合媒体集和传送集等资产类型。

![从AEM资产下载资产时可用的选项](assets/asset_download_dialog.png)*图：从AEM资产下载资产时可用的选项*

以下是“导出／下载”选项。 动态演绎版是Dynamic Media特有的，它允许您在动态生成演绎版的同时选择资产——只有在启用了Dynamic Media的情况下，此选项才可用。

| 导出或下载选项 | 描述 |
|---|---|
| [!UICONTROL 资产] | 选择此选项可以下载资产的原始形式，而无需任何演绎版。 |
| [!UICONTROL 演绎版] | 演绎版是资产的二进制表示形式。资产具有主要表示形式——已上传文件的表示形式。 他们可以有任意数量的表示形式。 <br> 通过此选项，您可以选择要下载的演绎版。 可用的演绎版取决于您选择的资产。 |
| [!UICONTROL 动态演绎版] | 动态演绎版可动态生成其他演绎版。选择此选项后，您还可以从图像预设列表中选择要动态创建的演绎版。 此外，您还可以选择大小和度量单位、格式、色彩空间、分辨率以及任何图像修饰符（例如反转图像） |
| [!UICONTROL 为每个资产创建单独的文件夹] | 选择此选项可在下载资产时保留文件夹层次结构。 默认情况下，文件夹层次结构将被忽略，所有资产都下载在本地系统的一个文件夹中。 |

如果资产有任何演绎版，则选项演绎版选项可用。 如果资产包含子资产，则子资产选项可用。

当您选择要下载的文件夹时，将下载该文件夹下的完整资产层次结构。 要将您下载的每个资产（包括嵌套在父文件夹下的子文件夹中的资产）包含在单个文件夹中，请为每个资 **[!UICONTROL 产选择创建单独的文件夹]**。

## 启用资产下载servlet {#enable-asset-download-servlet}

AEM中的默认servlet允许经过身份验证的用户发出任意大的并发下载请求，以创建对他们可见的资产的ZIP文件，这些文件可能会使服务器和网络过载。 为了减轻由此功能引起的潜在DoS风险， `AssetDownloadServlet` OSGi组件在默认情况下对发布实例处于禁用状态。

要允许从您的DAM下载资产，例如，在使用类似于Asset Share Commons或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议尽可能低地设置允许的下载大小，而不影响日常下载要求。 高价值可能会影响性能。

1. 创建一个以发布运行模式为目标的命名约定的文件夹，即 `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在config文件夹中，创建一个名为的新文 `nt:file` 件类型 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. 填充 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 以下内容。 将下载的最大大小（以字节为单位）设置为 `asset.download.prezip.maxcontentsize`。 以下示例将ZIP下载的最大大小配置为不超过100 kB。

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用资产下载servlet {#disable-asset-download-servlet}

可以 `Asset Download Servlet` 通过更新调度程序配置来阻止任何资产下载请求，在AEM发布实例上禁用该功能。 也可以直接通过OSGi控制台手动禁用Servlet。

1. 要通过调度程序配置阻止资产下载请求，请编辑 `dispatcher.any` 配置，并向过滤器部分添加新 [规则](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资源](drm.md)
>* [在Win或Mac桌面上使用AEM桌面应用程序下载资源](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [从支持的Adobe Creative Cloud应用程序中使用Adobe Assets Link下载资源](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


<!-- FULL ARTICLE ARCHIVE IS BELOW 

You can download assets including static and dynamic renditions. Alternatively, you can send emails with links to assets directly from AEM Assets. Downloaded assets are bundled in a ZIP file. The compressed ZIP file has a maximum file size of 1 GB for the export job. You are allowed a maximum of 500 total assets per export job.

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.

To download assets, navigate to an asset, select the asset, and tap/click the **[!UICONTROL Download]** icon from the toolbar. In the resulting dialog, specify your download options.

The asset types Image Sets, Spin Sets, Mixed Media Sets, and Carousel Sets cannot be downloaded.

![Available options when downloading assets from AEM Assets](assets/asset_download_dialog.png)
*Figure: Available options when downloading assets from AEM Assets*

The following are the Export/Download options. Dynamic renditions are unique to Dynamic Media and let you generate renditions on-the-fly in addition to the asset you selected - that option is only available if you have Dynamic Media enabled.

|Export or download options|Descriptions|
|---|---|
| [!UICONTROL Assets]| Select this to download the asset in its original form without any renditions.|
| [!UICONTROL Renditions] |A rendition is the binary representation of an asset. Assets have a primary representation - that of the uploaded file. They can have any number of representations. <br> With this option, you can select the renditions you want downloaded. The renditions available depend on the asset you select.|
| [!UICONTROL Dynamic Renditions] |A dynamic rendition generates other renditions on-the-fly. When you select this option, you also select the renditions you want to create dynamically by selecting from the image presets list. In addition, you can select the size and unit of measurement, format, color space, resolution, and any image modifiers (for example to invert the image)|
| [!UICONTROL Email] |An email notification is sent to the user. Standard emails templates are available at the following locations:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Templates that you customize during deployment should be present at these locations: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>You can store tenant-specific custom templates at these locations:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>|
| [!UICONTROL Create separate folder for each asset] |Select this to preserve the folder hierarchy while downloading assets. By default, the folder hierarchy is ignored and all assets are downloaded in one folder in your local system.|

The option renditions option is available if the asset has any renditions. The subassets option is available if the asset includes subassets.

When you select a folder to download, the complete asset hierarchy under the folder is downloaded. To include each asset you download (including assets in child folders nested under the parent folder) in an individual folder, select **[!UICONTROL Create separate folder for each asset]**.

## Enable asset download servlet {#enable-asset-download-servlet}

The default servlet in AEM allows authenticated users to issue arbitrarily-large, concurrent download requests for creating ZIP files of assets visible to them that can overload the server and the network. To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

To allow downloading assets from your DAM, say when using something like Asset Share Commons or other portal-like implementation, manually enable the servlet via an OSGi configuration. Adobe recommends setting the permissible download size as low as possible without affecting the day-to-day download requirements. A high value may impact performance.

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Sets a maximum size (in bytes) for the download as value of `asset.download.prezip.maxcontentsize`. The below sample configures the maximum size of the ZIP download to not exceed 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. The servlet can also be manually disabled via the OSGi console directly.

1. To block asset download requests via a dispatcher configuration edit the `dispatcher.any` configuration and add a new rule to the [filter section](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Download DRM protected assets](drm.md)
>* [Download assets using AEM desktop app on Win or Mac desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Download assets using Adobe Assets Link from within the supported Adobe Creative Cloud apps](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


-->