---
title: 记录
description: 了解如何为中央日志记录服务配置全局参数、各个服务的特定设置或如何请求数据记录。
translation-type: tm+mt
source-git-commit: 0e4de19f4ae53414d90f6979980f3ce79f49394d

---


# 记录{#logging}

AEM作为云服务优惠，您可以配置：

* 中央日志记录服务的全局参数
* 请求数据记录；请求信息的专用日志记录配置
* 具体服务设置；例如，单个日志文件和日志消息的格式

对于本地开发，日志条目将写入文件夹中的本地 `/crx-quickstart/logs` 文件。

在Cloud环境中，开发人员可以通过Cloud Manager下载日志，或使用命令行工具跟踪日志。

>[!NOTE]
>
>以云服务身份登录AEM基于Sling原则。 有关更 [多信息，请参阅](https://sling.apache.org/site/logging.html) Sling日志记录。

## 全局日志记录 {#global-logging}

[Apache Sling日志记录配置](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based) (Apache Sling Logging Configuration)用于配置根记录器。 这为以云服务身份登录AEM定义了全局设置：

* 记录级别
* 中央日志文件的位置
* 要保存的版本数
* 版本旋转；最大大小或时间间隔
* 编写日志消息时使用的格式

## 记事员与个人服务作者 {#loggers-and-writers-for-individual-services}

除了全局日志记录设置之外，AEM作为云服务还允许您为单个服务配置特定设置：

* 特定日志记录级别
* 单个日志文件的位置
* 要保存的版本数
* 版本旋转；最大大小或时间间隔
* 编写日志消息时使用的格式
* 记录器（提供日志消息的OSGi服务）

这允许您将单个服务的日志消息渠道到单独的文件中。 这在开发或测试过程中特别有用；例如，当您需要特定服务的更高日志级别时。

AEM作为云服务，使用以下方法将日志消息写入文件：

1. OSGi服 **务** （记录器）写入日志消息。
1. 记 **录器会采用此消息** ，并根据您的规范设置其格式。
1. 记 **录编写器** ，将所有这些消息写入您定义的物理文件。

这些元素通过相应元素的以下参数进行链接：

* **记录器（记录器）**

   定义生成消息的服务。

* **日志文件（记录器）**

   定义用于存储日志消息的物理文件。

   这用于将记录器与记录写入器链接。 该值必须与要建立连接的记录写入程序配置中的相同参数相同。

* **日志文件（记录编写器）**

   定义将写入日志消息的物理文件。

   这必须与“记录编写器”配置中的相同参数相同，否则将不匹配。 如果没有匹配项，则将使用默认配置（每日日志旋转）创建隐式编写器。

### 标准记事员和作者 {#standard-loggers-and-writers}

标准AEM中包含某些记录程序和作者作为云服务安装。

第一种是特殊情况，因为它同时控制文件 `request.log` 和文 `access.log` 件：

* 记录器：

   * Apache Sling可自定义的请求数据记录器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 将有关请求内容的消息写入 `request.log`。

* 链接到：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 将消息写入或 `request.log` 中 `access.log`。

如果需要，可以自定义这些配置，但标准配置适用于大多数安装。

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

* 不链接到特定的Writer，因此将创建并使用具有默认配置（每日日志旋转）的隐式Writer。

## 设置日志级别 {#setting-the-log-level}

要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后进行完全重新部署。 由于这不是即时的，因此请务必小心为收到大量流量的生产环境启用详细日志。 将来，可能会有一些机制来更快速地更改日志级别。

> [!NOTE]
> 
> 要执行下面列出的配置更改，您需要在本地开发环境上创建这些更改，然后将其作为云服务实例推送到AEM。 有关如何执行此操作的详细信息，请参 [阅将AEM部署为云服务](/help/implementing/deploying/overview.md)。

### 激活调试日志级别 {#activating-the-debug-log-level}

> [!WARNING]
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

   1. 指定日志文件。
   1. 指定记录器。
   1. 根据需要配置其他参数。

1. 创建工厂配置Apache Sling日志记录编写 [器配置的新实例](https://sling.apache.org/documentation/development/logging.html#user-configuration---osgi-based)。

   1. 指定日志文件——该文件必须与为记录器指定的文件匹配。
   1. 根据需要配置其他参数。

### 创建自定义日志文件 {#create-a-custom-log-file}

>[!NOTE]
>
>使用Adobe Experience Manager时，可以通过多种方法管理此类服务的配置设置。

在某些情况下，您可能希望创建具有不同日志级别的自定义日志文件。 您可以通过以下方式在存储库中执行此操作：

1. 如果项目尚未存在，请为项目创建新的配置文 `sling:Folder`件夹() `/apps/<*project-name*>/config`。
1. 在下 `/apps/<*project-name*>/config`面，为新的Apache Sling Logging Logger配置创建一个节点：

   * 名称： `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` （因为这是记录器）

      其中， `<*identifier*>` 将替换为您（必须）输入以标识实例的自由文本（您不能忽略此信息）。

      例如，`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   >
   >虽然不是技术要求，但最好是使其与众不同 `<*identifier*>` 。

1. 在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型：字符串

      值：指定日志文件；例如， `logs/myLogFile.log`

   * 名称: `org.apache.sling.commons.log.names`

      类型：字符串[] （字符串+多个）

      值：指定记录器要为其记录消息的OSGi服务；例如，以下所有内容：

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名称: `org.apache.sling.commons.log.level`

      类型：字符串

      值：指定所需的日志级 `debug`别( `info`、 `warn` 或 `error`);示例 `debug`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.pattern`

         类型: `String`

         值：根据需要指定日志消息的模式；例如，

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` 最多支持六个参数。

   >{0}类型的时间戳 `java.util.Date`
   >
   >{1} log marker{2} the name of current thread{3} the logger{4} the log level{5} the log message

   >如果日志调用包括堆栈 `Throwable` 跟踪，则该堆栈跟踪将附加到消息。

   >[!CAUTION]
   org.apache.sling.commons.log.names必须具有值。

   >[!NOTE]
   日志写入程序路径是相对于位置 `crx-quickstart` 的。
   因此，日志文件指定为：
   `logs/thelog.log`

   >写入：
   `` ` ` `<*cq-installation-dir*>/``crx-quickstart/logs/thelog.log。
   以及指定为：
   `../logs/thelog.log`

   >写入到目录：
   ` <*cq-installation-dir*>/logs/`
&quot;(即，在 ` `&lt;*cq-installation-dir*`crx-quickstart/`>/旁)

1. 仅当需要新的Writer时（即，配置与默认Writer不同），才需要执行此步骤。

   >[!CAUTION]
   仅当现有默认值不适合时，才需要新的日志记录写入程序配置。

   >如果未配置显式编写器，则系统将根据默认值自动生成隐式编写器。

   在 `/apps/<*project-name*>/config`下，为新配置创建一个 `Apache Sling Logging Writer` 节点：

   * 名称：( `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` 作者为作者)

      与记录器一样， `<*identifier*>` 将替换为您（必须）输入用来标识实例的自由文本（您不能忽略此信息）。 例如，`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 类型: `sling:OsgiConfig`
   >[!NOTE]
   虽然不是技术要求，但最好是使其与众不同 `<*identifier*>` 。

   在此节点上设置以下属性：

   * 名称: `org.apache.sling.commons.log.file`

      类型: `String`

      值：指定日志文件，使其与记录器中指定的文件匹配；

      例如， `../logs/myLogFile.log`

   * 根据需要配置其他参数：

      * 名称: `org.apache.sling.commons.log.file.number`

         类型: `Long`

         值：指定要保留的日志文件数；例如， `5`

      * 名称: `org.apache.sling.commons.log.file.size`

         类型: `String`

         值：根据大小／日期指定控制文件旋转的要求；例如， `'.'yyyy-MM-dd`
   >[!NOTE]
   `org.apache.sling.commons.log.file.size` 通过设置以下任一项来控制日志文件的旋转：
   * 最大文件大小
   * 时间／日期计划
   以指示何时创建新文件（以及根据名称模式重命名的现有文件）。
   * 可以用数字指定大小限制。 如果未提供大小指示符，则将其视为字节数，或者您可以添加大小指示符 `KB`- `MB`、 `GB` 或（忽略大小写）。
   * 时间／日期计划可以指定为模 `java.util.SimpleDateFormat` 式。 这定义了文件旋转的时间段；还有附加到旋转文件（用于标识）的后缀。
   默认为 &#39;.&#39;yyyy-MM-dd（用于日志旋转）。
   例如，在2010年1月20日午夜（或者，当这之后的第一条日志消息准确无误时）,../logs/error.log将更名为../logs/error.log.2010-01-20。 1月21日的日志记录将输出到../logs/error.log（新的和空的），直到在下一天的更改时滚过。
       | `&#39;.&#39;yyyy-MM`|每月初的轮换|
    |—|—|
    |“”yyyy-ww`|每周第一天的旋转（取决于区域设置）。 |
       | `&#39;.&#39;yyyy-MM-dd`每天午夜时分旋转。 |
       | `&#39;.&#39;yyyy-MM-dd-a每天午夜和中午的轮换。 |
       | `&#39;.&#39;yyyy-MM-dd-HH`每小时的顶部旋转。 |
       | `&#39;.&#39;yyyy-MM-dd-HH-mm`每分钟开始时的旋转。 |
 注     
    意：指定时间／日期时：
      1. 您应该在单引号(&#39; &#39;)中“转义”文本；
  这     是为了避免某些字符被解释为模式字母。
       1. 在选项中的任意位置仅使用允许用于有效文件名的字符。
   

1. 使用所选工具阅读新的日志文件。

   此示例创建的日志文件将为 `../crx-quickstart/logs/myLogFile.log`。

Felix Console还提供有关Sling Log支持的信息，网址为 `../system/console/slinglog`;例如 `https://localhost:4502/system/console/slinglog`,