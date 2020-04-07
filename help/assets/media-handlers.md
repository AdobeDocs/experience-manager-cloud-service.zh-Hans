---
title: 使用媒体处理函数和工作流处理资源
description: 了解各种媒体处理程序以及如何在工作流中使用它们对资产执行任务。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# 使用媒体处理函数和工作流处理资源 {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager(AEM)资产附带一组用于处理资产的默认工作流和媒体处理程序。 该工作流定义要对资产执行的常规任务，然后将特定任务委派给媒体处理程序，例如缩略图生成或元数据提取。

可以定义一个工作流，该工作流将在特定类型的资产上传到服务器时自动执行。 这些处理步骤是根据一系列AEM Assets媒体处理程序定义的。 AEM提供一些 [内置的处理函数](#default-media-handlers) ，其他处理函数可以是自定义 [开发的](#creating-a-new-media-handler) ，也可以通过将进程委派到命令行工具来 [定义](#command-line-based-media-handler)。

媒体处理程序是AEM资产中对资产执行特定操作的服务。 例如，当MP3音频文件上传到AEM时，工作流会触发一个MP3处理程序，该处理程序提取元数据并生成缩略图。 媒体处理程序通常与工作流结合使用。 AEM中支持大多数常见的MIME类型。 通过扩展／创建任务、扩展／创建媒体处理函数或禁用／启用媒体处理函数，可以对资产执行特定工作流。

>[!NOTE]
>
>有关AEM [资产支持的所有格式](file-format-support.md) ，以及每种格式支持的功能的说明，请参阅资产支持的文件格式文章。

## 默认媒体处理函数 {#default-media-handlers}

AEM资产中提供以下媒体处理函数，并处理最常见的MIME类型：

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

<table>
 <tbody>
  <tr>
   <td>处理程序名称</td>
   <td>服务名称（在系统控制台中）</td>
   <td>支持的MIME类型</td>
  </tr>
  <tr>
   <td>TextHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.TextHandler</p> </td>
   <td>text/plain</td>
  </tr>
  <tr>
   <td>PdfHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pdf.PdfHandler</p> </td>
   <td><p>application/pdf<br /> application/illustrator</p> </td>
  </tr>
  <tr>
   <td>JpegHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.JpegHandler</p> </td>
   <td>image/jpeg</td>
  </tr>
  <tr>
   <td>Mp3Handler</td>
   <td><p>com.day.cq.dam.handler.standard.mp3.Mp3Handler</p> </td>
   <td><p>audio/mpeg</p> </td>
  </tr>
  <tr>
   <td>ZipHandler</td>
   <td><p>com.day.cq.dam.handler.standard.zip.ZipHandler</p> </td>
   <td><p>application/java-archive</p> <p>application/zip</p> </td>
  </tr>
  <tr>
   <td>PictHandler</td>
   <td><p>com.day.cq.dam.handler.standard.pict.PictHandler</p> </td>
   <td><p>image/pict</p> </td>
  </tr>
  <tr>
   <td>StandardImageHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.StandardImageHandler</p> </td>
   <td><p>image/gif</p> <p>image/png</p> <p>application/photoshop</p> <p>image/jpeg</p> <p>image/tiff</p> <p>image/x-ms-bmp</p> <p>image/bmp</p> </td>
  </tr>
  <tr>
   <td>MSOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler</td>
   <td>application/msword<br /> </td>
  </tr>
  <tr>
   <td>MSPowerPointHandler</td>
   <td>com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler</td>
   <td>application/vnd.ms-powerpoint<br /> </td>
  </tr>
  <tr>
   <td>OpenOfficeHandler</td>
   <td>com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler</td>
   <td>application/vnd.openxmlformats-officedocument.wordprocessingml.文档application/vnd.openxmlformats<br /> -officedocument.spreadsheetml.sheet<br /> application/vnd.openxmlformats-officedocument.presentationml.presentation<br /><br /> </td>
  </tr>
  <tr>
   <td>EPubHandler</td>
   <td>com.day.cq.dam.handler.standard.epub.EPubHandler</td>
   <td>application/epub+zip</td>
  </tr>
  <tr>
   <td>GenericAssetHandler</td>
   <td><p>com.day.cq.dam.core.impl.handler.GenericAssetHandler</p> </td>
   <td>回退，以防发现其他处理函数从资产中提取数据</td>
  </tr>
 </tbody>
</table>

所有处理函数都执行以下任务:

* 从资产中提取所有可用元数据。
* 从资产中创建缩略图。

可以视图活动媒体处理程序：

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. 单击链接 `com.day.cq.dam.core.impl.store.AssetStoreImpl`。
1. 将显示包含所有活动媒体处理函数的列表。

## 使用工作流中的媒体处理程序对资产执行任务 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

媒体处理程序是通常与工作流结合使用的服务。

AEM具有一些用于处理资产的默认工作流。 要视图这些模型，请打开工作流控制台，然后单击“模 **[!UICONTROL 型]** ”选项卡：与AEM资产开始的工作流标题是特定于资产的标题。

现有工作流可以扩展，也可以创建新的，以根据特定要求处理资产。

以下示例演示如何增强 **[!UICONTROL AEM Assets 同步工作流]**，以便为除 PDF 文档外的所有资产生成子资产。

### 禁用／启用媒体处理程序 {#disabling-enabling-a-media-handler}

媒体处理程序可以通过Apache Felix Web管理控制台禁用或启用。 禁用媒体处理程序后，不会对资产执行其任务。

要启用／禁用媒体处理程序，请执行以下操作：

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. 单 **[!UICONTROL 击媒体处理程序名称旁的]** “禁用”。 For example: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. 刷新页面：媒体处理程序旁边会显示一个图标，指示它已禁用。
1. 要启用媒体处理程序，请单 **[!UICONTROL 击媒体]** 处理程序名称旁边的“启用”。

### 创建新的媒体处理程序 {#creating-a-new-media-handler}

要支持新的媒体类型或对资产执行特定任务，必须创建新的媒体处理程序。 本节介绍如何继续。

#### 重要类和接口 {#important-classes-and-interfaces}

开始实现的最佳方法是继承所提供的抽象实现，该实现能够处理大多数事务并提供合理的默认行为：课 `com.day.cq.dam.core.AbstractAssetHandler` 程。

该类已经提供抽象服务描述符。 因此，如果您从此类继承并使用maven-sling-plugin，请确保将inherit标志设置为 `true`。

实现以下方法：

* `extractMetadata()`:提取所有可用的元数据。
* `getThumbnailImage()`:从传递的资产中创建缩略图。
* `getMimeTypes()`:返回资产MIME类型。

以下是示例模板：

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler` 接口：此界面描述添加对特定MIME类型的支持的服务。 添加新的MIME类型需要实现此接口。 该界面包含导入和导出特定文档、创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` class:此类用作所有其他资产处理函数实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:
   * 该类用作所有其他资产处理程序实现的基础，并为子资产提取提供常用功能以及常用功能。
   * 开始实现的最佳方法是继承所提供的抽象实现，该实现能够处理大多数事务并提供合理的默认行为：com.day.cq.dam.core.AbstractAssetHandler类。
   * 该类已经提供抽象服务描述符。 因此，如果您从此类继承并使用maven-sling-plugin，请确保将inherit标志设置为true。

需要实现以下方法：

* `extractMetadata()`:此方法提取所有可用的元数据。
* `getThumbnailImage()`:此方法会从传递的资产中创建缩略图。
* `getMimeTypes()`:此方法返回资产MIME类型。

以下是示例模板：

打包my.own.stuff;/&amp;ast;&amp;ast;&amp;ast;@scr.component inherit=&quot;true&quot; &amp;ast;@scr.service &amp;ast;/公共类MyMediaHandler扩展com.day.cq.dam.core.AbstractAssetHandler { //实现相关部分}

接口和类包括：

* `com.day.cq.dam.api.handler.AssetHandler` 接口：此界面描述添加对特定MIME类型的支持的服务。 添加新的MIME类型需要实现此接口。 该界面包含导入和导出特定文档、创建缩略图和提取元数据的方法。
* `com.day.cq.dam.core.AbstractAssetHandler` class:此类用作所有其他资产处理函数实现的基础，并提供常用功能。
* `com.day.cq.dam.core.AbstractSubAssetHandler` class:该类用作所有其他资产处理程序实现的基础，并为子资产提取提供常用功能和常用功能。

<!--
#### Example: create a specific Text Handler {#example-create-a-specific-text-handler}

In this section, you will create a specific Text Handler that generates thumbnails with a watermark.

Proceed as follows:

Refer to [Development Tools](../sites-developing/dev-tools.md) to install and set up Eclipse with a Maven plugin and for setting up the dependencies that are needed for the Maven project.

After you perform the following procedure, when you upload a txt file into AEM, the file's metadata are extracted and two thumbnails with a watermark are generated.

1. In Eclipse, create `myBundle` Maven project:

    1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
    1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
    1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
    1. Define the Maven project:

        * Group Id: com.day.cq5.myhandler
        * Artifact Id: myBundle
        * Name: My AEM bundle
        * Description: This is my AEM bundle

    1. Click **[!UICONTROL Finish]**.

1. Set the Java Compiler to version 1.5:

    1. Right-click the `myBundle` project, select Properties.
    1. Select Java Compiler and set following properties to 1.5:

        * Compiler compliance level
        * Generated .class files compatibility
        * Source compatibility

    1. Click **[!UICONTROL OK]**. In the dialog window, click Yes.

1. Replace the code in the pom.xml file with the following code:

1. Create the package `com.day.cq5.myhandler` that contains the Java classes under `myBundle/src/main/java`:

    1. Under myBundle, right-click `src/main/java`, select New, then Package.
    1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

    1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
    1. In the dialog window, name the Java Class MyHandler and click Finish. Eclipse creates and opens the file MyHandler.java.
    1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;

   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/

   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }

    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the Java class and create the bundle:

    1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
    1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). The new text handler is now active in AEM.
