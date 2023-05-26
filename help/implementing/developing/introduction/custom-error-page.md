---
title: 自定义错误页面
description: AEM提供了用于处理HTTP错误的标准错误处理程序，该处理程序可以自定义。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: b20d40a9f5f4bda51c67cda1164d0c4d74943aa1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 自定义错误页面 {#customizing-error-pages}

AEM附带了用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![标准错误消息](assets/error-message-standard.png)

为了响应错误，AEM提供了 `404.jsp` 下的脚本 `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>由于AEM基于Apache Sling，因此提供了更多信息 [（在Apache错误处理文档中）。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在创作实例上， [CQ WCM调试过滤器](/help/implementing/deploying/configuring-osgi.md) 默认情况下处于启用状态。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪进行响应。
>
>在发布实例上，CQ WCM调试过滤器为 **始终** 已禁用（即使配置为已启用）。

## 如何自定义错误处理程序显示的页面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以开发自己的脚本，以自定义遇到错误时错误处理程序显示的页面。 为此，您将利用 [AEM标准叠加机制](/help/implementing/developing/introduction/overlays.md) 以使您的自定义页面创建在 `/apps` 和覆盖下的默认页面 `/libs`.

1. 在存储库中，复制默认脚本：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   默认情况下，目标路径不存在，因此，在首次执行该操作时，您需要创建该路径。

1. 导航到 `/apps/sling/servlet/errorhandler`。在此，您可以：

   * 编辑相应的现有脚本以提供所需的信息。 或者
   * 为所需代码创建和编辑新脚本。

1. 保存更改并进行测试。

>[!CAUTION]
>
>此 `404.jsp` 脚本专门设计用于满足AEM身份验证；特别是允许在出现这些错误时进行系统登录。
>
>因此，应谨慎替换此脚本。

### 自定义对HTTP 500错误的响应 {#customizing-the-response-to-http-errors}

HTTP [500内部服务器错误](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 表示服务器端错误，例如服务器遇到阻止其完成请求的意外情况。

当请求处理导致异常时，Apache Sling框架(AEM基于此框架构建)：

* 记录异常
* 并在响应正文中返回：
   * HTTP响应代码500
   * 异常栈栈跟踪

按 [自定义错误处理程序显示的页面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可创建脚本。 但是，它仅在以下情况下使用 `HttpServletResponse.sendError(500)` 显式执行；即从异常捕获器中执行。

否则，响应代码将设置为500，但 `500.jsp` 脚本未执行。

要处理500个错误，错误处理程序脚本的文件名必须与exception类（或超类）相同。 要处理所有此类例外，您可以创建一个脚本 `/apps/sling/servlet/errorhandler/Throwable.jsp` 或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>在AEM as aCloud Service中，当从后端收到5XX错误时，CDN会提供一个通用错误页。 要允许后端的实际响应通过，您需要将以下标头添加到响应： `x-aem-error-pass: true`.
>这仅适用于来自AEM或Apache/Dispatcher层的响应。 来自中间基础结构层的其他意外错误仍会显示通用错误页面。

>[!CAUTION]
>
>在创作实例上， [CQ WCM调试过滤器](/help/implementing/deploying/configuring-osgi.md) 默认情况下处于启用状态。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪进行响应。
>
>对于自定义错误处理程序，需要代码为500的响应，因此 [需要禁用CQ WCM调试过滤器。](/help/implementing/deploying/configuring-osgi.md) 这样可确保返回响应代码500，这反过来会触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试过滤器为 **始终** 已禁用（即使配置为已启用）。
