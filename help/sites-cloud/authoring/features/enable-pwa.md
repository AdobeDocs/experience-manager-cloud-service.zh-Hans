---
title: 启用渐进式Web应用程序功能
description: AEM Sites允许内容作者通过简单的配置而不是编码，向任何站点提供渐进式Web应用程序功能。
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 071eefa3b6f5e9636ace612e968b6a9627c98550
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# 启用渐进式Web应用程序功能{#enabling-pwa}

通过简单的配置，内容作者现在可以为在AEM Sites创建的体验启用渐进式Web应用程序(PWA)功能。

>[!CAUTION]
>
>这是一项高级功能，它需要：
>
>* PWA知识
>* 了解您的站点和内容结构
>* 了解缓存策略
>* 开发团队的支持

>
>
建议您在使用此功能之前与开发团队讨论此功能，以定义将其用于您的项目的最佳方式。

## 简介 {#introduction}

[渐进式Web应用程序(PWA](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) )允许AEM站点在本地存储在用户的机器上并脱机访问，从而为它们提供令人痴迷的类似应用程序的体验。即使失去Internet连接，用户也可以在外出时浏览站点。 PWA提供无缝体验，即使网络丢失或不稳定。

内容作者无需对站点进行任何重新编码，而是可以将PWA属性配置为站点[页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)中的附加选项卡。

* 保存或发布时，此配置会触发一个事件处理程序，该处理程序会写出[清单文件](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服务工作者](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)，它们在站点上启用PWA功能。
* 清单和服务工作者存储在适用于站点的[上下文感知配置](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html)中。 还维护了sling映射，以确保从应用程序的根服务服务工作者，以启用代理内容，从而允许应用程序内的脱机功能。

通过PWA，用户可以获得站点的本地副本，即使没有Internet连接，也能提供类似于应用程序的体验。