1. In your browser, open the Apache Felix Web Management Console. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

-->

## 基于命令行的媒体处理程序 {#command-line-based-media-handler}

AEM允许您在工作流中运行任何命令行工具来转换资产（如ImageMagick）并将新再现添加到资产。 您只需在承载AEM服务器的磁盘上安装命令行工具，并向工作流中添加和配置进程步骤。 调用的过程(称 `CommandLineProcess`为)还允许根据特定MIME类型进行筛选，并基于新再现创建多个缩略图。

以下转换可以自动运行并存储在AEM资产中：

* 使用ImageMagick和 [Ghostscript的EPS和AI](https://www.imagemagick.org/script/index.php) 转 [换](https://www.ghostscript.com/)
* 使用FFmpeg的FLV视频转 [码](https://ffmpeg.org/)
* 使用 [LAME进行MP3编码](http://lame.sourceforge.net/)
* 使用 [SOX的音频处理](http://sox.sourceforge.net/)

>[!NOTE]
>
>在非Windows系统上，FFMpeg工具在为文件名中只有单引号(&#39;)的视频资产生成再现时返回错误。 如果视频文件的名称包含单引号，请在上传到AEM之前将其删除。

该流 `CommandLineProcess` 程按列出顺序执行以下操作：

* 过滤器文件，如果指定，则根据特定MIME类型。
* 在承载AEM服务器的磁盘上创建一个临时目录。
* 将原始文件流化到临时目录。
* 执行由步骤的参数定义的命令。 该命令将在具有运行AEM的用户权限的临时目录中执行。
* 将结果流化回AEM服务器的再现文件夹。
* 删除临时目录。
* 根据这些演绎版创建缩略图（如果已指定）。 缩略图的编号和尺寸由步骤的参数定义。

### 使用ImageMagick的示例 {#an-example-using-imagemagick}

以下示例显示如何设置命令行处理步骤，以便每次将mime-type gif或tiff的资产添加到AEM服务器上的/content/dam时，将创建原始图像的翻转图像以及三个额外的缩略图（140x100、48x48和10x250）。

为此，您将使用ImageMagick。 ImageMagick是用于创建、编辑和合成位图图像的免费软件套件，通常使用命令行。

首先在承载AEM服务器的磁盘上安装ImageMagick:

1. 安装ImageMagick:请参 [阅ImageMagick文档](https://www.imagemagick.org/script/download.php)。
1. 设置该工具，以便在命令行上运行转换。
1. 要查看该工具是否正确安装，请在命令行中 `convert -h` 运行以下命令。

   它会显示一个包含转换工具所有可能选项的帮助屏幕。

   >[!NOTE]
   >
   >在某些版本的Windows（例如Windows SE）中，convert命令可能无法运行，因为它与Windows安装中的本机转换实用程序相冲突。 在这种情况下，请提及用于将图像文件转换为缩略图的ImageMagick实用程序的完整路径。 For example, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. 要查看该工具是否运行正确，请向工作目录中添加。jpg图像，然后在命令行上运 `<image-name>.jpg -flip <image-name>-flipped.jpg` 行转换命令。

   翻转后的图像会添加到目录中。

然后，将命令行流程步骤添加到 **[!UICONTROL DAM 更新资产]**&#x200B;工作流：

1. 转到“工作 **[!UICONTROL 流]** ”控制台。
1. 在“模 **[!UICONTROL 型]** ”选项卡中，编辑 **[!UICONTROL DAM更新资产模型]** 。
1. 按如下方式更改启用 **[!UICONTROL Web的再现步骤]** 的设置：

   **参数**:

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. 保存工作流。

要测试修改后的工作流，请向中添加资产 `/content/dam`。

1. 在文件系统中，获取您选择的。tiff图像。 将其重命名 `myImage.tiff` 为并复制到 `/content/dam`其中，例如使用WebDAV。
1. 例如，转 **[!UICONTROL 到CQ5 DAM]** 控制台 `http://localhost:4502/libs/wcm/core/content/damadmin.html`。
1. 打开资 **[!UICONTROL 源myImage.tiff]** ，并验证已翻转的图像和三个缩略图是否已创建。

#### 配置CommandLineProcess进程步骤 {#configuring-the-commandlineprocess-process-step}

本节介绍如何设置 **CommandLineProcess** 的&#x200B;**进程参数**。

“进程参 **数** ”的值必须用逗号分隔，不得与空格开始。

<table>
 <tbody>
  <tr>
   <td> 参数格式</td>
   <td>描述</td>
  </tr>
  <tr>
   <td> mime:&lt;mime类型&gt;</td>
   <td><p>可选参数。 如果资产的MIME类型与其中一个参数的MIME类型相同，则会应用该过程。</p> <p>可以定义多种MIME类型。</p> </td>
  </tr>
  <tr>
   <td> tn:&lt;width&gt;:&lt;height&gt;</td>
   <td><p>可选参数。 该过程创建一个缩略图，其尺寸在参数中定义。</p> <p>可以定义多个缩略图。<br /> </p> </td>
  </tr>
  <tr>
   <td> cmd:&lt;命令&gt;</td>
   <td><p>定义将执行的命令。 语法取决于命令行工具。</p> <p>只能定义一个命令。</p> <p>以下变量可用于创建命令：<br/></p> <p><code>${filename}</code>:输入文件的名称，例如“original.jpg”<br/><code>${file}</code>:输入文件的完整路径名，例如“/tmp/cqdam0816.tmp/original.jpg”<br/><code>${directory}</code>:目录，例如“/tmp/cqdam0816.tmp”。<br/> <code>${basename}</code>:不带扩展名的输入文件的名称，例如原始文件<br/><code>${extension}</code>:输入文件的扩展名，例如JPG<br/></p></td>
  </tr>
 </tbody>
</table>

例如，如果ImageMagick安装在承载AEM服务器的磁盘上，并且如果您使用 **CommandLineProcess** as Implementation创建进程步骤，并将以下值作为 **Process Arguments**:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

然后，在工作流运行时，该步骤仅应用于具有image/gif或mime:image/tiff作为mime类型的资产，它将创建翻转后的原始图像，将其转换为。jpg并创建具有尺寸的三个缩略图：140x100、48x48和10x250。

使用以下 **进程参数** ，使用ImageMagick创建三个标准缩略图：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

使用以下 **进程参数** ，使用ImageMagick创建支持Web的再现：

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>CommandLineProcess **步骤仅适用于资产(类型的节**`dam:Asset`点)或资产的后代。
