---
title: 网络连接测试
description: 使用Cloud Manager中的“网络连接测试”，在环境上启用联网之前，从程序的出口路径验证高级联网和VPN配置。
feature: Security
role: Admin
source-git-commit: b29b3a980a0bc1c619fb23c52acda79fae9bf945
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---


# 网络连接测试 {#network-connectivity-test}

**网络连接测试**&#x200B;是一种Cloud Manager诊断工具，可让您在环境中启用高级联网之前，以及在上线之前验证高级联网和VPN配置。 使用它来验证AEM必须访问的主机与端口（包括内部或私有端点）是否可通过“高级联网”将使用的同一连接路径访问。

测试从属于程序高级联网设置的&#x200B;**出口代理基础结构**&#x200B;运行，而不是从创作或发布面板运行。 当高级联网处于活动状态时，它使用与AEM相同的出站网络路径。 该设计对于&#x200B;**VPN**&#x200B;方案特别有用：您可以在启用前确认私有或内部部署系统的DNS解析、网络路由、防火墙规则和服务可用性。

有关预配VPN、专用出口IP或灵活端口出口的背景，请参阅[为AEM as a Cloud Service配置高级网络](/help/security/configuring-advanced-networking.md)。

>[!IMPORTANT]
>
>成功的连接测试证明，高级联网的网络路径可以到达您的目标。 您的应用程序代码仍必须配置为根据需要使用高级联网代理（例如，与代理相关的环境变量和端口转发）。 如果代码绕过代理，那么即使测试通过，您也可能看不到来自预期出口路径的流量。

## 何时使用此工具 {#when-to-use}

* 在&#x200B;**高级网络**&#x200B;在&#x200B;**程序**&#x200B;级别创建，在&#x200B;**之前创建**&#x200B;或在在&#x200B;**环境**&#x200B;上启用它时创建。
* 验证&#x200B;**VPN**&#x200B;与您运行的专用或本地系统（例如，内部主机名或专用IP地址）的连接。
* 当服务未按预期响应时，缩小DNS问题与防火墙或路由问题的对比。

>[!NOTE]
>
>此工具适用于使用高级网络（VPN、专用出口IP或灵活端口出口）的程序。 它不是没有高级联网的标准AEM连接的通用测试。

## 先决条件 {#prerequisites}

* Cloud Manager程序。
* 已为程序创建高级网络基础架构（请参阅[配置高级网络](/help/security/configuring-advanced-networking.md)）。

## 如何运行测试 {#how-to-run-a-test}

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并打开您的组织和程序。
1. 打开程序的&#x200B;**环境**&#x200B;选项卡。 在左侧边栏中，选择&#x200B;**网络基础架构**。

1. 在&#x200B;**网络基础架构**&#x200B;页面上，在表中找到您的基础架构。 选择一行以打开测试体验，或打开行操作菜单（![水平省略号行操作菜单](assets/ellipsis.svg)的Adobe Spectrum Small More图标），然后选择&#x200B;**测试**。

   ![Cloud Manager程序环境区域，其中包含用于启动网络连接测试的网络基础结构表、基础结构行和行操作菜单](assets/network-connectivity-test-cloud-manager-open-test-from-infrastructure-list.png)

1. **网络测试**&#x200B;对话框打开。 输入&#x200B;**主机**&#x200B;和&#x200B;**端口**，选择&#x200B;**测试**，然后在结果区域中查看DNS解析、端口打开、HTTP连接和可访问性。 对话框中显示可选操作，例如&#x200B;**复制到剪贴板**&#x200B;和最近的测试历史记录。 请参阅[了解结果](#understanding-results)，了解如何解释每个节。

   ![包含“主机”和“端口”字段的“Cloud Manager网络连接测试”对话框、“测试”操作，以及DNS解析、端口打开、HTTP连接和可访问性的结果](assets/network-connectivity-test-cloud-manager-results-dialog.png)

### 输入字段 {#input-fields}

| 字段 | 描述 | 示例 |
| --- | --- | --- |
| **主机** | AEM应到达的服务的主机名或IP地址。 | `internal-api.example.com`、`10.0.1.50` |
| **端口** | 目标主机上的TCP端口(1-65535)。 公共值可能显示在快捷键列表中（例如，80、443、587、22）。 | `443` |

### 步骤 {#test-steps}

