---
title: 自定义代码质量规则
description: 了解Cloud Manager的自定义代码质量规则，这些规则基于Adobe Experience Manager工程最佳实践，旨在通过彻底测试确保高质量的代码。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2573eb5f8a8ff21a8e30b94287b554885cd1cd89
workflow-type: tm+mt
source-wordcount: '4421'
ht-degree: 66%

---

# 自定义代码质量规则 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自定义代码质量规则"
>abstract="了解Cloud Manager的自定义代码质量规则，这些规则基于Adobe Experience Manager工程最佳实践，旨在通过彻底测试确保高质量的代码。"

了解Cloud Manager的自定义代码质量规则，这些规则基于Adobe Experience Manager工程最佳实践，旨在通过彻底测试确保高质量的代码。 另请参阅[代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)。

>[!NOTE]
>
>由于是 Adobe 专有信息，因此无法下载完整的 SonarQube 规则。可[使用此链接](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)下载规则的完整列表。有关规则的描述和示例，请继续阅读本文档。

>[!NOTE]
>
>此处提供的代码示例仅用于说明目的。 请参阅 SonarQube 的[概念文档](https://docs.sonarsource.com/sonarqube/latest/)，了解 SonarQube 概念和质量规则。

## SonarQube 规则 {#sonarqube-rules}

以下部分详细介绍了 Cloud Manager 执行的 SonarQube 规则。

### 请勿使用有潜在危险的功能 {#do-not-use-potentially-dangerous-functions}

* **密钥**：CQRules:CWE-676
* **类型**：漏洞
* **严重性**：主要
* **开始版本**：版本 2018.4.0

`Thread.stop()` 和 `Thread.interrupt()` 方法可能会产生难以重现的问题，并且有时会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

#### 不合规的代码 {#non-compliant-code}

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

#### 合规的代码 {#compliant-code}

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

### 请勿使用可能受到外部控制的格式字符串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **密钥**：CQRules:CWE-134
* **类型**：漏洞
* **严重性**：主要
* **开始版本**：版本 2018.4.0

使用来自外部源的格式字符串（如请求参数或用户生成的内容）可能会使应用程序遭受拒绝服务攻击。在某些情况下，虽然格式字符串可能会受到外部控制，但仅允许来自受信任源。

#### 不合规的代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP 请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **密钥**：CQRules:ConnectionTimeoutMechanism
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.6.0

在Experience Manager应用程序内发出HTTP请求时，必须配置适当的超时以防止不必要的线程消耗。
默认情况下，Java™ HTTP客户端(java.net.HttpUrlConnection)和广泛使用的Apache HTTP组件客户端都不规定超时，因此必须手动配置它们。 作为最佳实践，超时应设置为等于或少于60秒。

#### 不合规的代码 {#non-compliant-code-2}

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

#### 合规的代码 {#compliant-code-1}

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

public void orDoThis () {
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

### ResourceResolver 对象应始终关闭 {#resourceresolver-objects-should-always-be-closed}

* **密钥**：CQRules:CQBP-72
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

从`ResourceResolverFactory`获取的ResourceResolver对象占用系统资源。 虽然可以采取一些措施以在不再使用 `ResourceResolver` 时回收这些资源，但通过调用 `close()` 方法明确关闭任何打开的 `ResourceResolver` 对象会更有效。

一个常见的误解是，使用现有JCR会话创建的`ResourceResolver`对象不应显式关闭，或者关闭它们会影响JCR会话。 此信息不正确。 `ResourceResolver`在不再需要时应始终关闭。 由于`ResourceResolver`实现`Closeable`接口，您还可以使用`try-with-resources`语法而不是直接调用`close()`。

#### 不合规的代码 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 合规的代码 {#compliant-code-2}

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

### 请勿使用 Sling Servlet 路径来注册 Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **密钥**：CQRules:CQBP-75
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2018.4.0

如 [Sling 文档](https://sling.apache.org/documentation/the-sling-engine/servlets.html)所述，建议不要通过路径绑定 servlet。路径绑定的 servlet 不能使用标准 JCR 访问控制，因此，需要额外的安全严密性。 建议在存储库中创建节点并按资源类型注册 servlet，而不是使用路径绑定的 servlet。

#### 不合规的代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应被记录或引发，而不是同时记录和引发 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **密钥**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

通常，一个异常应只记录一次。 多次记录异常可能会导致混淆。 原因在于，不清楚发生了多少次异常。 导致出现此效果的最常见模式是记录并引发捕获的异常。

#### 不合规的代码 {#non-compliant-code-6}

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

#### 合规的代码 {#compliant-code-3}

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

### 避免 Log 语句紧跟 Throw 语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **密钥**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

另一个要避免的常见模式是记录一条消息，然后立即引发异常。 该实践通常表明异常消息最终会在日志文件中重复。

#### 不合规的代码 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 合规的代码 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 在处理 GET 或 HEAD 请求时，避免在 INFO 级别进行记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **密钥**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **类型**：代码异味
* **严重性**：轻微

通常，应使用 INFO 日志级别来划分重要操作，默认情况下，Experience Manager 配置为在 INFO 级别或更高级别进行记录。 GET 和 HEAD 方法只能为只读操作，因此，不会构成重要操作。 在 INFO 级别进行记录来响应 GET 或 HEAD 请求可能会产生大量日志噪音，导致更难以识别日志文件中的有用信息。 在处理GET或HEAD请求时，如果出现错误，请记录WARN或ERROR级别。 如果需要详细的疑难解答信息，请使用DEBUG或TRACE级别。

>[!NOTE]
>
>不适用于每个请求的`access.log`类型日志记录。

#### 不合规的代码 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 合规的代码 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 请勿使用 Exception.getMessage() 作为 Logging 语句的第一个参数 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **密钥**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然也可以使用堆栈跟踪来确定上下文，但通常日志消息将更易于阅读和理解。 因此，在记录异常时，将异常消息用作日志消息是一种不好的做法。 异常消息将说明所发生的问题，而日志消息应告知读者异常发生时应用程序正在做什么。 仍会记录异常消息。 通过指定您自己的消息，可使日志更易于理解。

#### 不合规的代码 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 合规的代码 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 应在 WARN 或 ERROR 级别记录 Catch 块 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **密钥**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

顾名思义，Java™ 异常应始终在异常情况下使用。 因此，当捕获到异常时，请务必确保在适当的级别记录日志消息：WARN 或 ERROR。 此过程可确保这些消息正确显示在日志中。

#### 不合规的代码 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 合规的代码 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿将堆栈跟踪输出到控制台 {#do-not-print-stack-traces-to-the-console}

* **密钥**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

如前所述，上下文对于理解日志消息是至关重要的。 使用 `Exception.printStackTrace()` 会导致仅将堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在像 Experience Manager 这样的多线程应用程序中，如果使用此方法并行打印多个异常，则其堆栈跟踪可能会发生重叠，从而导致产生严重混淆。应仅通过记录框架来记录异常。

#### 不合规的代码 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 合规的代码 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 请勿输出到标准输出或标准错误 {#do-not-output-to-standard-output-or-standard-error}

* **密钥**：CQRules:CQBP-44—LogLevelConsolePrinters
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

Experience Manager 中的记录应始终通过记录框架 (SLF4J) 完成。 直接输出到标准输出或标准错误流将丢失记录框架提供的结构和上下文信息。有时，它可能会导致性能问题。

#### 不合规的代码 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 合规的代码 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬编码应用程序和库路径 {#avoid-hardcoded-apps-and-libs-paths}

* **密钥**：CQRules:CQBP-71
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2018.4.0

以 `/libs` 和 `/apps` 开头的路径通常不应进行硬编码。这些路径通常相对于Sling搜索路径（默认为`/libs,/apps`）进行存储。 使用绝对路径可能会引入细微的缺陷，这些缺陷只会在项目生命周期的后期才会出现。

#### 不合规的代码 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 合规的代码 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不要使用 Sling 调度程序 {#sonarqube-sling-scheduler}

* **密钥**：CQRules:AMSCORE-554
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

Sling 调度程序不得用于需要保证执行的任务。 Sling 计划作业可保证执行，并且更适合集群和非集群环境。

请参阅 [Apache Sling 事件和作业处理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)，详细了解如何在集群环境中处理 Sling 作业。

### 不要使用 Experience Manager 弃用的 API {#sonarqube-aem-deprecated}

* **密钥**：AMSCORE-553
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

Experience Manager API 接口正在不断修订，以识别建议不要使用的 API，从而将其弃用。

通常情况下，使用标准 Java™ `@Deprecated` 注释来弃用这些 API，如 `squid:CallToDeprecatedMethod` 所标识。

但在某些情况下，API 会在 Experience Manager 上下文中被弃用，但在其他上下文中可能不会被弃用。 此规则标识第二个类。

### 请勿在Sling模型中将@Inject注释与@Optional一起使用 {#sonarqube-slingmodels-inject-optional}

* **Key**： InjectAnnotationWithOptionalInjectionCheck
* **类型**：软件质量
* **严重性**：轻微
* **自**：版本2023.11

Apache Sling项目不鼓励在Sling模型的上下文中使用`@Inject`注释，因为它可能会导致与`DefaultInjectionStrategy.OPTIONAL`结合使用时性能不佳（在字段或类级别）。 相反，应使用更具体的注入（如`@ValueMapValue`或`@OsgiInjector`注释）。

查看[Apache Sling文档](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1)，了解有关推荐的注释以及最初提出此推荐的原因的更多信息。


### 重用HTTPClient实例 {#sonarqube-reuse-httpclient}

* **密钥**： AEMSRE-870
* **类型**：软件质量
* **严重性**：轻微
* **自**：版本2023.11

AEM应用程序经常使用HTTP协议与其他应用程序联系，Apache HttpClient是实现这一目标的常用库。 但是，创建此类HttpClient对象会带来一些开销，因此应尽可能重用这些对象。

此规则检查此类HttpClient对象在方法中是否不是私有的，而是在类级别上是全局的，以便可以重复使用。 在这种情况下，应在类的构造函数或`activate()`方法（如果此类是OSGi组件/服务）中设置HttpClient字段。

有关使用HttpClient的一些最佳实践，请查看HttpClient的[优化指南](https://hc.apache.org/httpclient-legacy/performance.html)。

#### 不合规的代码 {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### 合规的代码 {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## OakPAL 内容规则 {#oakpal-rules}

以下部分详细介绍了 Cloud Manager 执行的 OakPAL 检查。

>[!NOTE]
>
>OakPAL 是一个框架，它使用独立的 Oak 存储库来验证内容包。 2019年Experience ManagerRockstar北美奖的得主Experience Manager合作伙伴开发了该软件。

### 客户不应实施或扩展用@ProviderType注释的产品API{#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **密钥**：CQBP-84
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2018.7.0

Experience ManagerAPI包含Java™接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，只有Experience Manager应该实现`com.day.cq.wcm.api.Page`接口。

将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码。 因此，向这些接口添加新方法被认为是向后兼容的。但是，如果自定义代码实现了其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

由 Experience Manager 实现的接口和类通过 `org.osgi.annotation.versioning.ProviderType` 进行注释，有时会通过类似的旧批注 `aQute.bnd.annotation.ProviderType` 进行注释。 此规则标识自定义代码实现此类接口或扩展类的情况。

#### 不合规的代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自定义 Lucene Oak 索引必须具有 Tika 配置 {#oakpal-indextikanode}

* **密钥**：IndexTikaNode
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.8.0

多个现成的 Experience Manager Oak 索引包含一个 Tika 配置，这些索引的自定义必须包含 Tika 配置。 此规则检查 `damAssetLucene`、`lucene` 和 `graphqlConfig` 索引的自定义，如果缺少 `tika` 节点或 `tika` 节点缺少名为 `config.xml` 的子节点，则会引发问题。

有关自定义索引定义的更多信息，请参阅[索引文档。](/help/operations/indexing.md#preparing-the-new-index-definition)

#### 不合规的代码 {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### 合规的代码 {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自定义 Lucene Oak 索引不得同步 {#oakpal-indexasync}

* **密钥**：IndexAsyncProperty
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.8.0

`lucene`类型的 Oak 索引必须始终异步索引。 不这样做可能会导致系统不稳定。 有关Lucene索引结构的更多信息，请参阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)。

#### 不合规的代码 {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### 合规的代码 {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 自定义 DAM 资源 Lucene Oak 指数结构合理 {#oakpal-damAssetLucene-sanity-check}

* **密钥**：IndexDamAssetLucene
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.6.0

要使资源搜索在Experience Manager Assets中正确运行，`damAssetLucene` Oak索引的自定义必须遵循一组特定于此索引的准则。 此规则检查索引定义是否必须具有名为`tags`的多值属性，该属性包含值`visualSimilaritySearch`。

#### 不合规的代码 {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### 合规的代码 {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 客户包不应在库下创建或修改节点 {#oakpal-customer-package}

* **密钥**：BannedPath
* **类型**：错误
* **严重性**：严重
* **开始版本**：版本 2019.6.0

客户应将 Experience Manager 内容存储库中的 `/libs` 内容树视为只读，这是一个长期存在的最佳实践。修改 `/libs` 下的节点和属性会给主要和次要更新带来重大风险。 通过官方渠道使用Adobe修改`/libs`。

### 包不应包含重复的 OSGi 配置 {#oakpal-package-osgi}

* **密钥**：DuplicateOsgiConfigurations
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

复杂项目中的一个常见问题是将同一个 OSGi 组件配置多次。该问题会导致无法明确哪种配置是适用的。 此规则是“运行模式感知型”的，因为它只会识别在同一运行模式或运行模式组合中多次配置同一组件的问题。

>[!NOTE]
>
>此规则会产生在多个包中定义相同配置、相同路径的问题，包括在构建包的总体列表中重复相同包的情况。
>
>例如，如果版本生成名为 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` 的包，其中 `com.myco:com.myco.all` 嵌入 `com.myco:com.myco.ui.apps`，则 `com.myco:com.myco.ui.apps` 中的所有配置都会报告为重复。
>
>通常，此情况是不遵循[内容包结构指南](/help/implementing/developing/introduction/aem-project-content-package-structure.md)的情况。 在此示例中，包`com.myco:com.myco.ui.apps`缺少`<cloudManagerTarget>none</cloudManagerTarget>`属性。

#### 不合规的代码 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 合规的代码 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Config 和 Install 文件夹应只包含 OSGi 节点 {#oakpal-config-install}

* **密钥**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2019.6.0

出于安全原因，包含 `/config/` 和 `/install/` 的路径只能由 Experience Manager 中的管理用户读取，并且只能用于 OSGi 配置和 OSGi 捆绑包。 将其他类型的内容放在包含这些区段的路径下会导致管理用户和非管理用户之间的应用程序行为无意间有所不同。

一个常见问题是，在组件对话框中或在为内联编辑指定富文本编辑器配置时使用名为 `config` 的节点。 要解决此问题，应将违规节点重命名为合规的名称。 对于富文本编辑器配置，使用 `cq:inplaceEditing` 节点上的 `configPath` 属性指定新位置。

#### 不合规的代码 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 合规的代码 {#compliant-code-config-install}

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

与[包不应包含重复的OSGi配置规则](#oakpal-package-osgi)类似，这种情况是复杂项目中的一个常见问题，其中同一节点路径被多个单独的内容包写入。 虽然可使用内容包依赖项来确保获得一致的结果，但最好是完全避免重叠。

### 默认创作模式不应是经典UI {#oakpal-default-authoring}

* **密钥**：ClassicUIAuthoringMode
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

OSGi 配置 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 定义 Experience Manager 中的默认创作模式。 由于经典 UI 自 Experience Manager 6.4 之后已被弃用，因此，在将默认创作模式配置为经典 UI 时，现在会引发问题。

### 带对话框的组件应具有Touch UI对话框 {#oakpal-components-dialogs}

* **密钥**：ComponentWithOnlyClassicUIDialog
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

具有Classic UI对话框的Experience Manager组件应始终具有相应的Touch UI对话框。 两者都提供了与不再支持Classic UI的Cloud Service部署模型兼容的最佳创作体验。 此规则验证以下场景：

* 具有经典 UI 对话框（即 `dialog` 子节点）的组件必须具有相应的 Touch UI 对话框（即 `cq:dialog` 子节点）。
* 具有经典 UI 设计对话框（即 `design_dialog` 节点）的组件必须具有相应的 Touch UI 设计对话框（即 `cq:design_dialog` 子节点）。
* 具有经典 UI 对话框和经典 UI 设计对话框的组件必须具有相应的 Touch UI 对话框和Touch UI 设计对话框。

Experience Manager 现代化工具文档提供了有关如何将组件从经典 UI 转换为 Touch UI 的文档以及使用的工具。 有关更多详细信息，请参阅 [Experience Manager 现代化工具文档。](https://opensource.adobe.com/aem-modernize-tools/)

### 包不应混合可变和不可变的内容 {#oakpal-packages-immutable}

* **密钥**：ImmutableMutableMixedPackage
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

要与 Cloud Service 部署模型兼容，各个内容包必须包含存储库的不可变区域（即 `/apps` 和 `/libs`）的内容或可变区域的内容（即未在 `/apps` 或 `/libs` 中的内容），但不能同时包含这两个区域的内容。 例如，同时包含`/apps/myco/components/text`和`/etc/clientlibs/myco`的包不与Cloud Service兼容，并导致报告问题。

>[!NOTE]
>
>规则[客户包不应在libs](#oakpal-customer-package)下创建或修改节点。

有关更多详细信息，请参阅[ Experience Manager 项目结构。](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

### 不应使用反向复制代理 {#oakpal-reverse-replication}

* **密钥**：ReverseReplication
* **类型**：代码异味/Cloud Service 兼容性
* **严重性**：轻微
* **开始版本**：版本 2020.5.0

Cloud Service 部署中不支持反向复制，如 Experience Manager as a Cloud Service 的[发行说明中所述。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向复制的客户应联系 Adobe 以获取替代解决方案。

### 启用代理的客户端库中包含的资源应位于名为 resources 的文件夹中 {#oakpal-resources-proxy}

* **密钥**：ClientlibProxyResource
* **类型**：错误
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager 客户端库可能包含静态资源，如图像和字体。如文档[使用预处理器](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors)中所述，在使用代理的客户端库时，这些静态资源必须包含在名为`resources`的子文件夹中，才能在发布实例上有效引用这些资源。

#### 不合规的代码 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 合规的代码 {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### 与 Cloud Service 不兼容的工作流的使用 {#oakpal-usage-cloud-service}

* **密钥**：CloudServiceIncompatibleWorkflowProcess
* **类型**：错误
* **严重性**：主要
* **开始版本**：版本 2021.2.0

随着在Adobe Experience Manager as a Cloud Service中迁移到资源微服务以进行资源处理，现在不支持在内部部署和AMS版本中使用的多个工作流进程。 其中许多工作流程也变得没有必要。

[Experience Manager as a Cloud Service Assets GitHub 存储库](https://github.com/adobe/aem-cloud-migration)中的迁移工具可在迁移到 Experience Manager as a Cloud Service 的过程中用于更新工作流模型。

### 建议不要使用静态模板来支持可编辑的模板 {#oakpal-static-template}

* **密钥**：StaticTemplateUsage
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

虽然静态模板的使用历来在 Experience Manager 项目中非常普遍，但 Adobe 建议使用可编辑的模板，因为它们提供了最大的灵活性，并支持静态模板中不存在的附加功能。 要获取更多信息，请参阅文档[页面模板。](/help/implementing/developing/components/templates.md)

可以使用[Experience Manager现代化工具](https://opensource.adobe.com/aem-modernize-tools/)在很大程度上实现从静态模板到可编辑模板的迁移的自动化。

### 建议不要使用旧的基础组件 {#oakpal-usage-legacy}

* **密钥**：LegacyFoundationComponentUsage
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

旧的基础组件（即 `/libs/foundation` 下的组件）已在多个 Experience Manager 版本中弃用以支持核心组件。建议不要使用基础组件作为自定义组件的基础（无论是通过叠加还是继承），并且应将这些基础组件转换为相应的核心组件。

[Experience Manager现代化工具](https://opensource.adobe.com/aem-modernize-tools/)可以促进此转换。

### 仅应使用受支持的运行模式名称和排序 {#oakpal-supported-runmodes}

* **密钥**：SupportedRunmode
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 对运行模式名称实施严格的命名策略，并对这些运行模式进行严格的排序。 支持运行模式的列表在文档[部署到Experience Manageras a Cloud Service](/help/implementing/deploying/overview.md#runmodes)中创建，任何偏离此列表的情况都将被视为问题。

### 自定义搜索索引定义节点必须是 `/oak:index` 的直接子节点 {#oakpal-custom-search}

* **密钥**：OakIndexLocation
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）是 `/oak:index` 的直接子节点。 必须移动其他位置的索引才能与 Experience Manager as a Cloud Service 兼容。有关搜索索引的更多信息，请参阅[“内容搜索和索引编制”文档。](/help/operations/indexing.md)

### 自定义搜索索引定义节点的 compatVersion 必须为 2 {#oakpal-custom-search-compatVersion}

* **密钥**：IndexCompatVersion
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 要求自定义搜索索引定义（例如 `oak:QueryIndexDefinition` 类型的节点）必须将 `compatVersion` 属性设置为 `2`。Adobe Experience Manager as a Cloud Service不支持任何其他值。 有关搜索索引的更多信息，请参阅[内容搜索和索引](/help/operations/indexing.md)。

### 自定义搜索索引定义节点的后代节点的类型必须是`nt:unstructured `{#oakpal-descendent-nodes}

* **密钥**：IndexDescendantNodeType
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

当自定义搜索索引定义节点具有无序子节点时，可能会出现难以解决的问题。 为了避免出现此情况，建议 `oak:QueryIndexDefinition` 节点的所有后代节点的类型为 `nt:unstructured`。

### 自定义搜索索引定义节点必须包含一个名为 indexRules 的具有子节点的子节点 {#oakpal-custom-search-index}

* **密钥**：IndexRulesNode
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

正确定义的自定义搜索索引定义节点必须包含一个名为`indexRules`的子节点，而该子节点必须具有至少一个子节点。 有关更多信息，请参阅 [Oak 文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### 自定义搜索索引定义节点必须遵循命名惯例 {#oakpal-custom-search-definitions}

* **密钥**：IndexName
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）必须按照[内容搜索和索引编制](/help/operations/indexing.md)文档中所述的特定模式进行命名。

### 自定义搜索索引定义节点必须使用索引类型 lucene {#oakpal-index-type-lucene}

* **密钥**：IndexType
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2021.2.0（类型和严重性更改于 2021.8.0 版本）

Experience Manager as a Cloud Service 要求自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）必须将 `type` 属性的值设置为 `lucene`。 在迁移到 Experience Manager as a Cloud Service 之前，必须更新使用旧索引类型的索引编制。有关更多信息，请参阅[内容搜索和索引](/help/operations/indexing.md#how-to-use)。

### 自定义搜索索引定义节点不得包含名为 seed 的属性 {#oakpal-property-name-seed}

* **密钥**：IndexSeedProperty
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 禁止自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）包含名为 `seed` 的属性。 在迁移到 Experience Manager as a Cloud Service 之前，必须更新使用此属性的索引编制。 有关更多信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#how-to-use)。

### 自定义搜索索引定义节点不得包含名为 reindex 的属性 {#oakpal-reindex-property}

* **密钥**：IndexReindexProperty
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2021.2.0

Experience Manager as a Cloud Service 禁止自定义搜索索引定义（即 `oak:QueryIndexDefinition` 类型的节点）包含名为 `reindex` 的属性。 在迁移到Experience Manageras a之前，必须更新使用此属性的索引编制
Cloud Service。 有关更多信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md#how-to-use)。

### 自定义DAM资源Lucene节点不得指定`queryPaths` {#oakpal-damAssetLucene-queryPaths}

* **密钥**：IndexDamAssetLucene
* **类型**：错误
* **严重性**：阻断
* **开始版本**：版本 2022.1.0

#### 不合规的代码 {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### 合规的代码 {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### 如果自定义搜索索引定义包含`compatVersion`，则必须将其设置为2 {#oakpal-compatVersion}

* **密钥**：IndexCompatVersion
* **类型**：代码异味
* **严重性**：主要
* **开始版本**：版本 2022.1.0


### 指定`includedPaths`的索引节点还应使用相同的值指定`queryPaths` {#oakpal-included-paths-without-query-paths}

* **键**： IndexIncludedPathsWithoutQueryPaths
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

对于自定义索引，请使用相同的值配置`includedPaths`和`queryPaths`。 如果指定了一个，则另一个必须与它匹配。 但是，`damAssetLucene`的索引（包括其自定义版本）有一个特殊情况。 对于这些情况，仅提供`includedPaths`。

### 在泛型节点类型上指定`nodeScopeIndex`的索引节点也应指定`includedPaths`和`queryPaths` {#oakpal-full-text-on-generic-node-type}

* **Key**： IndexFulltextOnGenericType
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

在诸如`nt:unstructured`或`nt:base`之类的“通用”节点类型上设置`nodeScopeIndex`属性时，还必须指定`includedPaths`和`queryPaths`属性。
节点类型`nt:base`可以视为“通用”，因为所有节点类型都继承自它。 因此，在`nt:base`上设置`nodeScopeIndex`会使其索引存储库中的所有节点。 同样，`nt:unstructured`也视为“通用”，因为存储库中有许多节点属于此类型。

#### 不合规的代码 {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### 合规的代码 {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### 不应覆盖查询引擎的queryLimitReads属性 {#oakpal-query-limit-reads}

* **键**： OverrideOfQueryLimitReads
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

覆盖默认值可能会导致页面读取缓慢，尤其是在添加更多内容时。

### 同一索引的多个活动版本 {#oakpal-multiple-active-versions}

* **Key**： IndexDetectMultipleActiveVersionsOfSameIndex
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

#### 不合规的代码 {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### 合规的代码 {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### 完全自定义的索引定义的名称应符合官方指南 {#oakpal-fully-custom-index-name}

* **Key**： IndexValidFullyCustomName
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

完全自定义索引名称的预期模式为： `[prefix].[indexName]-custom-[version]`。 有关详细信息，请参阅文档[内容搜索和索引](/help/operations/indexing.md)。

### 具有相同索引定义中不同分析值的相同属性 {#oakpal-same-property-different-analyzed-values}

#### 不合规的代码 {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### 合规的代码 {#compliant-code-same-property-different-analyzed-values}

示例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

示例：

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

如果未显式设置分析的属性，则其默认值为false。

### 标记属性 {#tags-property}

* **密钥**： IndexHasValidTagsProperty
* **类型**：代码异味
* **严重性**：轻微
* **开始版本**：版本 2023.1.0

对于特定索引，请确保保留tags属性及其当前值。 虽然向tags属性添加新值是允许的，但删除任何现有值（或同时删除属性）可能会导致意外结果。

### 索引定义节点不得部署在 UI 内容包中 {#oakpal-ui-content-package}

* **键**：IndexNotUnderUIContent
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.6.0

AEM Cloud Service 禁止在 UI 内容包中部署自定义搜索索引定义（类型为 `oak:QueryIndexDefinition` 的节点）。

>[!WARNING]
>
>您应尽快解决此问题，因为它可能会导致从[Cloud Manager 2024年8月版](/help/implementing/cloud-manager/release-notes/current.md)开始的管道故障。

### 类型damAssetLucene的自定义全文索引定义必须正确带有“damAssetLucene”前缀 {#oakpal-dam-asset-lucene}

* **键**：CustomFulltextIndexesOfTheDamAssetCheck
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.6.0

AEM Cloud Service 禁止类型 `damAssetLucene` 的自定义全文索引定义使用除 `damAssetLucene` 之外的任何内容作为前缀。

>[!WARNING]
>
>尽快解决此问题，因为它可能会导致从[Cloud Manager 2024年8月版](/help/implementing/cloud-manager/release-notes/current.md)开始的管道故障。

### 索引定义节点不得包含同名的属性 {#oakpal-index-property-name}

* **键**：DuplicateNameProperty
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.6.0

AEM Cloud Service 禁止自定义搜索索引定义（即，类型为 `oak:QueryIndexDefinition` 的节点）包含同名的属性。

>[!WARNING]
>
>尽快解决此问题，因为它可能会导致从[Cloud Manager 2024年8月版](/help/implementing/cloud-manager/release-notes/current.md)开始的管道故障。

### 禁止自定义某些现成的索引定义 {#oakpal-customizing-ootb-index}

* **键**：RestrictIndexCustomization
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.6.0

AEM Cloud Service 禁止对以下 OOTB 索引进行未经授权的修改：

* `nodetypeLucene`
* `slingResourceResolver`
* `socialLucene`
* `appsLibsLucene`
* `authorizables`
* `pathReference`

>[!WARNING]
>
>尽快解决此问题，因为它可能会导致从[Cloud Manager 2024年8月版](/help/implementing/cloud-manager/release-notes/current.md)开始的管道故障。

### 分析器中标记器的配置应以“tokenizer”名称创建 {#oakpal-tokenizer}

* **键**：AnalyzerTokenizerConfigCheck
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.6.0

AEM Cloud Service禁止在分析器中创建名称不正确的令牌化器。 标记器应始终定义为 `tokenizer`。

>[!WARNING]
>
>尽快解决此问题，因为它可能会导致从[Cloud Manager 2024年8月版](/help/implementing/cloud-manager/release-notes/current.md)开始的管道故障。

### 索引定义的配置不应包含空格 {#oakpal-indexing-definitions-spaces}

* **Key**: PathSpacesCheckKey
* **类型**：改进
* **严重性**：轻微
* **开始版本**：版本 2024.7.0

AEM Cloud Service 禁止创建包含带空格属性的索引定义。
