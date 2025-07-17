---
title: HTML5 forms服务代理
description: HTML5 forms Service Proxy是用于注册提交服务的代理的配置。 要配置服务代理，请通过请求参数submissionServiceProxy指定提交服务的URL。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 1%

---

# HTML5 forms服务代理{#html-forms-service-proxy}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5 forms Service Proxy是用于注册提交服务的代理的配置。 要配置服务代理，请通过请求参数&#x200B;*submissionServiceProxy*&#x200B;指定提交服务的URL。

## Service Proxy的优势 {#benefits-of-service-proxy-br}

服务代理消除了以下情况：

* HTML5 forms workflow要求为HTML5 forms用户打开提交服务“/content/xfaforms/submission/default”。 它向更广泛的意外受众公开AEM服务器。
* 服务URL将嵌入到表单的运行时模型中。 无法更改服务URL路径。
* 提交分为两步。 要提交表单数据，提交至少需要两次历程才能到达服务器。 因此，会增加服务器的负载。
* HTML5 forms在POST请求中发送数据，而不是PDF请求。 对于同时包含PDF和HTML5表单的工作流，需要使用两种不同的方法处理提交。

### 拓扑 {#topologies-br}

HTML5 forms可以使用以下拓扑连接到AEM服务器。

* AEM Server或HTML5表单通过POST将数据发送到服务器的拓扑。
* 代理服务器向服务器发送POST数据的拓扑。

![HTML5 forms服务代理拓扑](assets/topology.png)

HTML5 forms服务代理拓扑

HTML5 forms连接到AEM服务器以运行服务器端脚本、Web服务和提交。 HTML5表单的XFA运行时使用对“/bin/xfaforms/submitaction”端点的Ajax调用和各种参数连接到AEM服务器。 HTML5 forms连接AEM服务器以执行以下操作：

#### 执行服务器端脚本和Web服务 {#execute-server-sided-scripts-and-web-services}

标记为在服务器上运行的脚本称为服务器端脚本。 下表列出了服务器端脚本和Web服务中使用的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>活动</p> </td>
   <td><p>活动包含触发请求的事件。 例如，单击、退出或更改</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom包含执行事件的对象的SOM表达式。</p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>模板包含用于呈现表单的模板。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot包含用于呈现表单的模板根目录。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>数据包含用于呈现表单的bata字节。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom包含JSON格式的HTML5表单的DOM。</p> </td>
  </tr>
  <tr>
   <td><p>数据包</p> </td>
   <td><p>数据包被指定为表单。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir包含用于呈现表单的调试目录。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交数据 {#submit-data}

单击“提交”按钮时，HTML5 Forms会将数据发送到服务器。 下表列出了HTML5 Forms发送到服务器的所有参数。

<table>
 <tbody>
  <tr>
   <td><p><strong>参数</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>模板</p> </td>
   <td><p>用于呈现表单的模板。</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>用于呈现表单的模板根目录。</p> </td>
  </tr>
  <tr>
   <td><p>数据</p> </td>
   <td><p>用于呈现表单的bata字节。</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>HTML5表单的DOM（JSON格式）。</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>发布数据XML的URL。</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>用于呈现表单的调试目录。</p> </td>
  </tr>
 </tbody>
</table>

#### 提交代理的工作方式 {#how-nbsp-the-nbsp-submit-proxy-works}

如果请求参数中不存在提交URL，则提交服务代理将充当传递。 它充当传递函数。 它将请求发送到/bin/xfaforms/submitaction终结点，并将响应发送到XFA运行时。

如果submiturl出现在请求参数中，则提交服务代理会选择拓扑。

* 如果AEM服务器发布数据，则代理服务将充当传递服务器。 它将请求发送到/bin/xfaforms/submitaction终结点，并将响应发送到XFA运行时。
* 如果代理发布数据，则代理服务会将submitUrl以外的所有参数传递到&#x200B;*/bin/xfaforms/submitaction*&#x200B;终结点，并在响应流中接收xml字节。 然后，代理服务将数据xml字节发布到submitUrl进行处理。

* 在将数据（POST请求）发送到服务器之前，HTML5表单会验证服务器的连接性和可用性。 为了验证连接和可用性，HTML表单向服务器发送一个空的head请求。 如果服务器可用，HTML5表单会向服务器发送数据（POST请求）。 如果服务器不可用，则显示错误消息&#x200B;*无法连接到服务器*。 该预先检测可以防止用户重新填写表单的麻烦。 代理servlet处理head请求并且不会引发异常。
