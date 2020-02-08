---
title: 将 AEM Assets 与 InDesign Server 集成
description: 了解如何将AEM资产与InDesign server集成。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 将 AEM Assets 与 InDesign Server 集成 {#integrating-aem-assets-with-indesign-server}

Adobe Experience Manager(AEM)资产使用：

* 用于分配特定处理任务负载的代理。 代理是与代理Worker通信以完成特定任务的AEM实例，其他AEM实例则用于传送结果。
* 用于定义和管理特定任务的代理Worker。
这些任务可以涵盖各种任务；例如，使用InDesign server处理文件。

要将文件完全上传到您使用Adobe inDesign创建的AEM资产，请使用代理。 它使用代理Worker与Adobe inDesign server通信，在Adobe inDesign server中运行脚 [本](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) ，以提取元数据并为AEM资产生成各种再现。 代理Worker支持InDesign server与云配置中的AEM实例之间的双向通信。

>[!NOTE]
>
>Adobe inDesign提供两种产品：
>
>* [InDesign](https://www.adobe.com/products/indesign.html)
   >  这允许您为印刷和／或数字分发设计页面布局。
   >
   >
* [InDesign Server](https://www.adobe.com/products/indesignserver.html)
   >  此引擎使您能够根据您使用InDesign创建的内容有计划地创建自动化文档。 它作为服务运行，为其 [ExtendScript引擎提供接口](https://www.adobe.com/devnet/scripting.html) 。
   >  脚本以extendscript编写，与javascript类似。 有关Indesign脚本的信息，请参 [阅https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)。
>



## 提取的工作原理 {#how-the-extraction-works}

Adobe inDesign server可以与AEM资产集成，以便上传使用InDesign创建的INDD文件、生成演绎版、提取所有媒体（例如，视频）并存储为资产：

>[!NOTE]
>
>以前版本的AEM能够提取XMP和缩略图，现在可以提取所有媒体。

1. 将INDD文件上传到AEM资产。
1. 框架通过SOAP（简单对象访问协议）将命令脚本发送到InDesign Server。
此命令脚本将：

   * 检索INDD文件。
   * 执行InDesign server命令：

      * 将提取结构、文本和任何媒体文件。
      * 将生成PDF和JPG再现。
      * 将生成HTML和IDML再现。
   * 将生成的文件发布回AEM资产。
   >[!NOTE]
   >
   >IDML是一种基于XML的格式，可呈现InDesign *文件中* 的所有内容。 它使用 [Zip压缩作为压缩包存](https://www.techterms.com/definition/zip) 储。
   >
   >
   >有关 [更多信息，请参阅Adobe Press - inDesign Interchange Formats INX和IDML](https://www.adobepress.com/articles/article.asp?p=1381880&seqNum=8) 。

   >[!CAUTION]
   >
   >如果未安装或未配置InDesign Server，则仍可将INDD文件上传到AEM。 但是，生成的演绎版将限于PNG和JPEG。 您将无法生成HTML、.idml或页面再现。

1. 提取和再现生成后：

   * 此结构将复制到一 `cq:Page` 个（演绎版类型）。
   * 提取的文本和文件存储在AEM资产中。
   * 所有演绎版都存储在AEM资产中，位于资产本身中。

## 将InDesign server与AEM集成 {#integrating-the-indesign-server-with-aem}

要集成InDesign server以与AEM资产一起使用，并在配置代理后，您需要：

1. [安装InDesign Server](#installing-the-indesign-server)。
1. 如果需要， [请配置AEM资产工作流](#configuring-the-aem-assets-workflow)。
仅当默认值不适用于您的实例时，才需要这样做。

1. 为InDesign [Server配置代理Worker](#configuring-the-proxy-worker-for-indesign-server)。

### 安装InDesign Server {#installing-the-indesign-server}

安装并启动InDesign server以与AEM一起使用：

1. 下载并安装Adobe inDesign Server。

   >[!NOTE]
   >
   >InDesign Server（CS6和更高版本）。

1. 如果需要，您可以自定义InDesign server实例的配置。

1. 从命令行启动服务器：

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   这将启动服务器，SOAP插件在端口8080上侦听。 所有日志消息和输出都直接写入命令窗口。

   >[!NOTE]
   >
   >如果要将输出消息保存到文件，则使用重定向；例如，在Windows下：
   >
   >
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### 配置AEM Assets工作流 {#configuring-the-aem-assets-workflow}

AEM资产有一个预配置的工作流 **程DAM更新资产**，该流程具有几个专门用于InDesign的流程步骤：

* [媒体提取](#media-extraction)
* [页面提取](#page-extraction)

<!--
BROKEN LINK This workflow is setup with default values that can be adapted for your setup on the various author instances (this is a standard workflow, so further information is available under [Editing a Workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). If you are using the default values (including the SOAP port), then no configuration is needed. BROKEN LINK
-->

设置完成后，将InDesign文件上传到AEM资产（通过任何常用方法）将触发处理资产和准备各种演绎版所需的工作流。 通过将文件上传到AEM资 `.indd` 产来测试您的配置，以确认您在 `<*your_asset*>.indd/Renditions`

#### 媒体提取 {#media-extraction}

此步骤控制从INDD文件提取媒体。

要进行自定义，可以编辑“ **媒体提取** ”步骤的“ **参数”选项卡** 。

![媒体提取参数和脚本路径](assets/media_extraction_arguments_scripts.png)

媒体提取参数和脚本路径

* **ExtendScript库**&#x200B;这是一个简单的http get/post方法库，其他脚本需要它。

* **扩展脚本**&#x200B;您可以在此处指定不同的脚本组合。 如果希望在InDesign server上执行您自己的脚本，请将这些脚本保存在 `/apps/settings/dam/indesign/scripts`。
有关Indesign脚本的信息，请参阅：
   [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>不 **要更** 改 **ExtendScript库**。

>此库提供与Sling通信所需的HTTP功能。 此设置指定要发送到InDesign server以供在InDesign server上使用的库。
>
由“ `ThumbnailExport.jsx` 媒体提取”工作流步骤运行的脚本生成。jpg格式的缩略图再现。 此演绎版由流程缩略图工作流步骤使用，以生成AEM所需的静态演绎版。

您可以配置“流程缩略图”工作流步骤以生成大小不同的静态演绎版。 请确保不删除默认值，因为AEM资产UI要求使用默认值。 最后，删除图像预览演绎版工作流步骤会删除。jpg缩略图演绎版，因为不再需要它。

#### 页面提取 {#page-extraction}

这将从提取的元素创建AEM页面。 提取处理函数用于从再现（当前为HTML或IDML）中提取数据。 此数据随后用于使用PageBuilder创建页面。

要进行自定义，可以编辑“页 **面提取** ”步骤的“ **参数”选项卡** 。

![chlimage_1-96](assets/chlimage_1-96.png)

* **页面提取处**&#x200B;理函数从下拉列表中，选择要使用的处理函数。 提取处理函数对特定再现进行操作，该再现由相关的再现选 `RenditionPicker` 择(请参阅 `ExtractionHandler` API)。
在标准AEM安装中，可以使用以下选项：

   * IDML导出提取处理程序对在MediaExtract步 `IDML` 骤中生成的再现进行操作。

* **页面名**&#x200B;称指定要分配给结果页面的名称。 如果留空，则名称为“page”（如果“page”已存在，则为派生名称）。

* **页面标**&#x200B;题指定要分配给结果页面的标题。

* **页面根路径**生成页面的根位置的路径。
如果保留为空，则将使用包含资产演绎版的节点。

* **页面模**&#x200B;板生成结果页面时使用的模板。

* **页面设**&#x200B;计生成页面时要使用的页面设计。

### 为InDesign server配置代理Worker {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
该worker驻留在代理实例上。

1. 在工具控制台中，展开 **左侧窗格中的云服务配置** 。 然后展开 **云代理配置**。

1. 双击 **IDS worker以打开** ，进行配置。

1. 单击 **[!UICONTROL 编辑]** ，打开配置对话框并定义所需的设置：

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS池**&#x200B;用于与InDesign server通信的SOAP端点。 您可以添加、删除和订购项目。

1. 单击确定进行保存。

### 配置Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

如果InDesign服务器和AEM在不同的主机上运行，或者这两个应用程序都不在默认端口上运行，请配置 **Day CQ Link Externalizer** ，以设置InDesign服务器的主机名、端口和内容路径。

1. 访问URL上的配置管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 找到配置 **Day CQ Link Externalizer**，然后单击“编 **辑** ”图标以将其打开。
1. 指定Indesign服务器的主机名和上下文路径，然后单击“保 **存”**。

   ![chlimage_1-97](assets/chlimage_1-97.png)

### 为InDesign Server启用并行作业处理 {#enabling-parallel-job-processing-for-indesign-server-s}

您现在可以为IDS启用并行作业处理。

首先，您需要确定InDesign server可处理的最大并行作`x`业数():

* 在单个多处理器计算机上，InDesign server可处理的并行作业(x)的最大数目比运行IDS的处理器数目少一个。
* 在多台计算机上运行ID时，您需要计算可用处理器的总数（即在所有计算机上），然后减去计算机的总数。

要配置并行IDS作业的数量，请执行以下操作：

1. 打开Felix **Console的** “配置”选项卡；例如： `https://[aem_server]:[port]/system/console/configMgr`.

1. 在以下位置选择IDS处理队列：

   `Apache Sling Job Queue Configuration`

1. 套:

   * **类型** - `Parallel`
   * **最大并行作业** - `<*x*>` （如上所计算）

1. 保存这些更改。
1. 通过检查以下链接，启用CS6（及更高版本）的多会话支持：

   `enable.multisession.name` 复选框

   下：

   `com.day.cq.dam.ids.impl.IDSJobProcessor.name configuration`

1. 通过向 [IDS worker配 `<*x*>` 置添加SOAP端点，创建IDS Worker池](#configuring-the-proxy-worker-for-indesign-server)。

   如果有多台计算机运行InDesign Server，请为每台计算机添加SOAP端点（每台计算机的处理器数-1）。

   >[!NOTE]
   您可以选择在处理大量员工时启用IDS工作人员的黑名单。
   为此，请在配置下启用“enable.retry.name”复选框，该 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` 配置将启用IDS作业检索。
   此外，在该配 `com.day.cq.dam.ids.impl.IDSPoolImpl.name` 置下，为参数设置一个正值，该参数在将IDS从作业处理程序列表中禁止之 `max.errors.to.blacklist` 前确定作业检索的数量
   默认情况下，在IDS worker经过可配置(retry.interval.to.whitelist.name)时间（以分钟为单位）后，将重新验证IDS Worker。 如果在线找到该工作者，则该工作者会从黑名单中删除

## 支持InDesign Server 10.0或更高版本 {#enabling-support-for-indesign-server-or-higher}

对于InDesign Server 10.0或更高版本，请执行以下步骤以启用多会话支持。

1. 从AEM资产实例中打开配置管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 编辑配置 `com.day.cq.dam.ids.impl.IDSJobProcessor.name`。
1. Select the **[!UICONTROL ids.cc.enable]** option, and click **[!UICONTROL Save]**.

>[!NOTE]
对于与AEM Assets的InDesign server集成，请使用多核处理器，因为单核系统不支持进行集成所需的会话支持功能。

## 配置AEM凭据 {#configure-aem-credentials}

您可以更改从AEM实例访问InDesign服务器的默认管理员凭据（用户名和密码），而不中断与InDesign服务器的集成。

1. 转到 `/etc/cloudservices/proxy.html`.
1. 在对话框中，指定新的用户名和密码。
1. 保存凭据。
