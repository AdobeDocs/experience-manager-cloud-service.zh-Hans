---
title: AEM as a Cloud Service Developer Console (Beta)
description: 了解CRX/DE Lite和AEM as a Cloud Service Developer Console
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 16379d9cb7cdf876502205c12a233a95b410a67a
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---


# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>本文介绍了经过改版的AEM Cloud Service Developer Console体验，该体验现在为测试版，可通过单击经典UI顶部的按钮向某些客户提供。 感谢您向`aemcs-new-devconsole-ui-beta@adobe.com`发送任何反馈。 有关经典AEM Developer Console的信息，请参阅[本文](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

## AEM as a Cloud Service 开发工具 {#aem-as-a-cloud-service-development-tools}

>[!NOTE]
>不应混淆AEM as a Cloud Service Developer Console与类似名称的&#x200B;[*Adobe Developer Console*](https://developer.adobe.com/developer-console/)。
>

客户可以在创作层的开发环境中访问CRXDE Lite，但不能在暂存或生产环境中访问。 运行时无法写入不可变存储库(`/libs`， `/apps`)，因此尝试这样做会导致错误。

相反，存储库浏览器可以从AEM as a Cloud Service Developer Console启动，为创作、发布和预览层上的所有环境提供到存储库的只读视图。 有关详细信息，请参阅[存储库浏览器](/help/implementing/developing/tools/repository-browser.md)。

AEM as a Cloud Service Developer Console中为RDE、开发、暂存和生产环境提供了一组用于调试AEM as a Cloud Service开发人员环境的工具。 可以通过调整Author或Publish服务URL来确定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作为快捷方式，以下Cloud Manager CLI命令可用于基于如下所述的环境参数启动AEM as a Cloud Service Developer Console：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

有关详细信息，请参阅[发行信息](/help/release-notes/home.md)。

开发人员可以生成状态信息，并解析各种资源。

如下图所示，可用状态信息包括包、组件、OSGI配置、Oak索引、OSGI服务和Sling作业的状态。

### OSGi包 {#osgi-bundles}

![开发控制台中的新OSGi包屏幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 这将生成在选定环境类型上部署的OSGI捆绑包概述。 它支持全文搜索。
* 获取环境中捆绑包的实际状态信息很有用。 您可以获取相关信息，例如导出的资源包、导入的资源包、使用的服务等。
* 开发人员希望在实际环境中进行验证，并检查捆绑包是否实现了他们期望的功能。
* **示例用例：**&#x200B;您的捆绑包中指定了依赖项的版本范围。 依赖项出现问题。 您希望检查将哪个依赖项版本连接到捆绑包中。 要检查此问题，请转到捆绑包详细信息，然后使用导入捆绑包/包来检查运行时使用的是哪个捆绑包版本或包版本，以查明该捆绑包版本。 利用此信息，您可以调整maven依赖项版本范围或调整代码。

### Java包 {#java-packages}

开发控制台UI中的![Java包选项卡](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 这将提供一个搜索提示，您可以使用它来搜索环境的OSGI系统中活动的包。 在此位置中，您可以看到哪个捆绑包导出（或提供）包，以及哪个捆绑包导入（或使用）包。 您还可以检查重复的软件包（同一软件包、不同版本），这在某些情况下会导致问题。
* **示例用例：**&#x200B;使用[动态类加载器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)的自定义服务正在加载未指定版本的类（该版本由具有不同版本的多个捆绑包导出），从而导致实现不同且行为发生变化。 开发人员希望查看环境中有哪些软件包，而不分析功能模型，因此他们搜索此软件包并查看正在导出的所有版本。 这为他们提供了输入更好的版本范围的信息。

### Servlet {#servlets}

开发控制台UI中的![Servlet选项卡](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* 这将提供搜索提示，您可以在其中指定带有选择器的路径以及带有GET或POST的扩展名。 然后，它会按优先顺序提供servlet的结果，这些结果将在Sling中处理请求。
* **示例用例：**&#x200B;您有一个应该在请求上激活的OSGI servlet并将某些内容打印到响应，但您收到的是空响应。 您需要检查由于更具体的选择器、`resourceType`、扩展或排名，某些其他servlet是否优先于您的servlet。 搜索预期路径，然后发现另一个排名较高的servlet处于活动状态。 然后，您决定是否可以通过添加选择器来获得排名在前的servlet，例如。

### 服务 {#services}

开发控制台UI中的![服务选项卡](/help/implementing/developing/introduction/assets/services-dev-console.png)

* 与OSGI组件视图类似，但基于服务。 您可以快速搜索哪些服务提供了某些属性。

### OSGi组件 {#osgi-components}

开发控制台UI中的![OSGi组件选项卡](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 这会生成所选环境类型中存在的OSGI组件的概述。 它支持全文搜索。
* 您可以获取环境中OSGI组件的实时状态。 您可以看到它满足哪些服务、提供服务的捆绑包以及激活类型（立即或延迟）。
* **示例用例1：**&#x200B;作为开发人员，您要验证通过配置激活的组件是否在特定环境中处于活动状态，因为您没有获得预期的行为。 您只需在搜索中查找该组件，并检查该组件是否处于活动状态。
* **用例2：**&#x200B;您有兴趣了解环境中存在哪些开箱即用的组件以及它们满足哪些服务，以了解有关Adobe Experience Manager as a Cloud Service的更多信息。 您可以在组件列表中签出它们。

### 集成 {#integrations}

开发控制台UI中的![集成选项卡](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 使管理员能够生成、重命名和删除服务凭据和开发人员令牌。

### 存储库 {#repository}

* 打开[存储库浏览器](/help/implementing/developing/tools/repository-browser.md)。

### 状态转储/查询 {#status-dumps-queries}

![开发控制台UI中的“状态转储/查询”选项卡](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* 提供包、包、配置、服务、组件、sling作业或oak定义的当前状态的全文或JSON转储。
* 如果开发人员发现一些意外的状态，并且希望与其他开发人员进行通信或记录此状态，此功能会特别有用。 下载转储将为您提供状态的快照以供以后参考。

### 配置 {#configurations}

开发控制台UI中的![配置选项卡](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 这将为您提供在环境中处于活动状态的可搜索配置列表。 您可以通过查看详细信息页面来查看配置提供了哪些属性。
* **示例用例：**&#x200B;开发人员希望确保他们指定的配置实际存在于环境中。 如果缺少配置，他们可以检查特征模型或配置运行模式或文件夹。

对于生产程序，对AEM as a Cloud Service Developer Console的访问权限由Adobe Admin Console中的“Cloud Manager — 开发人员角色”定义，而对于沙盒程序，AEM as a Cloud Service Developer Console可供任何拥有产品配置文件的用户访问AEM as a Cloud Service。 对于所有程序，状态转储和存储库浏览器需要“Cloud Manager — 开发人员角色”，您还必须在创作和发布服务的AEM用户或AEM管理员产品配置文件中定义用户，才能查看来自这两个服务的数据。 有关设置用户权限的详细信息，请参阅[Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。