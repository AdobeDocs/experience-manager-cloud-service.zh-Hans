---
title: SPA和服务器端渲染
description: 在SPA中使用服务器端渲染(SSR)可以加速页面的初始加载，然后将进一步渲染传递给客户端。
translation-type: tm+mt
source-git-commit: 10012f6dc75da0c199dd5452ceef16ec7f29389b
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# SPA和服务器端渲染{#spa-and-server-side-rendering}

单页应用程序(SPA)可以优惠用户丰富的动态体验，这种体验以熟悉的方式反应和行为，通常就像本机应用程序一样。 [这是通过依赖客户端预先加载内容，然后进行处理用户交互的重](introduction.md#how-does-a-spa-work) 力提升，从而最小化客户端和服务器之间需要的通信量，使应用更加被动。

但是，这会导致较长的初始加载时间，尤其是当SPA较大且内容丰富时。 为了优化加载时间，某些内容可在服务器端呈现。 使用服务器端渲染(SSR)可以加速页面的初始加载，然后将进一步的渲染传递给客户端。

## 何时使用SSR {#when-to-use-ssr}

并非所有项目都需要SSR。 尽管AEM完全支持SPA的JS SSR，但Adobe不建议对每个项目系统地实施它。

在决定实施SSR时，您首先必须估计SSR的实际额外复杂度、工作量和成本增加，包括长期维护。 SSR结构只有在增值明显超过估计成本时才能选择。

SSR通常在以下任一问题有明确的“是”时提供一些值：

* **SEO:** SSR是否仍然需要通过带来流量的搜索引擎正确编制网站索引？请记住，主搜索引擎爬网程序现在对JS进行评估。
* **页面速度：** SSR能否在实际环境中提供可衡量的速度改进，并增加整体用户体验？

只有当这两个问题中至少有一个得到明确的“是”回答时，Adobe才建议实施SSR。 以下各节介绍如何使用Adobe I/O Runtime实现此操作。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您[确信您的项目需要实施SSR](#when-to-use-ssr)，则Adobe建议的解决方案是使用Adobe I/O Runtime。

有关Adobe I/O Runtime的更多信息，请参阅

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 有关服务的概述
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 有关该平台的详细文档

以下各节详细介绍了如何使用Adobe I/O Runtime在两种不同的模型中为SPA实现SSR:

* [AEM驱动通信流](#aem-driven-communication-flow)
* [Adobe I/O Runtime驱动的通信流](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建议为每个AEM环境（创作、发布、舞台等）使用一个单独的Adobe I/O Runtime实例。

## 远程渲染器配置{#remote-content-renderer-configuration}

AEM必须知道可在何处检索远程渲染的内容。 无论您选择为SSR实现哪种模式[,](#adobe-i-o-runtime)都需要指定AEM如何访问此远程渲染服务。

这是通过&#x200B;**RemoteContentRenderer - Configuration Factory OSGi服务**&#x200B;完成的。 在位于`http://<host>:<port>/system/console/configMgr`的“Web控制台配置”控制台中搜索字符串“RemoteContentRenderer”。

![渲染器配置](assets/renderer-configuration.png)

以下字段可用于配置：

* **内容路径模式**  — 根据需要，为匹配部分内容而定期表达式
* **远程端点** URL — 负责生成内容的端点的URL
   * 如果不在本地网络中，请使用安全的HTTPS协议。
* **附加请求标头**  — 要添加到发送到远程端点的请求的附加标头
   * 图案：`key=value`
* **请求超时**  — 远程主机请求超时（以毫秒为单位）

>[!NOTE]
>
>无论您选择实现[AEM驱动的通信流](#aem-driven-communication-flow)还是[Adobe I/O Runtime驱动的流，](#adobe-i-o-runtime-driven-communication-flow)都必须定义远程内容呈示器配置。

>[!NOTE]
>
>此配置利用[远程内容渲染器](#remote-content-renderer)，后者具有其他可用的扩展和自定义选项。

## AEM驱动通信流{#aem-driven-communication-flow}

使用SSR时，AEM中的[组件交互工作流](introduction.md#interaction-with-the-spa-editor)包括在Adobe I/O Runtime上生成应用程序初始内容的阶段。

1. 浏览器从AEM请求SSR内容。
1. AEM将模型发布到Adobe I/O Runtime。
1. Adobe I/O Runtime返回生成的内容。
1. AEM通过后端页面组件的HTL模板为Adobe I/O Runtime返回的HTML提供服务。

![SSE CMS驱动的AEMAdobe I/O](assets/ssr-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驱动通信流{#adobe-i-o-runtime-driven-communication-flow}

上一节介绍与AEM中的SPA相关的服务器端渲染的标准和建议实现，在中，AEM执行内容的引导和服务。

或者，SSR可以实现，使Adobe I/O Runtime负责引导，有效地逆转通信流。

两种型号均有效，且受AEM支持。 然而，在实施特定模式之前，应考虑每种模式的优缺点。

<table>
 <tbody>
  <tr>
   <th><strong>引导</strong></th>
   <th><strong>优势</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>通过AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM在需要时管理注入库</li>
     <li>只需在AEM<br />上维护资源 </li>
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
     <li>更熟悉SPA开发人员<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM开发人员需要通过<code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code>属性<br />使应用程序所需的Clientlib资源（如CSS和JavaScript）可用 </li>
     <li>必须在AEM和Adobe I/O Runtime<br />之间同步资源 </li>
     <li>要启用SPA的创作，可能需要Adobe I/O Runtime的代理服务器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR {#planning-for-ssr}的规划

通常，只需要使应用程序的一部分在服务器端呈现。 常见示例是呈现在页面初始加载时折叠上方显示的内容。 这通过交付到客户端（已呈现的内容）来节省时间。 当用户与SPA交互时，其他内容由客户端呈现。

在考虑为SPA实施服务器端渲染时，您需要查看应用程序中需要哪些部分。

## 使用SSR {#developing-an-spa-using-ssr}开发SPA

SPA组件可以由客户端（在浏览器中）或服务器端呈现。 呈现服务器端时，浏览器属性（如窗口大小和位置）不存在。 因此，SPA组件应是同构的，不应假设它们将呈现在何处。

要利用SSR，您需要在AEM以及负责服务器端渲染的Adobe I/O Runtime中部署代码。 大多数代码将相同，但特定于服务器的任务会有所不同。

## AEM {#ssr-for-spas-in-aem}中的SPA的SSR

AEM中的SPA SSR需要Adobe I/O Runtime，用于渲染应用程序内容服务器端。 在应用程序的HTL中，调用Adobe I/O Runtime上的资源来呈现内容。

正如AEM支持Angular和React SPA框架即装即用一样，Angular和React应用程序也支持服务器端渲染。 有关更多详细信息，请参阅这两个框架的NPM文档。

## 远程内容渲染器{#remote-content-renderer}

在AEM中与SPA一起使用SSR时需要的[远程内容渲染器配置](#remote-content-renderer-configuration)可接入更广义的渲染服务，该服务可进行扩展和自定义以满足您的需求。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是用于检索在远程服务器上呈现的内容(如从Adobe I/O)的OSGi服务。发送到远程服务器的内容基于传递的请求参数。

`RemoteContentRenderingService` 当需要进行其他内容处理时，可通过依赖性反转注入自定义Sling模型或servlet。

此服务由[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet)在内部使用。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet`可用于以编程方式设置请求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`提供的默认请求处理程序实现允许您创建多个OSGi配置，以便将内容结构中的位置映射到远程端点。

要添加自定义请求处理程序，请实现`RemoteContentRendererRequestHandler`接口。 请务必将`Constants.SERVICE_RANKING`组件属性设置为大于100的整数，该整数是`DefaultRemoteContentRendererRequestHandlerImpl`的排名。

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置默认处理函数{#configure-default-handler}的OSGi配置

必须按照[远程内容渲染器配置](#remote-content-renderer-configuration)部分中的说明配置默认处理程序。

### 远程内容渲染器使用{#usage}

要使Servlet获取并返回某些可插入页面的内容，请执行以下操作：

1. 确保远程服务器可访问。
1. 将以下代码片段之一添加到AEM组件的HTL模板。
1. （可选）创建或修改OSGi配置。
1. 浏览站点内容

通常，页面组件的HTL模板是此类功能的主要收件人。

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求{#requirements}

Servlet利用Sling Model Exporter来序列化组件数据。 默认情况下，`com.adobe.cq.export.json.ContainerExporter`和`com.adobe.cq.export.json.ComponentExporter`都支持作为Sling Model适配器。 如有必要，您可以添加类，请求应调整为使用`RemoteContentRendererServlet`并实现`RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`。 其他类必须扩展`ComponentExporter`。
