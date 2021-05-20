---
title: 自定义错误页
description: AEM附带一个用于处理HTTP错误的标准错误处理程序，该处理程序可进行自定义。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# 自定义错误页{#customizing-error-pages}

AEM附带用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![标准错误消息](assets/error-message-standard.png)

为响应错误，AEM在`/libs/sling/servlet/errorhandler`下提供了`404.jsp`脚本。

>[!TIP]
>
>由于AEM基于Apache Sling，因此在Apache错误处理文档中，[提供了更多信息。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在创作实例上，默认启用[CQ WCM调试过滤器](/help/implementing/deploying/configuring-osgi.md)。 这始终会导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应进行响应。
>
>在发布实例上，CQ WCM调试过滤器&#x200B;**始终**&#x200B;处于禁用状态（即使配置为启用）。

## 如何自定义错误处理程序{#how-to-customize-pages-shown-by-the-error-handler}显示的页面

您可以开发自己的脚本，以在遇到错误时自定义错误处理程序显示的页面。 为此，您将利用[AEM标准叠加机制](/help/implementing/developing/introduction/overlays.md)，以便在`/apps`下创建自定义页面，并叠加`/libs`下的默认页面。

1. 在存储库中，复制默认脚本：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 到 `/apps/sling/servlet/errorhandler/`

   默认情况下，目标路径不存在，因此您需要在首次执行此操作时创建该路径。

1. 导航至 `/apps/sling/servlet/errorhandler`. 在此，您可以：

   * 编辑相应的现有脚本以提供所需的信息。 或者
   * 创建和编辑所需代码的新脚本。

1. 保存更改并测试。

>[!CAUTION]
>
>`404.jsp`脚本专门设计为满足AEM身份验证的要求；特别是，允许在出现这些错误时进行系统登录。
>
>因此，应当非常谨慎地替换此脚本。

### 自定义对HTTP 500错误的响应{#customizing-the-response-to-http-errors}

HTTP [500内部服务器错误](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)表示服务器端错误，例如服务器遇到意外情况，导致其无法执行请求。

当请求处理导致异常时，Apache Sling框架(基于其构建的AEM):

* 记录异常
* 和在响应正文中返回：
   * HTTP响应代码500
   * 异常堆栈跟踪

通过[自定义错误处理程序](#how-to-customize-pages-shown-by-the-error-handler)显示的页面，可以创建`500.jsp`脚本。 但是，仅当显式执行`HttpServletResponse.sendError(500)`时，才使用此选项；例如从例外捕手那里。

否则，响应代码将设置为500，但不执行`500.jsp`脚本。

要处理500错误，错误处理程序脚本的文件名必须与异常类（或超类）相同。 要处理所有此类例外，可以创建脚本`/apps/sling/servlet/errorhandler/Throwable.jsp`或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在创作实例上，默认启用[CQ WCM调试过滤器](/help/implementing/deploying/configuring-osgi.md)。 这始终会导致响应代码为200。 默认错误处理程序通过将整个堆栈跟踪写入响应进行响应。
>
>对于自定义错误处理程序，需要代码为500的响应 — 因此需要禁用[CQ WCM调试筛选器。](/help/implementing/deploying/configuring-osgi.md) 这可确保返回响应代码500，这反过来又触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试过滤器&#x200B;**始终**&#x200B;处于禁用状态（即使配置为启用）。
