---
title: 使用 JavaScript 获取 JSON 内容
description: 探索使用 CodePen 应用程序和适用于 JavaScript 的 AEM Headless Client 从您的试用环境中获取 JSON 内容。
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 使用 JavaScript 获取 JSON 内容 {#fetch-json}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="使用 JavaScript 获取 JSON 内容"
>abstract="探索使用 CodePen 应用程序和适用于 JavaScript 的 AEM Headless Client 从您的试用环境中获取 JSON 内容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="启动示例 CodePen 应用程序"
>abstract="我们已经整合了一个小型 CodePen 应用程序，以便介绍如何使用 GraphQL 持久查询从您的试用环境中获取 JSON 数据。<br><br>单击下方按钮启动 CodePen 示例，然后遵循此指南来了解更多。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在此模块中，您学习了如何使用适用于 JavaScript 的 AEM Headless Client，通过 GraphQL 持久查询从您的试用环境中获取 JSON 数据。<br><br>现在，您了解了如何使用此客户端来使用您自己的 Web 应用程序中的数据。"
>abstract=""

## 简介 {#intro}

您可从 CodePen 应用程序开始操作，其为通过[适用于 JavaScript 的 AEM Headless Client](https://github.com/adobe/aem-headless-client-js) 提取 JSON 数据的最简单示例。该示例应用程序旨在渲染返回的任何 JSON 内容，而不管底层内容片段模型的结构如何。CodePen 应用程序尝试详细说明遇到的任何错误，因此您可能会在应用程序的底部窗格中看到以下错误消息：

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

这是一个预期错误，因为应用程序尚未配置为使用您在上一个模块中保存和发布的持久查询。在以下步骤中，将配置该应用程序以从您的特定查询中提取数据。

## CodePen 演练 {#code-walkthrough}

CodePen 上的 JS (Javascript) 窗格包含示例应用程序的重要内容。从第 2 行开始，我们从 Skypack CDN 导入适用于 JavaScript 的 AEM Headless Client。Skypack 用于在没有构建步骤的情况下加快开发，但您也可以在自己的项目中将 AEM Headless Client 与 NPM 或 Yarn 结合使用。查看[自述文件](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript)中的使用说明，了解更多详细信息。

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第 6 行上，我们从 `publishHost` 查询参数中读取您的发布主机详细信息。这是 AEM Headless Client 将从中提取数据的主机。该过程通常会编码到您的应用程序中，但我们使用查询参数来使 CodePen 应用程序能够在不同的环境中更轻松地运行。

我们在第 12 行上将 AEM Headless Client 配置为使用代理 Adobe IO 运行时函数来避免 CORS 问题。您自己的项目不一定得采用相同配置，但必须为 CodePen 应用程序执行此操作，以便其可在您的试用环境中工作。代理函数已配置为使用查询参数中提供的 `publishHost` 值。

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最后，使用函数 `fetchJsonFromGraphQL()` 在 AEM Headless Client 中执行提取请求。每次更改代码时都会调用该函数，也可以通过按“重新提取”链接来触发它。实际的 `aemHeadlessClient.runPersistedQuery(..)` 调用是在第 34 行上执行的。稍后，我们将更改此 JSON 数据的呈现方式，但现在我们只需使用 `resultToPreTag(queryResult)` 函数将其输出到 `#output` div。

## 从持久查询中提取数据 {#use-persisted-query}

在第 25 行上，我们指出了应用程序应从中提取数据的 GraphQL 持久查询。该持久查询的名称是一个组合，依次包含项目名称（即`your-project`）、正斜杠和查询名称。

更新 `persistedQueryName` 变量以使用您在上一个模块中创建的持久查询。如果您完全遵循命名建议，则将在 `your-project` 项目中创建一个名为 `adventures` 的持久查询，并将 `persistedQueryName` 变量设置为 `your-project/adventures`：

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

做出此更改后，应用程序将自动刷新，并将来自持久查询的原始 JSON 响应输出到 `#output` div。如果显示一条错误消息，请在控制台中查看更多详细信息。

此 JSON 是否包含您的应用程序所需的确切属性？如果没有，请返回您的 AEM Author 环境、工具、GraphQL 查询编辑器（或导航至 `/aem/graphiql.html` 路径）并更改您的持久查询。请记住，完成后保存并发布查询。

## 更改 JSON 渲染 {#change-rendering}

目前，JSON 将按原样渲染在 `pre` 标记中，这并不是很有创意。我们可以切换 CodePen，改用 `resultToDom()` 函数来说明如何迭代 JSON 响应，创建更有趣的结果。

要进行此更改，请注释掉第 37 行并删除第 40 行中的注释：

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

此函数还会将包含在 JSON 响应中的所有图像渲染为 `img` 标记。如果您创建的“冒险”内容片段不包含任何图像，则可以通过修改第 25 行来尝试切换为使用 `aem-demo-assets/adventures-all` 持久查询：

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

此查询将产生一个包含图像的 JSON 响应，并且 `resultToDom()` 函数将以内联方式渲染其中图像。

![adventures-all 查询和 resultToDom 渲染函数的结果](assets/do-not-localize/adventures-all-query-result.png)
