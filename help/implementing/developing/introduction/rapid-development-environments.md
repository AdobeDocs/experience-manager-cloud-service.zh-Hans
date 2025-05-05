---
title: 快速开发环境
description: 了解如何使用快速开发环境在云环境中进行快速开发迭代。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 68937e844712ad639a495e87363d49a8bef25e05
workflow-type: tm+mt
source-wordcount: '5392'
ht-degree: 3%

---

# 快速开发环境 {#rapid-development-environments}

要部署更改，当前云开发环境需要使用采用称为CI/CD管道的广泛代码安全和质量规则的流程。 对于需要快速更改和迭代更改的情况，Adobe引入了快速开发环境（简称RDE）。

RDE使开发人员能够快速部署和审查更改，从而最大限度地减少测试在本地开发环境中已证明可以正常工作的功能所需的时间。

在RDE中测试更改后，可以通过Cloud Manager管道将它们部署到常规云开发环境。

>[!NOTE]
> 与RDE开发人员联系，了解Adobe的[不和谐频道](https://discord.com/channels/1131492224371277874/1245304281184079872)。 欢迎您就RDE主题提出任何问题或给予反馈。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以看到其他视频演示[如何设置它](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup)、[如何使用它](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use)以及使用RDE的[开发生命周期](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle)。

## 简介 {#introduction}

RDE可用于代码、内容以及Apache或Dispatcher配置。 与常规云开发环境不同，开发人员可以使用本地命令行工具将本地构建的代码同步到RDE。

每个项目均配备RDE。 如果存在沙盒帐户，则它们在处于非使用状态数小时后会休眠。

创建后，会将RDE设置为最新可用的Adobe Experience Manager (AEM)版本。 可以使用Cloud Manager执行的RDE重置会循环RDE并将其设置为最新可用的AEM版本。

通常，单个开发人员在给定时间使用RDE来测试和调试特定功能。 当开发会话完成后，RDE可以重置为默认状态以供下次使用。

可以为生产（非沙盒）程序许可其他RDE。

## 在程序中启用RDE {#enabling-rde-in-a-program}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要向其添加RDE的程序以显示其详细信息。

   * RDE可以添加到[沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)和[生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。

1. 从&#x200B;**项目概述**&#x200B;页面，在&#x200B;**环境**&#x200B;信息卡上，单击&#x200B;**添加环境**。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

     ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在&#x200B;**添加环境**&#x200B;对话框中，执行以下操作：

   * 在&#x200B;**选择环境类型**&#x200B;标题下选择&#x200B;**快速开发**。
      * 可用/已用环境的数量显示在环境类型后面的括号中。
   * 为环境提供&#x200B;**名称**。
   * 为环境提供可选的&#x200B;**描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。

创建后，会将RDE设置为最新可用的AEM版本。 RDE重置(也可以使用Cloud Manager执行)可循环RDE并将其设置为最新可用的AEM版本。

有关使用Cloud Manager创建环境、管理谁有权访问这些环境以及分配自定义域的更多信息，请参阅Cloud Manager文档中的[程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

## 安装RDE命令行工具 {#installing-the-rde-command-line-tools}

在使用Cloud Manager为程序添加RDE后，您可以通过设置命令行工具与其交互，如以下步骤中所述：

>[!IMPORTANT]
>
>确保已安装[Node和](https://nodejs.org/en/download/)的20版的NPM，以便Adobe I/O (AIO) CLI和相关插件正常工作。


1. 按照此[过程](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)安装AIO CLI工具。
1. 安装AIO CLI工具AEM RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 使用Adobe I/O (AIO)客户端登录。

   ```
   aio login
   ```

   登录信息（令牌）存储在全局aio配置中，因此仅支持一个登录和组织。 如果要使用需要不同登录或组织的多个RDE，请遵循以下引入上下文的示例。

   <details><summary>按照此示例为某个RDE登录设置本地上下文</summary>
   要将登录信息本地存储到特定上下文当前目录的“.aio”文件中，请执行以下步骤。 上下文也是设置CI/CD环境或脚本的一种巧妙方法。  要使用此功能，请确保至少使用aio-cli版本10.3.1。使用“npm install -g @adobe/aio-cli”更新它。

   现在，创建名为m`ycontext`的上下文，在调用登录命令之前，请使用auth插件将该上下文设置为默认上下文。

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > 带有`--no-open`选项的登录命令在终端中输出URL，而不是打开默认浏览器。 您可以在浏览器的&#x200B;**无痕窗口**&#x200B;中复制并打开它。 此功能可确保主浏览器窗口中的当前会话不受影响，从而允许您使用任务所需的特定帐户和组织登录。

   第一个命令将在您的本地`.aio`配置文件中创建一个名为`mycontext`的新登录上下文配置（如果需要，将创建该文件）。 第二个命令将上下文`mycontext`设置为“当前”上下文；即默认值。

   有了此配置，登录命令会自动将登录令牌存储在上下文`mycontext`中，从而使其保持在本地。

   通过将本地配置保留在多个文件夹中，可以管理多个上下文。 或者，也可以在单个配置文件中设置多个上下文，并通过更改“当前”上下文在它们之间切换。
   </details>

1. 配置RDE插件以使用您的组织、项目和环境。 下面的设置命令以交互方式为用户提供了其组织中的程序列表，并显示该程序中可供选择的RDE环境。

   ```
   aio aem:rde:setup
   ```

   如果您使用脚本环境，则可以跳过设置步骤。 在这种情况下，请直接在每个命令中包括组织、程序和环境值。 [有关详细信息，请参阅下面的RDE命令](#rde-cli-commands)。

### 交互式设置 {#installing-the-rde-command-line-tools-interactive}

setup命令会询问所提供的配置是应本地存储还是全局存储。

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

选择`no`以

* 在aio配置中全局存储组织、项目和环境。
* 仅适用于单个RDE。

选择`yes`以执行以下操作：

* 将组织、程序和环境本地存储在当前目录的`.aio`文件中。 如果您希望将文件提交到版本控制，以便其他克隆Git存储库的用户可以使用它，则此方法非常方便。
* 能够使用多个RDE ，因此切换到另一个目录时会使用该配置。
* 在脚本之类的程序化上下文中使用该配置，脚本可以引用该配置。


选择本地或全局配置后，setup命令将尝试从当前登录中读取组织id，然后读取组织的程序。 如果找不到组织，您可以手动输入该组织并提供一些指导。

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

检索程序后，用户可以从列表中选择程序，也可以键入以进行筛选。 选择程序后，将列出可供选择的RDE环境列表。 如果只有一个程序，或只有一个RDE环境可用，或两者都可用，则会自动选择该程序。

要查看当前环境上下文，请运行以下命令：

```aio aem rde setup --show```

该命令将做出响应，得到类似于以下内容的结果：

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### 非交互环境中的手动设置过程 {#manual-setup}

在没有用户可以以交互方式运行安装命令（如CI/CD或脚本）的环境中，需要手动配置。 您可以使用以下步骤设置组织、项目和环境参数。


<details>
  <summary>展开以查找有关如何手动配置的详细信息</summary>

1. 配置您的组织ID并将字母数字字符串替换为您自己的组织ID。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * 可以使用[查看组织ID](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255)下记录的方法查找您自己的组织ID。

1. 接下来，配置您的项目ID：

   `aio config:set cloudmanager_programid 12345`

1. 然后，配置要将RDE附加到的环境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 配置完插件后，请通过执行

   `aio login`

   这些步骤要求您成为Cloud Manager **开发人员 — Cloud Service**&#x200B;产品配置文件的成员。 有关更多详细信息，请参阅[将团队成员分配给Cloud Manager产品配置文件 — 分配开发人员产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)。

有关更多信息和演示，请观看视频教程[如何设置RDE (06:24)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup)。
</details>

## 在开发新功能时使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建议通过以下工作流程来开发新功能：

* 当达到中间里程碑并成功通过AEM as a Cloud Service SDK本地验证时，将代码提交到Git功能分支。 分支还不应是主行的一部分，但提交Git是可选的。 构成“中间里程碑”的因素因团队习惯而异。 示例包括几行新代码、半天的工作或完成一个子功能。

* 如果RDE已由其他功能使用，并且您希望[将其重置为默认状态](#reset-rde)，请重置该RDE。 <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->重置需要几分钟时间，并且所有现有内容和代码都会被删除。 可以使用RDE状态命令确认RDE已就绪。 RDE将随最新的AEM发行版本一起提供。

  >[!IMPORTANT]
  >
  >如果您的暂存环境和生产环境未收到自动的AEM版本更新，并且它们落后于最新版本，则RDE可能会运行其他版本的AEM。 因此，RDE中的代码行为可能与它在暂存和生产中的功能不匹配。 在这种情况下，在将代码部署到生产环境之前，务必要在暂存环境中对代码执行彻底的测试。


* 使用RDE命令行界面，将本地代码同步到RDE。 您可以安装各种类型的文件，包括：

   * 内容包
   * 特定包
   * OSGi配置文件
   * 内容文件
   * 包含Apache/Dispatcher配置的ZIP文件

  也可以引用远程内容包。 有关详细信息，请参阅[RDE命令行工具](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands)。 可以使用status命令验证部署是否成功。 或者，使用包管理器安装内容包。

* 在RDE中测试代码。 在Cloud Manager中提供了“创作”和“发布”URL。

* 如果代码的行为与预期不符，请使用标准调试技术了解问题并进行适当的更改。 无需将代码修改提交到Git（因为它们尚未验证），请使用本地CLI将代码同步到RDE。 不断迭代，直到问题得到解决。

* 一旦代码按预期运行，将代码提交到Git功能分支。

* 同步到RDE的代码不使用Cloud Manager管道，因此现在应使用Cloud Manager非生产管道将Git功能分支部署到云开发环境。 此过程会验证代码是否通过了Cloud Manager质量关卡，并让您确信代码稍后可以使用Cloud Manager生产管道成功部署。

* 对每个中间里程碑重复上述步骤，直到功能的所有代码准备就绪，并在RDE和云开发环境中正常运行。

* 通过Cloud Manager生产管道将代码部署到生产环境。

## 使用RDE调试现有功能 {#use-rde-to-debug-an-existing-feature}

该工作流与开发新功能类似。 不同之处在于，同步到RDE的代码反映的是推送到出现问题的环境的Git标签。 此工作流有助于在调查或重现问题时确保一致性。 此外，部署与上游环境匹配的内容可能很有用。 这种方法可通过导出和导入内容包来实现。

## 多位开发人员在同一个RDE上协作 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支持一个项目。 由于代码从本地开发环境同步到RDE环境，因此对于一个开发人员而言，在给定时间自行使用代码是最自然的事情。

但是，通过仔细的协调，多个开发人员可以验证特定功能或调试特定问题。 关键是每个开发人员保持其本地项目的同步，以便特定开发人员所做的代码更改被其他开发人员吸收。 否则，一个开发人员可能会无意中覆盖另一个开发人员的代码。 推荐的策略是，每个开发人员在同步到RDE之前将其更改提交到共享Git分支，以便其他开发人员在做出自己的更改之前提取更改。

## RDE命令行工具命令 {#rde-cli-commands}

### 帮助/一般信息 {#help}

* 要获取命令列表，请键入：

  `aio aem:rde`

* 有关命令的详细帮助，请键入：

  `aio aem rde <command> --help`

### 全局标志 {#global-flags}

* 对于不太详细的输出，请使用quiet标志：

  `aio aem rde <command> --quiet`

  此标记可删除某些元素，例如旋转线和进度条，并限制对用户输入的需要。

* 对于JSON，请使用json标记，而不是控制台日志输出：

  `aio aem rde <command> --json`

  在禁止任何控制台输出时，此标志返回有效的JSON。 请参阅下面的JSON示例。

* 要避免使用setup命令或任何aio配置创建来配置RDE连接信息，请使用组织、程序和环境的三个标志：

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  需要执行```aio login```。

### 部署到RDE {#deploying-to-rde}

本节介绍如何使用RDE CLI来部署、安装或更新各种资源。 这些资源包括：

* 内容包
* OSGi 配置
* 包
* 内容文件
* Apache或Dispatcher配置

常规使用模式为`aio aem:rde:install <artifact>`。

您可以找到下面的一些示例：

#### 部署内容包 {#deploy-content-package}

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的响应类似于以下内容：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

或者，您可以引用远程存储库：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

默认情况下，工件会同时部署到创作层和发布层，但`-s`标记可用于定位特定层。

可以部署任何AEM包，例如包含代码、内容或[容器包](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages)的包（也称为“所有”包）。

>[!IMPORTANT]
>
>上述内容包安装不会为WKND项目部署Dispatcher配置。 按照“部署Apache/Dispatcher配置”步骤单独部署它。

#### 部署OSGI配置 {#deploy-OSGI-config}

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

成功部署的响应类似于以下内容：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

#### 部署捆绑包 {#deploy-bundle}

要部署捆绑包，请使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

成功部署的响应类似于以下内容：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

#### 部署内容文件 {#deploy-content-file}

要部署内容文件，请使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

成功部署的响应类似于以下内容：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

#### 部署Apache/Dispatcher配置 {#deploy-apache-config}

对于此类配置，整个文件夹结构必须采用zip文件的形式。

在AEM项目的`dispatcher`模块中，您可以通过运行以下maven命令来压缩Dispatcher配置：

`mvn clean package`

或者使用`dispatcher`模块的`src`目录中的以下zip命令：

`zip -y -r dispatcher.zip .`

然后使用此命令部署配置：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假定您正在部署[WKND](https://github.com/adobe/aem-guides-wknd)项目的Dispatcher配置。 在部署项目的Dispatcher配置时，请确保将`X.X.X`替换为相应的WKND项目版本号或特定于项目的版本号。

>[!NOTE]
>
>RDE支持“灵活模式”Dispatcher配置，但不支持“旧版模式”Dispatcher配置。 有关这两种模式的信息，请参阅[Dispatcher文档](/help/implementing/dispatcher/disp-overview.md#validation-debug)。 您还可以参阅有关[迁移到灵活模式](/help/implementing/dispatcher/validation-debug.md#migrating)的文档（如果尚未这样做）。

成功的部署会生成类似于以下内容的响应：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的代码不通过Cloud Manager管道及其相关质量审核。 但是，代码确实会执行一些分析，这些分析会报告错误，如下面的代码示例所示：

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

上述代码示例说明了捆绑包无法解析时的行为。 在这种情况下，它是“暂存”的，并且仅在通过安装其他代码来满足其要求（在本例中缺少导入）时才进行安装。

#### 部署配置管道相关配置（yaml配置） {#deploy-config-pipeline}

可以按如下方式部署项目[使用配置管道](/help/operations/config-pipeline.md)中描述的特定于环境的配置（一个或多个yaml文件）：

`aio aem:rde:install -t env-config ./my-config-folder`
其中，`my-config-folder`是包含yaml配置的父文件夹。

或者，也可以安装包含配置文件夹树的zip文件：

`aio aem:rde:install -t env-config config.zip`

请注意，yaml文件的envTypes数组包括值`rde`，如下面的示例所示：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### 根据站点主题和站点模板部署前端代码 {#deploying-themes-to-rde}

RDE支持使用[站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)和[站点模板](/help/sites-cloud/administering/site-creation/site-templates.md)构建的前端代码。 RDE不使用像其他环境类型一样的Cloud Manager [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)，而是使用命令行指令部署前端包。

与往常一样，使用npm构建前端软件包：

`npm run build`

它生成一个`dist/`文件夹，因此您的前端包文件夹包含`package.json`文件和`dist`文件夹：

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```

现在，您可以通过以下方式指向前端包文件夹，将前端包部署到RDE：

```
aio aem:rde:install -t frontend ./path-to-frontend-pkg-folder/
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

或者，您可以压缩`package.json`文件和`dist`文件夹并部署该zip文件：

`zip -r frontend-pkg.zip ./path-to-frontend-pkg-folder/dist ./path-to-frontend-pkg-folder/package.json`

```
aio aem:rde:install -t frontend frontend-pkg.zip
...
#1: deploy completed for frontend frontend-pipeline.zip on author,publish - done by ... at 2024-01-18T15:33:22.898Z
Logs:
> Deployed artifact wknd-1.0.0-1705592008-26e7ec1a
> with workspace hash 692021864642a20d6d298044a927d66c0d9cf2adf42d4cca0c800a378ac3f8d3
```

>[!NOTE]
>
>前端软件包中文件的命名必须遵循以下命名约定：
>
> * `dist`文件夹，用于npm生成输出包文件夹
> * `package.json`文件，用于npm依赖项包

>[!TIP]
>
>如果您在2023年4月之前创建RDE，并且在首次使用前端功能时遇到`UNEXPECTED_API_ERROR`，则可能是由于设置已过时。 要解决此问题，请删除环境并创建新环境。

### 检查RDE的状态 {#checking-rde-status}

您可以使用RDE CLI检查环境是否已准备好部署到，以及通过RDE插件进行了哪些部署。

运行以下命令：

`aio aem:rde:status`

返回以下内容：

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

如果该命令返回有关实例部署的注释，您仍可以执行下一次更新，但您的上一次更新可能尚未在该实例中显示。

### 显示部署历史记录 {#show-deployment-history}

您可以通过运行以下命令来检查对RDE进行的部署的历史记录：

`aio aem:rde:history`

将返回响应，其形式为：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 从RDE中删除 {#deleting-from-rde}

您可以使用CLI工具删除以前部署到RDE的配置和捆绑包。 使用`status`命令可获取可删除内容的列表，其中包括要在delete命令中引用的包的`bsn`和配置的`pid`。

例如，如果已安装`com.adobe.granite.demo.MyServlet.cfg.json`，则`bsn`只是`com.adobe.granite.demo.MyServlet`，不带&#x200B;**cfg.json**&#x200B;后缀。

不支持删除内容包或内容文件。 要移除它们，请重置RDE，以使其返回到默认状态。

有关更多详细信息，请参阅以下示例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

有关更多信息和演示，请参阅视频教程[如何使用RDE命令(10:01)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use)。


## 从外部Git提供商部署到RDE {#deploy-to-rde}

>[!NOTE]
>
>此功能可通过率先采用者计划获取。 如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[CloudManager_BYOG@adobe.com](mailto:cloudmanager_byog@adobe.com)发送电子邮件。 请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

在使用[自带Git (BYOG)配置](/help/implementing/cloud-manager/managing-code/external-repositories.md)时，Cloud Manager支持直接从外部Git提供程序将代码部署到RDE。

从外部Git存储库部署到RDE需要满足以下条件：

* 使用与Cloud Manager集成的外部Git存储库（BYOG设置）。
* 您的项目必须配置一个或多个RDE环境。
* 如果您使用`github.com`，则必须查看并接受更新的GitHub应用程序安装以授予所需的新权限。

**使用说明**

* 当前，仅AEM内容和Dispatcher包支持部署到RDE。
* 尚不支持部署其他包类型(例如，完整的AEM应用程序包)。
* 目前，不支持使用注释重置RDE环境。 相反，必须使用现有的AIO CLI重置命令，如此处[&#128279;](/help/implementing/developing/introduction/rapid-development-environments.md#reset-the-rde-command-line)所述的。

**工作方式**

1. **代码质量验证消息。**

   当拉取请求(PR)触发代码质量管道运行时，验证结果指示部署是否可以继续到RDE环境。

   它在GitHub Enterprise上的外观：
   GitHub Enterprise上的![代码质量验证消息](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   它在GitLab上的外观：
   在GitLab上![代码质量验证消息](/help/implementing/developing/introduction/assets/rde-gitlab-code-quality-validation-message.png)

   它对Bitbucket的看法：
   ![比特桶上的代码质量验证消息](/help/implementing/developing/introduction/assets/rde-bitbucket-code-quality-validation-message.png)

1. **使用注释触发部署。**

   要启动部署，请按以下格式向PR添加注释： `deploy on rde-environment-<envName>`

   ![使用注释触发部署](/help/implementing/developing/introduction/assets/rde-trigger-deployment-using-comment.png)

   `<envName>`必须与现有RDE环境的名称匹配。 如果未找到该名称，则会返回一条注释，指示环境无效。

   如果环境状态未就绪，您将获得以下注释：

   ![环境未准备好部署](/help/implementing/developing/introduction/assets/rde-environment-not-ready.png)

1. **环境检查和工件部署。**

   如果RDE已准备就绪，Cloud Manager会向PR发布一个新检查。

   它在GitHub Enterprise上的外观：

   GitHub上的![环境状态](/help/implementing/developing/introduction/assets/rde-github-environment-status-is-ready.png)

   它在GitLab上的外观：

   GitLab上的![环境状态](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-1.png)

   它对Bitbucket的看法：

   Bitbucket上的![环境状态](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-1.png)

1. **部署消息成功。**

   部署完成后，Cloud Manager会发布一条成功消息，概述部署到目标环境的工件。

   它在GitHub Enterprise上的外观：

   GitHub上![环境的部署状态](/help/implementing/developing/introduction/assets/rde-github-environment-deployed-artifacts.png)

   它在GitLab上的外观：

   GitLab上的![环境的部署状态](/help/implementing/developing/introduction/assets/rde-gitlab-deployment-2.png)

   它对Bitbucket的看法：

   ![Bitbucket上环境的部署状态](/help/implementing/developing/introduction/assets/rde-bitbucket-deployment-2.png)




## 日志 {#rde-logging}

与其他环境类型类似，可以通过修改OSGi配置来设置日志级别，但如上所述，RDE的部署模型涉及命令行而不是Cloud Manager部署。 查看[日志记录文档](/help/implementing/developing/introduction/logging.md)以了解有关如何查看、下载和解释日志的详细信息。

RDE CLI还有自己的log命令，用于快速配置记录哪些类和包以及在哪个日志级别。 这些配置可以视为临时配置，因为它们不会修改版本控制中的OSGI属性。 此功能侧重于实时跟踪日志，而不是查找很久以前的日志。

以下示例说明如何跟踪创作层，其中有一个包设置为调试日志级别，两个包（以空格分隔）设置为信息调试级别。 包含&#x200B;**身份验证**&#x200B;包的输出突出显示。

`aio aem:rde:logs --target=author --debug=org.apache.sling --info=org.apache.sling.commons.threads.impl org.apache.sling.jcr.resource.internal.helper.jcr -H .auth.`

>[!TIP]
>
>如果您在播放创作服务的日志命令时看到错误`RDECLI:UNEXPECTED_API_ERROR`，请重置您的环境并重试。 如果最新的重置操作发生在2024年5月底之前，则会引发此错误。
>
>```
>aio aem:rde:reset
>```

有关完整的命令行选项集，请参阅`aio aem:rde:logs --help`。

功能包括：

* 在每个包或类级别上声明日志级别
* 自定义日志输出格式
* 最多跟踪四个当前日志配置，每个配置位于自己的终端中
* 突出显示特定日志

请注意，日志存储在RDE的内存中，如果日志没有尾随或网络速度太慢，这些日志将被回收并丢弃。


## 重置RDE {#reset-rde}

重置RDE会同时从创作实例和发布实例中删除所有自定义代码、配置和内容。 完成一项功能的测试并希望在测试另一项功能之前将环境恢复到默认状态时，重置RDE会很有帮助。

重置会将RDE设置为最新可用的AEM版本。

您可以使用[Cloud Manager](#reset-the-rde-cloud-manager)或[命令行](#reset-the-rde-command-line)重置RDE。 重置需要几分钟时间，并且所有现有内容和代码都将从RDE中删除。

>[!NOTE]
>
>在使用重置功能之前，请确保已为您分配Cloud Manager开发人员角色。 否则，重置操作将失败，并出现错误。

### 使用命令行重置RDE {#reset-the-rde-command-line}

通过运行以下命令，可以重置RDE并将其返回到默认状态：

`aio aem:rde:reset`

此过程通常需要几分钟时间，并在成功时报告```Environment reset.```或报告错误```Failed to reset the environment.```。 有关结构化输出，请参阅下面有关```--json```输出的章节。

使用[状态命令](#checking-rde-status)检查环境何时再次准备就绪。

### 在Cloud Manager中重置RDE {#reset-the-rde-cloud-manager}

您可以使用Cloud Manager通过以下步骤重置RDE：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要为其重置RDE的程序。

1. 在&#x200B;**概述**&#x200B;页面中，单击屏幕顶部的&#x200B;**环境**&#x200B;选项卡。

   ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**全部显示**&#x200B;按钮，直接跳转到&#x200B;**环境**&#x200B;选项卡。

     ![显示所有选项](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 将打开&#x200B;**环境**&#x200B;窗口并列出程序的所有环境。

   ![“环境”选项卡](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 单击要重置的RDE的省略号按钮，然后选择&#x200B;**重置**。

   ![查看环境详细信息](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 单击对话框中的&#x200B;**重置**&#x200B;确认要重置RDE。

   ![确认重置](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager通过横幅通知确认重置过程已开始。

   ![重置横幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重置启动后，通常需要几分钟才能完成并将环境恢复到默认状态。 您随时可以在&#x200B;**环境**&#x200B;信息卡或窗口的&#x200B;**状态**&#x200B;列中查看重置状态。

![RDE重置状态](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您还可以直接从&#x200B;**概述**&#x200B;页面上的&#x200B;**环境**&#x200B;信息卡中使用省略号按钮重置RDE。

![从环境信息卡重置RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有关如何使用Cloud Manager管理环境的更多信息，请参阅[Cloud Manager文档](/help/implementing/cloud-manager/manage-environments.md)。

## 支持JSON输出的命令 {#json-commands}

大多数命令支持全局```--json```标志，该标志禁止控制台输出并返回要在脚本中处理的有效json。 以下是一些受支持的命令以及json输出示例。

### 状态 {#status}

<details>
  <summary>展开以查看状态示例</summary>

#### 干净的RDE {#clean-rde}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Modification in progress | Deployment in progress | Upload in progress | Ready (instances are currently deploying) | Ready",
  "author": {
    "osgiBundles": [],
    "osgiConfigs": []
  },
  "publish": {
    "osgiBundles": [],
    "osgiConfigs": []
  }
}
```

#### 带有一些已安装捆绑包的RDE {#rde-installed-bundles}

```$ aio aem rde status --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "author": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  },
  "publish": {
    "osgiBundles": [
      {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "updateId": "80",
        "service": "author",
        "type": "osgi-bundle",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        }
      }
    ],
    "osgiConfigs": [
      {
        "id": "publish_osgi-config_com.adobe.granite.demo.MyServlet",
        "updateId": "80",
        "service": "publish",
        "type": "osgi-config",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "configPid": "com.adobe.granite.demo.MyServlet"
        }
      }
    ]
  }
}
```

</details>

### 安装 {#install}

<details>
  <summary>展开以查看安装示例</summary>

```$ aio aem rde install ~/Downloads/hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "4",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:30:44.578Z",
        "processed": "2024-05-21T12:31:07.886468Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### 删除 {#delete}

<details>
  <summary>展开以查看删除示例</summary>

```$ aio aem rde delete com.adobe.granite.hotdev.demo-1.0.0.SNAPSHOT --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "items": [
    {
      "updateId": "84",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:16.889Z",
        "processed": "2024-05-21T11:49:18.188420Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    },
    {
      "updateId": "85",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T11:49:23.857Z",
        "processed": "2024-05-21T11:49:25.237930Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "83"
      },
      "hash": "636f6d2e",
      "logs": [
        "No logs available for this update."
      ]
    }
  ]
}
```

</details>

### 历史记录 {#history}

<details>
  <summary>展开以查看历史记录示例</summary>

```$ aio aem rde history --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "Ready",
  "items": [
    {
      "updateId": "112",
      "info": "delete publish_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:07.934Z",
        "processed": "2024-05-21T12:53:09.118766Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "publish_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "publish",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "111",
      "info": "delete author_osgi-bundle_com.adobe.granite.hotdev.demo",
      "action": "delete",
      "metadata": {},
      "services": [
        "author"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:53:00.824Z",
        "processed": "2024-05-21T12:53:02.101560Z"
      },
      "user": "userId",
      "type": "osgi-bundle",
      "deletedArtifact": {
        "id": "author_osgi-bundle_com.adobe.granite.hotdev.demo",
        "metadata": {
          "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip",
          "bundleSymbolicName": "com.adobe.granite.hotdev.demo",
          "bundleName": "HotDev Bundle",
          "bundleVersion": "1.0.0.SNAPSHOT"
        },
        "service": "author",
        "type": "osgi-bundle",
        "updateId": "110"
      },
      "hash": "636f6d2e"
    },
    {
      "updateId": "110",
      "info": "deploy",
      "action": "deploy",
      "metadata": {
        "name": "hotdev.demo.ui.apps.all-1.0.0-SNAPSHOT.zip"
      },
      "services": [
        "author",
        "publish"
      ],
      "status": "completed",
      "timestamps": {
        "received": "2024-05-21T12:52:12.123Z",
        "processed": "2024-05-21T12:52:31.026147Z"
      },
      "user": "userId",
      "type": "content-package",
      "hash": "2ad73507"
    }
  ]
}
```

</details>

### 重置 {#reset}

<details>
  <summary>展开以查看重置示例</summary>

#### 放火忘却，等等 {#fire-no-wait}

```$ aio aem rde reset --no-wait --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "resetting"
}
```

#### 等待完成，已成功重置 {#wait-success}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset"
}
```

#### 等待完成，重置失败 {#wait-failed}

```$ aio aem rde reset --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "reset_failed"
}
```

</details>

### 重新启动 {#restart}

<details>
  <summary>展开以查看重新启动示例</summary>

```$ aio aem rde restart --json```

```json
{
  "programId": "myProgram",
  "environmentId": "myEnv",
  "status": "restarted"
}
```

</details>

## 运行模式 {#runmodes}

可以通过在文件夹名称上使用后缀来应用特定于RDE的OSGI配置，如下例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

有关运行模式的一般信息，请参阅[运行模式文档](/help/implementing/deploying/overview.md#runmodes)。

>[!NOTE]
>
>RDE OSGI配置的唯一性在于，它继承由捆绑包的`dev`运行模式声明的任何OSGI属性的值。

RDE不同于其他环境，因为内容可以安装在`/apps`下的`install.rde`文件夹（或`install.author.rde`或`install.publish.rde`）中。 此功能允许您使用命令行工具将内容提交到Git并将其交付到RDE。

## 填充内容 {#populating-content}

重置RDE时，将删除所有内容，因此如果需要，必须执行显式操作以添加内容。 作为最佳实践，请考虑汇编一组内容以用作测试内容，以便在RDE中验证或调试功能。 可以使用以下几种策略来使用该内容填充RDE：

1. 使用命令行工具将内容包显式同步到RDE

1. 将示例内容放置在Git中的`/apps`下的`install.rde`文件夹内并提交它，然后使用命令行工具将总体内容包同步到RDE。

1. 使用[内容复制工具](/help/implementing/developing/tools/content-copy.md)从生产、暂存或开发环境或其他RDE中复制定义的内容集。

1. 使用包管理器

同步内容包时，您的限制为1 GB。


## RDE与云开发环境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

虽然RDE在许多方面与云开发环境类似，但在体系结构上有一些细微的差异，以便允许快速同步代码。 将代码发送到RDE的机制不同 — 对于RDE，一个代码从本地开发环境同步代码，而对于Cloud Development环境，一个代码通过Cloud Manager部署代码。

出于这些原因，建议在RDE环境中验证代码后，使用非生产管道将代码部署到云开发环境。 最后，在使用生产管道进行部署之前测试代码。

另请注意以下注意事项：

* RDE不包含预览层
* RDE当前不支持预发行版渠道。


## 我需要多少个RDE？ {#how-many-rds-do-i-need}

RDE可用于每个已许可解决方案，Adobe还提供了其他RDE，这些RDE可以被许可用于生产（非沙盒）程序。

所需的RDE数量取决于组织的组成和流程。 最灵活的模型是，组织为每个AEM Cloud Service开发人员购买专用RDE。 在此模型中，每个开发人员都可以在RDE上测试其代码，而无需与其他团队成员协调RDE环境是否可用。

在另一个极端情况下，只有一个RDE的团队可以依靠内部协调来决定哪个开发人员在给定时间使用环境。 当开发人员达到功能里程碑并需要在Cloud环境中验证其工作，并且灵活地做出快速更改时，这种方法可正常工作。

中间模型是指一个组织购买多个RDE，因此存在更大可能未使用的RDE的模型。 一种策略可以是为每个Scrum团队或主要功能分配RDE。 内部进程可用于协调环境的使用。

## AEM Forms Cloud Service RDE与其他环境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms开发人员可以使用AEM Forms Cloud Service快速开发环境快速开发自适应Forms、工作流和自定义项，如自定义核心组件、与第三方系统的集成等。 AEM Forms Cloud Service快速开发环境(RDE)不支持通信API。 它还不支持需要记录文档的功能，例如在提交自适应表单时生成记录文档。 下面列出的AEM Forms功能在快速开发环境(RDE)中不可用：

* 为自适应表单配置记录文档
* 在提交自适应表单时生成记录文档或执行工作流步骤
* 使用电子邮件提交操作或工作流中的电子邮件步骤将记录文档作为附件发送
* 在自适应表单或工作流步骤中使用Adobe Sign
* 通信API

>[!NOTE]
>
> 快速开发环境(RDE)的UI与Forms的其他Cloud Service环境之间没有区别。 所有与记录文档相关的选项（如为自适应表单选择记录文档模板）将继续显示在UI中。 这些环境没有通信API和记录文档功能来测试这些选项。 因此，如果您选择的选项需要通信API或记录文档功能，则系统不会执行该操作。 而是显示错误消息。

## rde教程

要了解AEM as a Cloud Service中的RDE，请参阅视频教程，其中演示了[如何设置它、如何使用它以及开发生命周期(01:25)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/rde/overview)。

## 疑难解答 {#troubleshooting}

### RDE故障诊断(#rde-troublehooting)

#### 如何为现有RDE获取最新的AEM版本 {#get-latest-aem-version}

创建后，会将RDE设置为最新可用的Adobe Experience Manager (AEM)版本。 可以使用Cloud Manager或`aio aem:rde:reset`命令执行的[RDE重置](#reset-rde)会循环RDE并将其设置为最新可用的AEM版本。

### aio RDE插件故障诊断 {#aio-rde-plugin-troubleshooting}

#### 权限不足错误 {#insufficient-permissions}

要使用RDE插件，它要求您是Cloud Manager **开发人员 — Cloud Service**&#x200B;产品配置文件的成员。 有关更多详细信息，请参阅[将团队成员分配给Cloud Manager产品配置文件 — 分配开发人员产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)。

或者，如果您通过运行以下命令登录到开发人员控制台，则可以确认您具有此开发人员角色：

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>如果看到`Warning: cloudmanager:* is not a aio command.`错误，则必须通过运行以下命令来安装[aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)：
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

通过运行以下命令，验证登录是否成功完成：

`aio cloudmanager:list-programs`

此过程列出已配置组织下的所有程序，并确认您分配了正确的角色。

#### 使用已弃用的上下文`aio-cli-plugin-cloudmanager` {#aio-rde-plugin-troubleshooting-deprecatedcontext}

由于`aio-cli-plugin-aem-rde`的历史记录，上下文名称`aio-cli-plugin-cloudmanager`已使用一段时间。 RDE插件现在使用IMS方法管理上下文信息，从而允许您全局或本地存储上下文。 您还可以配置默认上下文以自动应用于所有AIO调用。 配置的默认上下文存储在本地，使开发人员能够跟踪和使用文件夹中的各个上下文及其信息。 有关详细信息，请阅读[以上设置本地上下文的示例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)。

同时使用插件`aio-cli-plugin-cloudmanager`和`aio-cli-plugin-aem-rde`并希望将所有信息保存在同一上下文中的开发人员现在可以选择以下选项：

##### 继续使用上下文`aio-cli-plugin-cloudmanager`

仍可以使用上下文。 RDE插件中将显示弃用警告。 可以使用```--quiet```模式忽略此警告。 较新版本的RDE插件不再提供回退以读取上下文`aio-cli-plugin-cloudmanager`。 要继续使用它，只需将默认上下文配置为`aio-cli-plugin-cloudmanager`。 请参阅[以上设置本地上下文](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)的示例。

##### 还将任何其他上下文名称用于Cloud Manager插件

Cloud Manager插件提供了一个参数来定义要使用的上下文。 它目前尚不支持IMS默认上下文配置。 为此，请使用[示例配置RDE插件以设置本地上下文](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)，并告知Cloud Manager插件在每次调用时都使用`myContext`，如```--imsContextName=myContext```。
