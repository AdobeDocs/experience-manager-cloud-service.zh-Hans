---
title: 记录
description: 了解如何为中央日志记录服务配置全局参数、各个服务的特定设置或如何请求数据记录。
translation-type: tm+mt
source-git-commit: ae04553b17fcb7b9660f709565faed791a0c930e

---


# 记录{#logging}

AEM作为云服务，是客户包含自定义代码以为其客户群创建独特体验的平台。 考虑到这一点，在云环境上调试自定义代码(尤其是本地开发环境)时，日志记录是一个关键功能。


<!-- ## Global Logging {#global-logging}

[Apache Sling Logging Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) is used to configure the root logger. This defines the global settings for logging in AEM as a Cloud Service:

* the logging level
* the location of the central log file
* the number of versions to be kept
* version rotation; either maximum size or a time interval
* the format to be used when writing the log messages
-->

## AEM作为云服务记录 {#aem-as-a-cloud-service-logging}

AEM作为云服务优惠，您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 单个服务的特定设置

对于本地开发，日志条目将写入文件夹中的本地 `/crx-quickstart/logs` 文件。

在Cloud环境中，开发人员可以通过Cloud Manager下载日志，或使用命令行工具跟踪日志。

>[!NOTE]
>
>以云服务身份登录AEM基于Sling原则。 有关更 [多信息，请参阅](https://sling.apache.org/site/logging.html) Sling日志记录。

## AEM作为云服务Java日志记录 {#aem-as-a-cloud-service-java-logging}

### 标准记事员和作者 {#standard-loggers-and-writers}

> [!IMPORTANT]
> 如果需要，可以自定义这些配置，但标准配置适用于大多数安装。 但是，如果您需要自定义标准日志记录配置，请确保仅在环境上执行该操 `dev` 作。

标准AEM中包含某些记录程序和作者作为云服务安装。

第一种是特殊情况，因为它同时控制 `request` 和日 `access` 志：

* 记录器：

   * Apache Sling可自定义的请求数据记录器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 将有关请求内容的消息写入 `request.log`。

* 链接到：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 将消息写入或 `request.log` 中 `access.log`。

其他对遵循标准配置：

* 记录器：

   * Apache Sling Logging Logger配置

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 将消 `Information` 息写入 `logs/error.log`。

* 指向作者的链接：

   * Apache Sling日志记录编写器配置

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 记录器：

   * Apache Sling Logging Logger Configuration(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 为服 `Warning` 务将消 `../logs/error.log` 息写入 `org.apache.pdfbox`。

* 不链接到特定的Writer，因此将创建并使用具有默认配置的隐式Writer。

**AEM作为云服务HTTP请求日志记录**

此处将注册对AEM WCM和存储库的所有访问请求。

输出示例：

**AEM作为云服务HTTP请求／响应访问日志**

每个访问请求都在此处注册，并随响应一起注册。

输出示例：

**Apache Web Server/调度程序日志记录**

这是用于调试Dispatcher问题的日志。 有关详细信息，请参 [阅调试Apache和Dispatcher配置](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/)。

<!-- Besides the three types of logs present on an AEM as a Cloud Service instance (`request`, `access` and `error` logs) there is another dispatcher/overview.html#debugging-apache-and-dispatcher-configuration.

leftover text from the last breakaway chunk (re dispatcher) -->

就最新实践而言，建议您与AEM中当前存在的配置（作为Cloud Service Maven原型）保持一致。 这些设置为特定环境类型设置不同的日志设置和级别：

* 对于 `local dev` 和 `dev` 环境，将记录器设置为 **DEBUG** 级别 `error.log`
* 对于 `stage`，将记录器设置为 **WARN** 级别 `error.log`
* 对于 `prod`，将记录器设置为 **ERROR** 级别设置为 `error.log`

请查找以下每种配置的示例：

* `dev` 环境:

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="debug"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```


* `stage` 环境:

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="warn"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

* `prod` 环境:

```
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
    org.apache.sling.commons.log.level="error"
    org.apache.sling.commons.log.names="[com.mycompany.myapp]" />
```

### 记事员与个人服务作者 {#loggers-and-writers-for-individual-services}

除了全局日志记录设置之外，AEM作为云服务还允许您为单个服务配置特定设置：

* 特定日志记录级别
* 记录器（提供日志消息的OSGi服务）

这允许您将单个服务的日志消息渠道到单独的文件中。 这在开发或测试过程中特别有用；例如，当您需要特定服务的更高日志级别时。

AEM作为云服务，使用以下方法将日志消息写入文件：

1. OSGi服 **务** （记录器）写入日志消息。
1. 记 **录器会采用此消息** ，并根据您的规范设置其格式。
1. 记 **录编写器** ，将所有这些消息写入您定义的物理文件。

这些元素通过相应元素的以下参数进行链接：

* **记录器（记录器）**

   定义生成消息的服务。

<!-- * **Log File (Logging Logger)**

  Define the physical file for storing the log messages.

  This is used to link a Logging Logger with a Logging Writer. The value must be identical to the same parameter in the Logging Writer configuration for the connection to be made.

* **Log File (Logging Writer)**

  Define the physical file that the log messages will be written to.

  This must be identical to the same parameter in the Logging Writer configuration, or the match will not be made. If there is no match then an implicit Writer will be created with default configuration (daily log rotation).
-->

### 设置日志级别 {#setting-the-log-level}

要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后进行完全重新部署。 由于这不是即时的，因此请务必小心为收到大量流量的生产环境启用详细日志。 将来，可能会有一些机制来更快速地更改日志级别。

>[!NOTE]
>
> 要执行下面列出的配置更改，您需要在本地开发环境上创建这些更改，然后将其作为云服务实例推送到AEM。 有关如何执行此操作的详细信息，请参 [阅将AEM部署为云服务](/help/implementing/deploying/overview.md)。

**激活调试日志级别**

>[!WARNING]
>
> 全局激活DEBUG日志级别将生成大量难以筛选的信息。 建议仅为需要调试的服务启用它。 有关详细信息，请参 [阅Loggers和Writers for Individual Services](logging.md#loggers-and-writers-for-individual-services)。

默认日志级别为INFO，即DEBUG消息未记录。
要激活调试日志级别，请设置

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

要调试的属性。 不要将DEBUG日志级别的日志保留得比必需的时间长，因为它会生成大量日志。
调试文件中的一行通常与DEBUG开始，然后提供日志级别、安装程序操作和日志消息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作已失败。 安装将继续进行，但CRX的某部分安装不正确，将无法正常工作。 |
| 2 | 警告 | 该操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 该操作已成功。 |

### 创建您自己的伐木工和作者 {#creating-your-own-loggers-and-writers}

您可以定义自己的记录器／写入器对：

1. 创建工厂配置Apache Sling日志记录 [器配置的新实例](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based)。

   1. 指定记录器。

<!-- 1. Create a new instance of the Factory Configuration [Apache Sling Logging Writer Configuration](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based).

    1. Specify the Log File - this must match that specified for the Logger.
    1. Configure the other parameters as required. -->

### 配置日志记录 {#configure-logging}

>[!NOTE]
>
>使用Adobe Experience Manager时，可以通过多种方法管理此类服务的配置设置。

在某些情况下，您可能希望创建具有不同日志级别的自定义日志。 您可以通过以下方式在存储库中执行此操作：

1. 如果项目尚未存在，请为项目创建新的配置文 `sling:Folder`件夹() `/apps/<*project-name*>/config`。
1. 在下 `/apps/<*project-name*>/config`面，为新的Apache Sling Logging Logger配置创建一个节点：

   * 名称： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` （因为这是记录器）

      其中， `<*identifier*>` 将替换为您（必须）输入以标识实例的自由文本（您不能忽略此信息）。

      例如，`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但最好是使其与众不同 `<*identifier*>` 。

<!-- 1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: String

      Value: specify the Log File; for example, `logs/myLogFile.log`

    * Name: `org.apache.sling.commons.log.names`

      Type: String[] (String + Multi)

      Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`
        * `org.apache.felix`
        * `com.day`

    * Name: `org.apache.sling.commons.log.level`

      Type: String

      Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern`

          Type: `String`

          Value: specify the pattern of the log message as required; for example,

          `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` supports up to six arguments.

   >
   >
   >{0} The timestamp of type `java.util.Date`
   >{1} the log marker
   >{2} the name of the current thread
   >{3} the name of the logger
   >{4} the log level
   >{5} the log message

   >
   >
   >If the log call includes a `Throwable` the stacktrace is appended to the message.

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names must have a value.

   >[!NOTE]
   >
   >Log writer paths are relative to the `crx-quickstart` location.
   >
   >
   >Therefore, a log file specified as:
   >
   >
   >`logs/thelog.log`

   >
   >
   >writes to:
   >
   >
   >`` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log`.
   >
   >
   >And a log file specified as:
   >
   >
   >`../logs/thelog.log`

   >
   >
   >writes to a directory:
   >
   >
   >` <*cq-installation-dir*>/logs/`
   >``(i.e. next to ` `<*cq-installation-dir*>/`crx-quickstart/`)
 -->

<!-- open question: see if we need to leave the above warning note in place, but adjust it so that it doesn't mention filenames -->

<!-- 1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer).

   >[!CAUTION]
   >
   >A new Logging Writer Configuration is only required when the existing default is not suitable.

   >
   >
   >If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.

   Under `/apps/<*project-name*>/config`, create a node for the new `Apache Sling Logging Writer` Configuration:

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer)

      As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`

    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   >Although not a technical requirement, it is advisable to make `<*identifier*>` unique.

   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`

      Type: `String`

      Value: specify the Log File so that it matches the file specified in the Logger;

      for this example, `../logs/myLogFile.log`.

    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number`

          Type: `Long`

          Value: specify the number of log files you want kept; for example, `5`

        * Name: `org.apache.sling.commons.log.file.size`

          Type: `String`

          Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` controls the rotation of the log file by setting either:
   >
   >* a maximum file size
   >* a time/date schedule
   >
   >to indicate when a new file will be created (and the existing file renamed according to the name pattern).
   >
   >* A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - `KB`, `MB`, or `GB` (case is ignored).
   >* A time/date schedule can be specified as a `java.util.SimpleDateFormat` pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).
   >
   >The default is '.'yyyy-MM-dd (for daily log rotation).
   >
   >So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.
   >
   >      | `'.'yyyy-MM` |Rotation at the beginning of each month |
   >      |---|---|
   >      | `'.'yyyy-ww` |Rotation at the first day of each week (depends on the locale). |
   >      | `'.'yyyy-MM-dd` |Rotation at midnight each day. |
   >      | `'.'yyyy-MM-dd-a` |Rotation at midnight and midday of each day. |
   >      | `'.'yyyy-MM-dd-HH` |Rotation at the top of every hour. |
   >      | `'.'yyyy-MM-dd-HH-mm` |Rotation at the beginning of every minute. |
   >
   >      Note: When specifying a time/date:
   >      1. You should "escape" literal text within a pair of single quotes (' ');
   >      this is to avoid certain characters being interpreted as pattern letters.
   >      1. Only use characters allowed for a valid file name anywhere in the option.

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`. -->

Felix Console还提供有关Sling Log支持的信息，网址为 `../system/console/slinglog`;例 `https://localhost:4502/system/console/slinglog`如。draf

## 访问和管理日志 {#manage-logs}

有关如何访问和管理日志的信息，请参阅 [Cloud Manager文档](/help/implementing/cloud-manager/manage-logs.md)。