1. 输入&#x200B;**主机**&#x200B;和&#x200B;**端口**。
1. 选择&#x200B;**测试**。 结果通常会在几秒内显示。
1. 可选：使用&#x200B;**复制到剪贴板**&#x200B;来捕获完整的JSON结果（对于支持案例很有用）。
1. 可能会列出最近的测试以快速重新运行。

## 了解结果 {#understanding-results}

该工具报告多个维度。 它们共同描述目标是否可以从高级联网中访问以及HTTP感知检查的行为方式。

### DNS 解析 {#dns-resolution}

| 结果 | 含义 |
| --- | --- |
| `ips: ["10.0.1.50"]` | DNS解析成功。 主机名使用与高级网络配置关联的解析器解析为列出的IP地址。 |
| `error: "DNS resolution error: ..."` | dns解析失败。 配置的DNS服务器无法解析主机名（名称错误、无法联系解析程序、缺少记录以及类似原因）。 |

>[!NOTE]
>
>如果输入&#x200B;**数字IP**&#x200B;而不是主机名，将跳过该值的DNS解析，并直接使用该IP。

### 端口打开 {#port-open}

| 结果 | 含义 |
| --- | --- |
| `Yes` / true | TCP连接成功 — 端口已打开并接受连接。 |
| `No` / false | 端口已关闭、被防火墙过滤或主机无法访问。 |

### HTTP 连接 {#http-connectivity}

在&#x200B;**每个端口**&#x200B;上尝试了HTTP/HTTPS请求。 该工具始终先尝试&#x200B;**HTTPS**，然后回退到&#x200B;**HTTP**。 如果两者都不起作用，则结果将映射到简短的可读&#x200B;**错误**&#x200B;消息（请参阅下表）。

**成功输出**

| 输出 | 含义 |
| --- | --- |
| `protocol: "https"`、`status_code: 200`、`reason: "200 OK"` | HTTPS连接成功。 |
| `protocol: "http"`、`status_code: 301`、`reason: "301 Moved Permanently"` | HTTP连接成功；服务正在重定向（通常重定向到HTTPS）。 这是正常的。 |

**分类错误输出**

| 错误 | 注意 | 含义 |
| --- | --- | --- |
| `"Not an HTTP/HTTPS service"` | `"The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."` | 端口已打开，但服务不说HTTP。 数据库、 SFTP 、自定义TCP和类似服务需要这样做。 |
| `"Connection refused"` | `"The port is not accepting connections. Verify the service is running and listening on this port."` | 此端口上无任何收听。 |
| `"Connection timed out"` | `"The connection timed out. Check firewall rules and network routing."` | 防火墙或路由问题阻止连接。 |
| `"No IPs resolved for host"` | — | DNS解析失败；无法测试HTTP。 |

>[!NOTE]
>
>来自目标服务的任何HTTP状态代码（例如，`200`、`301`、`302`、`403`、`404`或`500`）都是用于连接的&#x200B;**成功信号**，这意味着&#x200B;**网络路径**&#x200B;有效。 状态代码反映的是服务自身的响应，而不是总体网络运行状况。 对于非HTTP服务，该工具指示&#x200B;**不是HTTP/HTTPS服务**；使用&#x200B;**端口打开**&#x200B;和&#x200B;**可访问性**&#x200B;作为这些服务的可靠指示器。

### 可触达性 {#reachability}

| 结果 | 含义 |
| --- | --- |
| **可访问** | 目标主机和端口可以从高级网络基础架构中访问。 网络配置正确。 |
| **不可访问：端口不可访问** | DNS解析成功，但到端口的TCP未成功。 这通常是防火墙或路由问题。 |
| **不可访问： DNS解析失败** | 无法使用您的配置解析主机名。 这表明DNS配置有问题。 |

### 多个DNS解析器 {#multiple-dns-resolvers}

如果高级网络基础结构定义&#x200B;**多个DNS解析程序**：

* 当&#x200B;**所有解析程序返回相同结果**&#x200B;时，您会看到标记为&#x200B;**的**&#x200B;单个合并`default`结果。
* 当解析程序返回&#x200B;**不同的结果**&#x200B;时，每个解析程序的结果将分别显示&#x200B;**个**（标记为`resolver_1`、`resolver_2`等）、**和解析程序IP**，以便您查看导致不一致的DNS服务器。

## 疑难解答 {#troubleshooting}

