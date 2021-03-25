---
title: 启用渐进式Web应用程序功能
description: AEM Sites允许内容作者通过简单的配置而非编码向任何站点提供渐进式Web应用程序功能。
translation-type: tm+mt
source-git-commit: f130fe34e5c57b9fc78697374a5a9772da3c4c17
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 0%

---


# 启用渐进式Web应用程序功能{#enabling-pwa}

通过简单的配置，内容作者现在可以为在AEM Sites中创建的体验启用渐进式Web应用程序(PWA)功能。

>[!CAUTION]
>
>这是一项高级功能，它需要：
>
>* PWA
>* 了解您的站点和内容结构
>* 了解缓存策略
>* 开发团队的支持

>
>
建议您在使用此功能之前与开发团队讨论此功能，以定义将其用于您的项目的最佳方式。

>[!NOTE]
>
>本文档中描述的功能计划在AEM的[ 2021年3月版本中作为Cloud Service提供。](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## 简介 {#introduction}

[渐进式Web应用程序(PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) )允许将AEM站点存储在用户机器上的本地并脱机访问，从而为它们提供令人痴迷的类似应用程序的体验。即使失去Internet连接，用户也可以在外出时浏览站点。 PWA提供无缝体验，即使网络丢失或不稳定。

内容作者无需对站点进行任何重新编码，而是能够将PWA属性配置为站点[页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)中的附加选项卡。

* 保存或发布时，此配置会触发一个事件处理函数，该处理函数会写出[清单文件](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服务worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)，以在站点上启用PWA功能。
* 还维护Sling映射，以确保从应用程序的根服务Service Worker，以启用代理内容，允许应用程序内的脱机功能。

借助PWA，用户可以获得站点的本地副本，即使没有Internet连接，也能提供类似App的体验。

>[!NOTE]
>
>渐进式Web应用程序是一种不断发展的技术，支持本地应用程序安装，其他功能[取决于您使用的浏览器。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 前提条件 {#prerequisites}

为了能够对您的站点使用PWA功能，您的项目环境有两个要求：

1. [使用核](#adjust-components) 心组件来利用此功能
1. [调整调](#adjust-dispatcher) 度程序规则以公开所需的文件

这些是作者需要与开发团队协调的技术步骤。 每个站点只需执行一次这些步骤。

### 使用核心组件 {#adjust-components}

核心组件2.15.0及更高版本完全支持AEM站点的PWA功能。 由于AEMaCS始终包含最新版核心组件，您可以利用现成的PWA功能。 您的AEMaCS项目自动满足此要求。

>[!NOTE]
>
>Adobe不建议对自定义组件或从核心组件扩展的组件使用PWA功能。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)[
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer will need to add the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer will also need to add the following link to the `customfooterlibs.html` file of your page component.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```
-->

### 调整调度程序{#adjust-dispatcher}

PWA功能生成并使用`/content/<sitename>/manifest.webmanifest`文件。 默认情况下，[调度程序](/help/implementing/dispatcher/overview.md)不公开此类文件。 要公开这些文件，开发人员必须将以下配置添加到您的站点项目。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

根据您的项目，您可能希望包含重写规则的不同类型的扩展。 当您引入了隐藏和重定向到`/content/<projectName>`的请求的规则时，`webmanifest`扩展在重写条件中可能很有用。

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## 为您的站点{#enabling-pwa-for-your-site}启用PWA

满足[先决条件](#prerequisites)后，内容作者很容易为站点启用PWA功能。 以下是如何执行此操作的基本概述。 各个选项详见[详细选项部分。](#detailed-options)

1. 登录AEM。
1. 在主菜单中，点按或单击&#x200B;**导航** -> **站点**。
1. 选择您的站点项目，然后点按或单击&#x200B;[**属性**](/help/sites-cloud/authoring/fundamentals/page-properties.md)&#x200B;或使用热键`p`。
1. 选择&#x200B;**渐进式Web应用程序**&#x200B;选项卡并配置适用的属性。 您至少希望：
   1. 选择选项&#x200B;**启用PWA**。
   1. 定义&#x200B;**启动URL**。

      ![启用 PWA](../assets/pwa-enable.png)

   1. 将512x512 png图标上传到DAM，并引用该图标作为应用程序的图标。

      ![定义PWA图标](../assets/pwa-icon.png)

   1. 配置您希望服务工作者脱机的路径。 典型路径为：
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * 任何第三方字体引用
      * `/etc/clientlibs/<sitename>`

      ![定义PWA脱机路径](../assets/pwa-offline.png)


1. 点按或单击&#x200B;**保存并关闭**。

您的站点现已配置完毕，您可以[将其作为本地应用程序安装。](#using-pwa-enabled-site)

## 使用启用PWA的站点{#using-pwa-enabled-site}

现在，您已将[站点配置为支持PWA,](#enabling-pwa-for-your-site)您可以亲身体验。

1. 在[支持的浏览器中访问站点。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 浏览器的地址栏中将显示一个新图标，指示站点可以作为本地应用程序安装。
   * 根据浏览器的不同，图标可能会有所不同，而且浏览器还可能显示通知（如横幅或对话框），指明可以作为本地应用程序进行安装。
1. 安装应用程序。
1. 应用程序将安装在设备的主屏幕上。
1. 打开应用程序，浏览一下，然后查看页面是否可脱机使用。

## 详细选项{#detailed-options}

下节提供了在[配置站点以进行PWA时可用选项的详细信息。](#enabling-pwa-for-your-site)

### 配置可安装体验{#configure-installable-experience}

这些设置使您的站点像本机应用程序一样运行，它可安装在访客的主屏幕上并可脱机使用。

* **启用PWA**  — 这是为站点启用PWA的主要切换。
* **启动URL**  — 这是用户 [加载本](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 地安装的应用程序时，应用程序将打开的首选开始URL。
   * 这可以是内容结构中的任何路径。
   * 这不必是根，通常是应用程序的专用欢迎页。
   * 如果此URL为相对URL，则使用清单URL作为基本URL进行解析。
   * 如果留空，该功能将使用we App从中安装的网页地址。
   * 建议设置值。
* **显示模式**  — 支持PWA的应用程序仍是通过浏览器提供的AEM站点。[这些显](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 示选项定义如何隐藏浏览器或以其他方式向本地设备上的用户显示浏览器。
   * **独立**  — 浏览器对用户完全隐藏，而且它显示为本机应用程序。这是默认值。
      * 使用此选项，应用程序导航必须在不使用浏览器的导航控件的情况下，使用站点页面上的链接和组件完全通过您的内容实现。
   * **浏览器**  — 浏览器与访问站点时的正常情况相同。
   * **最低UI**  — 浏览器大多是隐藏的，就像本机应用程序一样，但基本的导航控件会公开。
   * **全屏**  — 浏览器与本机应用程序一样完全隐藏，但以全屏模式呈现。
      * 使用此选项，应用程序导航必须在不使用浏览器的导航控件的情况下，使用站点页面上的链接和组件完全通过您的内容实现。
* **屏幕方向**  — 作为本地应用程序，PWA需要知道如何处理设 [备方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **任意**  — 应用程序会根据用户设备的方向进行调整。这是默认值。
   * **纵向**  — 这会强制应用程序以纵向布局打开，而不管用户设备的方向如何。
   * **横向**  — 这会强制应用程序以横向布局打开，而不管用户设备的方向。
* **主题颜色**  — 定义应用 [程序的颜](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 色，该颜色会影响本地用户操作系统显示本机UI工具栏和导航控件的方式。它可能会影响其他应用程序演示文稿元素，具体取决于浏览器。
   * 使用“颜色井”弹出框选择颜色。
   * 颜色也可以由十六进制或RGB值定义。
* **背景颜色**  — 定义应 [用程序的背景颜色，](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 当应用程序加载时显示。
   * 使用“颜色井”弹出框选择颜色。
   * 颜色也可以由十六进制或RGB值定义。
   * 某些浏览器[会从应用程序名称、背景颜色和图标自动](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)构建初始屏幕。
* **图标**  — 它定 [义](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 表示用户设备上应用程序的图标。
   * 图标必须是大小为512x512像素的png文件。
   * 图标必须存储在DAM中。](/help/assets/overview.md)[

### 缓存管理（高级）{#offline-configuration}

这些设置使此站点的某些部分脱机可用，并可在访客的设备上本地使用。 这允许控制Web应用程序的缓存以优化网络请求和支持脱机体验。

* **缓存策略和内容刷新频率**  — 此设置定义PWA的缓存模型。
   * **适中** - [此](https://web.dev/stale-while-revalidate/) 设置适用于大多数站点，是默认值。
      * 通过此设置，用户首次查看的内容将从缓存中加载，当用户使用该内容时，将重新验证缓存中的其余内容。
   * **频繁**  — 对于需要快速更新的网站，如拍卖行，情况就是如此。
      * 使用此设置，应用程序将首先通过网络查找最新内容，如果不可用，将回退到本地缓存。
   * **很少**  — 对于几乎是静态的站点，如参考页面。
      * 使用此设置，应用程序将首先在缓存中查找内容，如果不可用，将回退到网络以检索它。
* **文件预缓存**  — 在安装服务worker时和使用它之前，这些托管在AEM上的文件将保存到本地浏览器缓存中。这保证了Web应用程序在脱机时能够完全正常工作。
* **路径包含**  — 截取对已定义路径的网络请求，并根据所配置的缓存策略和内 **容刷新频率返回缓存内容**。
* **缓存排除**  — 无论文件预缓存和路径包含下的设 **置如何，** 这些文 **件将不**&#x200B;会缓存。

>[!TIP]
>
>您的开发人员团队可能在如何设置您的脱机配置方面有宝贵的意见。

## 限制和Recommendations {#limitations-recommendations}

并非所有PWA功能都适用于AEM Sites。 这些是一些显着的局限性。

* 如果用户未使用应用程序，则不会自动同步或更新页面。

Adobe在您实施PWA时还会提出以下建议。

### 最大限度地减少预缓存的资源数。{#minimize-precache}

Adobe建议您限制要预缓存的页数。

* 嵌入库可减少预缓存时要管理的条目数。
* 将图像变量的数量限制为预缓存。

### 在项目脚本和样式表稳定后启用PWA。{#pwa-stabilized}

通过添加一个缓存选择器来传送客户端库，该选择器遵循以下模式`lc-<checksumHash>-lc`。 每次组成库的文件（和依赖项）中的一个发生更改时，此选择器都会发生更改。 如果列出了要由service-worker预缓存的客户端库，并且您想引用新版本，则可以手动检索并更新该条目。 因此，我们建议您在项目脚本和样式表稳定后将站点配置为PWA。

### 最大限度地减少图像变化的数量。{#minimize-variations}

AEM核心组件的图像组件可确定要获取的最佳再现的前端之一。 此机制还包括与该资源的上次修改时间对应的时间戳。 此机制使PWA预缓存的配置变得复杂。

配置预缓存时，用户需要列表所有可获取的路径变量。 这些变化由质量和宽度等参数组成。 强烈建议将这些变量的数量减少到最多3个 — 小、中、大。 可以通过[图像组件的content-policy对话框执行此操作。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

如果配置不当，内存和网络消耗会严重影响PWA的性能。 此外，如果您打算预缓存（例如50张图像），并且每张图像的宽度为3，则维护站点的用户必须在页面属性的“PWA预缓存”部分中保留多达150个条目的列表。

Adobe还建议您在项目使用图像稳定后将站点配置为PWA。
