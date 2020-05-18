---
title: 从 AEM 下载资产
description: 了解如何从AEM下载资产以及启用或禁用下载功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c978be66702b7f032f78a1509f2a11315d1ed89f
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 9%

---


# 从 AEM 下载资产 {#download-assets-from-aem}

您可以下载包括静态和动态演绎版在内的资产。 下载的资产会打包在ZIP文件中。 对于导出作业，压缩的 ZIP 文件大小最大为 1 GB。每个导出作业最多允许处理的资产总数为 500 个。

>[!NOTE]
>
>要能够下载资产，成员必须具有启动触发资产下载的工作流的权限。

要下载资产，请导航到资产，选择资产，然后点按／单击工 **[!UICONTROL 具栏]** 中的下载图标。 在显示的对话框中，指定下载选项。

无法下载图像集、旋转集、混合媒体集和传送集等资产类型。

![从AEM资产下载资产时的可用选项](assets/asset_download_dialog.png)

*图： 从AEM资产下载资产时可用的选项。*

以下是“导出／下载”选项。 动态演绎版是Dynamic Media特有的选项，通过它，您除了可以选择的资产外，还可以动态生成演绎版——只有在启用了Dynamic Media的情况下，此选项才可用。

| 导出或下载选项 | 描述 |
|---|---|
| [!UICONTROL 资产] | 选择此选项可下载资产的原始形式，而不下载任何演绎版。 |
| [!UICONTROL 演绎版] | 演绎版是资产的二进制表示形式。资产具有主要表示形式——即已上传文件的表示形式。 它们可以有任意数量的表示。 <br> 通过此选项，您可以选择要下载的演绎版。 可用的演绎版取决于您选择的资产。 |
| [!UICONTROL 动态演绎版] | 动态演绎版可动态生成其他演绎版。当您选择此选项时，您还可以从图像预设列表中选择要动态创建的演绎版。 此外，您还可以选择大小和度量单位、格式、色彩空间、分辨率以及任何图像修饰符（例如反转图像） |
| [!UICONTROL 为每个资产创建单独的文件夹] | 选择此项可在下载资产时保留文件夹层次结构。 默认情况下，文件夹层次结构会被忽略，所有资产都下载到本地系统的一个文件夹中。 |

如果资产具有任何演绎版，则可使用选项演绎版选项。 如果资产包含子资产，则子资产选项可用。

当您选择要下载的文件夹时，将下载该文件夹下的完整资产层次结构。 要将您下载的每个资产（包括嵌套在父文件夹下的子文件夹中的资产）包含在单个文件夹中，请选 **[!UICONTROL 择为每个资产创建单独的文件夹]**。

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

通过 `Asset Download Servlet` 更新调度程序配置来阻止任何资产下载请求，可以在AEM发布实例上禁用该功能。 也可以直接通过OSGi控制台手动禁用servlet。

1. 要通过调度程序配置阻止资产下载请求，请 `dispatcher.any` 编辑配置，并向过滤器部分添加 [新规则](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)。

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [下载受DRM保护的资源](drm.md)
>* [在Win或Mac桌面上使用AEM桌面应用程序下载资源](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [从支持的Adobe Creative Cloud应用程序中使用Adobe Assets Link下载资产](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html)

