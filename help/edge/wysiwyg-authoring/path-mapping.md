---
title: Edge Delivery Services 的路径映射
description: 了解如何将 AEM 创作实例上使用的页面路径映射到网站上使用的公共页面路径，并控制将哪些内容发布到 Edge Delivery Services。
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
source-git-commit: 01966d837391d13577956a733c2ee7dc02f88103
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 100%

---

# Edge Delivery Services 的路径映射 {#path-mapping}

了解如何将 AEM 创作实例上使用的页面路径映射到网站上使用的公共页面路径，并控制将哪些内容发布到 Edge Delivery Services。

## 概述 {#overview}

为了能够使用 AEM 创作所见即所得的内容并将其发布到 Edge Delivery Services，您必须设置项目的路径映射。这种映射有两个目的。

* 它映射并创建 AEM 创作实例上使用的页面路径与您网站上使用的公共页面路径之间的关系。
* 它控制哪些内容（页面、工作表、资产等）发布到 Edge Delivery Services。


必须根据项目的内容和 URL 结构为每个项目单独配置路径映射。AEM 在内容发布期间以及在 [通用编辑器中编辑内容时会使用它。](/help/sites-cloud/authoring/universal-editor/navigation.md)

## 配置格式 {#configuration-format}

路径映射配置的格式包含两个部分（`mappings` 和 `includes`），类似于以下示例。

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

 `mappings` 配置包含内部路径（在 AEM 创作实例上）和外部 URL 路径（在公共网站上）的数组。

格式为 `<internal paths>:<external path>`. 它通常至少包含两个条目。

1. 示例中的第一个条目是网站页面的路径映射。
1. 第二个条目控制 `.helix/config.json` 到 AEM 创作存储库中相应电子表格页面的映射。

在此示例中，存储在`/content/aem-boilerplate/...`下的所有页面都将在直接位于`https://main--my-site--org.aem.live/....`下的 Edge Delivery Services 网站上公开访问。

>[!TIP]
>
>所有以电子表格形式管理的表格数据（例如元数据、重定向和分类法）通常作为 `.json` API URL 在 Edge Delivery Services 上发布。为此，必须在映射配置中单独列出它们。
>
>请参阅文档 [使用电子表格管理表格数据](/help/edge/wysiwyg-authoring/tabular-data.md) 了解更多信息。

### 包括 {#includes}

 `includes` 配置控制哪些内容路径实际复制到 Edge Delivery Services。它还可以保存任何路径数组，并且通常包含网站的顶级根页面。

Edge Delivery Services 页面上使用的资产通常与网页一起发布。它们将自动从 AEM 创作实例导出到 Edge Delivery Services。

>[!TIP]
>
>如果您有一个用例，希望将资产直接发布到 Edge Delivery Services（例如，您希望图像或 PDF 可通过页面上下文之外的 URL 直接访问），则您还必须将 DAM 路径添加到配置的`includes`部分。
>
>例如，如果包含一组 PDF 的资产根文件夹（如 `/content/dam/my-site/documents`）应通过`/assets/...`公开访问，则必须在配置的 `includes` 部分添加一个条目。

## 如何配置 {#how-to-configure}

根据您的项目设置，您可以用两种方式之一来配置路径映射。

1. 如果项目配置为 `aem.live` 并使用 [配置服务](https://www.aem.live/docs/config-service-setup) 对于集中配置，每个网站的路径映射都通过此配置服务进行配置。

   * 下面是配置路径映射的 cURL 请求示例。

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
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

1. 如果项目不使用配置服务，则路径映射通过 `paths.json` 项目 GitHub 存储库中的文件。

   * 看[`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json)举个例子。

在这两种情况下，一旦配置了路径映射，就可以通过可公开访问的配置 URL 检查配置 `https://<branch>--<site>--<org>.aem.page/config.json`。
