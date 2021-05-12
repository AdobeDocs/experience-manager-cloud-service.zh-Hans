---
title: 下载资产
description: 从 [!DNL Adobe Experience Manager Assets] 下载资源，然后启用或禁用下载功能。
contentOwner: AG
feature: 资产管理
role: Business Practitioner
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
translation-type: tm+mt
source-git-commit: a14d5ec69889ef3d89e595cd837f182c499d0ebc
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 7%

---

# 从[!DNL Adobe Experience Manager] {#download-assets-from-aem}下载资源

您可以下载包括静态和动态演绎版在内的资产。 或者，您也可以从[!DNL Adobe Experience Manager Assets]直接发送包含指向资产链接的电子邮件。 下载的资产会打包在 ZIP 文件中。对于导出作业，压缩的 ZIP 文件大小最大为 1 GB。每个导出作业最多允许总共500个资产。

>[!NOTE]
>
>收件人封电子邮件必须是`dam-users`组的成员才能访问电子邮件中的ZIP下载链接。 要能够下载资产，成员必须具有启动工作流的权限，以触发资产下载。

无法下载图像集、旋转集、混合媒体集和传送集等资产类型。

您可以使用以下方法下载Experience Manager资源：

* [Experience Manager用户界面](#download-in-aem)
* 资产链接共享用户界面
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## 使用[!DNL Experience Manager]接口{#download-in-aem}下载资源

异步下载服务为大型资源的无缝下载提供了一个框架。 从用户界面实时下载较小的文件。 大型文件会异步下载，用户会通过收件箱中的Experience Manager通知获得完成通知。 请参阅[了解Experience Manager收件箱](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html)。

![下载通知](assets/download-notification.png)

*图：通过收件箱下 [!DNL Experience Manager] 载通知。*

在以下任一情况下将触发异步下载：

* 如果要下载的资源超过10个或超过100 MB。
* 如果下载需要30秒以上的时间准备。

要下载资产，请执行以下步骤：

1. 在[!DNL Experience Manager]用户界面中，单击&#x200B;**[!UICONTROL 资产]** > **[!UICONTROL 文件]**。
1. 导航到要下载的资产。 选择文件夹，或在文件夹中选择一个或多个资产。 在工具栏上，单击&#x200B;**[!UICONTROL 下载]**。

   ![从下载资产时的可用选项  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *图：下载对话框选项。*

1. 在“下载”对话框中，选择所需的下载选项。

   | 下载选项 | 描述 |
   |---|---|
   | **[!UICONTROL 为每个资产创建单独的文件夹]** | 选择此选项可将您下载的每个资产（包括嵌套在资产父文件夹下的子文件夹中的资产）包含到本地计算机上的一个文件夹中。 如果此选项为&#x200B;*not*&#x200B;选择，则默认情况下，文件夹层次结构将被忽略，所有资产都将下载到本地计算机中的一个文件夹中。 |
   | **[!UICONTROL 电子邮件]** | 选择此选项可向收件人发送电子邮件通知。 标准电子邮件模板可在以下位置使用：<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> 您在部署过程中自定义的模板可在以下位置使用： <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>您可以在以下位置存储特定于租户的自定义模板：<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL 资产]** | 选择此选项可下载资产的原始形式，而不下载任何演绎版。<br>如果原始资产包含子资产，则子资产选项可用。 |
   | **[!UICONTROL 演绎版]** | 演绎版是资产的二进制表示形式。资产具有主要表示形式 — 已上传文件的表示形式。 他们可以有任意数量的表示形式。 <br> 通过此选项，您可以选择要下载的演绎版。可用的演绎版取决于您选择的资产。 |
   | **[!UICONTROL 智能裁剪]** | 选择此选项可从[!DNL Experience Manager]中下载选定资产的所有智能裁剪演绎版。 系统会创建包含智能裁剪演绎版的zip文件，并将其下载到您的本地计算机。 |
   | **[!UICONTROL 动态演绎版]** | 选择此选项可实时生成一系列替代演绎版。 当您选择此选项时，您还可以从[图像预设](/help/assets/dynamic-media/image-presets.md)列表中选择要动态创建的演绎版。 <br>此外，您还可以选择大小和度量单位、格式、色彩空间、分辨率以及任何可选的图像修饰符（如反转图像）。仅当您启用了[!DNL Dynamic Media]时，此选项才可用。 |

1. 在对话框中，单击&#x200B;**[!UICONTROL 下载]**。

## 启用资产下载servlet {#enable-asset-download-servlet}

[!DNL Experience Manager]中的默认servlet允许经过身份验证的用户发出任意大型的并发下载请求，以创建资源的ZIP文件。 下载准备可能会影响性能，甚至可能使服务器和网络过载。 要减轻由此功能引起的类似DoS的潜在风险，将对发布实例禁用`AssetDownloadServlet` OSGi组件。 如果您在创作实例上不需要下载功能，请在创作时禁用servlet。

要允许从您的DAM下载资产，例如，在使用Asset Share Commons或其他类似门户的实施时，请通过OSGi配置手动启用servlet。 Adobe建议尽可能低地设置允许的下载大小，而不影响日常下载要求。 高价值可能会影响性能。

1. 创建一个具有命名约定的文件夹，该命名约定目标发布运行模式，即`config.publish`:

   `/apps/<your-app-name>/config.publish`

1. 在config文件夹中，创建一个名为`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`的类型为`nt:file`的新文件。
1. 使用以下填充`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`。 将下载的最大大小（以字节为单位）设置为`asset.download.prezip.maxcontentsize`值。 以下示例将ZIP下载的最大大小配置为不超过100 kB。

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## 禁用资源下载servlet {#disable-asset-download-servlet}

如果您不需要下载功能，请禁用servlet以防止任何类似DoS的风险。 `Asset Download Servlet`可以通过更新调度程序配置来阻止任何资产下载请求，在[!DNL Experience Manager]作者实例和发布实例上禁用。 也可以直接通过OSGi控制台手动禁用Servlet。

1. 要通过调度程序配置阻止资源下载请求，请编辑`dispatcher.any`配置，并向[过滤器部分](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)添加新规则。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资源](drm.md)
>* [在Win或Mac桌面上使用Experience Manager桌面应用程序下载资源](https://helpx.adobe.com/cn/experience-manager/desktop-app/aem-desktop-app.html)
>* [使用支持的Adobe Creative Cloud应用程序中的Adobe Assets链接下载资源](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)

