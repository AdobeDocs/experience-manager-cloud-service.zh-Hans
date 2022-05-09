---
title: 为 AEM as a Cloud Service 配置高级联网功能
description: 了解如何为 AEM as a Cloud Service 配置高级联网功能，如 VPN 或者灵活或专用出口 IP 地址
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: 3325a7a0f99c427040e868f9cafc5f9890d97d69
workflow-type: tm+mt
source-wordcount: '2964'
ht-degree: 99%

---

# 为 AEM as a Cloud Service 配置高级联网功能 {#configuring-advanced-networking}

本文意在介绍 AEM as a Cloud Service 中的各种高级联网功能，包括 VPN 的自助预配、非标准端口以及专用出口 IP 地址。

>[!INFO]
>
>您还可以在此[位置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=zh-hans)找到一系列旨在引导您了解各个高级联网选项的文章。

## 概述 {#overview}

AEM as a Cloud Service 提供了多种高级联网功能，客户可以使用 Cloud Manager API 配置这些功能。这些功能包括：

* [灵活端口出口](#flexible-port-egress) - 将 AEM as a Cloud Service 配置为允许从非标准端口传出流量
* [专用出口 IP 地址](#dedicated-egress-IP-address) - 配置从唯一 IP 传出 AEM as a Cloud Service 的流量
* [虚拟专用网络 (VPN)](#vpn) - 面向采用 VPN 技术的客户，保护客户的基础设施与 AEM as a Cloud Service 之间的流量

此文章详细介绍了上述各个选项，包括如何对它们进行配置。作为常规配置策略，在程序级别调用 `/networkInfrastructures` API 端点，以声明所需的高级联网类型，接着调用每个环境的 `/advancedNetworking` 端点，以启用基础设施并配置特定于环境的参数。要了解每个正式语法以及请求和响应示例，请参考 Cloud Manager API 文档中的相应端点。

一个程序可以预配一个高级联网变体。在灵活端口出口和专用出口 IP 地址之间进行选择时，如果无需特定 IP 地址，则建议您选择灵活端口出口，因为 Adobe 可以优化灵活端口出口流量的性能。

>[!INFO]
>
>高级联网对沙盒程序不可用。
>此外，环境必须升级到 AEM 版本 5958 或更高版本。

>[!NOTE]
>
>对于已经预配了旧版专用出口技术的客户，在需要配置这些选项之一时，不应这样操作，否则网站连接可能会受到影响。如需帮助，请与 Adobe 支持部门联系。

## 灵活端口出口 {#flexible-port-egress}

此高级联网功能允许您对 AEM as a Cloud Service 进行配置，通过默认打开的 HTTP（端口 80）和 HTTPS（端口 443）以外的端口来传入流量。

### 注意事项 {#flexible-port-egress-considerations}

如果流量不依赖于专用出口就可以实现较高的吞吐量，因而您不需要 VPN 和专用出口 IP 地址，那么推荐选择灵活端口出口。

### 配置 {#configuring-flexible-port-egress-provision}

每个程序调用一次 POST `/program/<programId>/networkInfrastructures` 端点，只需传递 `kind` 参数和区域的 `flexiblePortEgress` 值。端点使用 `network_id` 以及包括状态在内的其他信息进行响应。要查看完整的参数集和确切的语法，可参阅 API 文档。

在调用后，通常需要大约 15 分钟来预配联网基础设施。对 Cloud Manager 的[网络基础设施 GET 端点](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) 的调用将显示状态“就绪”。

如果整个程序的灵活端口出口配置已就绪，则必须对每个环境调用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点，以在环境级别启用联网，并可以选择声明任何端口转发规则。可以根据各个环境来配置参数以提供灵活性。

对于 80/443 之外的任何端口，均应通过指定目标主机集（名称或 IP 以及端口）来声明端口转发规则。对于每个目标主机，必须将指向的目标端口映射到 30000 到 30999 之间的端口。

API 应在几秒内响应，指示更新的状态，然后在大约 10 分钟后，端点的 `GET` 方法应指示高级联网已启用。

### 更新 {#updating-flexible-port-egress-provision}

程序级别的配置可以通过调用 `PUT /api/program/<program_id>/network/<network_id>` 端点来更新，并将在几分钟内生效。

>[!NOTE]
>
> “kind”参数（`flexiblePortEgress`、`dedicatedEgressIP` 或 `VPN`）无法修改。如需帮助，请联系客户支持，说明已经创建的内容以及进行更改的原因。

每个环境的端口转发规则同样可以通过调用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端点进行更新，确保包括完整的配置参数集而不是其子集。

### 删除或禁用灵活端口出口 {#deleting-disabling-flexible-port-egress-provision}

至 **删除** 程序的网络基础结构，调用 `DELETE /program/{program ID}/ networkinfrastructure/{networkinfrastructureID}`.

要&#x200B;**禁用**&#x200B;特定环境的灵活端口出口，请调用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`。

有关API的更多信息，请参阅 [Cloud Manager API文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### 流量路由 {#flexible-port-egress-traffic-routing}

对于流向 80 或 443 端口以外端口的 http 或 https 流量，应使用以下主机和端口环境变量来配置代理。

* 对于 HTTP：`AEM_PROXY_HOST`/`AEM_HTTP_PROXY_PORT `（在 AEM 版本 6094 之前，默认为 `proxy.tunnel:3128`）
* 对于 HTTPS：`AEM_PROXY_HOST`/`AEM_HTTPS_PROXY_PORT `（在 AEM 版本 6094 之前，默认为 `proxy.tunnel:3128`）

例如，以下是发送请求到 `www.example.com:8443` 的示例代码：

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

如果使用非标准 Java 联网库，请使用以上属性为所有流量配置代理。

如果非 http/https 流量流经 `portForwards` 参数中声明的端口，应该引用名为 `AEM_PROXY_HOST` 的属性以及映射的端口。例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

下表描述了流量路由：

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目标条件</th>
    <th>端口</th>
    <th>连接</th>
    <th>外部目标示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 协议</b></td>
    <td>标准 http/https 流量</td>
    <td>80 或 443</td>
    <td>允许</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>非标准流量（在 80 或 443 以外的端口上），这些流量流经使用以下环境变量和代理端口号配置的 http 代理。不要在 Cloud Manager API 调用的 portForwards 参数中声明目标端口：<br><ul>
     <li>AEM_PROXY_HOST（在 AEM 版本 6094 之前，默认为“proxy.tunnel”）</li>
     <li>AEM_HTTPS_PROXY_PORT（在 AEM 版本 6094 之前，默认为端口 3128）</li>
    </ul>
    <td>80 或 443 以外的端口</td>
    <td>允许</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>不使用 http 代理的非标准流量（位于端口 80 或 443 之外的其他端口）</td>
    <td>80 或 443 以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>客户端使用在 <code>portForwards</code> API 参数中声明的 <code>portOrig</code> 连接到 <code>AEM_PROXY_HOST</code> 环境变量。</td>
    <td>任意</td>
    <td>允许</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他所有条件</td>
    <td>任意</td>
    <td>已阻止</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Apache/Dispatcher 配置**

AEM Cloud Service Apache/Dispatcher 层的 `mod_proxy` 指令可以使用上述属性进行配置。

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 专用出口 IP 地址 {#dedicated-egress-IP-address}

>[!NOTE]
>
>如果您已在 2021 年 9 月发布 (10/6/21) 之前预配了专用出口 IP，请参阅[旧版专用出口地址客户](#legacy-dedicated-egress-address-customers)。

### 好处 {#benefits}

在与 SaaS 供应商（例如 CRM 供应商）集成时，或者对于在 AEM as a Cloud Service 之外提供 IP 地址允许列表的其他集成，此专用 IP 地址可以增强安全性。通过将专用 IP 地址添加到允许列表，可以确保只有来自客户的 AEM Cloud Service 的流量允许流向外部服务。这是在允许的其他所有 IP 之外的流量。

未启用专用 IP 地址功能时，传出 AEM as a Cloud Service 的流量会流经与其他客户共享的一组 IP。

### 配置 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>无法对专用出口 IP 地址使用 Splunk 转发功能。

专用出口 IP 地址的配置方法与[灵活端口出口](#configuring-flexible-port-egress-provision)相同。

主要差别在于，该流量始终从专用的唯一 IP 地址传出。要查找该 IP，请使用 DNS 解析器来确定与 `p{PROGRAM_ID}.external.adobeaemcloud.com` 关联的 IP 地址。该 IP 地址不应改变，但如果未来需要改变，则会提供高级通知。

除了 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点中的灵活端口出口支持的路由规则之外，专用出口 IP 地址还支持 `nonProxyHosts` 参数。这使得您可以声明一组主机，并且这组主机应通过共享 IP 地址范围而不是专用 IP 进行路由，由于通过共享 IP 传出的流量可能会进一步进行优化，此功能可能会很有用。`nonProxyHost` URL 可能会遵循 `example.com` 或 `*.example.com` 的模式，这种情况下仅支持在域的开头使用通配符。

在灵活端口出口和专用出口 IP 地址之间进行选择时，如果无需特定 IP 地址，客户应选择灵活端口出口，因为 Adobe 可以优化灵活端口出口流量的性能。

### 流量路由 {#dedcated-egress-ip-traffic-routing}

通过端口 80 或 443 传输到目标的 http 或 https 流量将流过预先配置的代理（假定使用标准 Java 联网库）。对于流经其他端口的 http 或 https 流量，应使用以下属性来配置代理。

```
AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST
AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT
```

例如，以下是发送请求到 `www.example.com:8443` 的示例代码：

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
int proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));

HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

如果使用非标准 Java 联网库，请使用以上属性为所有流量配置代理。

如果非 http/https 流量流经 `portForwards` 参数中声明的端口，应该引用名为 `AEM_PROXY_HOST` 的属性以及映射的端口。例如：

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目标条件</th>
    <th>端口</th>
    <th>连接</th>
    <th>外部目标示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 协议</b></td>
    <td>流向 Azure 或 Adobe 服务的流量</td>
    <td>任意</td>
    <td>通过共享集群 IP（而非专用 IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>主机匹配 <code>nonProxyHosts</code> 参数</td>
    <td>80 或 443</td>
    <td>通过共享集群 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>主机匹配 <code>nonProxyHosts</code> 参数</td>
    <td>80 或 443 以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>通过 http 代理配置，默认情况下使用标准 Java HTTP 客户端库为 http/https 流量进行配置。</td>
    <td>任意</td>
    <td>通过专用出口 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http 代理配置（例如，如果明确从标准 Java HTTP 客户端库中删除，或者如果使用的 Java 库忽略标准代理配置）</td>
    <td>80 或 443</td>
    <td>通过共享集群 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http 代理配置（例如，如果明确从标准 Java HTTP 客户端库中删除，或者如果使用的 Java 库忽略标准代理配置）</td>
    <td>80 或 443 以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>客户端使用在 <code>portForwards</code> API 参数中声明的 <code>portOrig</code> 连接到 <code>AEM_PROXY_HOST</code> 环境变量</td>
    <td>任意</td>
    <td>通过专用出口 IP</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他所有条件</td>
    <td></td>
    <td>已阻止</td>
    <td></td>
  </tr>
</tbody>
</table>

## 功能用法 {#feature-usage}

该功能与产生传出流量的 Java 代码或库兼容，前提是它们的代理配置使用了标准 Java 系统属性。实际上，这应该包括了大多数常用库。

下面是代码示例：

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

一些库需要明确配置，以便为代理配置使用标准 Java 系统属性。

使用 Apache HttpClient 的示例，其中需要明确调用 
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) 或使用
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem())：

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

相同的专用 IP 应用到客户在其 Adobe 组织中的所有程序，并用于其各个程序的所有环境。它适用于创作和发布服务。

### 调试注意事项 {#debugging-considerations}

为了验证该流量是否确实在预期的专用 IP 地址上传出，请查看目标服务中的日志（如果可用）。否则，调用 [https://ifconfig.me/IP](https://ifconfig.me/IP) 等调试服务可能会有帮助，调试服务会返回调用 IP 地址。

## 旧版专用出口地址客户 {#legacy-dedicated-egress-address-customers}

如果在 2021 年 9 月 30 日之前已为您配置了专用出口 IP，则您的专用出口 IP 功能仅支持 HTTP 和 HTTPS 端口。这包括 HTTP/1.1 以及加密的 HTTP/2。

## 虚拟专用网络 (VPN) {#vpn}

利用 VPN 可从创作、发布或预览服务连接到内部部署基础设施或数据中心。例如，用于访问数据库。

它还允许连接到 SaaS 供应商（例如支持 VPN 的 CRM 供应商），或者允许从公司网络连接到 AEM as a Cloud Service 的创作、预览或发布服务。

支持大部分采用 IPSec 技术的 VPN 设备。请根据 **RouteBased 配置说明**&#x200B;列的信息，查阅[此页面](https://docs.microsoft.com/zh-cn/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)中的设备列表。按表中所述配置设备。

### 常规注意事项 {#general-vpn-considerations}

* 仅限于支持单个 VPN 连接
* 无法在 VPN 连接上使用 Splunk 转发功能。

### 创建 {#vpn-creation}

每个程序调用一次 POST `/program/<programId>/networkInfrastructures` 端点，传入配置信息的负载，包括：`kind` 参数的“VPN”值、区域、地址空间（CIDR 列表，请注意此项以后不可修改）、DNS 解析器（用于解析客户网络中的名称）以及 VPN 连接信息（例如网关配置、共享 VPN 密钥以及 IP 安全策略）。端点使用 `network_id` 以及包括状态在内的其他信息进行响应。要查看完整的参数集和确切的语法，可参阅 [API 文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure)。

在调用后，通常需要 45 到 60 分钟来预配联网基础设施。可以调用 API 的 GET 方法以返回当前状态，这最终会从 `creating` 翻转到 `ready`。请参考 API 文档来了解所有状态。

如果整个程序的 VPN 配置已就绪，则必须对每个环境调用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点，以在环境级别启用联网并声明任何端口转发规则。可以根据各个环境来配置参数以提供灵活性。

有关详细信息，请参阅 [API 文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration)。

对于应通过 VPN 路由的任何非 http/https TCP 流量，应通过指定目标主机集（名称或 IP 以及端口）来声明端口转发规则。对于每个目标主机，必须将指向的目标端口映射到 30000 到 30999 之间的端口，该值必须在程序的所有环境中唯一。客户还可以在 `nonProxyHosts` 参数中列出一组 URL，这会声明其流量应绕开 VPN 路由的 URL，改为通过共享 IP 范围进行传输。它遵循 `example.com` 或 `*.example.com` 的模式，这种情况下仅支持在域的开头使用通配符。

API 应在几秒钟内响应，指示状态 `updating`，然后在大约 10 分钟后，对 Cloud Manager 环境 GET 端点的调用将显示状态 `ready`，指示对环境的更新已应用。

请注意，即使没有环境流量路由规则（托管或绕过），仍必须调用 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`，只不过在调用时使用空负载。

### 更新 VPN {#updating-the-vpn}

程序级别的 VPN 可以通过调用 `PUT /api/program/<program_id>/network/<network_id>` 端点来更新。

请注意，在初始预配 VPN 之后，无法更改地址空间。如果必须要更改，请联系客户支持。此外，无法修改 `kind` 参数（`flexiblePortEgress`、`dedicatedEgressIP` 或 `VPN`）。如需帮助，请联系客户支持，说明已经创建的内容以及进行更改的原因。

每个环境的路由规则同样可以通过调用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端点进行更新，确保包括完整的配置参数集而不是其子集。环境更新的应用通常需要 5 到 10 分钟。

### 删除或禁用 VPN {#deleting-or-disabling-the-vpn}

要删除网络基础设施，请提交客户支持工单，说明已经创建的内容以及需要删除内容的原因。

要禁用特定环境的 VPN，请调用 `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`。有关详细信息，请参阅 [API 文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration)。

### 流量路由 {#vpn-traffic-routing}

下表描述了流量路由。

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目标条件</th>
    <th>端口</th>
    <th>连接</th>
    <th>外部目标示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http 或 https 协议</b></td>
    <td>流向 Azure 或 Adobe 服务的流量</td>
    <td>任意</td>
    <td>通过共享集群 IP（而非专用 IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>主机匹配 <code>nonProxyHosts</code> 参数</td>
    <td>80 或 443</td>
    <td>通过共享集群 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>主机匹配 <code>nonProxyHosts</code> 参数</td>
    <td>80 或 443 以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 处于 <i>VPN 网关地址</i>空间范围内，并且通过 http 代理配置传输流量（默认情况下使用标准 Java HTTP 客户端库为 http/https 流量进行配置）</td>
    <td>任意</td>
    <td>通过 VPN</td>
    <td><code>10.0.0.1:443</code>这也可以是主机名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 没有处于 <i>VPN 网关地址</i>空间范围内，并且通过 http 代理配置传输流量（默认情况下使用标准 Java HTTP 客户端库为 http/https 流量进行配置）</td>
    <td>任意</td>
    <td>通过专用出口 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http 代理配置（例如，如果明确从标准 Java HTTP 客户端库中删除，或者如果使用省略了标准代理配置的 Java 库）
</td>
    <td>80 或 443</td>
    <td>通过共享集群 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略 http 代理配置（例如，如果明确从标准 Java HTTP 客户端库中删除，或者如果使用省略了标准代理配置的 Java 库）</td>
    <td>80 或 443 以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非 http 或非 https</b></td>
    <td>如果 IP 处于 <i>VPN 网关地址空间</i>范围内，并且客户端使用在 <code>portForwards</code> API 参数中声明的 <code>portOrig</code> 连接到 <code>AEM_PROXY_HOST</code> 环境变量</td>
    <td>任意</td>
    <td>通过 VPN</td>
    <td><code>10.0.0.1:3306</code>这也可以是主机名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果 IP 没有处于 <i>VPN 网关地址空间</i>范围内，并且客户端使用在 <code>portForwards</code> API 参数中声明的 <code>portOrig</code> 连接到 <code>AEM_PROXY_HOST</code> 环境变量</td>
    <td>任意</td>
    <td>通过专用出口 IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>其他所有条件</td>
    <td>任意</td>
    <td>已阻止</td>
    <td></td>
  </tr>
</tbody>
</table>

### 在配置时非常有用的域{#vpn-useful-domains-for-configuration}

下图直观地展示了在配置和开发时非常有用的一组域和关联 IP。该图下方的表进一步说明了这些域和 IP。

![VPN 域配置](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>域模式</th>
    <th>出口（自 AEM）含义</th>
    <th>入口（至 AEM）含义</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>专用出口 IP 地址用于流向 Internet 的流量，而非通过专用网络的流量 </td>
    <td>来自 VPN 的连接将在 CDN 上显示为来自此 IP。要仅允许来自 VPN 的连接进入 AEM，请将 Cloud Manager 配置为仅允许此 IP 并阻止其他所有流量。有关详细信息，请参阅“将传入限制为 VPN 连接”。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>不适用</td>
    <td>AEM 侧 VPN 网关的 IP。客户的网络工程团队可以使用此项来仅允许源自特定 IP 地址的 VPN 连接进入其 VPN 网关。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>流量从 AEM 端的 VPN 流向客户端时使用的 IP。这可以列入客户配置的允许列表中，以确保只接受来自 AEM 的连接。</td>
    <td>如果客户希望只允许通过 VPN 访问 AEM，他们应该配置 CNAME DNS 条目以将 <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 和/或 <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 映射到此项。</td>
  </tr>
</tbody>
</table>

### 将传入限制为 VPN 连接 {#restrict-vpn-to-ingress-connections}

如果您希望只允许通过 VPN 访问 AEM，则可以在 Cloud Manager 中配置环境允许列表，这样可以只允许 `p{PROGRAM_ID}.external.adobeaemcloud.com` 定义的 IP 与环境通信。此操作与在 Cloud Manager 中定义其他任何基于 IP 的允许列表相同。

如果规则必须基于路径，则在 Dispatcher 级别使用标准 http 指令来拒绝或允许特定 IP。它们可以确保所需路径在 CDN 上不可缓存，因此请求始终将获取到来源。

**Httpd 配置示例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 高级联网类型之间的转换 {#transitioning-between-advanced-networking-types}

由于 `kind` 参数无法修改，如需帮助，请联系客户支持，说明已经创建的内容以及进行更改的原因。
