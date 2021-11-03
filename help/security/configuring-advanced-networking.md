---
title: 为AEMas a Cloud Service配置高级网络
description: 了解如何为AEMas a Cloud Service配置高级网络功能（如VPN）或灵活或专用的出口IP地址
source-git-commit: 2f9ba938d31c289201785de24aca2d617ab9dfca
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 1%

---


# 为AEMas a Cloud Service配置高级网络 {#configuring-advanced-networking}

本文旨在介绍AEMas a Cloud Service中的不同高级网络功能，包括VPN的自助配置、非标准端口和专用出口IP地址。

## 概述 {#overview}

AEM as a Cloud Service提供了多种类型的高级网络功能，这些功能可由使用Cloud Manager API的客户进行配置。 这些 Cookie 包括：

* [灵活的端口出口](#flexible-port-egress)  — 配置AEMas a Cloud Service以允许非标准端口外的出站流量
* [专用出口IP地址](#dedicated-egress-IP-address)  — 将AEMas a Cloud Service的流量配置为源自唯一IP
* [虚拟专用网(VPN)](#vpn)  — 为具有VPN技术的客户确保客户基础架构与AEMas a Cloud Service之间的流量

本文详细介绍了其中每个选项，包括如何配置它们。 作为一般配置策略， `/networkInfrastructures` 在程序级别调用API端点以声明所需类型的高级网络，然后调用 `/advancedNetworking` 每个环境的端点，以启用基础结构并配置特定于环境的参数。 请引用Cloud Manager API文档中每个正式语法的相应端点以及示例请求和响应。

计划可以配置单个高级网络变体。 在决定灵活端口出口和专用出口IP地址时，如果不需要特定的IP地址，建议选择灵活的端口出口，因为Adobe可以优化灵活端口出口流量的性能。

>[!INFO]
>
>沙盒项目不提供高级网络。
>此外，环境必须升级到AEM版本5958或更高版本。

>[!NOTE]
>
>已使用旧版专用出口技术配置、需要配置其中一个选项的客户不应这样做，否则站点连接可能会受到影响。 请联系Adobe支持以寻求帮助。

## 灵活的端口出口 {#flexible-port-egress}

此高级网络功能允许您配置AEMas a Cloud Service，以通过默认打开的HTTP（端口80）和HTTPS（端口443）以外的端口输出流量。

### 注意事项 {#flexible-port-egress-considerations}

如果您不需要VPN并且不需要专用出口IP地址，则建议选择灵活的端口出口，因为不依赖专用出口的流量可以获得更高的吞吐量。

### 配置 {#configuring-flexible-port-egress-provision}

每个项目一次，POST `/program/<programId>/networkInfrastructures` 会调用端点，只需传递 `flexiblePortEgress` 对于 `kind` 参数和区域。 端点将使用 `network_id`，以及其他信息（包括状态）。 API文档中应引用完整的参数和确切语法。

调用后，配置网络基础架构通常需要大约15分钟。 对Cloud Manager的调用 [网络基础架构GET端点](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) 将显示状态为“ready”。

如果程序范围的灵活端口出口配置已准备就绪，则 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 必须按环境调用端点，以在环境级别启用网络，并可选地声明任何端口转发规则。 为了提供灵活性，可以按环境配置参数。

应通过指定目标主机集（名称或IP，以及端口）来为80/443以外的任何端口声明端口转发规则。 对于每个目标主机，客户必须将目标端口映射到从30000到30999的端口。

API应在几秒后做出响应，指示更新状态，大约10分钟后，端点的 `GET` 方法应指示已启用高级联网。

### 更新 {#updating-flexible-port-egress-provision}

可以通过调用 `PUT /api/program/<program_id>/network/<network_id>` 和将在几分钟内生效。

>[!NOTE]
>
> “kind”参数(`flexiblePortEgress`, `dedicatedEgressIP` 或 `VPN`)。 请联系客户支持以获取帮助，介绍已创建的内容和更改的原因。

通过再次调用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端点，确保包含完整的配置参数集，而不是子集。

### 删除或禁用灵活端口出口 {#deleting-disabling-flexible-port-egress-provision}

为了 **删除** 网络基础架构，提交客户支持票证，说明已创建的内容以及删除原因。

为了 **禁用** 从特定环境发出灵活的端口出口，调用 `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

有关更多信息，请参阅 [Cloud Manager API文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### 流量路由 {#flexible-port-egress-traffic-routing}

通过端口80或443到达目标的HTTP或HTTPS流量将通过预配置的代理（假定已使用标准Java网络库）。 对于通过其他端口的http或https流量，应使用以下属性配置代理。

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

例如，以下是向发送请求的示例代码 `www.example.com:8443`:

```java
String url = "www.example.com:8443"
var proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
var proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

如果使用非标准Java网络库，请使用上述属性为所有流量配置代理。

通过 `portForwards` 参数应引用名为 `AEM_PROXY_HOST`，以及映射的端口。 例如：

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
    <th>示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https协议</b></td>
    <td>标准http/s流量</td>
    <td>80或443</td>
    <td>允许</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>使用以下环境变量配置的非标准流量（在80或443以外的其他端口上）通过http代理：<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>80或443以外的端口</td>
    <td>允许</td>
  </tr>
  <tr>
    <td></td>
    <td>非标准流量（在端口80或443以外的其他端口上）不使用http代理</td>
    <td>80或443以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>客户端连接到 <code>AEM_PROXY_HOST</code> 使用 <code>portOrig</code> 在 <code>portForwards</code> API参数。</td>
    <td>任意</td>
    <td>允许</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>其他所有内容</td>
    <td>任意</td>
    <td>已阻止</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Apache/Dispatcher配置**

AEM Cloud Service Apache/Dispatcher层 `mod_proxy` 可以使用上述属性配置指令。

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:${AEM_HTTP_PROXY_PORT}"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:${AEM_HTTPS_PROXY_PORT}"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## 专用出口IP地址 {#dedicated-egress-IP-address}

>[!NOTE]
>
>如果您在2021年9月版本(10/6/21)之前已使用专用出口IP进行配置，请参阅 [旧版专用出口地址客户](#legacy-dedicated-egress-address-customers).

### 优点 {#benefits}

当与SaaS供应商（如CRM供应商）集成或AEMas a Cloud Service之外提供IP地址的其他集成时，此专用IP地址可允许列表以增强安全性。 通过向添加专用IP地允许列表址，它可确保仅允许来自客户AEM Cloud Service的流量流入外部服务。 除了允许的来自任何其他IP的流量之外，

如果未启用专用IP地址功能，则来自AEMas a Cloud Service的流量将通过一组与其他客户共享的IP来流动。

### 配置 {#configuring-dedicated-egress-provision}

>[!INFO]
>
>无法从专用出口IP地址获取Splunk转发功能。

配置专用出口IP地址与 [灵活的端口出口](#configuring-flexible-port-egress-provision).

主要区别在于，流量将始终从专用的唯一IP中流出。 要查找该IP，请使用DNS解析程序来识别与 `p{PROGRAM_ID}.external.adobeaemcloud.com`. IP地址不会发生更改，但如果将来需要更改，将提供高级通知。

除了 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点，专用出口IP地址支持 `nonProxyHosts` 参数。 这允许您声明一组应通过共享IP地址范围而不是专用IP路由的主机，由于通过共享IP的流量分配可能会进一步优化，因此这些主机可能非常有用。 的 `nonProxyHost` URL可能遵循 `example.com` 或 `*.example.com`，其中仅在域开头支持通配符。

在决定灵活端口出口和专用出口IP地址之间时，如果不需要特定的IP地址，则客户应选择灵活的端口出口，因为Adobe可以优化灵活端口出口流量的性能。

### 流量路由 {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目标条件</th>
    <th>端口</th>
    <th>连接</th>
    <th>示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https协议</b></td>
    <td>Azure或Adobe服务的流量</td>
    <td>任意</td>
    <td>通过共享群集IP（而非专用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>与 <code>nonProxyHosts</code> 参数</td>
    <td>80或443</td>
    <td>通过共享群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>与 <code>nonProxyHosts</code> 参数</td>
    <td>80或443以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>通过http代理配置，默认情况下使用标准Java HTTP客户端库为http/s流量配置</td>
    <td>任意</td>
    <td>通过专用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果从标准Java HTTP客户端库中显式删除，或者如果使用忽略标准代理配置的Java库）</td>
    <td>80或443</td>
    <td>通过共享群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果从标准Java HTTP客户端库中显式删除，或者如果使用忽略标准代理配置的Java库）</td>
    <td>80或443以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>客户端连接到 <code>AEM_PROXY_HOST</code> 使用 <code>portOrig</code> 在 <code>portForwards</code> API参数</td>
    <td>任意</td>
    <td>通过专用出口IP</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>任何其他内容</td>
    <td></td>
    <td>已阻止</td>
    <td></td>
  </tr>
</tbody>
</table>

## 旧版专用出口地址客户 {#legacy-dedicated-egress-address-customers}

如果您在2021.09.30之前已使用专用出口IP进行配置，则您的专用出口IP功能将按如下所述工作。

### 功能使用 {#feature-usage}

该功能与导致出站流量的Java代码或库兼容，前提是它们使用标准Java系统属性进行代理配置。 实际上，这应该包括大多数常用的库。

以下是代码示例：

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

某些库需要显式配置才能将标准Java系统属性用于代理配置。

使用Apache HttpClient的示例，需要显式调用
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) 或使用
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

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

同一专用IP适用于其Adobe组织中的所有客户计划，也适用于其每个计划中的所有环境。 它适用于创作和发布服务。

仅支持HTTP和HTTPS端口。 这包括加密后的HTTP/1.1和HTTP/2。

### 调试注意事项 {#debugging-considerations}

要验证流量是否确实在预期的专用IP地址上传出，请检查目标服务中的日志（如果可用）。 否则，调用调试服务(例如 [https://ifconfig.me/IP](https://ifconfig.me/IP)，将返回调用的IP地址。

## 虚拟专用网(VPN) {#vpn}

VPN允许从创作、发布或预览连接到内部部署基础架构或数据中心。 例如，用于访问数据库的方式。

它还允许连接到支持VPN的SaaS供应商（如CRM供应商），或从企业网络连接到AEMas a Cloud Service创作、预览或发布。

大多数采用IPSec技术的VPN设备都受支持。 请参阅 [本页](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable)，基于 **基于路由的配置说明** 列。 按照表中所述配置设备。

### 一般注意事项 {#general-vpn-considerations}

* 仅支持单个VPN连接
* 无法通过VPN连接实现Splunk转发功能。

### 作品 {#vpn-creation}

每个项目一次，POST `/program/<programId>/networkInfrastructures` 将调用端点，从而传递配置信息的有效负载，包括：“vpn”的值 `kind` 参数、区域、地址空间（CIDR列表 — 请注意，以后无法修改）、 DNS解析器（用于解析客户网络中的名称）和VPN连接信息（如网关配置、共享VPN密钥和IP安全策略）。 端点将使用 `network_id`，以及其他信息（包括状态）。 在 [API文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

调用后，配置网络基础架构通常需要45到60分钟。 可以调用API的GET方法以返回当前状态，该状态最终将从 `creating` to `ready`. 请查阅API文档，了解所有状态。

如果程序范围的VPN配置已准备就绪，则 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 必须按环境调用端点，以在环境级别启用网络并声明任何端口转发规则。 为了提供灵活性，可以按环境配置参数。

请参阅 [API文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) 以了解更多信息。

应为任何非http/s协议TCP通信声明端口转发规则，这些通信应通过指定目标主机集（名称或IP，以及端口）通过VPN进行路由。 对于每个目标主机，客户必须将目标目标端口映射到从30000到30999的端口，在该端口中，值在程序中的各个环境中必须唯一。 客户还可以在 `nonProxyHosts` 参数，该参数声明流量应绕过VPN路由的URL，而是通过共享IP范围。 它遵循 `example.com` 或 `*.example.com`，其中仅在域开头支持通配符。

API应在几秒内做出响应，表示状态为 `updating` 大约10分钟后，对Cloud Manager环境GET端点的调用将显示状态为 `ready`，表示已应用环境更新。

请注意，即使不存在环境流量路由规则（主机或绕过）， `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 仍必须调用，只是使用空的有效负载。

### 更新VPN {#updating-the-vpn}

通过调用 `PUT /api/program/<program_id>/network/<network_id>` 端点。

请注意，在初始VPN配置后，地址空间无法更改。 如有必要，请联系客户支持。 此外， `kind` 参数(`flexiblePortEgress`, `dedicatedEgressIP` 或 `VPN`)。 请联系客户支持以获取帮助，介绍已创建的内容和更改的原因。

通过再次调用 `PUT /program/{programId}/environment/{environmentId}/advancedNetworking` 端点，确保包含完整的配置参数集，而不是子集。 环境更新通常需要5到10分钟才能应用。

### 删除或禁用VPN {#deleting-or-disabling-the-vpn}

要删除网络基础结构，请提交客户支持票证，说明已创建的内容以及需要删除的原因。

要为特定环境禁用VPN，请调用 `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. 有关 [API文档](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### 流量路由 {#vpn-traffic-routing}

下表描述了流量路由。

<table>
<thead>
  <tr>
    <th>流量</th>
    <th>目标条件</th>
    <th>端口</th>
    <th>连接</th>
    <th>示例</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Http或https协议</b></td>
    <td>Azure或Adobe服务的流量</td>
    <td>任意</td>
    <td>通过共享群集IP（而非专用IP）</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>与 <code>nonProxyHosts</code> 参数</td>
    <td>80或443</td>
    <td>通过共享群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>与 <code>nonProxyHosts</code> 参数</td>
    <td>80或443以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP位于 <i>VPN网关地址</i> 空间范围和通过http代理配置（默认情况下使用标准Java HTTP客户端库为http/s流量配置）</td>
    <td>任意</td>
    <td>通过VPN</td>
    <td><code>10.0.0.1:443</code>它也可以是主机名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP不在 <i>VPN网关地址空间</i> 范围，以及通过http代理配置（默认情况下使用标准Java HTTP客户端库为http/s流量配置）</td>
    <td>任意</td>
    <td>通过专用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果从标准Java HTTP客户端库中显式删除，或者如果使用忽略标准代理配置的Java库）
</td>
    <td>80或443</td>
    <td>通过共享群集IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>忽略http代理配置（例如，如果从标准Java HTTP客户端库中显式删除，或者如果使用忽略标准代理配置的Java库）</td>
    <td>80或443以外的端口</td>
    <td>已阻止</td>
    <td></td>
  </tr>
  <tr>
    <td><b>非http或非https</b></td>
    <td>如果IP位于 <i>VPN网关地址空间</i> 范围和客户端连接到 <code>AEM_PROXY_HOST</code> 使用 <code>portOrig</code> 在 <code>portForwards</code> API参数</td>
    <td>任意</td>
    <td>通过VPN</td>
    <td><code>10.0.0.1:3306</code>它也可以是主机名。</td>
  </tr>
  <tr>
    <td></td>
    <td>如果IP不在 <i>VPN网关地址空间</i> 范围和客户端连接到 <code>AEM_PROXY_HOST</code> 使用 <code>portOrig</code> 在 <code>portForwards</code> API参数</td>
    <td>任意</td>
    <td>通过专用出口IP</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>任何其他内容</td>
    <td>任意</td>
    <td>已阻止</td>
    <td></td>
  </tr>
</tbody>
</table>

### 配置的有用域{#vpn-useful-domains-for-configuration}

下图直观地显示了一组对配置和开发有用的域和关联的IP。 下图的下表进一步描述了这些域和IP。

![VPN域配置](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>域模式</th>
    <th>出口(来自AEM)表示</th>
    <th>入口(到AEM)表示</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>专用出口IP地址，用于访问Internet的流量，而不是通过专用网络。 </td>
    <td>来自VPN的连接将在CDN中显示为来自此IP。 要仅允许来自VPN的连接进入AEM，请配置Cloud Manager以仅允许此IP并阻止其他所有内容。 有关更多详细信息，请参阅“限制进入VPN连接”部分。</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>不适用</td>
    <td>AEM端VPN网关的IP。 客户的网络工程团队可以使用此功能，仅允许从特定IP地址到其VPN网关的VPN连接。 </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>从VPN的AEM端到客户端的流量IP。 可以在客列入允许列表户配置中进行此操作，以确保只能从AEM建立连接。</td>
    <td>如果客户希望仅允许VPN访问AEM，则应将CNAME DNS条目配置为映射 <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code>  和/或 <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> 到这个。</td>
  </tr>
</tbody>
</table>

### 将VPN限制为入口连接 {#restrict-vpn-to-ingress-connections}

如果您希望仅允许VPN访问AEM，则可以在Cloud 允许列表 Manager中配置环境，以便仅允许 `p{PROGRAM_ID}.external.adobeaemcloud.com` 允许与环境交谈。 此操作方式与Cloud Manager中任何其他基于IP的允许列表相同。

如果规则必须基于路径，请在调度程序级别使用标准http指令来拒绝或允许某些IP。 他们应确保CDN也无法缓存所需的路径，以便始终将请求置于原点。

**Httpd配置示例**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## 在高级网络类型之间进行转换 {#transitioning-between-advanced-networking-types}

自 `kind` 无法修改参数，请联系客户支持以获取帮助，说明已创建的内容和更改的原因。
