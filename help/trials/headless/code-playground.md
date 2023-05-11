---
title: 在简单的应用程序中呈现您的内容
description: 用 CodePen 示例应用程序和 JavaScript 版 AEM Headless 客户端探索从您的试用环境获取 JSON 内容。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1949ee211b4f816e05aa779deb9e287347f006ad
workflow-type: ht
source-wordcount: '987'
ht-degree: 100%

---


# 在简单的应用程序中呈现您的内容 {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="在简单的应用程序中呈现您的内容"
>abstract="用 CodePen 示例应用程序和 JavaScript 版 AEM Headless 客户端探索从您的试用环境获取 JSON 内容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="启动示例 CodePen 应用程序"
>abstract="本指南演练从您的试用环境查询 JSON 数据并将其传入一个基本的 JavaScript Web 应用程序。我们将使用您在早先学习模块中建模并创建的内容片段，因此请先阅读那些指南，然后再进入本指南。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在此模块中，您学习了如何使用适用于 JavaScript 的 AEM Headless Client，通过 GraphQL 持久查询从您的试用环境中获取 JSON 数据。<br><br>现在，您了解了如何使用此客户端来使用您自己的 Web 应用程序中的数据。"
>abstract=""

## CodePen {#codepen}

CodePen 是用于前端 Web 开发的在线代码编辑器和活动天地。它允许您在浏览器中编写 HTML、CSS 和 JavaScript 代码，并且几乎可以立即看到您的工作结果。您还可以保存您的工作并与他人分享。我们在 CodePen 中创建了一个应用程序，您可以使用[适用于 JavaScript 的 AEM Headless 客户端](https://github.com/adobe/aem-headless-client-js)从试用环境中获取 JSON 数据。您可以按原样使用此应用程序，或将其分叉到您自己的 CodePen 帐户中以进一步自定义。

点击试用版中的&#x200B;**启动示例 CodePen 应用程序**&#x200B;按钮，您将会进入 CodePen 中的应用程序。该应用程序用作使用 JavaScript 获取 JSON 数据的最小示例。该示例应用程序旨在渲染返回的任何 JSON 内容，而不管底层内容片段模型的结构如何。开箱即用，该应用程序将从您的试用环境中包含的`aem-demo-assets`持久查询中获取数据。您应该会看到类似于以下内容的 JSON 响应：

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp",
          "title": "Bali Surf Camp",
          "price": "$5000 USD",
          ...
```

如果您看到错误，请查看浏览器控制台以获取更多详细信息或通过[ Slack ](https://adobe-dx-support.slack.com)进行联系。

现在您对 CodePen 有了一些了解，接下来您将会配置该应用程序，以从您在上一个模块中创建的持久查询中获取数据。

## JavaScript 代码演练 {#code-walkthrough}

CodePen 右侧的 **JS** 窗格包含示例应用程序的 Javascript。从第 2 行开始，我们从 Skypack CDN 导入适用于 JavaScript 的 AEM Headless Client。Skypack 用于在没有构建步骤的情况下加快开发，但您也可以在自己的项目中将 AEM Headless Client 与 NPM 或 Yarn 结合使用。查看[自述文件](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript)中的使用说明，了解更多详细信息。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第 6 行上，我们从 `publishHost` 查询参数中读取您的发布主机详细信息。这是 AEM Headless Client 将从中提取数据的主机。该过程通常会编码到您的应用程序中，但我们使用查询参数来使 CodePen 应用程序能够在不同的环境中更轻松地运行。

我们在第 12 行配置 AEM Headless 客户端：

```javascript
const aemHeadlessClient = new AdobeAemHeadlessClientJs({
  // Use a proxy to avoid CORS issues
  serviceURL: 'https://102588-505tanocelot.adobeioruntime.net/api/v1/web/aem/proxy',
  headers: {
    'aem-url': publishHost
  }
});
```

>[!NOTE]
>
>该&#x200B;**服务网址**&#x200B;已设置为使用代理 Adobe IO 运行时功能来避免 CORS 问题。您自己的项目不一定得采用相同配置，但必须为 CodePen 应用程序执行此操作，以便其可在您的试用环境中工作。代理函数已配置为使用查询参数中提供的 **publishHost** 值。

最后，使用函数 `fetchJsonFromGraphQL()` 在 AEM Headless 客户端中执行提取请求。每次更改代码时都会调用该函数，也可以通过点击&#x200B;**“重新提取”**&#x200B;链接来触发它。实际的 `aemHeadlessClient.runPersistedQuery(..)` 调用是在第 34 行上执行的。稍后，我们将更改此 JSON 数据的呈现方式，但现在我们只需使用 `resultToPreTag(queryResult)` 函数将其输出到 `#output` div。

## 从持久查询中提取数据 {#use-persisted-query}

在第 25 行上，我们指出了应用程序应从中提取数据的 GraphQL 持久查询。该持久查询的名称是一个组合，依次包含端点名称（即`your-project` 或 `aem-demo-assets`）、正斜杠和查询名称。如果您完全按照前面的模块说明进行操作，您创建的持久查询将会位于 `your-project` 端点。

1. 更新 `persistedQueryName` 变量以使用您在上一个模块中创建的持久查询。如果您遵循命名建议，则将在 `your-project` 端点中创建一个名为 `adventure-list` 的持久查询，并将 `persistedQueryName` 变量设置为 `your-project/adventure-list`：

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. 做出此更改后，应用程序将自动刷新，并将来自持久查询的原始 JSON 响应输出到 `#output` div。如果显示一条错误消息，请在控制台中查看更多详细信息。如果您在此步骤中仍有问题，请通过 [Slack ](https://adobe-dx-support.slack.com)进行联系。

1. 此 JSON 是否包含您的应用程序所需的确切属性？如果没有，请返回[使用 GraphQL API 提取内容](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql)学习指南进行更改。请记住，请在完成后保存并发布您的查询。

## 更改 JSON 渲染 {#change-rendering}

JSON 按原样渲染在 `pre` 标记中，这并不是很有创意。我们可以切换 CodePen，改用 `resultToDom()` 函数来说明如何迭代 JSON 响应，创建更有趣的结果。

1. 要进行此更改，请注释掉第 37 行并删除第 40 行中的注释：

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. 此函数还会将包含在 JSON 响应中的所有图像渲染为 `img` 标记。如果您创建的&#x200B;**冒险**&#x200B;内容片段不包含任何图像，则可以通过修改第 25 行来尝试切换为使用 `aem-demo-assets/adventures-all` 持久查询：

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

此查询将产生一个包含图像的 JSON 响应，并且 `resultToDom()` 函数将以内联方式渲染其中图像。

![adventures-all 查询和 resultToDom 渲染函数的结果](assets/do-not-localize/adventures-all-query-result.png)

现在您已经完成了构建模型和查询的工作，您的内容团队可以轻松接手。我们将在下一个模块中展示内容创作流程。
