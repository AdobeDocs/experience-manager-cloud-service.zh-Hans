---
title: Screens as a Cloud Service 常见问题
description: 此页面介绍了 Screens as a Cloud Service 常见问题。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: ht
source-wordcount: '450'
ht-degree: 100%

---

# Screens as a Cloud Service 常见问题 {#screens-cloud-faqs}

以下部分提供了与 Screens as a Cloud Service 项目相关的常见问题 (FAQ) 的答案。

## 如果指向 Screens as a Cloud Service 的 AEM Screens 播放器未选取 /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 格式的自定义 clientlib，我该怎么办？

AEM as a Cloud Service 在每次部署时都更改长缓存键。AEM Screens 在修改内容时而非在 Cloud Manager 运行部署时生成离线缓存。清单中的这些长缓存键无效，因此播放器未能下载 *clientlib*。

在 `clientlib` 文件夹中使用 `longCacheKey="none"` 将删除 *clientlib* 的全部长缓存键。


## 如果离线清单未按预期包含所有资源，我该怎么办？ {#offline-manifest}

使用 **bulk-offline-update-screens-service** 服务用户生成离线缓存。`bulk-offline-update-screens-service` 无法访问的某些路径导致离线清单中缺少内容。

在您的代码（即 `ui.config or ui.apps`）中，在配置文件夹中创建具有以下内容的 OSGi 配置，并将文件名标题设为 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 建议使用哪些图像格式在 AEM Screens as a Cloud Service 渠道中无缝地呈现图像？{#screens-cloud-image-format}

Adobe 建议在 AEM Screens as a Cloud Service 渠道中使用 `.png` 和 `.jpeg` 格式的图像以获得最佳的数字标牌体验。
在 AEM Screens as a Cloud Service 中不支持 `*.tif` 格式（标签图像文件格式）的图像。如果渠道具有这种格式的图像，则在播放器端不呈现该图像。

## 如果处于开发人员模式（在线）的渠道不在 AEM Screens 播放器上呈现，我该怎么办？{#screens-cloud-online-channel-blank-iframe}

Adobe 建议您使用 AEM Screens 缓存功能。但是，如果您必须在开发人员模式下运行渠道并且 AEM Screens 播放器显示空白屏幕，请检查播放器的开发人员工具并查找 `X-Frame-Options` 或 `frame-ancestors` 错误。解决方案是配置 Dispatcher 以允许内容在 iFrame 中运行。以下配置一般起作用：

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## 注册码限制的用途是什么？

作为最佳实践，您可以限制注册码的使用。如果注册码已泄露，但注册次数上限为 100，则攻击者最多只能注册这个次数，而不能注册更多。在创建注册码且已注册部分客户播放器后，始终能够更新使用限制。如果客户发现特定注册代码的异常注册活动，他们可以在调查时实时降低限制。如果是误报，则他们可提高回该数字，而不影响已注册的播放器。
