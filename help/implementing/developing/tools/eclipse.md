---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概述 {#overview}

AEM Developer Tools for Eclipse是一个基于Apache License 2 [下发布的Apache Sling的Eclipse插件](https://sling.apache.org/documentation/development/ide-tooling.html) ,Eclipse插件是一个Eclipse插件。

它优惠了几个使AEM开发更容易的功能：

* 通过Eclipse Server Connector与AEM实例无缝集成
* 内容和OSGi包的同步
* 具有代码热插拔功能的调试支持
* 通过特定项目创建向导简单引导AEM项目
* 轻松编辑JCR属性

## 要求 {#requirements}

在使用AEM开发人员工具之前，您需要：

* 下载并安装适 [用于企业Java开发人员的Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 按照Eclipse常见问题解答中的说明，通过编辑配置文件，配置Eclipse安 `eclipse.ini` 装以确保至少拥有1 GB [堆内存](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)。

>[!NOTE]
>
>在macOS上，您需要右键单击Eclipse. **app** ，然后选择 **“显示包内容** ”才能找到您的 `eclipse.ini`**。**

## 如何安装AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

满足上述要求 [后](#requirements) ，您可以按如下方式安装插件：

1. 打开AEM [Developer Tools网站。](https://eclipse.adobe.com/aem/dev-tools/)

1. 复制安 **装链接**。

   请注意，您也可以下载存档文件，而不是使用安装链接。 这允许脱机安装，但您会以这种方式错过自动更新通知。

1. 在Eclipse中，打开“帮 **助** ”菜单。
1. 单击“ **安装新软件”**。
1. Click **Add...**.
1. 在名 **称中** ，输入 `AEM Developer Tools`。
1. 在 **位置** ，复制安装URL。
1. 单击&#x200B;**添加**。
1. 检查AEM **和****Sling** 插件。
1. 单击&#x200B;**下一步**。
1. 在“安装详 **细信息** ”窗口中，再 **次单击** “下一步”。
1. 接受许可协议，然后单击“ **完成**”。
1. 单击 **RestartNow** ，以重新启动Eclipse。

## AEM透视 {#the-aem-perspective}

在Eclipse中，透视图确定窗口中可用的操作和视图，并实现与Eclipse中资源的面向任务的交互。 有关“透视”的更多详细信息，请参 [阅Eclipse文档。](https://help.eclipse.org)

AEM Development Tools for Eclipse提供了AEM透视，它使您能够完全控制AEM项目和实例。 要打开AEM透视，请执行以下操作：

1. 从Eclipse菜单栏中，选 **择窗口** ->透 **视** - **>打开透** 视- **>其**&#x200B;他。
1. 在对 **话框** 中选择AEM，然后单击 **打开**。

![Eclipse中的AEM透视](assets/eclipse-aem-perspective.png)

## 示例多模块项目 {#sample-multi-module-project}

AEM Developer Tools for Eclipse附带一个范例、多模块项目，它可以帮助您快速掌握Eclipse中的项目设置，并作为几个AEM功能的最佳实践指南。 [进一步了解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

按照以下步骤创建示例项目：

1. 在“文 **件** ”>“新 **建”** >“项 **目”菜单中，浏** 览到AEM部分和选 ********&#x200B;择AEM示例多模块项目。

   ![AEM示例多模块项目](assets/aem-sample-project.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一些时间，因为m2eclipse需要扫描原型目录。

1. 从菜 `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` 单中进行选择，然后单击“下 **一步”**。

   ![选择原型版本](assets/select-archetype.png)

1. 为示例项目提供以下字段：

   * **名称**
   * **组ID**
   * **对象ID**
   * **appId** —— 您可能需要展开“高 **级** ”选项来设置此值。
   * **appTitle** —— 您可能需要展开“高 **级** ”选项来设置此值。
   * **包** -您可能需要展开“高 **级** ”选项来设置此值。

   ![定义原型属性](assets/archetype-properties.png)

1. 单击&#x200B;**下一步**。

1. 然后，配置Eclipse将连接到的AEM服务器。

   要使用调试器功能，您需要在调试模式下启动AEM —— 通过向命令行添加以下内容可以达到此目的：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![连接到AEM服务器](assets/connect-server.png)

1. 单击 **完成**。 将创建项目结构。

   >[!NOTE]
   >
   >在新安装（更确切地说，当从未下载过大量依赖项时）时，您可能会创建出错误的项目。 在这种情况下，请按照解决无效项目定 [义中所述的过程操作](#resolving-invalid-project-definition)。

## 如何导入现有项目 {#how-to-import-existing-projects}

您可以使用“ **新建项目** ”功能为您创建正确的结构：

1. 按照说明创建多 [模块示例项目](#sample-multi-module-project) ，您将为您创建以下项目，这样可以正常地分离问题：

   * `PROJECT.ui.apps` for `/apps` and `/etc` content
   * `PROJECT.ui.content` for `/content` that roumeded
   * `PROJECT.core` 对于Java捆绑套件（只要您想添加Java代码，这些捆绑套件就会变得有趣）
   * `PROJECT.it.launcher` 和 `PROJECT.it.tests` 集成测试

1. 将项目内容替 `PROJECT.ui.apps` 换为包 `apps` 和 `etc` 文件夹：

   1. 在“项目资源管理器”面板中， `PROJECT.ui.apps` 展开 `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 右键单击文件夹， `apps` 然后选择“ **显示在** ”>“ **系统资源管理器**”。
   1. 删除您现 `apps` 在应查 `etc` 看的文件夹和文件夹，并将其放置 `apps` 到您的内容包 `etc` 的文件夹和文件夹中。
   1. 在Eclipse中，右键单击项目并 `PROJECT.ui.apps` 选择“刷 **新”**。

1. 然后，对该文件夹执行 `PROJECT.ui.content` 同样的操作，并将其内容文件夹替换为您的某个包：

   1. 在“项目资源管理器”面板中， `PROJECT.ui.content` 展开 `src` > `main` > `content` > `jcr_root` > `content`。
   1. 右键单击更深层的内容文件夹，然后选择“ **显示在** ” -> **“系统资源管理器**”。
   1. 删除您现在应当看到的内容文件夹，并将其放置在内容包的内容文件夹中。
   1. 在Eclipse中，右键单击项目并 `PROJECT.ui.content` 选择“刷 **新”**。

1. 现在，您必须更新这 `filter.xml` 两个项目的文件，使其与内容包的内容相对应。 为此，请在单 `META-INF/vault/filter.xml` 独的文本／代码编辑器中打开内容包的文件。

   * 以下是文件外观 `filter.xml` 的示例：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 对于被拆分为两个项目的包的内容，您还必须将这些筛选器规则拆分为两个，并相应地更 `filter.xml` 新两个项目的文件。

   1. 在Eclipse中，打开 `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 将元素的内 `<workspaceFilter>` 容替换为包中开始的规则， `/apps` 并 `/etc`
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 然后打开 `PROJECT.ui.content/src/main/content/META-INF/filter.xml`。
   1. 将规则替换为开始包中的规则 `/content`。
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. 确保保存所有更改。 您现在可以将新内容同步到AEM实例。

1. 在“服务器”面板中，确保连接已启动，如果未开始连接。
1. 单击“清除并 **发布”图标** 。

完成后，您的包应在实例上运行，保存后，任何更改都会自动同步到实例。

如果要从项目中重新构建包，请右键单击或，然 `PROJECT.ui.apps` 后选 `PROJECT.ui.content` 择“运 **行方式** ”-> **“Maven Install**”。

现在，您有一个目标文件夹，它是在内部使用您的包创建的(例如， `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑难解答 {#troubleshooting}

### 解析无效的项目定义 {#resolving-invalid-project-definition}

要解析无效的依赖项，项目定义将按如下步骤进行：

1. 选择所有创建的项目。
1. 右键单击。
1. 在上下文菜单中，选择“ **Maven** ”->“ **更新项目”**。
1. 检查 **强制更新快照／版本**。
1. 单击&#x200B;**确定**。

Eclipse下载所需的依赖项。 这可能需要一点时间。

## More information {#more-information}

适用于Eclipse网站的Apache Sling IDE官方工具为您提供有用的信息：

* 本文 [**档为《Eclipse User Guide** 》提供的Apache Sling IDE工具](https://sling.apache.org/documentation/development/ide-tooling.html)，将指导您了解AEM Development Tools支持的总体概念、服务器集成和部署功能。
* 疑难 [解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* 已知 [问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官方 [Eclipse](https://eclipse.org/) 文档可以帮助您设置环境:

* [Eclipse快速入门](https://eclipse.org/users/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/luna/index.jsp)
* [Maven Integration(m2eclipse)](https://www.eclipse.org/m2e/)