以下方案将您在工具中可能看到的内容与缩小原因范围的步骤配对。 有关说明相同情况的完整&#x200B;**复制到剪贴板** JSON，请参阅[示例输出](#example-outputs)。

### DNS解析失败 {#dns-failed}

#### 输出

主机名未使用高级网络DNS设置解析，因此该工具无法测试端口。 在结果视图中，**DNS解析**&#x200B;显示一个错误字符串，**可访问性**&#x200B;报告DNS失败：

```
DNS Resolution: error: "DNS resolution error: ..."
Reachability: "Unreachable: DNS resolution failed"
```

#### 推荐

1. **验证主机名是否正确** — 检查拼写错误以及您是否正在使用预期的&#x200B;**DNS区域**（错误的区域是常见的错误）。
1. 确保&#x200B;**您的DNS解析器**（在网络基础架构中配置的解析器）可从高级网络CIDR范围&#x200B;**（该工具和AEM用于出站检查的地址空间相同）中**&#x200B;访问。 如果您依赖专用DNS，这些服务器必须可以通过VPN通道或在路由向高级网络公开的网络地址空间内访问。
1. **验证配置的DNS服务器是否可以解析主机名** — 高级网络仅使用&#x200B;**解析器**&#x200B;在网络基础结构设置中定义的解析器，**而非**&#x200B;公共DNS（例如`8.8.8.8`）。 如果您的内部DNS没有该主机名的记录，则解析失败。
1. **对于VPN设置：**&#x200B;确认DNS服务器IP地址位于VPN地址空间内（为通道构建的远程网络CIDR）。 无法从高级联网访问未通过VPN通道路由的子网上的解析器。

### DNS工作正常，但端口不可访问 {#dns-ok-port-blocked}

#### 输出

此工具可以解析主机，但无法成功将TCP发送到端口。 摘要通常如下所示：

```
DNS Resolution: ips: ["10.0.1.50"]
Port Open: No
Reachability: "Unreachable: Port not accessible"
```

#### 推荐

1. **查看目标服务上的防火墙和允许列表规则** — 必须允许来自高级网络基础架构CIDR范围的传入流量（以及AEM使用的出口IP地址）。 如果您使用VPN，请按照设计要求包含远程网络CIDR。
1. **验证服务是否正在运行**，**是否正在侦听您在测试中输入的主机和端口**。
1. **对于VPN设置：**&#x200B;确认通道已启动，路由到达目标子网，且目标地址位于通过VPN传送的远程网络地址空间中。
1. 在您的基础架构上，查看&#x200B;**网络安全组(NSG)、安全规则或等效项**，这些可能会阻止高级联网与目标之间的端口。
1. **确认端口号** — 确保进程实际上正在侦听您正在测试的端口。

### 测试显示可访问，但AEM未连接 {#reachable-but-aem-fails}

#### 输出

连接检查本身成功。 简短的摘要通常如下所示：

```
Port Open: Yes
Reachability: "Reachable"
```

该结果意味着从高级联网到您测试的主机和端口的路径是开放的。 它不保证AEM应用程序流量使用该路径：在您的代码运行时，服务日志可能仍不会显示来自您期望的出口IP的请求。

#### 推荐

1. **应用程序代码必须配置为使用代理**。 连接测试证明了网络路径有效，但AEM必须通过&#x200B;**高级联网代理**&#x200B;明确路由请求（例如，通过&#x200B;**`AEM_PROXY_HOST`**&#x200B;环境变量）。 如果代码在没有代理的情况下直接连接，则流量不会通过高级网络基础架构。
1. **查看HTTP客户端中的代理设置** - HTTP客户端应使用相同的代理配置（`AEM_PROXY_HOST`和适用的端口转发）。
1. **在**&#x200B;环境&#x200B;**级别验证高级联网的端口转发配置**：在`portForwards`中，每个条目必须将&#x200B;**`portOrig`**&#x200B;映射到右&#x200B;**`portDest`**&#x200B;目标主机&#x200B;**上的**。 **`portOrig`**&#x200B;是您的AEM应用程序代码在通过proxy打开出站连接时连接到&#x200B;**的**&#x200B;端口。 **`portDest`**&#x200B;是远程进程侦听的目标服务&#x200B;**上的**&#x200B;实际端口。 **目标主机**&#x200B;是转发中使用的服务&#x200B;**的**&#x200B;主机名或地址。 这三项都必须与写入应用程序以连接的方式匹配。
1. **检查`nonProxyHosts`**。 如果目标主机在该处列出，则请求&#x200B;**跳过该主机的代理**，并且不会遵循您验证的“高级联网”路径。

