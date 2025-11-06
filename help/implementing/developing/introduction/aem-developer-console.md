---
title: AEM AS A CLOUD SERVICE DEVELOPER CONSOLE - BETA
description: 了解CRXDE Lite和AEM as a Cloud Service Developer Console。
feature: Developing
role: Admin, Developer
exl-id: 4b0fc3e9-b7c4-4c95-bd97-8b24e4d5cb3d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# AEM as a Cloud Service Developer Console (Beta) {#developer-console}

>[!NOTE]
>
>本文介绍了经过改版的AEM Cloud Service Developer Console体验，该体验现在处于测试阶段。 某些客户可以通过单击经典UI顶部的按钮来访问此编辑器。 Adobe欢迎您提出任何反馈，只需将其发送给`aemcs-new-devconsole-ui-beta@adobe.com`即可。 有关经典AEM Developer Console的信息，请参阅[本文](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)。

AEM as a Cloud Service Developer Console包含一组用于在云环境中进行调试的工具。 可以通过Cloud Manager中的按环境链接访问该环境。

>[!NOTE]
>不应混淆AEM as a Cloud Service Developer Console与类似名称的&#x200B;[*Adobe Developer Console*](https://developer.adobe.com/developer-console/)。
>


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

开发人员可以访问下述功能：

## OSGi包 {#osgi-bundles}

![开发控制台中的新OSGi包屏幕](/help/implementing/developing/introduction/assets/osgi-bundles.png)

* 在所选环境类型中部署的OSGi包概述。 它支持全文搜索。
* 获取环境中捆绑包的实际状态信息很有用。 您可以获取相关信息，例如导出的资源包、导入的资源包、使用的服务等。
* 开发人员希望在实际环境中进行验证，并检查捆绑包是否实现了他们期望的功能。
* **示例用例：**&#x200B;您的捆绑包中指定了依赖项的版本范围。 依赖项出现问题。 您希望检查将哪个依赖项版本连接到捆绑包中。 要进行检查，请转到捆绑包详细信息，然后使用导入捆绑包/包来检查运行时使用的捆绑包版本或包版本。 利用此信息，您可以调整maven依赖项版本范围或调整代码。

## Java包 {#java-packages}

开发控制台UI中的![Java包选项卡](/help/implementing/developing/introduction/assets/java-packages-dev-console-ui.png)

* 搜索提示，可用于搜索在环境的OSGI系统中活动的包。 在此位置中，您可以看到哪个捆绑包导出（或提供）包，以及哪个捆绑包导入（或使用）包。 您还可以检查重复的软件包（同一软件包、不同版本），这在某些情况下会导致问题。
* **示例用例：**&#x200B;使用[动态类加载器](https://sling.apache.org/apidocs/sling9/org/apache/sling/commons/classloader/DynamicClassLoaderManager.html)的自定义服务加载类而不指定版本。 由于多个捆绑包导出不同的版本，因此实施会有所不同，从而导致行为发生变化。 开发人员希望检查哪些包位于环境中，而不分析功能模型。 他们搜索资源包，并查看所有导出的版本。 此功能为他们提供了输入更好的版本范围的信息。

## Servlet {#servlets}

开发控制台UI中的![Servlet选项卡](/help/implementing/developing/introduction/assets/servlets-dev-console-ui.png)

* 搜索提示，您可以在其中指定带有选择器的路径以及带有GET或POST的扩展名。 然后，它会按优先顺序提供servlet的结果，以在Sling中处理请求。
* **示例用例：**&#x200B;您有一个OSGI servlet，它应在请求时激活并将输出打印到响应。 但是，响应将返回空，而不是预期的输出。 您需要检查由于更具体的选择器、`resourceType`、扩展或排名，某些其他servlet是否优先于您的servlet。 搜索预期路径，然后发现另一个排名较高的servlet处于活动状态。 然后，您决定是否可以通过添加选择器来获得排名在前的servlet，例如。

## 服务 {#services}

开发控制台UI中的![服务选项卡](/help/implementing/developing/introduction/assets/services-dev-console.png)

* 与OSGI组件视图类似，但基于服务。 您可以快速搜索哪些服务提供了某些属性。

## OSGi组件 {#osgi-components}

开发控制台UI中的![OSGi组件选项卡](/help/implementing/developing/introduction/assets/osgi-components-dev-console.png)

* 所选环境类型中存在的OSGI组件概述。 它支持全文搜索。
* 您可以获取环境中OSGI组件的实时状态。 您可以看到它满足哪些服务、提供服务的捆绑包以及激活类型（立即或延迟）。
* **示例用例1：**&#x200B;作为开发人员，您需要检查通过配置激活的组件在特定环境中是否处于活动状态。 原因是预期行为未发生。 您只需在搜索中查找该组件，然后查看该组件是否处于活动状态。
* **用例2：**&#x200B;您希望查看环境中可用的现成组件，并确定它们支持的服务。 此功能可帮助您了解有关Adobe Experience Manager as a Cloud Service的更多信息。 您可以在组件列表中签出它们。

## 集成 {#integrations}

开发控制台UI中的![集成选项卡](/help/implementing/developing/introduction/assets/integrations-dev-console-ui.png)

* 管理员能够生成、重命名和删除服务凭据和开发人员令牌。

## 存储库 {#repository}

* 打开[存储库浏览器](/help/implementing/developing/tools/repository-browser.md)。

## 状态转储/查询 {#status-dumps-queries}

![开发控制台UI中的“状态转储/查询”选项卡](/help/implementing/developing/introduction/assets/status-dumps-queries.png)

* 包、包、配置、服务、组件、sling作业或Oak定义的当前状态的全文或JSON转储。
* 当开发人员发现一些意外的状态，并希望与其他开发人员通信或记录此状态时特别有用。 下载转储将为您提供状态的快照以供以后参考。

## 配置 {#configurations}

开发控制台UI中的![配置选项卡](/help/implementing/developing/introduction/assets/configurations-dev-console.png)

* 环境中活动的配置的可搜索列表。 您可以通过查看详细信息页面来查看配置提供了哪些属性。
* **示例用例：**&#x200B;开发人员希望确保他们指定的配置实际存在于环境中。 如果缺少配置，他们可以检查特征模型或配置运行模式或文件夹。

对于生产程序，Adobe Admin Console中的“Cloud Manager — 开发人员角色”可控制对AEM as a Cloud Service Developer Console的访问。 对于沙盒程序，任何拥有授予AEM访问权限的产品配置文件的用户都可以使用Developer Console。 对于所有程序，状态转储和访问存储库浏览器需要“Cloud Manager — 开发人员角色”。 要查看创作和发布服务中的数据，还必须将用户分配到这两个服务上的AEM用户或AEM管理员产品配置文件。

有关设置用户权限的详细信息，请参阅[Cloud Manager文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)。

