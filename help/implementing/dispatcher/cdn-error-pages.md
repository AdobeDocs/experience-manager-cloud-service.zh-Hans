---
title: 配置CDN错误页面
description: 了解如何覆盖默认错误页面，其中将静态文件托管在自托管存储(如Amazon S3或Azure Blob Storage)中，并在使用Cloud Manager配置管道部署的配置文件中引用它们。
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 137ea509de353f9f800f0b64bb8f2f6375e7d83d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---


# 配置CDN错误页面 {#cdn-error-pages}

万一[Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)无法访问AEM源服务器（这种情况不太可能发生），默认情况下，CDN会提供一个非品牌的一般错误页，指示无法访问服务器。 您可以覆盖默认错误页，方法是：将静态文件托管在自托管存储中(如Amazon S3或Azure Blob Storage)，然后在使用Cloud Manager [配置管道部署的配置文件中引用它们。](/help/operations/config-pipeline.md#managing-in-cloud-manager)

## 设置 {#setup}

在覆盖默认错误页之前，您需要执行以下操作：

1. 创建名为`cdn.yaml`或类似的文件，并引用下面的语法部分。

1. 将文件放置在名为&#x200B;*config*&#x200B;或类似的顶级文件夹下，如[使用配置管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 在Cloud Manager中创建配置管道，如[使用配置管道](/help/operations/config-pipeline.md#managing-in-cloud-manager)中所述。

1. 部署配置。

### 语法 {#syntax}

错误页面作为单页应用程序(SPA)实施，并引用一些属性，如下面的示例所示。  URL引用的静态文件应由您在可访问Internet的服务(如Amazon S3或Azure Blob Storage)上托管。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```
有关数据节点上方属性的说明，请参阅[使用配置管道](/help/operations/config-pipeline.md#common-syntax)。 kind属性值应为&#x200B;*CDN*，`version`属性应设置为&#x200B;*1*。


| 名称 | 允许的属性 | 含义 |
|-----------|--------------------------|-------------|
| **spa** | 标题 | 错误页面的标题。 |
|     | icoUrl | 图标文件的URL。 |
|     | cssUrl | CSS文件的URL。 |
|     | jsUrl | JavaScript文件的URL。 |

### 示例生成的HTML {#sample-generated-html}

由CDN生成并提供给客户端（如浏览器）的HTML代码将类似于以下代码片段（但不完全相同）：

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### 测试 {#testing}

出于测试目的，请使用支持的错误代码调用专用端点，例如：

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

支持的代码为：403、404、406、500和503。

这样，您就可以直接触发CDN的错误处理程序，以测试给定错误代码的综合响应。

### 教程

有关如何创建、部署和测试CDN提供的错误页面的分步说明，请参阅[CDN错误页面](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-error-pages#cdn-error-pages)教程。


