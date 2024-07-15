---
title: SPA和服务器端渲染
description: 在SPA中使用服务器端渲染(SSR)可以加快页面的初始加载，然后将进一步的渲染传递给客户端。
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 0%

---

# SPA和服务器端渲染{#spa-and-server-side-rendering}

单页应用程序(SPA)可以为用户提供丰富的动态体验，该体验会以熟悉的方式反应和行为，通常就像本机应用程序一样。 [此功能是通过依赖客户端先加载内容然后执行处理用户交互的重任务来实现的](introduction.md#how-does-a-spa-work)。 此过程可最大限度地减少客户端和服务器之间所需的通信量，从而使应用程序更加被动地工作。

但是，此过程可能会导致初始加载时间较长，尤其是当SPA较大且内容丰富时。 为了优化加载时间，可以在服务器端渲染某些内容。 使用服务器端渲染(SSR)可以加速页面的初始加载，然后将进一步的渲染传递给客户端。

## 何时使用SSR {#when-to-use-ssr}

并非所有项目都需要SSR。 尽管AEM完全支持用于SPA的JS SSR，但Adobe建议不要为每个项目系统地实施它。

在决定实施SSR时，您必须首先估计增加SSR对于项目（包括长期维护）实际上意味着什么额外的复杂性、工作量和成本。 只有在增加值明显超过估计成本时，才应选择SSR架构。

SSR通常在以下任一问题明确为“是”时提供一些值：

* **SEO：**&#x200B;您的网站是否仍需要SSR才能由带来流量的搜索引擎正确编制索引？ 请记住，主搜索引擎爬虫现在评估JS。
* **页面速度：** SSR是否可以在实际环境中提供可衡量的速度提升，并增加总体用户体验？

只有在以下两个问题中至少有一个问题得到明确的“是”回答时，Adobe才会建议实施SSR。 以下部分介绍了如何使用[App Builder](https://developer.adobe.com/app-builder)中的Adobe I/O Runtime实现此目的。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您[确信您的项目需要实施SSR](#when-to-use-ssr)，则Adobe推荐的解决方案是使用Adobe I/O Runtime。

有关Adobe I/O Runtime的更多信息，请参阅以下内容：

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) — 有关App Builder运行时功能的概述
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) — 以了解有关完整App Builder产品的详细信息
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) — 有关详细文档

以下部分详细介绍如何使用Adobe I/O Runtime在两种不同的模型中为SPA实施SSR：

