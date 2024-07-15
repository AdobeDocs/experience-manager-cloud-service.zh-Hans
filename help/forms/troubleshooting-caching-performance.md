---
title: 如何解决AEM Formsas a Cloud Service中与缓存相关的问题？
description: 解决AEM Forms的缓存相关问题as a Cloud Service。
contentOwner: khsingh
feature: Adaptive Forms
role: User
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---

# 缓存性能 {#caching-performance}

在Cloud Service环境中配置或使用自适应Forms缓存时，您可能会遇到以下一些问题：

## 某些包含图像或视频的自适应Forms不会从Dispatcher缓存中自动失效 {#images-videos-not-invalidated}

您可以从资产浏览器中选择图像或视频并将其添加到自适应表单。 在Assets编辑器中编辑这些图像时，包含这些图像的自适应表单的缓存版本不会失效。 自适应表单继续显示较旧的图像。

要解决此问题，请在发布图像和视频之后，明确取消发布并发布引用这些资源的自适应Forms。

## 某些包含内容片段或体验片段的自适应Forms不会从Dispatcher缓存中自动失效 {#content-fragments-experience-fragments-not-invalidated}

您可以将内容片段或体验片段添加到自适应表单。 独立编辑和发布这些片段时，包含这些片段的自适应表单的缓存版本不会失效。 自适应表单继续显示较旧的片段。

要解决此问题，请在发布更新的内容片段或体验片段后，明确取消发布并发布使用这些资源的自适应Forms。

## 仅缓存自适应Forms的第一个实例 {#only-first-instance-cached}

当自适应表单URL不包含任何本地化信息，并且启用了配置管理器中的使用浏览器区域设置选项时，将会提供自适应表单的本地化版本，并且会根据第一个请求（请求浏览器区域设置）缓存自适应表单的实例并将其交付给每个后续用户。

执行以下步骤来解决问题：

1. 打开您的Experience Manager项目。
1. 打开 `dispatcher/scr/conf.d/rewrites/rewrite.rules` 以供编辑。
1. 打开`conf.d/httpd-dispatcher.conf`或配置为在运行时加载的任何其他配置文件。
1. 将以下代码添加到文件中并进行保存。 它是一个示例代码，可对其进行修改以适合您的环境。

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## CDN缓存会在300秒后停止工作 {#cdn-caching-stops-working-after-300-seconds}

CDN缓存在300秒后停止工作，所有在CDN上缓存的请求都将被重定向到Dispatcher。

要解决此问题，请将页面标题设置为0：

1. 在`src\conf.d\available_vhosts`处创建文件

1. 将以下内容添加到文件以设置age标头

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. 保存并关闭该文件。
1. 修改`src\conf.d\enabled_vhosts\default.vhost`的软链接以指向新文件。
