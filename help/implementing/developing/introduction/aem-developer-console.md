---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: 了解AEM as a Cloud Service Developer Console及其一组用于调试云环境的只读工具。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: 51c14ba3c15e0136911003752253d21ed673a0eb
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

AEM as a Cloud Service Developer Console包含一组用于调试云环境的只读工具。 可以通过Cloud Manager中的按环境链接访问它，并提供查看捆绑包、OSGi设置、服务和servlet等的功能。

>[!NOTE]
>
>本文介绍了经过改版的AEM Cloud Service Developer Console体验，该体验现在处于测试阶段。
>
>* 有限的一组用户可以通过当前Developer Console顶部的按钮访问新控制台。
>* Adobe欢迎您提出任何反馈，您可以将这些反馈发送至`aemcs-new-devconsole-ui-beta@adobe.com`。
>* 有关当前AEM Developer Console的文档，请参阅[本文。](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)
>* 不应混淆AEM as a Cloud Service Developer Console与名称类似的&#x200B;[*Adobe Developer Console*.](https://developer.adobe.com/developer-console/)

>[!TIP]
>
>Developer Console是只读的。 如果您使用SDK进行本地开发，并且需要修改OSGi设置或存储库内容，则可以使用：
>
>* [CRXDE Lite](/help/implementing/developing/tools/crxde.md)

<!--
There are multiple ways of accessing it:

1. Launch from Cloud Manager  

1. Type a url that can be determined by adjusting the Author or Publish service urls as follows:
   ```  
   https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com
   ```  

1. As a shortcut, the following Cloud Manager CLI command can be used to launch the AEM as a Cloud Service Developer Console based on an environment parameter described below:    
   ```
   aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>
   ```
-->

## 先决条件 {#prerequisites}

Developer Console仅供在某些项目中拥有特定角色的用户访问。

* 对于生产程序，Adobe Admin Console中的“Cloud Manager — 开发人员角色”可控制对Developer Console的访问。
* 对于沙盒程序，任何拥有授予AEM访问权限的产品配置文件的用户都可以使用Developer Console。
* 对于所有程序，状态转储和访问存储库浏览器需要“Cloud Manager — 开发人员角色”。

要查看创作和发布服务中的数据，还必须将用户分配到这两个服务上的“AEM用户”或“AEM管理员产品配置文件”。

有关设置用户权限的详细信息，请参阅[Cloud Manager文档。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## “OSGi包”选项卡 {#osgi-bundles}

**OSGi包**&#x200B;选项卡概述了在选定环境中部署的OSGi包，并提供了全文搜索。

![Developer Console中的新OSGi包屏幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 选项卡提供有关环境中捆绑包的实际状态的信息，例如导出的资源包、导入的资源包、使用的服务等。
* 最好检查捆绑的状态，以查看捆绑是否按预期执行。

**示例用例：**&#x200B;假设您为捆绑包中的依赖项指定版本范围。 但依赖项出现问题，您需要检查捆绑包实际使用了依赖项的哪个版本。 要检查，请打开Developer Console并单击&#x200B;**OSGi包**&#x200B;选项卡上的包名称以访问包详细信息，并使用&#x200B;**导入包**&#x200B;折叠面板检查运行时使用的包版本或包版本。 利用此信息，您可以调整maven依赖项版本范围或调整代码。

## “Java包”选项卡 {#java-packages}

**Java包**&#x200B;选项卡提供了一个搜索字段，用于搜索在环境的OSGi系统中活动的包。

Developer Console UI中的![Java包选项卡](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 您可以查看哪个捆绑包导出（或提供）包，以及哪些捆绑包导入（或使用）包。
* 您还可以检查重复的软件包（同一软件包、不同版本），这在某些情况下会导致问题。

**示例用例：**&#x200B;假设使用[动态类加载器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)的自定义服务加载了类而没有指定版本。 由于多个捆绑包导出不同的版本，因此实施会有所不同，从而导致行为发生变化。 要检查哪些包位于环境中，而不分析特征模型。 使用此选项卡，您可以搜索包并查看所有导出的版本，然后可以使用更好的版本范围。

## “配置”选项卡 {#configurations}

**配置**&#x200B;选项卡提供了环境中活动的配置的可搜索列表。 您可以通过单击每个配置并查看详细信息页面来查看它提供了哪些属性。

Developer Console UI中的![配置选项卡](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* **示例用例：**&#x200B;假设您希望确保指定的配置实际存在于环境中。 如果在控制台中搜索&#x200B;**配置**&#x200B;选项卡并且缺少配置，则可以检查功能模型、配置运行模式或文件夹。

## Servlet选项卡 {#servlets}

**Servlet**&#x200B;选项卡提供了一个搜索字段，您可以在其中指定带有选择器的路径以及带有GET或POST的扩展。 然后，它会按首选项顺序提供servlet列表，以处理Sling中的请求。

Developer Console UI中的![Servlet选项卡](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

**示例用例：**&#x200B;假设您有一个OSGi servlet，它应该在请求时激活并将输出打印到响应。 但是，您得到的不是预期输出，而是空响应。 您需要检查由于更具体的选择器、`resourceType`、扩展或排名，某些其他servlet是否优先于您的servlet。 搜索预期路径，然后找到另一个排名较高且处于活动状态的servlet。 然后，您可以决定是否可以通过添加选择器来增加servlet的排名。

## “服务”选项卡 {#services}

**服务**&#x200B;选项卡提供所选环境中存在的服务的概览，并提供全文搜索。

Developer Console UI中的![服务选项卡](/help/implementing/developing/introduction/assets/services-dev-console.png)

单击服务可查看其详细信息。

## “OSGi组件”选项卡 {#osgi-components}

**OSGi组件**&#x200B;选项卡概述了所选环境类型中存在的OSGi组件，并提供了全文搜索。 您可以查看环境中OSGi组件的活动状态及其满足的服务、提供该组件的捆绑包以及激活类型（立即或延迟）。

Developer Console UI中的![OSGi组件选项卡](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* **示例用例1：**&#x200B;假设您需要检查通过配置激活的组件在特定环境中是否处于活动状态，因为您遇到意外行为。 您只需在搜索中查找该组件，然后查看该组件是否处于活动状态。
* **用例2：**&#x200B;假设您想查看环境中有哪些现成的组件可用，并确定这些组件支持的服务，以便了解有关Adobe Experience Manager as a Cloud Service的更多信息。 可以在组件列表中检查组件。

## “集成”选项卡 {#integrations}

**集成**&#x200B;选项卡允许管理员生成、重命名和删除服务凭据和开发人员令牌。

Developer Console UI中的![集成选项卡](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

## “存储库”选项卡 {#repository}

**存储库**&#x200B;选项卡打开[存储库浏览器。](/help/implementing/developing/tools/repository-browser.md)

## “状态转储/查询”选项卡 {#status-dumps-queries}

**状态转储/查询**&#x200B;选项卡允许您下载包、包、配置、服务、组件、sling作业或Oak定义的当前状态的全文或JSON转储。

Developer Console UI中的![状态转储/查询选项卡](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

您还可以打开[查询性能工具。](/help/operations/query-and-indexing-best-practices.md#query-performance-tool)

* **示例用例：**&#x200B;如果您遇到意外状态并且希望与其他开发人员进行通信或记录该状态，此选项卡特别有用。 下载转储将为您提供状态的快照以供以后参考。