### HTTP显示错误，但端口已打开 {#http-error-port-open}

#### 输出

TCP成功，但HTTP/HTTPS探测器仍报告失败。 摘要通常如下所示：

```
Port Open: Yes
HTTP Connectivity: error: "Connection error: ..." or "Both HTTPS and HTTP failed. ..."
Reachability: "Reachable"
```

#### 推荐

1. **服务可能不使用HTTP或HTTPS** — 例如，原始TCP、gRPC或其他协议。 当`Port open: Yes`和`Reachability: Reachable`仍确认网络路径正常工作时，HTTP探测可能会失败。 使用这些字段作为非HTTP服务的真实来源。
1. **调查TLS和证书配置**。 如果HTTPS失败但HTTP成功（有时由诸如`HTTPS failed, HTTP succeeded`之类的注释指示），则服务可能有证书问题或可能仅在该端口上提供HTTP。

### 请求超时 {#timeout}

#### 输出

```json
{ "error": "Request timeout" }
```

#### 推荐

1. **允许服务响应时间** — 检查使用5秒的超时。 应答速度慢于此的目标将超时，即使这些目标在其他方面比较健康。
1. **考虑网络延迟**。 在VPN连接上，高延迟或不正常的通道可能会使往返超过限制；请检查通道状态和路由。
1. **再次运行测试**。 一次性的网络故障可能会产生不重复的超时。

## 示例输出 {#example-outputs}

### 成功的HTTPS测试（例如，端口443上的内部API） {#example-output-successful-https}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "protocol": "https",
        "status_code": 200,
        "reason": "200 OK"
      },
      "reachability": "Reachable"
    }
  ]
}
```

### 成功的非HTTP服务测试（例如，端口5432上的数据库） {#example-output-successful-non-http}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "error": "Not an HTTP/HTTPS service",
        "note": "The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."
      },
      "reachability": "Reachable"
    }
  ]
}
```

>[!NOTE]
>
>非HTTP服务应出现HTTP错误。 **端口打开： true**&#x200B;和&#x200B;**可访问性：可访问**&#x200B;确认网络路径正常工作。

### DNS解析失败 {#example-output-dns-resolution-failure}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "error": "DNS resolution error: dial udp 10.0.0.2:53: i/o timeout"
      },
      "port_open": false,
      "http_connectivity": {
        "error": "DNS resolution failed"
      },
      "reachability": "Unreachable: DNS resolution failed"
    }
  ]
}
```

### 端口无法访问（防火墙/服务关闭） {#example-output-port-not-accessible}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": false,
      "http_connectivity": {
        "error": "Connection error: dial tcp 10.0.1.50:443: i/o timeout"
      },
      "reachability": "Unreachable: Port not accessible"
    }
  ]
}
```

## 重要说明 {#important-notes}

### 此测试没有执行的操作 {#what-this-test-does-not-do}

* 测试不会从AEM创作或发布面板内部运行。 它从&#x200B;**出口代理基础结构**&#x200B;运行。 这将验证代码中的网络层，而不是应用程序级别的代理配置。
* 它不会验证AEM应用程序的代理设置。 即使结果为`Reachable`，仍必须将AEM代码配置为使用代理。
* 它本身不会验证环境级别的端口转发配置。 它测试来自基础架构路径的原始连接。
* 它不会发送自定义负载。 HTTP测试向`GET`发出基本`/`请求。

### 响应时间 {#response-time}

* **典型值：**&#x200B;约2到3秒。
* **最大值：**&#x200B;大约五秒超时。
* **所有DNS解析器**&#x200B;和连接检查并行运行。

### HTTP与非HTTP服务 {#http-vs-non-http-services}

该工具会在每个端口上尝试HTTP/HTTPS连接。 对于非HTTP服务（例如，端口5432上的PostgreSQL、3306上的MySQL、22上的SFTP、6379上的Redis），HTTP检查可能会失败，并出现连接错误 — 这是正常情况。 依赖`Port open`和`Reachability`确认这些服务的连接。

## 相关信息 {#related-information}

* [为 AEM as a Cloud Service 配置高级联网功能](/help/security/configuring-advanced-networking.md)
* [关于Experience League的高级网络教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/networking/advanced-networking)
