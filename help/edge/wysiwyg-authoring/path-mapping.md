---
title: Edge Delivery Services的路径映射
description: 了解如何将AEM创作实例中使用的页面路径映射到网站中使用的公共页面路径，并控制将哪些内容发布到Edge Delivery Services。
feature: Edge Delivery Services
role: User
source-git-commit: 2727744f276ee5facae718a987dcc6dc54d4e917
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Edge Delivery Services的路径映射 {#path-mapping}

了解如何将AEM创作实例中使用的页面路径映射到网站中使用的公共页面路径，并控制将哪些内容发布到Edge Delivery Services。

## 概述 {#overview}

要使用AEM创作WYSIWYG内容并将其发布到Edge Delivery Services，您必须设置项目的路径映射。 此映射有两个用途。

* 它映射并创建在AEM创作实例中使用的页面路径与网站上使用的公共页面路径之间的关系。
* 它控制哪些内容（页面、工作表、资产等） 发布到Edge Delivery Services。

必须根据项目的内容和URL结构，为每个项目分别配置路径映射。 AEM在内容发布期间以及在[通用编辑器](/help/sites-cloud/authoring/universal-editor/navigation.md)中编辑内容时使用该编辑器。

## 配置格式 {#configuration-format}

路径映射配置的格式包含两个类似于以下示例的部分（`mappings`和`includes`）。

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### 映射 {#mappings}

`mappings`配置包含内部路径(在AEM创作实例上)和外部URL路径（在公共网站上）的数组。

格式为`<internal paths>:<external path>`。 它通常至少包含两个条目。

1. 示例中的第一个条目是网站页面的路径映射。
1. 第二个条目控制`.helix/config.json`到AEM创作存储库中相应电子表格页面的映射。

在此示例中，存储在`/content/aem-boilerplate/...`下的所有页面将可以在Edge Delivery Services站点的`https://main--my-site--org.aem.live/....`下直接公开访问。

>[!TIP]
>
>作为电子表格管理的所有表格式数据（例如元数据、重定向和分类）通常作为Edge Delivery Services上的`.json` API URL发布。 要实现此目的，必须在映射配置中单独列出这些实例。
>
>有关详细信息，请参阅文档[使用电子表格管理表格式数据](/help/edge/wysiwyg-authoring/tabular-data.md)。

### 包含 {#includes}

`includes`配置控制哪些内容路径实际复制到Edge Delivery Services。 它还可保存任意路径数组，通常包含站点顶级根页面。

Edge Delivery Services页面上使用的Assets通常与网页一起发布。 它们将自动从AEM创作实例导出到Edge Delivery Services。

>[!TIP]
>
>如果您有希望将资源直接发布到Edge Delivery Services的用例(例如，希望图像或PDF在页面上下文之外的URL直接访问它们)，则还必须将DAM路径添加到配置的`includes`部分。
>
>例如，如果包含一组PDF的资源根文件夹（如`/content/dam/my-site/documents`）应通过`/assets/...`公开访问，则必须将一个条目添加到配置的`includes`部分。

## 如何配置 {#how-to-configure}

根据项目的设置，可以使用以下两种方式之一配置路径映射。

1. 如果项目是为`aem.live`配置的，并且使用[配置服务](https://www.aem.live/docs/config-service-setup)进行集中式配置，则每个站点的路径映射都将通过此配置服务进行配置。

   * 以下是配置路径映射的示例cURL请求。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. 如果项目不使用配置服务，则通过项目GitHub存储库中的`paths.json`文件配置路径映射。

   * 有关示例，请参阅[`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json)。

在这两种情况下，配置路径映射后，您可以通过可公开访问的配置URL `https://<branch>--<site>--<org>.aem.page/config.json`检查配置。
