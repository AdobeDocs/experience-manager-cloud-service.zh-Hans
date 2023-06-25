---
title: 快速开发环境
description: 了解如何使用快速开发环境在云环境中进行快速开发迭代。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '3318'
ht-degree: 5%

---

# 快速开发环境 {#rapid-development-environments}

要部署更改，当前的云开发环境需要使用采用称为CI/CD管道的广泛代码安全和质量规则的流程。 对于需要快速和反复更改的情况，Adobe引入了快速开发环境（简称RDE）。

RDE允许开发人员快速部署和审查更改，从而最大限度地减少测试经验证可在本地开发环境中工作的功能所需的时间。

在RDE中测试更改后，可以通过Cloud Manager管道将它们部署到常规云开发环境。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以参考其他演示视频 [如何设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)， [如何使用](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)，以及 [开发生命周期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) 使用RDE。

## 简介 {#introduction}

RDE可用于代码、内容以及Apache或Dispatcher配置。 与常规云开发环境不同，开发人员可以使用本地命令行工具将本地构建的代码同步到RDE。

每个项目都配有RDE。 对于Sandbox帐户，它们会在数小时未使用后休眠。

创建后，会将RDE设置为最新可用的AEM版本。 可以使用Cloud Manager执行的RDE重置将循环RDE并将其设置为最新可用的AEM版本。

通常，单个开发人员在给定时间会使用RDE来测试和调试特定功能。 开发会话完成后，RDE可以重置为默认状态以供下次使用。

可以为生产（非沙盒）程序许可其他RDE。

## 在程序中启用RDE {#enabling-rde-in-a-program}

