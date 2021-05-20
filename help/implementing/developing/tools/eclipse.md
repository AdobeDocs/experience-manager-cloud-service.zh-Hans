---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---

# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## 概述 {#overview}

AEM Developer Tools for Eclipse是一个Eclipse插件，它基于根据Apache许可证2发布的适用于Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)的[Eclipse插件。

它提供了以下几项功能，可简化AEM开发：

* 通过Eclipse Server Connector与AEM实例无缝集成
* 内容和OSGi包的同步
* 具有代码热交换功能的调试支持
* 通过特定项目创建向导简单引导AEM项目
* 轻松编辑JCR属性

## 要求 {#requirements}

在使用AEM开发人员工具之前，您需要：

* 下载并安装面向企业Java开发人员的[Eclipse IDE](https://www.eclipse.org/downloads/packages/)。
* 按照[Eclipse常见问题解答](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse)中的所述，通过编辑`eclipse.ini`配置文件，配置Eclipse安装以确保您至少拥有1 GB的堆内存。

>[!NOTE]
>
>在macOS上，您需要右键单击&#x200B;**Eclipse.app**，然后选择&#x200B;**显示包内容**，才能找到&#x200B;`eclipse.ini`**。**

## 如何安装AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

满足上述[要求](#requirements)后，可按如下方式安装插件：

1. 打开[AEM Developer Tools Web站点。](https://eclipse.adobe.com/aem/dev-tools/)

1. 复制&#x200B;**Installation Link**。

   请注意，或者，您也可以下载存档文件，而不是使用安装链接。 这允许离线安装，但您将无法通过这种方式接收自动更新通知。

1. 在Eclipse中，打开&#x200B;**Help**&#x200B;菜单。
1. 单击&#x200B;**安装新软件**。
1. 单击&#x200B;**添加……**。
1. 在&#x200B;**名称**&#x200B;中，输入`AEM Developer Tools`。
1. 在&#x200B;**Location**&#x200B;中，复制安装URL。
1. 单击&#x200B;**添加**。
1. 同时检查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;插件。
1. 单击&#x200B;**下一步**。
1. 在&#x200B;**Install Details**&#x200B;窗口中，再次单击&#x200B;**Next**。
1. 接受许可协议，然后单击&#x200B;**完成**。
1. 单击&#x200B;**RestartNow**&#x200B;以重新启动Eclipse。

## AEM透视{#the-aem-perspective}

在Eclipse中，透视可确定窗口内可用的操作和视图，并在Eclipse中启用面向任务的资源交互。 有关“透视”的更多详细信息，请参阅[Eclipse文档。](https://help.eclipse.org)

AEM Development Tools for Eclipse提供了AEM Perspective，它使您能够完全控制AEM项目和实例。 要打开AEM透视图，请执行以下操作：

1. 从Eclipse菜单栏中，选择&#x200B;**Window** -> **Perspective** -> **Open Perspective** -> **Other**。
1. 在对话框中选择&#x200B;**AEM**，然后单击&#x200B;**打开**。

![Eclipse中的AEM视角](assets/eclipse-aem-perspective.png)

## 多模块项目{#sample-multi-module-project}示例

AEM Developer Tools for Eclipse附带一个示例的多模块项目，该项目可帮助您快速掌握Eclipse中项目设置的速度，并且是一些AEM功能的最佳实践指南。 [进一步了解项目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

按照以下步骤创建示例项目：

1. 在&#x200B;**文件** > **新建** > **项目**&#x200B;菜单中，浏览到&#x200B;**AEM**&#x200B;部分，然后选择&#x200B;**AEM示例多模块项目**。

   ![AEM多模块项目示例](assets/aem-sample-project.png)

1. 单击&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步骤可能需要一些时间，因为m2eclipse需要扫描原型目录。

1. 从菜单中选择`com.adobe.granite.archetypes : sample-project-archetype : <highest-number>`，然后单击&#x200B;**下一步**。

   ![选择原型版本](assets/select-archetype.png)

1. 为示例项目提供以下字段：

   * **名称**
   * **组ID**
   * **项目ID**
   * **appId**  — 您可能需要展开高级选 **** 项才能设置此值。
   * **appTitle**  — 您可能需要展开高级选 **** 项才能设置此值。
   * **包**  — 您可能需要展开高级选 **** 项才能设置此值。

   ![定义原型属性](assets/archetype-properties.png)

1. 单击&#x200B;**下一步**。

1. 然后，您将配置一个AEM服务器，Eclipse将连接到该服务器。

   要使用调试器功能，您需要在调试模式下启动AEM — 例如，通过将以下内容添加到命令行中即可实现：

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![连接到AEM服务器](assets/connect-server.png)

1. 单击&#x200B;**完成**。 随即会创建项目结构。

   >[!NOTE]
   >
   >在全新安装后（更具体地说，当从未下载Maven依赖项时），您可能会收到创建的项目并出现错误。 在这种情况下，请按照[解析无效项目定义](#resolving-invalid-project-definition)中描述的过程操作。

## 如何导入现有项目{#how-to-import-existing-projects}

您可以使用&#x200B;**新建项目**&#x200B;功能为您创建正确的结构：

1. 按照创建[示例多模块项目](#sample-multi-module-project)的说明操作，您将为您创建以下项目，这样可以正常地分离问题：

   * `PROJECT.ui.apps` 和 `/apps` 内 `/etc` 容
   * `PROJECT.ui.content`  `/content` 的
   * `PROJECT.core` （当您想要添加Java代码时，这些包会变得有趣）
   * `PROJECT.it.launcher` 和 `PROJECT.it.tests` 集成测试

1. 将`PROJECT.ui.apps`项目的内容替换为包的`apps`和`etc`文件夹：

   1. 在“项目资源管理器”面板中，展开`PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 右键单击`apps`文件夹，然后选择&#x200B;**显示在** > **系统资源管理器**&#x200B;中。
   1. 删除您现在应该看到的`apps`和`etc`文件夹，并将其放置到此处，查看内容包的`apps`和`etc`文件夹。
   1. 在Eclipse中，右键单击`PROJECT.ui.apps`项目并选择&#x200B;**刷新**。

1. 然后，对`PROJECT.ui.content`执行相同的操作，并将其content文件夹替换为您的包中的一个：

   1. 在“项目资源管理器”面板中，展开`PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 右键单击更深的内容文件夹，然后选择&#x200B;**显示在** -> **系统资源管理器**。
   1. 删除您现在应该看到的内容文件夹，并将其放置到此处，即内容包的内容文件夹。
   1. 在Eclipse中，右键单击`PROJECT.ui.content`项目并选择&#x200B;**刷新**。

1. 现在，您必须更新这两个项目的`filter.xml`文件，以与内容包的内容相对应。 为此，请在单独的文本/代码编辑器中打开内容包的`META-INF/vault/filter.xml`文件。

   * 以下是`filter.xml`文件外观的示例：

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

1. 至于已拆分为两个项目的包内容，您还必须将这些过滤器规则拆分为两个，并相应地更新两个项目的`filter.xml`文件。

   1. 在Eclipse中，打开`PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 将`<workspaceFilter>`元素的内容替换为包中以`/apps`和`/etc`开头的规则
      * 例如：

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. 然后打开`PROJECT.ui.content/src/main/content/META-INF/filter.xml`。
   1. 将规则替换为以`/content`开头的包规则。
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

1. 在“服务器”面板中，确保已启动连接，如果未启动连接，请确保已启动连接。
1. 单击&#x200B;**清理并发布**&#x200B;图标。

完成后，您应在实例上运行包，在保存后，任何更改都会自动同步到实例。

如果希望在项目外重新构建包，请右键单击`PROJECT.ui.apps`或`PROJECT.ui.content`并选择&#x200B;**以**&#x200B;方式运行 — > **Maven Install**。

现在，您有一个目标文件夹，该文件夹已随包一起创建(例如，`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`)。

## 疑难解答 {#troubleshooting}

### 解决无效的项目定义{#resolving-invalid-project-definition}

要解决无效的依赖项，项目定义将按如下步骤进行：

1. 选择所有已创建的项目。
1. 右键单击。
1. 在上下文菜单中，选择&#x200B;**Maven** -> **更新项目**。
1. 检查&#x200B;**Force Updates of Snapshot/Releases**。
1. 单击&#x200B;**确定**。

Eclipse下载所需的依赖项。 这可能需要一些时间。

## 更多信息{#more-information}

适用于Eclipse网站的官方Apache Sling IDE工具为您提供了以下有用信息：

* [**Apache Sling IDE Eclipse**&#x200B;用户指南](https://sling.apache.org/documentation/development/ide-tooling.html)工具中，本文档将指导您完成AEM开发工具支持的总体概念、服务器集成和部署功能。
* [疑难解答部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知问题列表](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官方的[Eclipse](https://eclipse.org/)文档可帮助设置您的环境：

* [Eclipse快速入门](https://eclipse.org/users/)
* [Eclipse Luna帮助系统](https://help.eclipse.org/luna/index.jsp)
* [Maven集成(m2eclipse)](https://www.eclipse.org/m2e/)
