---
title: AEM Edge函数
description: 了解如何使用AEM Edge功能在CDN层执行JavaScript，以在接近最终用户的地方实现个性化、安全和动态体验。
feature: Developing, Edge Delivery Services
role: Developer
source-git-commit: f8000bef01d6b72fb3ac2ae81be9fc19ed1a67d1
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 3%

---


# AEM Edge函数 {#aem-edge-functions}

>[!IMPORTANT]
>
>AEM Edge Functions是&#x200B;**测试版**&#x200B;功能。 功能和文档可能会发生更改，恕不另行通知。 若要加入提前访问计划并提供反馈，请发送电子邮件至[aemcs-edge-functions-feedback@adobe.com](mailto:aemcs-edge-functions-feedback@adobe.com)。

AEM Edge Functions允许您在CDN层执行JavaScript，使数据处理更接近于最终用户。 这样可以减少延迟，并提供响应迅速的动态体验，而无需往返于您的来源地。

常见的用例包括：

- 根据地理位置、设备类型或用户属性等信息个性化内容
- 充当 CDN 与您的源站之间的中间件
- 在第三方API响应到达浏览器之前重新设置格式或聚合响应
- 使用从多个后端拼接的内容在边缘合成和提供服务器渲染的HTML

AEM Edge函数与Edge Delivery Services和AEM Cloud Service Java栈栈兼容。

## 主要优点 {#key-benefits}

| 优势 | 描述 |
|---|---|
| **性能** | 通过边缘SSR快速TTFB返回完全渲染的HTML。 通过并行获取和优化的网络跃点进行的低延迟API调用。 |
| **SEO/地域** | 服务器HTML在首次抓取时编制了索引。 完全渲染的内容已准备好进行人工智能爬虫。 |
| **安全性** | 在服务器端保留API凭据，对客户端JavaScript隐藏。 使用身份提供程序进行身份验证并限制内容访问。 |
| **个性化** | 根据地域和设备信号，在页面加载之前个性化内容。 在边缘运行受众查找，以进行目标交付。 |

## 先决条件 {#prerequisites}