按照以下步骤使用Cloud Manager为您的项目创建RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要向其添加RDE的程序以显示其详细信息。

   * 可以将RDE添加到这两个 [沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [生产程序。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. 从&#x200B;**程序概述**&#x200B;页面，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**添加环境**&#x200B;以添加环境。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

     ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 选择 **快速开发** 在 **选择环境类型** 标题。
      * 可用/已用环境的数量显示在环境类型后面的括号中。
   * 提供 **名称** 环境方面的。
   * 提供一个可选的 **描述** 环境方面的。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。 

创建后，会将RDE设置为最新可用的AEM版本。 也可以使用Cloud Manager执行的RDE重置将循环RDE并将其设置为最新可用的AEM版本。

有关使用Cloud Manager创建环境、管理有权访问环境的人以及分配自定义域的更多信息，请参阅 [Cloud Manager文档。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安装RDE命令行工具 {#installing-the-rde-command-line-tools}

在使用Cloud Manager为程序添加RDE后，您可以通过设置命令行工具与其交互，如以下步骤中所述：

>[!IMPORTANT]
>
>确保您拥有最新版本的 [节点和NPM已安装](https://nodejs.org/en/download/) 以使Adobe I/OCLI和相关插件正常工作。


1. 按照以下步骤安装Adobe I/OCLI工具 [此处](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安装Adobe I/OCLI tools cloud manager插件，并按照所述对其进行配置 [此处](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 通过运行以下命令来安装Adobe I/OCLI工具AEM RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 为组织ID配置Cloud Manager插件：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   并将字母数字字符串替换为您自己的组织ID，您可以使用策略查找该ID [此处](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 接下来，配置您的项目ID：

   `aio config:set cloudmanager_programid 12345`

1. 然后，配置要将RDE附加到的环境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 配置完插件后，通过执行

   `aio login`

   成功登录时的响应应类似于下面的输出，但您可以忽略显示的值。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   注意：此步骤要求您是Cloud Manager的成员 **开发人员 — Cloud Service** 产品配置文件。 参见 [此页面](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 了解更多详细信息。

   或者，如果可以通过运行此命令登录到开发人员控制台，则可以确认您具有此开发人员角色：

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >如果您看到 `Warning: cloudmanager:list-programs is not a aio command.` 错误，您需要安装 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 通过运行以下命令：
   >
   >```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. 通过运行来验证登录是否成功完成

   `aio cloudmanager:list-programs`

   这应列出您配置的组织下的所有程序。


欲知更多信息和演示，请参见 [如何设置RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) 视频教程。

## 在开发新功能时使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建议通过以下工作流程来开发新功能：

* 当达到中间里程碑并通过AEMas a Cloud ServiceSDK在本地成功验证时，代码应提交到尚未成为主行一部分的Git功能分支，尽管提交到Git是可选的。 构成“中间里程碑”的因素因团队习惯而异。 示例包括几行新代码、半天的工作或完成一个子功能。

* 如果RDE已由其他功能使用并且您希望 [将其重置为默认状态](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重置将需要几分钟的时间，并且所有现有内容和代码都会被删除。 您可以使用RDE status命令确认RDE已就绪。 RDE将带回最新的AEM发行版本。

  >[!IMPORTANT]
  >
  > 如果您的暂存环境和生产环境未收到自动AEM版本更新，并且远低于最新的AEM版本版本，请注意，在RDE上运行的代码可能与代码在暂存环境和生产环境中的运行方式不匹配。 在这种情况下，在将代码部署到生产环境之前，在暂存环境中对代码执行彻底测试尤为重要。


* 使用RDE命令行界面，将本地代码同步到RDE。 选项包括安装内容包、特定捆绑包、OSGI配置文件、内容文件和Apache/Dispatcher配置的zip文件。 也可以引用远程内容包。 请参阅 [RDE命令行工具](#rde-cli-commands) 部分以了解更多信息。 您可以使用status命令来验证部署是否成功。 （可选）使用包管理器安装内容包。

* 在RDE中测试代码。 Cloud Manager中提供了作者和发布URL。

* 如果代码的行为与预期不符，请使用标准调试技术了解问题并进行适当的更改。 无需将代码修改提交到Git（因为它们尚未验证），请使用本地CLI将代码同步到RDE。 不断迭代，直到问题得到解决。

* 一旦代码按预期运行，将代码提交到Git功能分支。

* 同步到RDE的代码不使用Cloud Manager管道，因此现在应使用Cloud Manager非生产管道将Git功能分支部署到云开发环境。 这将验证代码是否通过Cloud Manager质量关卡，并让您确信代码稍后将使用Cloud Manager生产管道成功部署。

* 对每个中间里程碑重复上述步骤，直到功能的所有代码准备就绪，并在RDE和云开发环境中运行良好。

* 通过Cloud Manager生产管道将代码部署到生产环境。

## 使用RDE调试现有功能 {#use-rde-to-debug-an-existing-feature}

该工作流类似于开发新功能。 区别在于，同步到RDE的代码将反映推送到发现问题的环境的任何内容的Git标签。 此外，部署与上游环境匹配的内容可能很有用。 这可以通过导出和导入内容包来实现。

## 多个开发人员在同一个代码上协作 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支持一个项目。 由于代码从本地开发环境同步到RDE环境，因此对于一个开发人员而言，在给定时间自行使用它最为自然。

但是，通过仔细的协调，多个开发人员可以验证特定功能或调试特定问题。 关键是每个开发人员都会保持其本地项目的同步，以便特定开发人员所做的代码更改被其他开发人员吸收，否则一个开发人员可能会无意中覆盖另一个开发人员的代码。 推荐的策略是，每个开发人员在同步到RDE之前将其更改提交到共享Git分支，以便其他开发人员在做出自己的更改之前提取更改。

## RDE命令行工具命令 {#rde-cli-commands}

### 帮助/一般信息 {#help}

* 要获取命令列表，请键入：

  `aio aem:rde`

* 有关命令的详细帮助，请键入：

  `aio aem rde <command> --help`

### 部署到RDE {#deploying-to-rde}

本节介绍如何使用RDE CLI部署、安装或更新包、OSGI配置、内容包、单个内容文件以及Apache或Dispatcher配置。

一般使用模式为 `aio aem:rde:install <artifact>`.

您可以找到下面的一些示例：

<u>部署内容包</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的响应如下所示：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

或者，您可以引用远程存储库：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

默认情况下，工件会同时部署到创作层和发布层，但“ — s”标记可用于定位特定层。

可以部署任何AEM包，例如包含代码、内容或 [容器包](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （也称为“所有”包）。

>[!IMPORTANT]
>
>WKND项目的Dispatcher配置不是通过上述内容包安装部署的。 您需要按照“部署Apache/Dispatcher配置”步骤单独部署它。

<u>部署OSGI配置</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

其中成功部署的响应类似于以下内容：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署捆绑包</u>

要部署捆绑包，请使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

其中成功部署的响应类似于以下内容：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署内容文件</u>

要部署内容文件，请使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

其中成功部署的响应类似于以下内容：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher配置</u>

对于此类配置，整个文件夹结构需要采用zip文件的形式。

从 `dispatcher` AEM项目的模块，您可以通过运行以下maven命令来压缩Dispatcher配置：

`mvn clean package`

或使用以下zip命令 `src` 目录 `dispatcher` 模块：

`zip -y -r dispatcher.zip .`

然后使用此命令部署配置：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假定您部署的是 [WKND](https://github.com/adobe/aem-guides-wknd) 项目的Dispatcher配置。 请确保更换 `X.X.X` 使用相应的WKND项目版本号或特定于项目的版本号部署项目的Dispatcher配置时。

>[!NOTE]
>
>RDE支持“灵活模式”Dispatcher配置，但不支持“旧模式”Dispatcher配置。 参见 [dispatcher文档](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以了解有关这两种模式的信息。 您还可以参阅以下文档 [迁移到灵活模式](/help/implementing/dispatcher/validation-debug.md#migrating)，如果您尚未这样做。

成功部署将生成类似于以下内容的响应：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的代码不会经历Cloud Manager管道及其关联的质量关卡，但代码会经历一些分析，这些分析将报告错误，如下面的代码示例所示：

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

上述代码示例说明了当捆绑包未解析时的行为，在此情况下，捆绑包为“暂存”捆绑包，并且仅当通过安装其他代码来满足其要求（在本例中缺少导入）时，才会安装捆绑包。

### 检查RDE的状态 {#checking-rde-status}

您可以使用RDE CLI检查环境是否已准备好部署到，以及已通过RDE插件进行了哪些部署。

正在运行:

`aio aem:rde:status`

将返回：

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

如果该命令返回有关实例部署的注释，您仍然可以执行下一次更新，但您的上一个更新可能尚未在该实例上显示。

### 显示部署历史记录 {#show-deployment-history}

您可以通过运行以下命令来检查对RDE进行的部署的历史记录：

`aio aem:rde:history`

将返回响应，其形式为：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 从RDE删除 {#deleting-from-rde}

您可以通过CLI工具删除以前部署到RDE的配置和捆绑包。 使用 `status` 命令以列出可删除的内容，其中包括 `bsn` 对于捆绑包和 `pid` 用于在delete命令中引用的配置。

例如，如果 `com.adobe.granite.demo.MyServlet.cfg.json` 已安装， `bsn` 只是 `com.adobe.granite.demo.MyServlet`，不使用 **cfg.json** 后缀。

不支持删除内容包或内容文件。 要删除它们，应重置RDE，以使其恢复到默认状态。

有关更多详细信息，请参阅以下示例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

欲知更多信息和演示，请参见 [如何使用RDE命令](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) 视频教程。

## 重置 {#reset-rde}

重置RDE会同时从创作实例和发布实例中删除所有自定义代码、配置和内容。 例如，如果已使用RDE测试特定功能，并且您要将它重置为默认状态，以便可以测试其他功能，则这种重置非常有用。

重置会将RDE设置为最新可用的AEM版本。

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code is deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role to use the reset feature. If not, a reset action results in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

您可以使用Cloud Manager通过以下步骤重置RDE：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要为其重置RDE的程序。

1. 在&#x200B;**概述**&#x200B;页面中，单击屏幕顶部的&#x200B;**环境**&#x200B;选项卡。

   ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**全部显示**&#x200B;按钮，直接跳转到&#x200B;**环境**&#x200B;选项卡。

     ![显示所有选项](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 此 **环境** 窗口将打开并列出程序的所有环境。

   ![“环境”选项卡](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 单击要重置的RDE的省略号按钮，然后选择 **重置**.

   ![查看环境详细信息](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 通过单击确认要重置RDE **重置** 在对话框中。

   ![确认重置](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager通过横幅通知确认重置过程已启动。

   ![重置横幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重置过程启动后，通常需要几分钟才能完成，并且环境将恢复到其默认状态。 您可以随时在中查看重置过程的状态。 **状态** 列 **环境** 信息卡或 **环境** 窗口。

![RDE重置状态](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您还可以直接从使用省略号按钮重置RDE **环境** 上的信息卡 **概述** 页面。

![从环境信息卡重置RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有关如何使用Cloud Manager管理环境的更多信息，请参阅 [Cloud Manager文档。](/help/implementing/cloud-manager/manage-environments.md)

## 运行模式 {#runmodes}

可以通过在文件夹名称上使用后缀来应用特定于RDE的OSGI配置，如下面的示例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

请参阅 [运行模式文档](/help/implementing/deploying/overview.md#runmodes) 以获取有关运行模式的一般信息。

>[!NOTE]
>
>RDE OSGI配置的唯一之处在于，它继承由捆绑包的所声明的任何OSGI属性的值。 `dev` 运行模式。

RDE与其他环境不同，因为其内容可以安装在/apps下的install.rde文件夹（或install.author.rde或install.publish.rde）中。 这允许您使用命令行工具将内容提交到Git并将其交付到RDE。

## 使用内容填充 {#populating-content}

重置RDE时，将删除所有内容，因此如果需要，必须执行显式操作以添加内容。 作为最佳实践，请考虑汇编一组内容以用作测试内容，以便在RDE中验证或调试功能。 有几种可能的策略可使用该内容填充RDE：

1. 使用命令行工具将内容包显式同步到RDE

1. 将示例内容放置并提交git中的/apps下的install.rde文件夹中，然后使用命令行工具将总体内容包同步到RDE。

1. 使用 [内容复制工具](/help/implementing/developing/tools/content-copy.md) 从生产、暂存或开发环境或其他RDE中复制定义的内容集。

1. 使用包管理器

请注意，同步内容包时，限制为1GB。

## 日志记录 {#logging}

可以通过修改OSGi配置来设置日志级别。 查看 [文档](/help/implementing/developing/introduction/logging.md) 了解更多信息。

## RDE与云开发环境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

虽然RDE在许多方面类似于云开发环境，但在体系结构上存在细微差异，因此无法快速同步代码。 将代码获取到RDE的机制不同 — 对于RDE，一个代码从本地开发环境同步，而对于Cloud开发环境，一个代码通过Cloud Manager部署代码。

出于这些原因，建议在RDE环境中验证代码后，使用非生产管道将代码部署到云开发环境。 最后，在使用生产管道进行部署之前测试代码。

另请注意以下注意事项：

* RDE不包含预览层
* RDE当前不支持查看和调试使用Cloud Manager前端管道部署的前端代码。
* RDE当前不支持预发行版渠道。


## 我需要多少个RDE？ {#how-many-rds-do-i-need}

RDE可用于每个许可的解决方案，Adobe还提供了其他RDE，可以针对生产（非沙盒）程序授予许可。

所需的RDE数量取决于组织的构成和流程。 最灵活的模型是组织为每个AEM Cloud Service开发人员购买专用RDE。 在此模型中，每个开发人员都可以在RDE上测试其代码，而无需与其他团队成员就RDE环境是否可用进行协调。

在另一个极端情况下，具有单个RDE的团队可以使用内部进程来协调哪些开发人员可以在给定时间使用环境。 这可以是每当开发人员达到中间功能里程碑并准备好在云环境中进行验证时，开发人员可以在其中快速做出所需的更改。

中间模型是指组织购买多个RDE，因此存在更大可能性的未使用RDE可用。 一种策略可以是每个scrum团队或主要功能分配RDE。 可以使用内部进程来协调环境的使用。

## AEM FormsCloud Service快速开发环境(RDE)与其他环境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms开发人员可以使用AEM FormsCloud Service快速开发环境快速开发自适应Forms、工作流和自定义项，如自定义核心组件、与第三方系统的集成等。 AEM FormsCloud Service快速开发环境(RDE)不支持通信API以及需要记录文档的功能，例如在提交自适应表单时生成记录文档。 以下列出的AEM Forms功能在快速开发环境(RDE)中不可用：

* 为自适应表单配置记录文档
* 在提交自适应表单时或通过工作流步骤生成记录文档
* 通过电子邮件提交操作或工作流中的电子邮件步骤将记录文档作为附件发送
* 在自适应表单或工作流步骤中使用Adobe Sign
* 通信API

>[!NOTE]
>
> 快速开发环境(RDE)的UI与Forms的其他Cloud Service环境没有区别。 所有与记录文档相关的选项（如为自适应表单选择记录文档模板）将继续显示在UI中。 这些环境没有通信API和记录文档功能来测试这些选项。 因此，当您选择需要通信API或记录文档功能的任何选项时，不会执行任何操作，并且会显示或返回错误消息。

## rde教程

要了解AEMas a Cloud Service中的RDE，请参阅 [演示如何设置、如何使用以及开发生命周期的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
