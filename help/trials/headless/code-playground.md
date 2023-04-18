---
title: 使用 JavaScript 获取 JSON 内容
description: 探索使用 CodePen 应用程序和适用于 JavaScript 的 AEM Headless Client 从您的试用环境中获取 JSON 内容。
hidefromtoc: true
index: false
source-git-commit: 3aff5ef2fb9ecdd815f0bc1a813d3a3982b4e0ed
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 17%

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

您可以从CodePen应用程序开始，该应用程序是使用获取JSON数据的最小示例 [AEM Headless Client for JavaScript](https://github.com/adobe/aem-headless-client-js). 示例应用程序旨在呈现返回的任何JSON内容，而不考虑基础内容片段模型的结构。 CodePen应用程序会尝试使用冗余设置，但遇到任何错误，因此您可能会看到以下错误消息，这些消息会打印到应用程序的底部窗格：

```
{
  "status": "Failed to fetch persisted query: your-project/USE-YOUR-QUERY-HERE from publishHost: https://publish-p00000-e12345.adobeaemcloud.com",
  "message": "[AEMHeadless:REQUEST_ERROR] General Request error: Failed to fetch."
}
```

出现此错误是正常的，因为应用程序尚未配置为使用您在上一模块中保存并发布的持久查询。 在以下步骤中，您将配置应用程序以从特定查询中获取数据。

## CodePen演练 {#code-walkthrough}

CodePen上的JS(Javascript)窗格包含示例应用程序的大脑。 从第2行开始，我们从Skypack CDN导入AEM Headless Client for JavaScript。 Skypack用于促进开发而无需构建步骤，但您也可以在自己的项目中将AEM Headless Client与NPM或Hayr一起使用。 请查看 [自述文件](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript) 以了解更多详情。

```
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第6行，我们从 `publishHost` 查询参数。 这是AEM Headless Client将从中获取数据的主机。 这通常会编码到您的应用程序中，但我们使用查询参数来简化CodePen应用程序处理不同环境的过程。

我们在第12行上配置AEM无头客户端，以使用代理AdobeIO运行时函数来避免CORS问题。 这并非您自己的项目所必需，而是CodePen应用程序与试用环境结合使用所必需的。 代理函数配置为使用 `publishHost` 查询参数中提供的值。

```
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

最后，对函数进行了分析 `fetchJsonFromGraphQL()` 用于使用AEM Headless Client执行获取请求。 每次更改代码时都会调用该函数，或者可以通过按“Refetch”链接来触发该函数。 实际 `aemHeadlessClient.runPersistedQuery(..)` 34号线发生呼叫。 稍后，我们将更改此JSON数据的呈现方式，但现在，我们只会将其打印到 `#output` 使用div `resultToPreTag(queryResult)` 函数。

## 从保留查询中获取数据 {#use-persisted-query}

在第25行，我们指示应用程序应从中获取数据的GraphQL持久查询。 持久查询名称是项目名称(即， `your-project`)，后跟正斜杠，然后是查询的名称。

更新 `persistedQueryName` 变量来使用您在上一模块中创建的持久查询。 如果您完全遵循命名建议，则会创建一个名为的持久查询 `adventures` 在 `your-project` 项目，然后您 `persistedQueryName` 变量 `your-project/adventures`:

```
//
// TODO: Use your persisted query here
//
persistedQueryName = 'your-project/adventures';
```

进行此更改后，应用程序应自动刷新，并将来自保留查询的原始JSON响应打印到 `#output` div. 如果您看到错误消息，请检查控制台以了解更多详细信息。

此JSON是否包含您的应用程序所需的确切属性？ 如果没有，请返回到AEM创作环境、工具、GraphQL查询编辑器(或导航到 `/aem/graphiql.html` 路径)，并对保留的查询进行更改。 完成查询后，请不要忘记保存并发布该查询。

## 更改JSON渲染 {#change-rendering}

当前，JSON将按原样呈现到 `pre` 标记，这不是很有创意。 我们可以切换CodePen以使用 `resultToDom()` 函数，以说明如何迭代JSON响应以创建更有趣的结果。

要进行此更改，请注释第37行，并从第40行中删除注释：

```
// Output the results to a pre tag
//resultToPreTag(queryResult);

// Alternatively, build a colorful div structure with the JSON results and render images inline
resultToDom(queryResult);
```

此函数还会将JSON响应中包含的任何图像作为 `img` 标记。 如果您创建的“冒险”内容片段不包含任何图像，则可以尝试切换为使用 `aem-demo-assets/adventures-all` 通过修改行25持久查询：

```
persistedQueryName = 'aem-demo-assets/adventures-all';
```

此查询将生成包含图像的JSON响应，并且 `resultToDom()` 函数会将它们呈现在内联。

![adventures-all查询和resultToDom渲染函数的结果](assets/do-not-localize/adventures-all-query-result.png)