* [AEM驱动的通信流](#aem-driven-communication-flow)
* [Adobe I/O Runtime驱动的通信流](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建议为每个环境（暂存、生产、测试等）使用一个单独的Adobe I/O Runtime工作区。 这样做允许典型的系统开发生命周期(SDLC)模式与部署到不同环境的单个应用程序的不同版本。 有关详细信息，请参阅App Builder应用程序的[CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/)。
>
>每个实例（创作、发布）不需要单独的工作区，除非每个实例类型的运行时实施存在差异。

>[!NOTE]
>
>Cloud Manager不支持部署到Adobe I/O Runtime。 因此，必须设置您自己的基础架构，以便将SSR代码部署到Adobe I/O Runtime。

## 远程渲染器配置 {#remote-content-renderer-configuration}

AEM必须知道可在何处检索远程渲染的内容。 无论您选择为SSR实施哪种[模型，](#adobe-i-o-runtime)都必须向AEM指定如何访问此远程渲染服务。

此服务通过&#x200B;**RemoteContentRenderer - Configuration Factory OSGi服务**&#x200B;完成。 在`http://<host>:<port>/system/console/configMgr`处的Web控制台配置控制台中搜索字符串“RemoteContentRenderer”。

![渲染器配置](assets/renderer-configuration.png)

以下字段可用于配置：

* **内容路径模式** — 匹配部分内容的正则表达式（如有必要）
* **远程终结点URL** — 负责生成内容的终结点的URL
   * 如果不在本地网络中，请使用安全的HTTPS协议。
* **其他请求标头** — 要添加到发送到远程端点的请求的其他标头
   * 模式： `key=value`
* **请求超时** — 远程主机请求超时（以毫秒为单位）

>[!NOTE]
>
>无论您选择实施[AEM驱动的通信流](#aem-driven-communication-flow)还是[Adobe I/O Runtime驱动的通信流](#adobe-i-o-runtime-driven-communication-flow)，都必须定义远程内容渲染器配置。

>[!NOTE]
>
>此配置使用[远程内容渲染器](#remote-content-renderer)，它具有其他扩展和自定义选项。

## AEM驱动的通信流 {#aem-driven-communication-flow}

使用SSR时，AEM中SPA的[组件交互工作流](introduction.md#interaction-with-the-spa-editor)包含在Adobe I/O Runtime上生成应用程序初始内容的阶段。

1. 浏览器从AEM请求SSR内容。
1. AEM将模型发布到Adobe I/O Runtime。
1. Adobe I/O Runtime返回生成的内容。
1. AEM通过后端页面组件的HTL模板为Adobe I/O Runtime返回的HTML提供服务。

![SSE CMS驱动的AEMAdobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驱动的通信流 {#adobe-i-o-runtime-driven-communication-flow}

上一部分介绍了有关AEM中的SPA的服务器端渲染的标准实施和推荐实施，AEM在该环境中执行内容引导和提供。

或者，可以实现SSR，以便Adobe I/O Runtime负责引导，有效地反转通信流。

这两种模型均有效，并受AEM支持。 但是，在实施特定模型之前，应该考虑每个模型的优缺点。

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>通过AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM可根据需要管理注入库</li>
     <li>仅在AEM上维护资源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>可能不熟悉SPA开发人员<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>通过Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA开发人员更熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>应用程序所需的Clientlib资源(如CSS和JavaScript)必须由AEM开发人员通过<code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code>属性<br />提供 </li>
     <li>必须在AEM和Adobe I/O Runtime<br />之间同步资源 </li>
     <li>要启用SPA创作，可能需要Adobe I/O Runtime的代理服务器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 规划SSR {#planning-for-ssr}

通常，只有应用程序的一部分必须在服务器端渲染。 常见的示例是在页面初始加载时显示在折叠上方的内容在服务器端呈现。 此过程通过向客户端交付已渲染的内容来节省时间。 当用户与SPA交互时，其他内容由客户端渲染。

在考虑为SPA实施服务器端渲染时，请查看应用程序的哪些部分有必要。

## 使用SSR开发SPA {#developing-an-spa-using-ssr}

SPA组件可由客户端（在浏览器中）或服务器端渲染。 在渲染服务器端时，不存在浏览器属性，例如窗口大小和位置。 因此，SPA组件应该是同构的，并且不对其呈现的位置做出任何假设。

要使用SSR，您必须在AEM和Adobe I/O Runtime上部署代码，后者负责服务器端渲染。 大多数代码是相同的，但特定于服务器的任务有所不同。

## AEM中适用于SPA的SSR {#ssr-for-spas-in-aem}

AEM中适用于SPA的SSR需要使用Adobe I/O Runtime，应用程序内容服务器端渲染会调用此函数。 在应用程序的HTL中，调用Adobe I/O Runtime上的资源来渲染内容。

正如AEM支持开箱即用的Angular和React SPA框架一样，Angular和React应用程序也支持服务器端渲染。 有关更多详细信息，请参阅两个框架的NPM文档。

## 远程内容渲染器 {#remote-content-renderer}

在AEM中将SSR与SPA一起使用所需的[远程内容渲染器配置](#remote-content-renderer-configuration)将引入更为通用的渲染服务，可以根据您的需求对其进行扩展和自定义。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService`用于检索在远程服务器上呈现的内容(例如从Adobe I/O呈现的内容)的OSGi服务。发送到远程服务器的内容基于传递的请求参数。

`RemoteContentRenderingService`可以通过依赖关系反转插入到自定义Sling模型或servlet中，当需要额外的内容操作时。

此服务由[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet)在内部使用。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet`用于以编程方式设置请求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`是提供的默认请求处理程序实现，允许您创建多个OSGi配置，以便可以将内容结构中的位置映射到远程端点。

要添加自定义请求处理程序，请实现`RemoteContentRendererRequestHandler`接口。 请确保将`Constants.SERVICE_RANKING`组件属性设置为大于100的整数，即`DefaultRemoteContentRendererRequestHandlerImpl`的排名。

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置默认处理程序的OSGi配置 {#configure-default-handler}

默认处理程序的配置必须按照[远程内容渲染器配置](#remote-content-renderer-configuration)一节中的说明进行配置。

### 远程内容渲染器使用情况 {#usage}

执行servlet获取并返回一些插入到页面中的内容：

1. 确保您的远程服务器可访问。
1. 向AEM组件的HTL模板中添加以下代码片段之一。
1. （可选）创建或修改OSGi配置。
1. 浏览网站内容

通常，页面组件的HTL模板是此类功能的主要接收者。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

servlet使用Sling模型导出器序列化组件数据。 默认情况下，`com.adobe.cq.export.json.ContainerExporter`和`com.adobe.cq.export.json.ComponentExporter`都支持作为Sling模型适配器。 如有必要，您可以添加请求应调整为使用`RemoteContentRendererServlet`并实现`RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`的类。 附加类必须扩展`ComponentExporter`。
