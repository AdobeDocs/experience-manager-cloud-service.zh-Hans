---
title: 自定义代码质量规则
description: 本页介绍作为[代码质量测试]的一部分由Cloud Manager执行的自定义代码质量规则。 这些建议基于AEM工程部门的最佳实践。
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '3493'
ht-degree: 3%

---

# 自定义代码质量规则 {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="自定义代码质量规则"
>abstract="本页介绍在代码质量测试中由Cloud Manager执行的自定义代码质量规则。 这些建议基于AEM工程部门的最佳实践。"

本页介绍由Cloud Manager作为 [代码质量测试。](/help/implementing/cloud-manager/code-quality-testing.md) 这些建议基于AEM工程部门的最佳实践。

>[!NOTE]
>
>此处提供的代码示例仅供说明性用途。 看声呐 [概念文档](https://docs.sonarqube.org/7.4/user-guide/concepts/) 了解SonarQube概念和质量规则。

## SonarQube规则 {#sonarqube-rules}

以下部分详细介绍由Cloud Manager执行的SonarQube规则。

### 不要使用潜在危险的功能 {#do-not-use-potentially-dangerous-functions}

* **键**:CQRules:CWE-676
* **类型**:漏洞
* **严重性**:主要
* **自**:版本2018.4.0

方法 `Thread.stop()` 和 `Thread.interrupt()` 可能会产生难以重现的问题，并且在某些情况下会产生安全漏洞。 应严格监控和验证其使用情况。 总的来说，传递信息是实现类似目标的一种更安全的方式。

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

### 请勿使用可能由外部控制的字符串格式 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **键**:CQRules:CWE-134
* **类型**:漏洞
* **严重性**:主要
* **自**:版本2018.4.0

使用来自外部源（如请求参数或用户生成的内容）的格式字符串可以使应用程序暴露于拒绝服务攻击。 在某些情况下，格式字符串可能受外部控制，但仅允许来自受信任源。

#### 不符合代码 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP请求应始终具有套接字和连接超时 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **键**:CQRules:ConnectionTimeoutMechanism
* **类型**:错误
* **严重性**:关键
* **自**:版本2018.6.0

在从AEM应用程序内执行HTTP请求时，必须确保配置正确的超时，以避免不必要的线程消耗。 遗憾的是，两个Java默认HTTP客户端(`java.net.HttpUrlConnection`)，且常用的Apache HTTP组件客户端为从不超时，因此必须明确设置超时。 此外，作为最佳实践，这些超时不应超过60秒。

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

### 应始终关闭ResourceResolver对象 {#resourceresolver-objects-should-always-be-closed}

* **键**:CQRules:CQBP-72
* **类型**:代码气味
* **严重性**:主要
* **自**:版本2018.4.0

`ResourceResolver` 从 `ResourceResolverFactory` 消耗系统资源。 尽管已采取措施，在 `ResourceResolver` 不再使用，则更有效地显式关闭任何已打开的 `ResourceResolver` 对象 `close()` 方法。

一个相对常见的误解是 `ResourceResolver` 不应明确关闭使用现有JCR会话创建的对象，否则将关闭基础JCR会话。 情况并非如此。 无论 `ResourceResolver` 打开时，应该在不再使用时将其关闭。 自 `ResourceResolver` 实施 `Closeable` 界面中，还可以使用 `try-with-resources` 语法，而不是显式调用 `close()`.

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

* **键**:CQRules:CQBP-75
* **类型**:代码气味
* **严重性**:主要
* **自**:版本2018.4.0

如 [Sling文档](http://sling.apache.org/documentation/the-sling-engine/servlets.html)，不建议根据路径绑定servlet。 路径绑定的Servlet无法使用标准JCR访问控制，因此需要额外的安全严格性。 建议在存储库中创建节点并按资源类型注册Servlet，而不是使用路径绑定Servlet。

#### 不符合代码 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕获的异常应记录或引发，而不应同时记录或引发 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **键**:CQRules:CQBP-44—CatchAndEitherLogOrThrow
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

通常，例外应只记录一次。 多次记录异常可能会造成混淆，因为不清楚异常发生的次数。 导致这种情况的最常见模式是记录并引发捕获异常。

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

### 避免Log语句后跟Throw语句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **键**:CQRules:CQBP-44—ConcentiveLogAndThrow
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

要避免的另一种常见模式是，记录消息，然后立即引发异常。 这通常表示异常消息将在日志文件中重复出现。

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

### 在处理GET或HEAD请求时避免在信息处记录 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **键**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **类型**:代码气味
* **严重性**:次要

通常，应使用“信息”日志级别来标定重要操作，并且默认情况下，AEM配置为在“信息”级别或更高级别登录。 GET和HEAD方法只应是只读操作，因此不构成重要操作。 响应GET或HEAD请求在“信息”级别进行日志记录可能会产生严重的日志噪声，从而更难识别日志文件中的有用信息。 处理GET或HEAD请求时的日志记录应位于出现问题时的“警告”或“错误”级别，或者位于“调试”或“TRACE”级别（如果更深入的故障诊断信息会有所帮助）。

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

* **键**:CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

作为最佳实践，日志消息应提供有关应用程序中发生异常的位置的上下文信息。 虽然上下文也可以通过使用堆栈跟踪来确定，但一般来说，日志消息将更易于阅读和理解。 因此，在记录异常时，将异常的消息用作日志消息是一种不好的做法。 异常消息将包含错误内容，而日志消息应用于告知日志阅读器应用程序在异常发生时正在执行的操作。 例外消息仍将被记录。 通过指定您自己的消息，日志将更便于理解。

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

### 在捕获块中登录应处于警告或错误级别 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **键**:CQRules:CQBP-44—WrongLogLevelInCatchBlock
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

如名称所示，在特殊情况下应始终使用Java例外。 因此，当捕获到异常时，务必确保日志消息记录在适当的级别（“警告”或“错误”）。 这可确保这些消息在日志中正确显示。

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

* **键**:CQRules:CQBP-44—ExceptionPrintStackTrace
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

如上所述，了解日志消息时，上下文至关重要。 使用 `Exception.printStackTrace()` 仅导致堆栈跟踪输出到标准错误流，从而丢失所有上下文。 此外，在诸如AEM的多线程应用程序中，如果使用此方法并行打印多个例外，则其堆栈迹线可能会重叠，这会产生严重的混淆。 应仅通过日志记录框架记录例外。

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

* **键**:CQRules:CQBP-44—LogLevelConsolePrinters
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

登录AEM应始终通过日志记录框架(SLF4J)完成。 直接输出到标准输出或标准错误流会丢失由日志记录框架提供的结构和上下文信息，并且在某些情况下可能导致性能问题。

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

* **键**:CQRules:CQBP-71
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2018.4.0

通常，以开头的路径 `/libs` 和 `/apps` 不应进行硬编码，因为它们引用的路径最常存储为相对于Sling搜索路径的路径，该路径设置为 `/libs,/apps` 默认情况下。 使用绝对路径可能会引入一些细微的缺陷，这些缺陷仅在项目生命周期的后期才会出现。

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

### 不应使用Sling调度程序 {#sonarqube-sling-scheduler}

* **键**:CQRules:AMSCORE-554
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

Sling调度程序不得用于需要保证执行的任务。 Sling计划作业可确保执行，并且更适合群集和非群集环境。

请参阅 [Apache Sling事件和作业处理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 了解有关如何在群集环境中处理Sling作业的更多信息。

### AEM已弃用的API不应使用 {#sonarqube-aem-deprecated}

* **键**:AMSCORE-553
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

AEM API表面处于不断修订的状态，可识别不鼓励使用并因此被视为已弃用的API。

在很多情况下，这些API会使用标准Java被弃用 `@Deprecated` 注释，因此，标识为 `squid:CallToDeprecatedMethod`.

但是，在某些情况下，AEM上下文中已弃用API，但在其他上下文中可能不会弃用API。 此规则标识此第二类。


## OakPAL内容规则 {#oakpal-rules}

以下部分详细介绍了Cloud Manager执行的OakPAL检查。

>[!NOTE]
>
>OakPAL是一个框架，它使用独立的Oak存储库来验证内容包。 它由AEM Partner和2019年AEM Rockstar北美奖得主开发。

### 客户不应实施或扩@ProviderType带有注释的产品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **键**:CQBP-84
* **类型**:错误
* **严重性**:关键
* **自**:版本2018.7.0

AEM API包含Java接口和类，这些接口和类仅用于由自定义代码使用，但不能实现。 例如，界面 `com.day.cq.wcm.api.Page` 仅由AEM实施。

当将新方法添加到这些接口时，这些附加方法不会影响使用这些接口的现有代码，因此，向这些接口添加新方法被认为是向后兼容的。 但是，如果自定义代 码实现了 其中一个接口，则该自定义代码会给客户带来向后兼容性风险。

仅打算由AEM实现的接口和类将添加注释 `org.osgi.annotation.versioning.ProviderType` 或在某些情况下是类似的旧版注释 `aQute.bnd.annotation.ProviderType`. 此规则用于标识实现此类接口或通过自定义代码扩展类的情况。

#### 不符合代码 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 自定义Lucene Oak索引必须具有Tika配置 {#oakpal-indextikanode}

* **键**:IndexTikaNode
* **类型**:错误
* **严重性**:阻止程序
* **自**:2021.8.0

多个现成的AEM Oak索引包含tika配置，且这些索引的自定义必须包含tika配置。 此规则检查 `damAssetLucene`, `lucene`和 `graphqlConfig` 如果 `tika`  节点缺失或 `tika` 节点缺少名为的子节点 `config.xml`.

请参阅 [索引文档](/help/operations/indexing.md#preparing-the-new-index-definition) 有关自定义索引定义的详细信息。

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

* **键**:IndexAsyncProperty
* **类型**:错误
* **严重性**:阻止程序
* **自**:2021.8.0

类型的Oak索引 `lucene` 必须始终异步编入索引。 如果不这样做，可能会导致系统不稳定。 有关Lucene索引结构的详细信息，请参阅 [Oak文档。](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

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

* **键**:IndexDamAssetLucene
* **类型**:错误
* **严重性**:阻止程序
* **自**:2021.6.0

为了使资产搜索在AEM Assets中正常工作，需自定义 `damAssetLucene` Oak索引必须遵循一组特定于此索引的准则。 此规则检查索引定义是否必须具有名为的多值属性 `tags` 包含值 `visualSimilaritySearch`.

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

* **键**:UnbandedPath
* **类型**:错误
* **严重性**:关键
* **自**:版本2019.6.0

长期以来， `/libs` 客户应将AEM内容存储库中的内容树视为只读。 修改下的节点和属性 `/libs` 会对主要和次要更新造成重大风险。 对 `/libs` 只应通过官方渠道进行Adobe。

### 包不应包含重复的OSGi配置 {#oakpal-package-osgi}

* **键**:DuplicateOsgiConfigurations
* **类型**:错误
* **严重性**:主要
* **自**:版本2019.6.0

复杂项目中出现的常见问题是多次配置同一OSGi组件。 这会造成一个模糊，即哪种配置适用。 此规则“支持运行模式”，因为它将仅识别在同一运行模式或运行模式组合中多次配置同一组件的问题。

>[!NOTE]
>
>此规则将产生在多个包中定义相同配置（位于同一路径）的问题，包括在同一包的整个列表中复制相同包的情况。
>
>例如，如果内部版本生成名为的包 `com.myco:com.myco.ui.apps` 和 `com.myco:com.myco.all` where `com.myco:com.myco.all` 嵌入 `com.myco:com.myco.ui.apps`，然后是 `com.myco:com.myco.ui.apps` 将被报告为重复项。
>
>这通常是不遵循 [内容包结构指南。](/help/implementing/developing/introduction/aem-project-content-package-structure.md). 在此特定示例中，包 `com.myco:com.myco.ui.apps` 缺少 `<cloudManagerTarget>none</cloudManagerTarget>` 属性。

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

* **键**:ConfigAndInstallShouldOnlyContainOsgiNodes
* **类型**:错误
* **严重性**:主要
* **自**:版本2019.6.0

出于安全原因，包含 `/config/` 和 `/install/` 只能由AEM中的管理用户读取，且只能用于OSGi配置和OSGi包。 将其他类型的内容放在包含这些区段的路径下会导致应用程序行为，这些行为在管理用户和非管理用户之间会无意中发生变化。

一个常见问题是使用名为 `config` 在组件对话框中或指定用于内联编辑的富文本编辑器配置时。 要解决此问题，应将违规节点重命名为兼容名称。 对于富文本编辑器配置，请使用 `configPath` 属性 `cq:inplaceEditing` 节点来指定新位置。

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

* **键**:包重叠
* **类型**:错误
* **严重性**:主要
* **自**:版本2019.6.0

与 [包不应包含重复的OSGi配置规则，](#oakpal-package-osgi) 在多个单独的内容包写入同一节点路径的复杂项目中，这是一个常见的问题。 虽然可以使用内容包依赖关系确保结果一致，但最好避免完全重叠。

### 默认创作模式不应为经典UI {#oakpal-default-authoring}

* **键**:ClassicUIAuthoringMode
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

OSGi配置 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 在AEM中定义默认的创作模式。 因为 [经典UI自AEM 6.4起已弃用，](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 现在，将默认创作模式配置为经典UI后，会引发问题。

### 具有对话框的组件应具有触屏UI对话框 {#oakpal-components-dialogs}

* **键**:ComponentWithOnlyClassicUIDialog
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

具有经典UI对话框的AEM组件应始终具有相应的触屏UI对话框，以提供最佳创作体验，并与不支持经典UI的Cloud Service部署模型兼容。 此规则验证以下情况：

* 具有经典UI对话框的组件(即 `dialog` 子节点)必须具有相应的触屏UI对话框(即 `cq:dialog` 子节点)。
* 具有经典UI设计对话框的组件(例如， `design_dialog` 节点)必须具有相应的触屏UI设计对话框(即 `cq:design_dialog` 子节点)。
* 同时具有经典UI对话框和经典UI设计对话框的组件必须同时具有相应的触屏UI对话框和相应的触屏UI设计对话框。

AEM现代化工具文档提供了有关如何将组件从经典UI转换为触屏UI的文档和工具。 请参阅 [AEM现代化工具文档](https://opensource.adobe.com/aem-modernize-tools/) 以了解更多详细信息。

### 包不应混合使用可变和不可变内容 {#oakpal-packages-immutable}

* **键**:ImmutableMutableMixedPackage
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

为了与Cloud Service部署模型兼容，单个内容包必须包含存储库不可变区域(即 `/apps` 和 `/libs`)或可变区域(即 `/apps` 或 `/libs`)，但不能两者兼有。 例如，包中同时包含这两者 `/apps/myco/components/text and /etc/clientlibs/myco` 与Cloud Service不兼容，将导致报告问题。

>[!NOTE]
>
>规则 [客户包不应在/libs下创建或修改节点](#oakpal-customer-package) 始终适用。

请参阅 [AEM项目结构](/help/implementing/developing/introduction/aem-project-content-package-structure.md) 以了解更多详细信息。

### 不应使用反向复制代理 {#oakpal-reverse-replication}

* **键**:反向复制
* **类型**:代码气味/Cloud Service兼容性
* **严重性**:次要
* **自**:版本2020.5.0

在Cloud Service部署中不提供对反向复制的支持，如AEM as a Cloud Service的 [发行说明。](/help/release-notes/aem-cloud-changes.md#replication-agents)

使用反向复制的客户应与Adobe联系以获取其他解决方案。

### 启用代理的客户端库中包含的资源应位于名为“Resources”的文件夹中 {#oakpal-resources-proxy}

* **键**:ClientlibProxyResource
* **类型**:错误
* **严重性**:次要
* **自**:版本2021.2.0

AEM客户端库可能包含静态资源，如图像和字体。 如文档所述 [使用预处理器，](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) 使用代理客户端库时，这些静态资源必须包含在名为的子文件夹中 `resources` 以便在发布实例上有效引用。

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

* **键**:CloudServiceIncomplatibleWorkflowProcess
* **类型**:错误
* **严重性**:主要
* **自**:版本2021.2.0

随着在AEMas a Cloud Service上为资产处理转移到资产微服务，在AEM的内部部署版和AMS版本中使用的多个工作流进程变得不支持或不必要。

中的迁移工具 [AEM Assetsas a Cloud ServiceGitHub存储库](https://github.com/adobe/aem-cloud-migration) 可用于在迁移到AEMas a Cloud Service期间更新工作流模型。

### 不鼓励使用静态模板，转而使用可编辑的模板 {#oakpal-static-template}

* **键**:StaticTemplateUsage
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

尽管静态模板的使用在AEM项目中一直非常常见，但是强烈建议使用可编辑的模板，因为它们提供了最大的灵活性，并支持静态模板中不存在的其他功能。 有关详细信息，请参阅此文档 [页面模板。](/help/implementing/developing/components/templates.md)

从静态模板迁移到可编辑的模板，可以使用 [AEM现代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 不鼓励使用旧版基础组件 {#oakpal-usage-legacy}

* **键**:旧版FoundationComponentUsage
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

旧版基础组件(即 `/libs/foundation`) [已弃用多个AEM版本](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html) 支持核心组件。 不建议将基础组件用作自定义组件的基础（无论是通过叠加还是继承），并且应该将其转换为相应的核心组件。

可通过 [AEM现代化工具。](https://opensource.adobe.com/aem-modernize-tools/)

### 应仅使用支持的Runmode名称和排序 {#oakpal-supported-runmodes}

* **键**:受支持的运行模式
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service对运行模式名称强制实施严格的命名策略，并对这些运行模式实施严格的排序。 可在文档中找到支持的运行模式列表 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md#runmodes) 任何偏离都将被确定为问题。

### 自定义搜索索引定义节点必须是/oak:index的直接子节点 {#oakpal-custom-search}

* **键**:OakIndexLocation
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service要求自定义搜索索引定义（即，类型的节点） `oak:QueryIndexDefinition`)是 `/oak:index`. 必须移动其他位置的索引才能与AEMas a Cloud Service兼容。 有关搜索索引的详细信息，请参阅此文档 [内容搜索和索引。](/help/operations/indexing.md)

### 自定义搜索索引定义节点必须具有2的比较版本 {#oakpal-custom-search-compatVersion}

* **键**:IndexCompatVersion
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service要求自定义搜索索引定义（即，类型的节点） `oak:QueryIndexDefinition`)必须具有 `compatVersion` 属性设置为 `2`. AEM as a Cloud Service不支持任何其他值。 有关搜索索引的详细信息，请参阅 [内容搜索和索引。](/help/operations/indexing.md)

### 自定义搜索索引定义节点的子节点必须为Nt:Unstructured类型 {#oakpal-descendent-nodes}

* **键**:IndexDescendantNodeType
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

如果自定义搜索索引定义节点具有无序的子节点，则可能会发生难以排除的问题。 为避免出现这种情况，建议 `oak:QueryIndexDefinition` 节点类型 `nt:unstructured`.

### 自定义搜索索引定义节点必须包含一个名为indexRules的子节点，该子节点具有子节点 {#oakpal-custom-search-index}

* **键**:IndexRulesNode
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

正确定义的自定义搜索索引定义节点必须包含名为 `indexRules` 这个国家至少要有一个孩子。 有关详细信息，请参阅 [Oak文档。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### 自定义搜索索引定义节点必须遵循命名约定 {#oakpal-custom-search-definitions}

* **键**:IndexName
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service要求自定义搜索索引定义(即，类型的节点 `oak:QueryIndexDefinition`)必须按照文档中描述的特定模式命名 [内容搜索和索引。](/help/operations/indexing.md)

### 自定义搜索索引定义节点必须使用索引类型lucene  {#oakpal-index-type-lucene}

* **键**:IndexType
* **类型**:错误
* **严重性**:阻止程序
* **自**:版本2021.2.0（2021.8.0年更改了类型和严重性）

AEMas a Cloud Service要求自定义搜索索引定义（即，类型的节点） `oak:QueryIndexDefinition`)具有 `type` 值设置为的属性 `lucene`. 在迁移到AEMas a Cloud Service之前，必须更新使用旧索引类型的索引。 请参阅文档 [内容搜索和索引](/help/operations/indexing.md#how-to-use) 以了解更多信息。

### 自定义搜索索引定义节点不得包含名为Seed的属性 {#oakpal-property-name-seed}

* **键**:IndexSeedProperty
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service禁止自定义搜索索引定义(即，节点类型 `oak:QueryIndexDefinition`)来自包含名为 `seed`. 在迁移到AEMas a Cloud Service之前，必须更新使用此属性的索引。 查看文档 [内容搜索和索引](/help/operations/indexing.md#how-to-use) 以了解更多信息。

### 自定义搜索索引定义节点不得包含名为reindex的属性 {#oakpal-reindex-property}

* **键**:IndexReindexProperty
* **类型**:代码气味
* **严重性**:次要
* **自**:版本2021.2.0

AEMas a Cloud Service禁止自定义搜索索引定义(即，节点类型 `oak:QueryIndexDefinition`)来自包含名为 `reindex`. 在迁移到AEMas a Cloud Service之前，必须更新使用此属性的索引。 查看文档 [内容搜索和索引](/help/operations/indexing.md#how-to-use) 以了解更多信息。