>[!NOTE]
>
>渐进式Web应用程序是一种不断发展的技术，支持本地应用程序安装，其他功能[取决于您使用的浏览器。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## 前提条件 {#prerequisites}

为了能够对您的站点使用PWA功能，您的项目环境有两个要求：

1. [调整组](#adjust-components) 件以启用此功能
1. [调整调](#adjust-dispatcher) 度程序规则以显示所需文件

这些是作者需要与开发团队协调的技术步骤。 每个站点只需执行一次这些步骤。

### 调整组件{#adjust-components}

您的组件需要包括支持PWA功能的[清单文件](https://developer.mozilla.org/en-US/docs/Web/Manifest)和[服务工作者](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)。

为此，开发人员需要将以下链接添加到页面组件的`customheaderlibs.html`文件。

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

开发人员还需要将以下链接添加到页面组件的`customfooterlibs.html`文件。

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

>[!NOTE]
>
>[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)的未来版本将自动包含这些功能。 但是，如果您使用自定义组件而不是核心组件，则始终需要进行这些调整。

### 调整调度程序{#adjust-dispatcher}

PWA功能生成并使用`/content/<sitename>/manifest.webmanifest`文件。 默认情况下，[调度程序](/help/implementing/dispatcher/overview.md)不公开此类文件。 要公开这些文件，开发人员必须将以下配置添加到您的站点项目。

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing)的未来版本将包括此配置。

## 为站点启用PWA{#enabling-pwa-for-your-site}

满足[先决条件](#prerequisites)后，内容作者很容易为站点启用PWA功能。 下面是如何进行此操作的基本概述。 各个选项详见[详细选项部分。](#detailed-options)

1. 登录AEM。
1. 在主菜单中，点按或单击&#x200B;**导航** -> **站点**。
1. 选择您的站点项目，然后点按或单击&#x200B;[**属性**](/help/sites-cloud/authoring/fundamentals/page-properties.md)&#x200B;或使用热键`p`。
1. 选择&#x200B;**渐进式Web应用程序**&#x200B;选项卡并配置适用的属性。 您至少要：
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

1. 在支持的[浏览器中访问该站点。](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. 您将在浏览器的地址栏中看到一个`+`图标，表示该站点可以作为本地应用程序进行安装。
   * 根据浏览器的不同，它还可能显示一条通知（如横幅或对话框），指明可以作为本地应用程序进行安装。
1. 安装应用程序。
1. 应用程序将安装在设备的主屏幕上。
1. 打开应用程序，浏览一下，看看页面是否可脱机使用。

## 详细选项{#detailed-options}

下节提供了[配置站点以进行PWA时可用选项的详细信息。](#enabling-pwa-for-your-site)

### 配置可安装体验{#configure-installable-experience}

这些设置使您的站点像本机应用程序一样运行，它可安装在访客的主屏幕上并可脱机使用。

* **启用PWA** -这是为站点启用PWA的主要切换。
* **启动URL**  —— 这是用户 [加载本](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) 地安装的应用程序时，应用程序将打开的首选开始URL。
   * 这可以是内容结构中的任何路径。
   * 这不一定必须是根，并且通常是应用程序的专用欢迎页面。
   * 如果此URL为相对URL，则清单URL将用作解析该URL的基本URL。
   * 如果留空，该功能将使用wer应用程序从中安装的网页的地址。
   * 建议设置值。
* **显示模式** -支持PWA的应用程序仍是通过浏览器提供的AEM站点。[这些显](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) 示选项定义如何隐藏浏览器，或在本地设备上以其他方式向用户显示浏览器。
   * **独立** -浏览器对用户完全隐藏，而且它看起来像本机应用程序。这是默认值。
      * 使用此选项，应用程序导航必须完全可以通过您的内容进行，无需使用浏览器的导航控件，即可在站点页面上使用链接和组件。
   * **浏览器** -浏览器在访问站点时的显示方式与通常相同。
   * **最低UI**  —— 浏览器大多是隐藏的，如本机应用程序，但基本的导航控件会公开。
   * **全屏** -浏览器与本机应用程序一样完全隐藏，但以全屏模式呈现。
      * 使用此选项，应用程序导航必须完全可以通过您的内容进行，无需使用浏览器的导航控件，即可在站点页面上使用链接和组件。
* **屏幕方向** -作为本地应用程序，PWA需要知道如何处理设 [备方向。](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **任何** -应用程序会根据用户设备的方向进行调整。这是默认值。
   * **纵向** -这会强制应用程序以纵向布局打开，而不管用户设备的方向如何。
   * **横向** -这会强制应用程序以横向布局打开，而不管用户设备的方向如何。
* **主题颜色** -定义应用 [程序的](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) 颜色，该颜色会影响本地用户操作系统显示本机UI工具栏和导航控件的方式。它可能会影响其他应用程序演示文稿元素，具体取决于浏览器。
   * 使用颜色井弹出窗口选择颜色。
   * 颜色也可以由十六进制或RGB值定义。
* **背景颜色** -定义应 [用程序的背](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) 景颜色，当应用程序加载时显示。
   * 使用颜色井弹出窗口选择颜色。
   * 颜色也可以由十六进制或RGB值定义。
   * 某些浏览器[会从应用程序名称、背景颜色和图标自动](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens)构建初始屏幕。
* **图标** -它定 [义](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) 表示用户设备上的应用程序的图标。
   * 该图标必须是大小为512x512像素的png文件。
   * 图标必须存储在DAM中。](/help/assets/overview.md)[

### 缓存管理（高级）{#offline-configuration}

这些设置使此站点的某些部分脱机可用，并可在访客的设备上本地使用。 这允许控制Web应用程序的缓存以优化网络请求和支持脱机体验。

* **缓存策略和内容刷新频率** -此设置定义PWA的缓存模型。
   * **适中** - [此](https://web.dev/stale-while-revalidate/) 设置适用于大多数站点，是默认值。
      * 通过此设置，用户首次查看的内容将从缓存中加载，当用户使用该内容时，将重新验证缓存中的其余内容。
   * **频繁** -对于需要快速更新的网站，如拍卖行，情况就是这样。
      * 使用此设置，应用程序将首先通过网络查找最新内容，如果不可用，将返回到本地缓存。
   * **很少** -对于几乎为静态的站点，如引用页面，情况是如此。
      * 使用此设置，应用程序将首先在缓存中查找内容，如果不可用，将返回网络进行检索。
* **文件预缓存** -在安装服务工作者时和使用服务工作者之前，托管在AEM上的这些文件将保存到本地浏览器缓存中。这保证了Web应用程序在脱机时能够完全正常工作。
* **路径包含** -截取已定义路径的网络请求，并根据配置的缓存策略和内容刷 **新频率返回缓存内容**。
* **缓存排除** -无论文件预缓存和路径包含下的设置如何， **这些文件** 都不 **会进**&#x200B;行缓存。

>[!TIP]
>
>您的开发人员团队可能在如何设置脱机配置方面有宝贵意见。

## 限制 {#limitations}

并非所有PWA功能都适用于AEM Sites。 这些是一些明显的限制。

* 用户必须至少浏览页面一次，才能将其脱机缓存。
* 如果用户未使用应用程序，则不会自动同步或更新页面。