- AEM as a Cloud Service环境
- Cloud Service环境的创作实例上的AEM管理员产品配置文件，**或** Edge Delivery Services站点的Admin Console中的Cloud Manager部署管理员角色
- [Node.js和npm](https://nodejs.org/)

## 设置 {#setup}

### 安装Adobe CLI {#install-adobe-cli}

安装Adobe Developer CLI (`aio`)：

```bash
npm install -g @adobe/aio-cli
```

安装AEM Edge Functions插件：

```bash
aio plugins install @adobe/aio-cli-plugin-aem-edge-functions
```

针对您的环境验证并配置插件：

```bash
aio login
aio aem edge-functions setup
```

setup命令会提示您登录，然后选择要在其上使用AEM Edge Functions的AEM环境。

### 克隆样板 {#boilerplate}

将[aem-edge-functions-boilerplate](https://github.com/adobe/aem-edge-functions-boilerplate)复制到您自己的存储库，然后安装依赖项：

```bash
npm install
```

## 创建您的第一个函数 {#create-your-function}

AEM Edge功能服务在YAML配置文件中声明，并通过Cloud Manager配置管道进行部署。

### 1.设置配置管道 {#configuration-pipeline}

在创建边缘函数之前，请确保Cloud Manager中存在适用于您的环境的配置管道。 如果没有，则[先创建配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

>[!NOTE]
>
>如果您使用快速开发环境(RDE)，则可以直接使用`aio aem rde:install -t env-config ./config`部署配置，而不是通过配置管道进行部署。

### 2.声明您的Edge功能服务 {#declare-services}

在配置目录中创建名为`edgeFunctions.yaml`的文件：

```yaml
kind: "EdgeFunctions"
version: "1"
data:
  services:
    - name: first-function
    - name: second-function
    # Uncomment to enable secrets
    # secrets:
    #   - key: API_TOKEN
    #     value: ${{ API_TOKEN_SECRET }}
```

该配置最多支持三项服务。 顶级键包括：

| 键 | 描述 |
|---|---|
| `services` | 边缘函数服务列表，每个服务均由`name`标识。 |
| `configs` | 作为环境变量向所有Edge函数服务公开的键/值对。 |
| `secrets` | 引用Cloud Manager密钥的键/值对，对所有边缘函数服务公开。 |

### 3.添加CDN原点选择器规则 {#cdn-routing}

通过原始选择器规则将CDN流量路由到它们来调用Edge函数。 将以下内容添加到您的`cdn.yaml`配置文件中（如果该文件不存在，请创建一个）：

```yaml
kind: 'CDN'
version: '1'
data:
  originSelectors:
    rules:
      - name: route-to-first-function
        when: { reqProperty: path, equals: "/weather" }
        action:
          type: selectAemOrigin
          originName: edgefunction-first-function
      - name: route-to-second-function
        when: { reqProperty: path, equals: "/hello-world" }
        action:
          type: selectAemOrigin
          originName: edgefunction-second-function
```

通过原点选择器规则，可根据CDN规则引擎中可用的任何条件（如特定路径、域或请求标头），将流量路由到边缘函数。 有关完整的规则语法，请参阅[源选择器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)。

### 4.部署配置 {#deploy-configuration}

将`edgeFunctions.yaml`和`cdn.yaml`提交到Cloud Manager Git存储库并触发配置管道。 管道成功完成后，您的边缘函数端点在以下位置可用：

- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/weather`
- `publish-pXXXXX-eYYYYY.adobeaemcloud.com/hello-world`

其中`pXXXXX-eYYYYY`是您的环境坐标。 如果配置了自定义域，则也可以在这些域路径中访问函数（例如，`example.com/weather`）。

## 生成和部署AEM Edge函数代码 {#build-deploy}

### 生成 {#build}

将边缘函数代码打包以进行部署：

```bash
aio aem edge-functions build
```

### 部署 {#deploy}

将构建包部署到命名的边缘函数服务。 `function-name`参数必须与`name`中的`edgeFunctions.yaml`值匹配：

```bash
aio aem edge-functions deploy <function-name>
```

## 本地开发 {#local-development}

### 本地运行 {#local-run}

在`http://127.0.0.1:7676`处启动本地开发服务器：

```bash
aio aem edge-functions serve
```

有关本地运行时支持的详细信息，请参阅此[计算JavaScript文档](https://www.fastly.com/documentation/guides/compute/javascript/)。

### 测试 {#test}

使用[Mocha](https://mochajs.org/)运行测试包：

```bash
npm run test
```

### 远程调试 {#remote-debugging}

Adobe Managed CDN不会公开远程调试器，但会公开日志流。 跟踪已部署函数的日志，以直接在终端中接收`console.log`输出：

```bash
aio aem edge-functions tail-logs <function-name>
```

## 配置引用 {#configuration-reference}

### 来源 {#origins}

默认情况下，边缘函数可从任何源获取。 若要将函数限制为定义的源集合，请在`origins`中的`edgeFunctions.yaml`下声明它们：

```yaml
origins:
  - name: my-origin-name
    domain: example.com
```

使用`backend`获取选项引用函数代码中的命名原点：

```js
const request = new Request("https://example.com/test");
const response = await fetch(request, { backend: "my-origin-name" });
```

### 服务配置 {#service-configuration}

在`configs`中使用`edgeFunctions.yaml`键向函数公开环境变量。 值存储在名为`config_default`的配置存储中：

```yaml
configs:
  - key: LOG_LEVEL
    value: DEBUG
```

读取函数代码中的配置值：

```js
import { ConfigStore } from "fastly:config-store";

const config = new ConfigStore('config_default');
const logLevel = config.get('LOG_LEVEL') || 'info';
```

>[!NOTE]
>
>- 配置存储始终名为`config_default`。
>- 键名称区分大小写。
>- 配置存储在同一环境中的所有Edge函数服务之间共享。

### 服务密钥 {#service-secrets}

密钥在`edgeFunctions.yaml`中被引用，未存储。 `value`字段必须使用`${{SECRET_REFERENCE}}`语法指向Cloud Manager密钥。 首先在Cloud Manager中定义基础密码 — 请参阅[Cloud Manager密码变量](/help/implementing/cloud-manager/environment-variables.md)。

```yaml
secrets:
  - key: API_TOKEN
    value: ${{ API_TOKEN_SECRET }}
```

使用样板中的`SecretStoreManager`帮助程序检索函数代码中的密钥：

```js
import { SecretStoreManager } from "./lib/config";

const apiToken = await SecretStoreManager.getSecret('API_TOKEN');
```

>[!NOTE]
>
>- 密钥存储始终名为`secret_default`。
>- 键名称区分大小写。
>- 密钥一旦创建便不可更改。
>- 在同一环境中的所有Edge函数服务之间共享密钥存储。

### 记录 {#logging}

AEM Edge函数与[AEM日志转发](/help/implementing/developing/introduction/log-forwarding.md)功能集成。 在您的`logForwarding.yaml`旁创建一个`edgeFunctions.yaml`文件：

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["rde", "dev", "stage", "prod"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

使用函数代码中的记录器编写结构化日志条目：

```js
import { Logger } from "fastly:logger";

const logger = new Logger("customerSplunk");
logger.log(JSON.stringify({
  method: event.request.method,
  url: event.request.url
}));
```

>[!NOTE]
>
>对于Java栈栈环境，可以从Cloud Manager下载CDN日志（包括AEM Edge函数日志条目），但无法从Edge Delivery Services站点下载。
>
