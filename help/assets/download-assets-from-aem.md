---
title: 从 AEM 下载资产
description: 了解如何从AEM下载资产以及启用或禁用下载功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12575cd2f046d3a382786811dd28fec8df3be8bd
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

您可以下载包括静态和动态演绎版在内的资产。 或者，您也可以直接从发送电子邮件，其中包含指向资产的链 [!DNL Adobe Experience Manager Assets]接。 下载的资产会打包在 ZIP 文件中。对于导出作业，压缩的 ZIP 文件大小最大为 1 GB。每个导出作业最多允许500个资产总数。

>[!NOTE]
>
>收件人电子邮件必须是组的成 `dam-users` 员才能访问电子邮件中的ZIP下载链接。 要能够下载资产，成员必须具有启动触发资产下载的工作流的权限。

无法下载图像集、旋转集、混合媒体集和传送集等资产类型。

**要下载资源，**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Navigation]** (Compass icon).
1. 在导航页面上，点按资 **[!UICONTROL 产>文件]**。
1. 导航到包含要下载的资产的文件夹。
1. 选择文件夹，或在文件夹中选择一个或多个资产。
1. On the toolbar, tap **[!UICONTROL Download]**.

   ![从Experience Manager资产下载资产时可用的选项](/help/assets/assets/asset-download1.png)

   *下载对话框选项。*

1. 在“下载”对话框中，选择所需的下载选项。

   | 下载选项 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资产创建单独的文件夹]** | 选择此选项可将您下载的每个资产包括嵌套在资产父文件夹下的子文件夹中的资产，并包含到本地计算机上的一个文件夹中。 如果不选择此选项 ** ，则默认情况下，将忽略文件夹层次结构，并将所有资产下载到本地计算机上的一个文件夹中。 |
   | **[!UICONTROL 电子邮件]** | 选择此选项可向收件人发送电子邮件通知。 标准电子邮件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 在部署过程中自定义的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在以下位置存储特定于租户的自定义模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资产]** | 选择此选项可以下载资产的原始形式，而无需任何演绎版。<br>如果原始资产具有子资产，则子资产选项可用。 |
   | **[!UICONTROL 演绎版]** | 演绎版是资产的二进制表示形式。资产具有主要表示形式——即已上传文件的表示形式。 它们可以有任意数量的表示。 <br> 通过此选项，您可以选择要下载的演绎版。 可用的演绎版取决于您选择的资产。 |
   | **[!UICONTROL 智能裁剪]** | 选择此选项可从AEM中下载选定资产的所有智能裁剪演绎版。 系统会创建包含智能裁剪演绎版的zip文件，并将其下载到您的本地计算机。 |
   | **[!UICONTROL 动态演绎版]** | 选择此选项可实时生成一系列替代再现。 When you select this option, you also select the renditions that you want to create dynamically by selecting from the [Image Preset](/help/assets/dynamic-media/image-presets.md) list. <br>此外，您还可以选择大小和度量单位、格式、色彩空间、分辨率以及任何可选的图像修饰符（如反转图像）。 此选项仅在您已启用的情况下才 [!DNL Dynamic Media] 可用。 |

1. 在对话框中，点按下 **[!UICONTROL 载]**。


## 启用资产下载servlet {#enable-asset-download-servlet}

AEM中的默认servlet允许经过身份验证的用户发出任意大的并发下载请求，以创建对他们可见的资产的ZIP文件，这些文件可能会使服务器和网络过载。 为了减轻由此功能引起的潜在DoS风险， `AssetDownloadServlet` 默认情况下，发布实例会禁用OSGi组件。

要允许从DAM下载资产，例如，在使用诸如资产共享共享共享资源或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议尽可能将允许的下载大小设置为最小，而不影响日常下载要求。 高价值可能会影响性能。

1. 创建一个具有命名约定的文件夹，该命名约定目标发布运行模式，即 `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在config文件夹中，创建一个名为的新 `nt:file` 文件 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。
1. 填充 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` 以下内容。 将下载的最大大小（以字节为单位）设置为值 `asset.download.prezip.maxcontentsize`。 以下示例将ZIP下载的最大大小配置为不超过100 kB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用资产下载servlet {#disable-asset-download-servlet}

通过 `Asset Download Servlet` 更新调度程序配置以阻止任何资产下载请求，可以在AEM Publish实例上禁用该功能。 也可以直接通过OSGi控制台手动禁用servlet。

1. 要通过调度程序配置阻止资产下载请求，请 `dispatcher.any` 编辑配置，并向过滤器部分添加 [新规则](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资源](drm.md)
>* [在Win或Mac桌面上使用AEM桌面应用程序下载资源](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [从支持的Adobe Creative Cloud应用程序中使用Adobe Assets Link下载资产](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)

