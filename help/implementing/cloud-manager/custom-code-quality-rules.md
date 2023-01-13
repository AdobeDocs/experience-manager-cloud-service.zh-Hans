---
title: 自定义代码质量规则
description: 此页面描述了作为代码质量测试的一部分，Cloud Manager 执行的自定义代码质量规则。 这些建议基于Adobe Experience Manager工程部的最佳实践。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 2935338b847f7e852dfd31c93a61e737e8a3ec80
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 43%

---

# 自定义代码质量规则 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自定义代码质量规则"
>abstract="此页面描述了作为代码质量测试的一部分，Cloud Manager 执行的自定义代码质量规则。 这些建议基于Adobe Experience Manager工程部的最佳实践。"

本页介绍由Cloud Manager作为 [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md). 这些建议基于Experience Manager工程部门的最佳实践。

>[!NOTE]
>
>此处提供的代码示例仅用于说明目的。 请参阅 SonarQube 的[概念文档](https://docs.sonarqube.org/latest/)，了解 SonarQube 概念和质量规则。

## SonarQube规则 {#sonarqube-rules}

以下部分详细介绍了 Cloud Manager 执行的 SonarQube 规则。

### 不要使用潜在危险的功能 {#do-not-use-potentially-dangerous-functions}

* **密钥**：CQRules:CWE-676
* **类型**：漏洞
* **严重性**：主要
* **开始版本**：版本 2018.4.0

方法 `Thread.stop()` 和 `Thread.interrupt()` 可能会产生难以重现的问题，有时还会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不符合代码 {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### 兼容代码 {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### 请勿使用可能由外部控制的格式字符串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **密钥**：CQRules:CWE-134
* **类型**：漏洞
* **严重性**：主要
* **开始版本**：版本 2018.4.0

使用来自外部源的格式字符串（例如，请求参数或用户生成的内容）可能会使应用程序遭受拒绝服务攻击。在某些情况下，虽然格式字符串可能会受到外部控制，但仅允许来自受信任源。

#### 不符合代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **密钥**：CQRules:ConnectionTimeoutMechanism
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.6.0

在从Experience Manager应用程序内执行HTTP请求时，必须确保配置正确的超时，以避免不必要的线程消耗。 遗憾的是，两个Java™默认HTTP客户端(`java.net.HttpUrlConnection`)，且常用的Apache HTTP组件客户端从不超时，因此必须明确设置超时。 此外，作为最佳实践，这些超时不应超过 60 秒。

#### 不符合代码 {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### 兼容代码 {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### 始终关闭ResourceResolver对象 {#resourceresolver-objects-should-always-be-closed}

* **密钥**：CQRules:CQBP-72
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

从 `ResourceResolverFactory` 获取的 `ResourceResolver` 对象占用系统资源。 虽然可以采取一些措施以在不再使用 `ResourceResolver` 时回收这些资源，但通过调用 `close()` 方法显式关闭任何打开的 `ResourceResolver` 对象会更有效。

一个相对常见的误解是 `ResourceResolver` 不应明确关闭使用现有JCR会话创建的对象，或者这样做会关闭基础JCR会话。 情况并非如此。 无论 `ResourceResolver` 的打开方式如何，只要不再使用它，就应将它关闭。 由于 `ResourceResolver` 实施 `Closeable` 接口，也可以使用 `try-with-resources` 语法，而不是显式调用 `close()`。

#### 不符合代码 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 兼容代码 {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### 请勿使用Sling Servlet路径注册Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **密钥**：CQRules:CQBP-75
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

如 [Sling 文档](https://sling.apache.org/documentation/the-sling-engine/servlets.html)中所述，建议不要通过路径绑定 servlet。 路径绑定的 servlet 不能使用标准 JCR 访问控制，因此，需要额外的安全严密性。 建议在存储库中创建节点并按资源类型注册 servlet，而不是使用路径绑定的 servlet。

#### 不符合代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应记录或抛出，而不是同时记录或抛出 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **密钥**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

通常，一个异常应只记录一次。 将一个异常记录多次可能会导致混淆，因为不清楚该异常发生了几次。 导致出现此情况的最常见模式是记录并引发捕获的异常。

#### 不符合代码 {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### 兼容代码 {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### 避免日志语句后紧跟throw语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **密钥**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

另一个要避免的常见模式是记录一条消息，然后立即引发异常。 此做法通常表示异常消息在日志文件中出现重复。

#### 不符合代码 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 兼容代码 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在处理GET或HEAD请求时，避免在“信息”处记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **密钥**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **类型**：代码异味
* **严重性**：轻微

通常，应使用“信息”日志级别来标定重要操作，并且默认情况下，“Experience Manager”配置为在“信息”级别或更高级别登录。 GET 和 HEAD 方法只能为只读操作，因此，不会构成重要操作。 在“信息”级别登录以响应GET或HEAD请求可能会产生严重的日志噪声，从而更难在日志文件中识别有用信息。 处理 GET 或 HEAD 请求时，应在 WARN 或 ERROR 级别进行记录（如果出现问题），或在 DEBUG 或 TRACE 级别进行记录（如果更深入的故障排除信息会很有用）。

>[!NOTE]
>
>这不适用于 `access.log`-type日志记录。

#### 不符合代码 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 兼容代码 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 请勿将Exception.getMessage()用作日志记录语句的第一个参数 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **密钥**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然上下文也可以通过使用堆栈跟踪来确定，但通常日志消息将更易于阅读和理解。 因此，在记录异常时，将异常消息用作日志消息是一种不好的做法。 异常消息包含错误内容，而日志消息应用于告知日志阅读器应用程序在异常发生时正在执行的操作。 异常消息仍被记录。 通过指定您自己的消息，日志便更易于理解。

#### 不符合代码 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 兼容代码 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 在捕获块中登录应处于“警告”或“错误”级别 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **密钥**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

如名称所示，在特殊情况下应始终使用Java™例外。 因此，当捕获到异常时，请务必确保在适当的级别记录日志消息：WARN 或 ERROR。 这将确保这些消息正确显示在日志中。

#### 不符合代码 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 兼容代码 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿将堆栈跟踪打印到控制台 {#do-not-print-stack-traces-to-the-console}

* **密钥**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

如前所述，上下文对于理解日志消息是至关重要的。 使用 `Exception.printStackTrace()` 仅导致堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在诸如Experience Manager的多线程应用中，如果使用此方法并行打印多个例外，则其堆栈轨迹可能会重叠，这会产生明显的混淆。 应仅通过记录框架来记录异常。

#### 不符合代码 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 兼容代码 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不输出到标准输出或标准错误 {#do-not-output-to-standard-output-or-standard-error}

* **密钥**：CQRules:CQBP-44—LogLevelConsolePrinters
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

登录Experience Manager应始终通过日志记录框架(SLF4J)完成。 直接输出到标准输出或标准错误流会丢失由日志记录框架提供的结构和上下文信息。 有时，可能会导致性能问题。

#### 不符合代码 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 兼容代码 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬编码/apps和/libs路径 {#avoid-hardcoded-apps-and-libs-paths}

* **密钥**：CQRules:CQBP-71
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

通常，以 `/libs` 和 `/apps` 开头的路径不应进行硬编码，因为它们引用的路径最常存储为 Sling 搜索路径（默认情况下，设置为 `/libs,/apps`）的相对路径。 使用绝对路径可能会引入小缺陷，这些缺陷仅在项目生命周期的后期出现。

#### 不符合代码 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 兼容代码 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不使用Sling调度程序 {#sonarqube-sling-scheduler}

* **密钥**：CQRules:AMSCORE-554
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

对于需要保证执行的任务，请勿使用Sling计划程序。 Sling 计划作业可保证执行，并且更适合集群和非集群环境。

请参阅 [Apache Sling事件和作业处理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 了解有关如何在群集环境中处理Sling作业的更多信息。

### 请勿使用已弃用的Experience ManagerAPI {#sonarqube-aem-deprecated}

* **密钥**：AMSCORE-553
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

Experience ManagerAPI表面处于不断修订的状态，可识别不鼓励使用并因此被视为已弃用的API。

通常，使用标准Java™弃用这些API `@Deprecated` 注释，因此，标识为 `squid:CallToDeprecatedMethod`.

但是，在某些情况下，API在Experience Manager上下文中已弃用，但在其他上下文中可能不会弃用。 此规则标识第二个类。


## OakPAL内容规则 {#oakpal-rules}

以下部分详细介绍了 Cloud Manager 执行的 OakPAL 检查。

>[!NOTE]
>
>OakPAL 是一个框架，它使用独立的 Oak 存储库来验证内容包。 该奖项由Experience Manager合作伙伴及2019年Experience Manager罗克星北美奖得主开发。

### 客户不应实施或扩展带@ProviderType的产品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **密钥**：CQBP-84
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.7.0

Experience ManagerAPI包含Java™接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，界面 `com.day.cq.wcm.api.Page` 应仅由Experience Manager实施。

当向这些接口添加新方法时，这些附加方法不会影响使用这些接口的现有代码。 因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 码实现了 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

接口和类(由Experience Manager实现)使用 `org.osgi.annotation.versioning.ProviderType` 或有时使用类似的旧版注释 `aQute.bnd.annotation.ProviderType`. 此规则标识实现此类接口或自定义代码扩展类的情况。

#### 不符合代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自定义Lucene Oak索引必须具有Tika配置 {#oakpal-indextikanode}

* **密钥**：IndexTikaNode
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.8.0

多个现成的Experience ManagerOak索引包含Tika配置，且这些索引的自定义必须包含Tika配置。 此规则检查 `damAssetLucene`、`lucene` 和 `graphqlConfig` 索引的自定义，如果缺少 `tika` 节点或 `tika` 节点缺少名为 `config.xml` 的子节点，则会引发问题。

有关自定义索引定义的更多信息，请参阅[索引文档](/help/operations/indexing.md#preparing-the-new-index-definition)。

#### 不符合代码 {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 兼容代码 {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自定义Lucene Oak索引不能同步 {#oakpal-indexasync}

* **密钥**：IndexAsyncProperty
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.8.0

`lucene`类型的 Oak 索引必须始终异步索引。 否则可能导致系统不稳定。 有关Lucene索引结构的详细信息，请参阅 [Oak文档。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### 不符合代码 {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

#### 兼容代码 {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自定义DAM资产Lucene Oak索引的结构正确  {#oakpal-damAssetLucene-sanity-check}

* **密钥**：IndexDamAssetLucene
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.6.0

为使资产搜索在Experience Manager Assets中正常工作，需自定义 `damAssetLucene` Oak索引必须遵循一组特定于此索引的准则。 此规则检查索引定义是否必须具有名为 `tags` 的多值属性，该属性包含值 `visualSimilaritySearch`。

#### 不符合代码 {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      + tika
        + config.xml
```

#### 兼容代码 {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 客户包不应在/libs下创建或修改节点 {#oakpal-customer-package}

* **密钥**：BannedPath
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2019.6.0

长期以来， `/libs` Experience Manager内容存储库中的内容树应被客户视为只读。 修改 `/libs` 下的节点和属性会给主要和次要更新带来重大风险。 对 `/libs` 必须通过官方渠道进行Adobe。

### 包不应包含重复的OSGi配置 {#oakpal-package-osgi}

* **密钥**：DuplicateOsgiConfigurations
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

复杂项目中出现的一个常见问题是，将同一个 OSGi 组件配置多次。 此问题导致在哪种配置适用方面存在歧义。 此规则“支持运行模式”，因为它仅识别在同一运行模式或运行模式组合中多次配置同一组件的问题。

>[!NOTE]
>
>此规则会产生在多个包中定义相同配置（位于同一路径）的问题，包括在同一包的整个列表中复制同一包的情况。
>
>例如，如果内部版本生成名为的包 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` where `com.myco:com.myco.all` 嵌入 `com.myco:com.myco.ui.apps`，然后是 `com.myco:com.myco.ui.apps` 将报告为重复项。
>
>这通常是不遵循 [内容包结构指南](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 在此特定示例中，包 `com.myco:com.myco.ui.apps` 缺少 `<cloudManagerTarget>none</cloudManagerTarget>` 属性。

#### 不符合代码 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 兼容代码 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安装文件夹应仅包含OSGi节点 {#oakpal-config-install}

* **密钥**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

出于安全原因，包含 `/config/` 和 `/install/` 只能由Experience Manager中的管理用户读取，且只能用于OSGi配置和OSGi包。 如果将其他类型的内容放在包含这些区段的路径下，则会导致应用程序行为在管理用户和非管理用户之间无意中发生变化。

一个常见问题是，在组件对话框中或在为内联编辑指定富文本编辑器配置时使用名为 `config` 的节点。 要解决此问题，应将违规节点重命名为兼容名称。 对于富文本编辑器配置，请使用 `configPath` 属性 `cq:inplaceEditing` 节点来指定新位置。

#### 不符合代码 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 兼容代码 {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 包不应重叠 {#oakpal-no-overlap}

* **密钥**：PackageOverlaps
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

与[“包不应包含重复的 OSGi 配置”规则](#oakpal-package-osgi)类似，这是复杂项目中的一个常见问题，其中同一节点路径被多个单独的内容包写入。 虽然可使用内容包依赖项来确保获得一致的结果，但最好是完全避免重叠。

### 默认创作模式不应为经典UI {#oakpal-default-authoring}

* **密钥**：ClassicUIAuthoringMode
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

OSGi配置 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 在Experience Manager中定义默认的创作模式。 因为 [经典UI自Experience Manager6.4起已弃用](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html)，现在将默认创作模式配置为经典UI时，会引发问题。

### 具有对话框的组件应具有触屏UI对话框 {#oakpal-components-dialogs}

* **密钥**：ComponentWithOnlyClassicUIDialog
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

具有经典UI对话框的Experience Manager组件应始终具有相应的触屏UI对话框。 这两种方法都可提供最佳的创作体验，并且与不支持经典UI的Cloud Service部署模型兼容。 此规则验证以下场景：

* 具有经典 UI 对话框（即 `dialog` 子节点）的组件必须具有相应的 Touch UI 对话框（即 `cq:dialog` 子节点）。
* 具有经典 UI 设计对话框（即 `design_dialog` 节点）的组件必须具有相应的 Touch UI 设计对话框（即 `cq:design_dialog` 子节点）。
* 具有经典 UI 对话框和经典 UI 设计对话框的组件必须具有相应的 Touch UI 对话框和Touch UI 设计对话框。

Experience Manager现代化工具文档提供了有关如何将组件从经典UI转换为触屏UI的文档和工具。 请参阅 [Experience Manager现代化工具文档](https://opensource.adobe.com/aem-modernize-tools/) 以了解更多详细信息。

### 包不应混合使用可变和不可变内容 {#oakpal-packages-immutable}

* **密钥**：ImmutableMutableMixedPackage
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

要与Cloud Service部署模型兼容，单个内容包必须包含存储库不可变区域(`/apps` 和 `/libs`)或可变区域( `/apps` 或 `/libs`)，但不能两者兼有。 例如，包中同时包含这两者 `/apps/myco/components/text` 和 `/etc/clientlibs/myco` 与Cloud Service不兼容，并导致报告问题。

>[!NOTE]
>
>[客户包不应在 /libs 下创建或修改节点](#oakpal-customer-package)规则始终适用。

请参阅 [Experience Manager项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md) 以了解更多详细信息。

### 请勿使用反向复制代理 {#oakpal-reverse-replication}

* **密钥**：ReverseReplication
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

在Cloud Service部署中不提供对反向复制的支持，如Experience Manageras a Cloud Service的 [发行说明。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向复制的客户应联系 Adobe 以获取替代解决方案。

### 启用代理的客户端库中包含的资源应位于名为“resources”的文件夹中 {#oakpal-resources-proxy}

* **密钥**：ClientlibProxyResource
* **类型**：错误
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager客户端库可能包含静态资源，如图像和字体。 如[使用预处理器](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)文档中所述，在使用代理的客户端库时，这些静态资源必须包含在名为 `resources` 的子文件夹中，才能在发布实例上有效引用这些资源。

#### 不符合代码 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 兼容代码 {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### 使用Cloud Service不兼容的工作流流程 {#oakpal-usage-cloud-service}

* **密钥**：CloudServiceIncompatibleWorkflowProcess
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2021.2.0

随着在Experience Manageras a Cloud Service上移动到资产微服务以进行资产处理，在内部部署版和AMS版Experience Manager中使用的多个工作流流程变得不支持或不必要。

中的迁移工具 [Experience Manageras a Cloud Service资产GitHub存储库](https://github.com/adobe/aem-cloud-migration) 可用于在迁移期间更新工作流模型，以Experience Manageras a Cloud Service。

### 不鼓励使用静态模板，转而使用可编辑的模板 {#oakpal-static-template}

* **密钥**：StaticTemplateUsage
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

虽然静态模板在Experience Manager项目中的使用一直很常见，但Adobe建议使用可编辑的模板，因为它们提供了最大的灵活性，并支持静态模板中不存在的其他功能。 要获取更多信息，请参阅文档[页面模板](/help/implementing/developing/components/templates.md)。

从静态模板迁移到可编辑的模板，可以使用 [Experience Manager现代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 不鼓励使用旧版基础组件 {#oakpal-usage-legacy}

* **密钥**：LegacyFoundationComponentUsage
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

旧版基础组件(即 `/libs/foundation`) [已在多个Experience Manager版本中弃用](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 支持核心组件。 建议不要使用基础组件作为自定义组件的基础（无论是通过叠加还是继承），并且应将这些基础组件转换为相应的核心组件。

可通过 [Experience Manager现代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 仅使用支持的运行模式名称和排序 {#oakpal-supported-runmodes}

* **密钥**：SupportedRunmode
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service对运行模式名称强制实施严格的命名策略，并对这些运行模式实施严格的排序。 可在文档中找到支持的运行模式列表 [部署到Experience Manageras a Cloud Service](/help/implementing/deploying/overview.md#runmodes) 任何偏离都被认定为问题。

### 自定义搜索索引定义节点必须是/oak:index的直接子节点 {#oakpal-custom-search}

* **密钥**：OakIndexLocation
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service要求自定义搜索索引定义（即，类型的节点） `oak:QueryIndexDefinition`)是 `/oak:index`. 必须移动其他位置的索引才能与Experience Manageras a Cloud Service兼容。 有关搜索索引的更多信息，请参阅[“内容搜索和索引编制”文档](/help/operations/indexing.md)。

### 自定义搜索索引定义节点的compatVersion必须为2 {#oakpal-custom-search-compatVersion}

* **密钥**：IndexCompatVersion
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service要求自定义搜索索引定义（如类型的节点） `oak:QueryIndexDefinition`)必须具有 `compatVersion` 属性设置为 `2`. Experience Manageras a Cloud Service不支持任何其他值。 有关搜索索引的更多信息，请参阅[内容搜索和索引编制](/help/operations/indexing.md)。

### 自定义搜索索引定义节点的子节点类型必须为nt:unstructured {#oakpal-descendent-nodes}

* **密钥**：IndexDescendantNodeType
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

如果自定义搜索索引定义节点具有无序的子节点，则可能会出现难以排除的问题。 为避免这种情况，建议 `oak:QueryIndexDefinition` 节点类型 `nt:unstructured`.

### 自定义搜索索引定义节点必须包含一个名为indexRules的子节点，该子节点具有子节点 {#oakpal-custom-search-index}

* **密钥**：IndexRulesNode
* **类型**：代码异味
* **严重性**：轻微
* **从以下版本开始**：版本 2021.2.0

正确定义的自定义搜索索引定义节点必须包含一个名为 `indexRules` 的子节点，而该子节点必须具有至少一个子节点。有关更多信息，请参阅 [Oak 文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### 自定义搜索索引定义节点必须遵循命名约定 {#oakpal-custom-search-definitions}

* **密钥**：IndexName
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service要求自定义搜索索引定义(即，类型的节点 `oak:QueryIndexDefinition`)必须按照文档中描述的特定模式命名 [内容搜索和索引。](/help/operations/indexing.md)

### 自定义搜索索引定义节点必须使用索引类型Lucene  {#oakpal-index-type-lucene}

* **密钥**：IndexType
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.2.0（类型和严重性更改于 2021.8.0 版本）

Experience Manageras a Cloud Service要求自定义搜索索引定义（即，类型的节点） `oak:QueryIndexDefinition`)具有 `type` 值设置为的属性 `lucene`. 在迁移到Experience Manageras a Cloud Service之前，必须更新使用旧索引类型的索引。 请参阅 [内容搜索和索引](/help/operations/indexing.md#how-to-use) 以了解更多信息。

### 自定义搜索索引定义节点不得包含名为seed的属性 {#oakpal-property-name-seed}

* **密钥**：IndexSeedProperty
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service禁止自定义搜索索引定义(即，节点类型 `oak:QueryIndexDefinition`)来自包含名为 `seed`. 在迁移到Experience Manageras a Cloud Service之前，必须更新使用此属性的索引。 有关更多信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#how-to-use)。

### 自定义搜索索引定义节点不得包含名为reindex的属性 {#oakpal-reindex-property}

* **密钥**：IndexReindexProperty
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manageras a Cloud Service禁止自定义搜索索引定义(即，节点类型 `oak:QueryIndexDefinition`)来自包含名为 `reindex`. 在迁移到Experience Manageras a Cloud Service之前，必须更新使用此属性的索引。 有关更多信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#how-to-use)。
