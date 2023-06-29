---
title: 在简单的应用程序中呈现您的内容
description: 用 CodePen 示例应用程序和 JavaScript 版 AEM Headless 客户端探索从您的试用环境获取 JSON 内容。
hidefromtoc: true
index: false
exl-id: b7dc70f2-74a2-49f7-ae7e-776eab9845ae
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 55%

---


# 在简单的应用程序中呈现您的内容 {#render-content-simple-app}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript"
>title="在简单的应用程序中呈现您的内容"
>abstract="用 CodePen 示例应用程序和 JavaScript 版 AEM Headless 客户端探索从您的试用环境获取 JSON 内容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide"
>title="启动示例 CodePen 应用程序"
>abstract="本指南演练从您的试用环境查询 JSON 数据并将其传入一个基本的 JavaScript Web 应用程序。您可使用在之前的学习模块中建模并创建的内容片段。 如有必要，请先浏览这些指南，然后再跳转到本指南。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_fetch_json_with_javascript_guide_footer"
>title="在此模块中，您学习了如何使用适用于 JavaScript 的 AEM Headless Client，通过 GraphQL 持久查询从您的试用环境中获取 JSON 数据。<br><br>现在，您了解了如何使用此客户端来使用您自己的 Web 应用程序中的数据。"
>abstract=""

## CodePen {#codepen}

CodePen 是用于前端 Web 开发的在线代码编辑器和活动天地。它可让您在浏览器中编写HTML、CSS和JavaScript代码，并几乎立即查看您的工作结果。 您还可以保存您的工作并与他人分享。Adobe已在CodePen中创建了一个应用程序，您可以使用它从试用环境中提取JSON数据。 [适用于JavaScript的AEM Headless客户端](https://github.com/adobe/aem-headless-client-js). 您可以按原样使用此应用程序，或将其分叉到您自己的 CodePen 帐户中以进一步自定义。

单击 **启动示例代码笔应用程序** 试用版中的按钮会将您转到代码笔中的应用程序。 该应用程序用作使用 JavaScript 获取 JSON 数据的最小示例。该示例应用程序旨在渲染返回的任何 JSON 内容，而不管底层内容片段模型的结构如何。开箱即用的应用程序会从 `aem-demo-assets` 试用环境中包含的持久查询。 您应该会看到类似于以下内容的 JSON 响应：

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

此 **JS** codePen中右侧的窗格包含示例应用程序的JavaScript。 从第2行开始，您可以从Skypack CDN导入AEM Headless Client for JavaScript。 Skypack 用于在没有构建步骤的情况下加快开发，但您也可以在自己的项目中将 AEM Headless Client 与 NPM 或 Yarn 结合使用。查看[自述文件](https://github.com/adobe/aem-headless-client-js#aem-headless-client-for-javascript)中的使用说明，了解更多详细信息。

```javascript
import AdobeAemHeadlessClientJs from 'https://cdn.skypack.dev/@adobe/aem-headless-client-js@v3.2.0';
```

在第6行中，您的发布主机详细信息是从 `publishHost` 查询参数。 此参数是AEM Headless客户端从中提取数据的主机。 此功能通常会被编码到您的应用程序中，但您使用的是查询参数，以便让CodePen应用程序更轻松地与不同环境一起使用。

在第12行配置AEM Headless客户端：

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
>此 **serviceURL** 设置为使用代理Adobe I/O Runtime函数以避免CORS问题。 您自己的项目不需要此代理，但CodePen应用程序需要此代理才能与试用环境配合使用。 代理函数已配置为使用查询参数中提供的 **publishHost** 值。

最后，使用函数 `fetchJsonFromGraphQL()` 在 AEM Headless 客户端中执行提取请求。每次更改代码时都会调用该函数，也可以通过点击&#x200B;**“重新提取”**&#x200B;链接来触发它。实际的 `aemHeadlessClient.runPersistedQuery(..)` 调用是在第 34 行上执行的。稍后，您更改了此JSON数据的呈现方式，但现在，请将其打印到 `#output` div使用 `resultToPreTag(queryResult)` 函数。

## 从持久查询中提取数据 {#use-persisted-query}

在第25行，您可以指示GraphQL从哪个持久化查询应用程序中应获取数据。 持久查询名称是终结点名称(即， `your-project` 或 `aem-demo-assets`)，后跟一个正斜杠，然后是查询的名称。 如果您完全按照前面的模块说明进行操作，则您创建的持久查询位于 `your-project` 端点。

1. 更新 `persistedQueryName` 变量，以使其使用您在上一个模块中创建的持久查询。 如果您遵循命名建议，则将在 `your-project` 端点中创建一个名为 `adventure-list` 的持久查询，并将 `persistedQueryName` 变量设置为 `your-project/adventure-list`：

   ```javascript
   //
   // TODO: Use your persisted query here
   //
   persistedQueryName = 'your-project/adventure-list';
   ```

1. 做出此更改后，应用程序将自动刷新，并将来自持久查询的原始 JSON 响应输出到 `#output` div。如果显示一条错误消息，请在控制台中查看更多详细信息。如果您在此步骤中仍有问题，请通过 [Slack ](https://adobe-dx-support.slack.com)进行联系。

1. 此 JSON 是否包含您的应用程序所需的确切属性？如果没有，请返回[使用 GraphQL API 提取内容](https://experience.adobe.com/experiencemanager/learn/extract_content_using_graphql)学习指南进行更改。请记住，请在完成后保存并发布您的查询。

## 更改 JSON 渲染 {#change-rendering}

JSON按原样渲染到 `pre` 标记时不会太有创意。 您可以切换代码笔以使用 `resultToDom()` 函数，以说明如何迭代JSON响应以创建更有趣的结果。

1. 要进行此更改，请注释掉第 37 行并删除第 40 行中的注释：

   ```javascript
   // Output the results to a pre tag
   //resultToPreTag(queryResult);
   
   // Alternatively, build a colorful div structure with the JSON results and render images inline
   resultToDom(queryResult);
   ```

1. 此函数将JSON响应中包含的任何图像渲染为 `img` 标记之前。 如果您创建的&#x200B;**冒险**&#x200B;内容片段不包含任何图像，则可以通过修改第 25 行来尝试切换为使用 `aem-demo-assets/adventures-all` 持久查询：

   ```javascript
   persistedQueryName = 'aem-demo-assets/adventures-all';
   ```

此查询会生成一个包含图像的JSON响应，并且 `resultToDom()` 函数将它们渲染为内联。

![adventures-all 查询和 resultToDom 渲染函数的结果](assets/do-not-localize/adventures-all-query-result.png)

现在您已完成了构建模型和查询的工作，您的内容团队可以轻松接管。 在下一个模块中，您将展示内容创作流程。
