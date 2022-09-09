---
title: 缓存性能疑难解答
seo-title: Troubleshooting caching performance
description: 缓存性能疑难解答
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 缓存性能 {#caching-performance}

在Cloud Service环境中配置或使用自适应Forms缓存时，您可能会遇到以下一些问题：

## 某些包含图像或视频的自适应Forms不会从Dispatcher缓存中自动失效 {#images-videos-not-invalidated}

您可以从资产浏览器中选择图像或视频并将其添加到自适应表单。 在资产编辑器中编辑这些图像时，包含此类图像的自适应表单的缓存版本不会失效。 自适应表单会继续显示旧图像。

要解决此问题，请在发布图像和视频后，明确地取消发布和发布引用这些资产的自适应Forms。

## 某些包含内容片段或体验片段的自适应Forms不会从Dispatcher缓存中自动失效 {#content-fragments-experience-fragments-not-invalidated}

您可以将内容片段或体验片段添加到自适应表单。 独立编辑和发布这些片段时，包含此类片段的自适应表单的缓存版本不会失效。 自适应表单会继续显示旧片段。

要解决此问题，请在发布更新的内容片段或体验片段后，明确地取消发布和发布使用这些资产的自适应Forms。

## 仅缓存自适应Forms的第一个实例 {#only-first-instance-cached}

当自适应表单URL不包含任何本地化信息，并且启用了配置管理器中的“使用浏览器区域设置”选项时，将提供自适应表单的本地化版本，并根据第一个请求（请求的浏览器区域设置）缓存自适应表单的实例，并将其交付给每个后续用户。

执行以下步骤以解决问题：

1. 打开您的Experience Manager项目。
1. 打开 `dispatcher/scr/conf.d/rewrites/rewrite.rules` 进行编辑。
1. 打开 `conf.d/httpd-dispatcher.conf` 或配置为在运行时加载的任何其他配置文件。
1. 将以下代码添加到文件中并进行保存。 它是一个代码示例，可根据您的环境对其进行修改。

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN缓存在300秒后停止工作 {#cdn-caching-stops-working-after-300-seconds}

CDN缓存在300秒后停止工作，所有在CDN上缓存的请求都将被重定向到Dispatcher。

要解决此问题，请将页面标题设置为0:

1. 在 `src\conf.d\available_vhosts`

1. 将以下内容添加到文件中以设置页面标题

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. 保存并关闭文件。
1. 修改软链接 `src\conf.d\enabled_vhosts\default.vhost` 指向新文件。
