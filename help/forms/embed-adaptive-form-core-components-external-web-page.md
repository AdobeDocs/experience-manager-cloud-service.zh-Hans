---
title: 如何将自适应表单嵌入到外部网页中？
description: 了解将自适应表单嵌入到外部网页中
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 198f6f76-1134-4818-89a0-6ddc84ff956c
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 98%

---

# 将基于核心组件的自适应表单嵌入到外部网页 {#embed-adaptive-form-in-external-web-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | 本文 |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html) |


可[将自适应表单嵌入到 AEM Sites 页面](/help/forms/embed-adaptive-form-aem-sites.md)或托管在 AEM 之外的网页中。嵌入的自适应表单功能齐全，用户无需离开页面即可填写并提交表单。它帮助用户留在网页上其他元素的上下文中，并同时与该表单交互。

## 前提条件 {#prerequisites}

在将自适应表单嵌入到外部网站之前，请执行以下步骤：

* 发布要嵌入到 AEM Forms 服务器的发布实例的自适应表单。
* 在您的网站上创建或标识一个网页以托管该自适应表单。确保该网页可[从 CDN 读取 jQuery 文件](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)或嵌入了 jQuery 的本地副本。渲染自适应表单需要 jQuery。
* 当 AEM 服务器与该网页不在相同域中时，执行在[使 AEM Forms 可将自适应表单提供给跨域站点](#cross-site)部分中列出的步骤。

## 嵌入自适应表单 {#embed-adaptive-form}

通过在网页中插入几行 JavaScript 即可嵌入自适应表单。这段代码中的 API 将一个 HTTP 请求发送到自适应表单资源的 AEM 服务器，然后将该自适应表单注入到指定的表单容器中。

要嵌入自适应表单，请执行以下操作：

1. 用以下代码在您的网站上创建一个网页：

   ```html
        <!doctype html>
        <html>
          <head>
            <title>This is the title of the webpage!</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
          </head>
          <body>
          <div class="customafsection"/>
            <p>This section is replaced with the adaptive form.</p>
   
         <script>
         var options = {path:"/content/forms/af/myadaptiveform.html", CSS_Selector:".customafsection"};
         alert(options.path);
         var loadAdaptiveForm = function(options){
         //alert(options.path);
            if(options.path) {
                // options.path refers to the path of the adaptive form
                // For Example: /content/forms/af/ABC, where ABC is the adaptive form
                // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
                var path = options.path;
                $.ajax({
                    url  : path ,
                    type : "GET",
                    data : {
                        // wcmmode=disabled is only required for author instance
                        // wcmmode : "disabled"
                    },
                    async: false,
                    success: function (data) {
                        // If jquery is loaded, set the inner html of the container
                        // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not        evaluate the script tag in HTML as per the HTML5 spec
                        // For example: document.getElementById().innerHTML
                        if(window.$ && options.CSS_Selector){
                            // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the        script tag.
                            $(options.CSS_Selector).html(data);
                        }
                    },
                    error: function (data) {
                        // any error handler
                    }
                });
            } else {
                if (typeof(console) !== "undefined") {
                    console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
                }
            }
         }(options);
   
         </script>
          </body>
        </html>
   ```

1. 在嵌入的代码中：

   * 将 *options.path* 变量的值更改为该自适应表单的发布 URL 的路径。如果 AEM 服务器在某个上下文路径上运行，请确保该 URL 包含该上下文路径。始终提及该自适应表单的完整名称（包括扩展名）。例如，上述代码和自适应表单驻留在同一 AEM Forms 服务器上，因此，该示例使用自适应表单的上下文路径 /content/forms/af/locbasic.html。
   * CSS_Selector 是将自适应表单嵌入到其中的表单容器的 CSS 选择器。例如，.customafsection css 类是上面示例中的 CSS 选择器。

自适应表单嵌入到网页中。在嵌入的自适应表单中观察以下各项：

* 可在 Forms Portal 的“草稿”和“提交”选项卡中找到草稿和提交的表单。
* 在原始自适应表单上配置的提交操作保留在嵌入的表单中。
* 自适应表单规则保留在嵌入的表单中并功能齐全。
* 在原始自适应表单中配置的体验定位和 A/B 测试在嵌入的表单中不起作用。
* 如果在原始表单上配置了 Adobe Analytics，则将分析数据捕获到 Adobe Analytics 服务器中。但是，在表单分析报告中找不到这些数据。
* 在基于核心组件的自适应表单中包括客户端库 (ClientLibs)，并与表单的页眉和页脚组件一起加载它们。因此，当您将某个基于核心组件的自适应表单嵌入到网页时，它始终包括表单的页眉和页脚。

## 示例拓扑 {#sample-topology}

嵌入自适应表单的外部网页将请求发送到 AEM 服务器，该服务器通常位于专用网络中的防火墙后面。为了确保将请求安全地定向到 AEM 服务器，建议设置反向代理服务器。

让我们看一个如何无需 Dispatcher 即可设置 Apache 2.4 反向代理服务器的示例。在此示例中，您将使用 `/forms` 上下文路径托管 AEM 服务器，并为该反向代理映射 `/forms`。这样确保将 Apache 服务器上对 `/forms` 的任何请求都定向到 AEM 实例。此拓扑有助于减少 Dispatcher 层的规则数量，因为所有前缀为 `/forms` 的请求都路由到 AEM 服务器。

1. 打开 `httpd.conf` 配置文件，并将下面几行代码解除注释。或者，还可在该文件中添加这几行代码。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通过在 `httpd-proxy.conf` 配置文件中添加以下代码行而设置代理规则。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   将 `[AEM_Instance]` 替换为规则中的 AEM 服务器发布 URL。

如果不将 AEM 服务器挂载到某个上下文路径，则 Apache 层的代理规则将如下所示：

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>如果设置了任何其他拓扑，请确保将提交、预填充和其他 URL 添加到 Dispatcher 层的允许列表。

## 最佳实践 {#best-practices}

将自适应表单嵌入到网页中时，请考虑遵循以下最佳实践：

* 确保在网页 CSS 中定义的样式规则不与表单对象 CSS 发生冲突。要避免发生冲突，可使用 AEM 客户端库在自适应表单主题中重用网页 CSS。有关在自适应表单主题中使用客户端库的信息，请参阅 [AEM Forms 中的主题](/help/forms/using-themes-in-core-components.md)。
* 让该网页中的表单容器使用整个窗口宽度。这样确保为移动设备配置的 CSS 规则不作任何更改地正常工作。如果表单容器不占用整个窗口宽度，则需要编写自定义 CSS 以使表单适应不同的移动设备。
* 使用 `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API 获取客户端中表单数据的 XML 或 JSON 表示形式。
* 使用 `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API 从 HTML DOM 卸载该自适应表单。
* 设置从 AEM 服务器发送响应时的 access-control-origin 标头。

## 使 AEM Forms 可将自适应表单提供给跨域站点 {#cross-site}

1. 在 AEM 发布实例上，转到 `https://'[server]:[port]'/system/console/configMgr` 上的 AEM Web 控制台配置管理器。
1. 找到并打开 **Apache Sling 反向链接过滤器**&#x200B;配置。
1. 在“允许的主机”字段中，指定该网页所在的域。这样使主机可向 AEM 服务器发出 POST 请求。还可使用正则表达式指定一系列外部应用程序域。

<!--

>[!MORELIKETHIS]
>
>* [Embed adaptive form based on core components to AEM sites](/help/forms/embed-adaptive-form-core-components-aem-sites.md)

-->