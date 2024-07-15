---
title: 配置CDN错误页面
description: 了解如何覆盖默认错误页面，其中将静态文件托管在自托管存储(如Amazon S3或Azure Blob Storage)中，并在使用Cloud Manager配置管道部署的配置文件中引用它们。
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 5%

---

# 配置CDN错误页面 {#cdn-error-pages}

万一[Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)无法访问AEM源服务器（这种情况不太可能发生），默认情况下，CDN会提供一个非品牌的一般错误页，指示无法访问服务器。 您可以覆盖默认错误页，方法是：将静态文件托管在自托管存储中(如Amazon S3或Azure Blob Storage)，然后在使用[Cloud Manager配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)部署的配置文件中引用它们。

## 设置 {#setup}

在覆盖默认错误页之前，您需要执行以下操作：

* 在Git项目的顶级文件夹中创建此文件夹和文件结构：

```
config/
     cdn.yaml
```

* `cdn.yaml`配置文件应同时包含元数据和以下示例中描述的规则。 `kind`参数应设置为`CDN`，版本应设置为架构版本，当前版本为`1`。

* 在Cloud Manager中创建目标部署配置管道。 请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

**注释**

* RDE当前不支持配置管道。
* 您可以使用 `yq` 在本地验证配置文件（例如 `yq cdn.yaml`）的 YAML 格式。

### 配置 {#configuration}

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
