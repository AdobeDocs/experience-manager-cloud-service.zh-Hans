---
title: 将自适应表单嵌入到外部网页中
description: 了解如何将自适应表单嵌入到外部网页中
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
source-git-commit: 6d0e3ee08862030e9eb7d068b251d13bc3e8e08f
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 2%

---


# 将基于核心组件的自适应表单嵌入到外部网页 {#embed-adaptive-form-in-external-web-page}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | 本文 |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html) |


您可以 [在AEM Sites页面中嵌入自适应表单](/help/forms/embed-adaptive-form-aem-sites.md) 或托管在AEM外部的网页。 嵌入式自适应表单功能齐全，用户无需离开页面即可填写和提交表单。 它有助于用户停留在网页上其他元素的上下文中，同时与表单交互。

## 前提条件 {#prerequisites}

将自适应表单嵌入到外部网站之前，请执行以下步骤

* 发布要嵌入到AEM Forms服务器发布实例的自适应表单。
* 在您的网站上创建或识别要托管自适应表单的网页。 确保网页可以 [从CDN读取jQuery文件](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 或嵌入了jQuery的本地副本。 呈现自适应表单需要jQuery。
* 当AEM服务器和网页位于不同的域时，请执行部分中列出的步骤， [启用AEM Forms以向跨域站点提供自适应表单](#cross-site).

## 嵌入自适应表单 {#embed-adaptive-form}

通过在网页中插入几行JavaScript，可以嵌入自适应表单。 代码中的API向AEM服务器发送获取自适应表单资源的HTTP请求，并将自适应表单注入指定的表单容器中。

嵌入自适应表单：

1. 使用以下代码在您的网站上创建网页：

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

1. 在嵌入代码中：

   * 更改的值 *选项路径* 变量填充自适应表单的发布URL的路径。 如果AEM服务器在上下文路径上运行，请确保URL包含上下文路径。 始终提及自适应表单的完整名称，包括扩展。   例如，上述代码和自适应表单位于同一AEM表单服务器上，因此该示例使用自适应表单/content/forms/af/locbasic.html的上下文路径。
   * CSS_Selector是嵌入了自适应表单的表单容器的CSS选择器。 例如，.customafsection css类是上述示例中的CSS选择器。

自适应表单将嵌入到网页中。 在嵌入的自适应表单中观察以下情况：

* 草稿和已提交的表单可在Forms门户的草稿和提交选项卡中获取。
* 在原始自适应表单上配置的提交操作将保留在嵌入表单中。
* 自适应表单规则会保留，并在嵌入表单中充分发挥作用。
* 在原始自适应表单中配置的体验定位和A/B测试在嵌入表单中不起作用。
* 如果在原始表单上配置了Adobe Analytics，则Adobe Analytics服务器会捕获Analytics数据。 但是，它在Forms Analytics报表中不可用。
* 在基于核心组件的自适应Forms中，包含客户端库(ClientLibs)并与表单的页眉和页脚组件一起加载。 因此，在嵌入基于核心组件的自适应Forms到网页时，它始终包括表单的页眉和页脚。

## 示例拓扑 {#sample-topology}

嵌入自适应表单的外部网页将请求发送到AEM服务器，该服务器通常位于专用网络的防火墙之后。 为确保请求安全定向到AEM服务器，建议设置反向代理服务器。

让我们看一个示例，如何在不使用Dispatcher的情况下设置Apache 2.4反向代理服务器。 AEM在此示例中，您将使用 `/forms` 上下文路径和映射 `/forms` 用于反向代理。 它确保任何请求 `/forms` Apache Server上的代码被定向到AEM实例。 此拓扑有助于减少Dispatcher层中的规则数量，因为所有请求都以为前缀 `/forms` 路由到AEM服务器。

1. 打开 `httpd.conf` 配置文件并取消注释以下代码行。 或者，您可以在文件中添加这些代码行。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 通过将下面几行代码添加到 `httpd-proxy.conf` 配置文件。

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   替换 `[AEM_Instance]` 将AEM服务器发布URL添加到规则中。

如果您没有在上下文路径上装载AEM服务器，则Apache层的代理规则将如下所示：

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
>列入允许列表如果设置了任何其他拓扑，请确保将提交、预填充和其他URL添加到Dispatcher层的。

## 最佳实践 {#best-practices}

在网页中嵌入自适应表单时，请考虑以下最佳实践：

* 确保在网页CSS中定义的样式规则不会与表单对象CSS冲突。 要避免冲突，您可以使用AEM客户端库在自适应表单主题中重用网页CSS。 有关在自适应表单主题中使用客户端库的信息，请参阅 [AEM Forms中的主题](/help/forms/using-themes-in-core-components.md).
* 使网页中的表单容器使用整个窗口宽度。 这可确保为移动设备配置的CSS规则在没有任何更改的情况下正常工作。 如果表单容器未采用整个窗口宽度，则需要编写自定义CSS以使表单适应不同的移动设备。
* 使用 `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` 用于在客户端获取表单数据的XML或JSON表示形式的API。
* 使用 `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` 用于从HTMLDOM卸载自适应表单的API。
* 设置从AEM服务器发送响应时的访问控制源标头。

## 启用AEM Forms以向跨域站点提供自适应表单 {#cross-site}

1. 在AEM发布实例上，转到位于的AEM Web控制台配置管理器 `https://'[server]:[port]'/system/console/configMgr`.
1. 找到并打开 **Apache Sling引用过滤器** 配置。
1. 在允许的主机字段中，指定网页所在的域。 它使主机能够向AEM服务器发出POST请求。 还可以使用正则表达式指定一系列外部应用程序域。



