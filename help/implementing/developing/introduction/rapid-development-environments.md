---
title: 快速开发环境
description: 了解如何使用快速开发环境在云环境中进行快速开发迭代。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '4990'
ht-degree: 3%

---

# 快速开发环境 {#rapid-development-environments}

要部署更改，当前云开发环境需要使用采用称为CI/CD管道的广泛代码安全和质量规则的流程。 对于需要快速和反复更改的情况，Adobe引入了快速开发环境（简称RDE）。

RDE允许开发人员快速部署和审查更改，从而最大限度地减少测试经验证可在本地开发环境中工作的功能所需的时间。

在RDE中测试更改后，可以通过Cloud Manager管道将它们部署到常规云开发环境。

>[!NOTE]
> 在[不和谐频道](https://discord.com/channels/1131492224371277874/1245304281184079872)上联系RDE开发人员。 欢迎您就RDE主题提出任何问题或给予反馈。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以看到其他视频演示[如何设置它](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)、[如何使用它](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)以及使用RDE的[开发生命周期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html)。

## 简介 {#introduction}

RDE可用于代码、内容以及Apache或Dispatcher配置。 与常规云开发环境不同，开发人员可以使用本地命令行工具将本地构建的代码同步到RDE。

每个项目均配备RDE。 如果存在沙盒帐户，则它们在处于非使用状态数小时后会休眠。

创建后，会将RDE设置为最新可用的Adobe Experience Manager (AEM)版本。 可以使用Cloud Manager执行的RDE重置会循环RDE并将其设置为最新可用的AEM版本。

通常，单个开发人员在给定时间使用RDE来测试和调试特定功能。 当开发会话完成后，RDE可以重置为默认状态以供下次使用。

可以为生产（非沙盒）程序许可其他RDE。

## 在程序中启用RDE {#enabling-rde-in-a-program}

请按照以下步骤操作，以便您可以使用Cloud Manager为您的项目创建RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要向其添加RDE的程序以显示其详细信息。

   * RDE可以添加到[沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)和[生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。

1. 从&#x200B;**程序概述**&#x200B;页面，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**添加环境**&#x200B;以添加环境。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

     ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 在&#x200B;**选择环境类型**&#x200B;标题下选择&#x200B;**快速开发**。
      * 可用/已用环境的数量显示在环境类型后面的括号中。
   * 为环境提供&#x200B;**名称**。
   * 为环境提供可选的&#x200B;**描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。

创建后，RDE将设置为最新可用的AEM版本。 RDE重置(也可以使用Cloud Manager执行)可循环RDE并将其设置为最新可用的AEM版本。

有关使用Cloud Manager创建环境、管理谁有权访问这些环境以及分配自定义域的更多信息，请参阅[Cloud Manager文档](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)。

## 安装RDE命令行工具 {#installing-the-rde-command-line-tools}

在使用Cloud Manager为程序添加RDE后，您可以通过设置命令行工具与其交互，如以下步骤中所述：

>[!IMPORTANT]
>
>确保已安装[Node和](https://nodejs.org/en/download/)的20版和NPM，以便Adobe I/OCLI和相关插件正常工作。


1. 按照此[过程](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)安装Adobe I/OCLI工具。
1. 安装Adobe I/OCLI工具AEM RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 使用aio客户端登录。

   ```
   aio login
   ```

   登录信息（令牌）存储在全局aio配置中，因此仅支持一个登录和组织。 如果您要使用需要不同登录或组织的多个RDE，请遵循以下示例来引入上下文。

   <details><summary>按照此示例为某个RDE登录设置本地上下文</summary>
   要将登录信息本地存储到特定上下文当前目录的.aio文件中，请执行以下步骤。 上下文也是设置CI/CD环境或脚本的一种巧妙方法。  要使用此功能，请确保至少使用aio-cli版本10.3.1。使用“npm install -g @adobe/aio-cli”更新它

   让我们创建一个名为“mycontext”的上下文，然后在调用登录命令之前使用auth插件将该上下文设置为默认上下文。

   ```
   aio config set --json -l "ims.contexts.mycontext" "{ cli.bare-output: false }"
   aio auth ctx -s mycontext
   aio login --no-open
   ```

   >[!NOTE]
   > 带`--no-open`选项的登录命令将在终端中输出一个URL，而不是打开默认浏览器。 这样，您就可以使用浏览器的&#x200B;**无痕显示**&#x200B;窗口复制并打开它。 这样，您在普通浏览器窗口中当前登录的会话将保持不变，您可以确保使用您的上下文所需的特定登录和组织。

   第一个命令将在您的本地`.aio`配置文件中创建一个名为`mycontext`的新登录上下文配置（如果需要，将创建该文件）。 第二个命令将上下文`mycontext`设置为“当前”上下文，即默认值。

   有了此配置，登录命令会自动将登录令牌存储在上下文`mycontext`中，从而使其保持在本地。

   通过将本地配置保留在多个文件夹中，可以管理多个上下文。 或者，也可以在单个配置文件中设置多个上下文，并通过更改“当前”上下文在它们之间切换。
   </details>

1. 配置RDE插件以使用您的组织、项目和环境。 下面的设置命令将以交互方式向用户提供其组织中的程序列表，并显示该程序中可供选择的RDE环境。

   ```
   aio aem:rde:setup
   ```

   如果目的是使用脚本环境，则可以跳过设置步骤，在这种情况下，组织、程序和环境值可以包含在每个命令中。 [有关详细信息，请参阅下面的rde命令](#rde-cli-commands)。

### 交互式设置 {#installing-the-rde-command-line-tools-interactive}

setup命令将询问所提供的配置是应本地存储还是全局存储。

```
Setup the CLI configuration necessary to use the RDE commands.
? Do you want to store the information you enter in this setup procedure locally? (y/N)
```

选择`no`以
* 在aio配置中全局存储组织、项目和环境。
* 仅适用于单个RDE。

选择`yes`以
* 将组织、程序和环境本地存储在当前目录的`.aio`文件中。 如果您希望将文件提交到版本控制，以便其他克隆Git存储库的人可以使用它，这非常方便。
* 与许多RDE配合使用，以便切换到另一个目录时使用该配置。
* 在脚本之类的程序化上下文中使用配置，脚本可以引用该配置。


选择本地或全局配置后，setup命令将尝试从当前登录中读取组织id，然后读取组织的程序。 如果找不到组织，您可以手动输入该组织并提供一些指导。

```
Selected only organization: XYXYXYXYXYXYXYXXYY
retrieving programs of your organization ...
```

检索程序后，用户可以从列表中选择程序，也可以键入以进行筛选。
选择项目后，将列出可供选择的RDE环境列表。
如果只有一个项目和/或RDE环境可用，则会自动选择该环境。

要查看当前环境上下文，请执行：

```aio aem rde setup --show```

该命令将做出响应，得到类似于以下内容的结果：

```Current configuration: cm-p1-e1: programName - environmentName (organization: ...@AdobeOrg)```

### 非交互环境中的手动设置过程 {#manual-setup}

对于没有用户可以交互式运行上述设置命令的环境（如CI/CD或脚本），可以按照以下步骤手动配置组织、程序和环境的三个参数。


<details>
  <summary>展开以查找有关如何手动配置的详细信息</summary>

1. 配置您的组织ID并将字母数字字符串替换为您自己的组织ID。

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   * 可以使用[查看组织ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255)下记录的方法查找您自己的组织ID。

1. 接下来，配置您的项目ID：

   `aio config:set cloudmanager_programid 12345`

1. 然后，配置要将RDE附加到的环境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 配置完插件后，请通过执行

   `aio login`

   这些步骤要求您成为Cloud Manager **开发人员 — Cloud Service**&#x200B;产品配置文件的成员。 有关更多详细信息，请参阅[将团队成员分配给Cloud Manager产品配置文件 — 分配开发人员产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)。

有关更多信息和演示，请观看视频教程[如何设置RDE (06:24)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)。
</details>

## 在开发新功能时使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建议通过以下工作流程来开发新功能：

* 当达到中间里程碑并成功通过AEM as a Cloud Service SDK本地验证时，将代码提交到Git功能分支。 分支还不应是主行的一部分，但提交Git是可选的。 构成“中间里程碑”的因素因团队习惯而异。 示例包括几行新代码、半天的工作或完成一个子功能。

* 如果RDE已由其他功能使用，并且您希望[将其重置为默认状态](#reset-rde)，请重置该RDE。 <!-- Alexandru: hiding for now, do not delete This can be done by way of [Cloud Manager](#reset-the-rde-cloud-manager) or by way of the [command line](#reset-the-rde-command-line). -->重置需要几分钟时间，并且所有现有内容和代码都会被删除。 可以使用RDE状态命令确认RDE已就绪。 RDE将随最新的AEM发行版本一起提供。

  >[!IMPORTANT]
  >
  > 如果您的暂存环境和生产环境未收到自动AEM版本更新，并且位于最新的AEM版本之后，则在RDE上运行的代码可能与暂存环境和生产环境中运行的代码不匹配。 在这种情况下，在将代码部署到生产环境之前，在暂存环境中对代码执行彻底测试尤为重要。


* 使用RDE命令行界面，将本地代码同步到RDE。 选项包括安装内容包、特定捆绑包、OSGI配置文件、内容文件和Apache/Dispatcher配置的zip文件。 也可以引用远程内容包。 有关详细信息，请参阅[RDE命令行工具](/help/implementing/developing/introduction/rapid-development-environments.md#rde-cli-commands)。 可以使用status命令验证部署是否成功。 或者，使用包管理器安装内容包。

* 在RDE中测试代码。 创作和Publish URL在Cloud Manager中可用。

* 如果代码的行为与预期不符，请使用标准调试技术了解问题并进行适当的更改。 无需将代码修改提交到Git（因为它们尚未验证），请使用本地CLI将代码同步到RDE。 不断迭代，直到问题得到解决。

* 一旦代码按预期运行，将代码提交到Git功能分支。

* 同步到RDE的代码不使用Cloud Manager管道，因此现在应使用Cloud Manager非生产管道将Git功能分支部署到云开发环境。 这将验证代码是否通过Cloud Manager质量关卡，并让您确信稍后将使用Cloud Manager生产管道成功部署代码。

* 对每个中间里程碑重复上述步骤，直到功能的所有代码准备就绪，并在RDE和云开发环境中正常运行。

* 通过Cloud Manager生产管道将代码部署到生产环境。

## 使用RDE调试现有功能 {#use-rde-to-debug-an-existing-feature}

该工作流与开发新功能类似。 不同之处在于，同步到RDE的代码将反映推送到发现问题的环境的任何内容的Git标签。 此外，部署与上游环境匹配的内容可能很有用。 这可以通过导出和导入内容包来实现。

## 多位开发人员在同一个RDE上协作 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支持一个项目。 由于代码从本地开发环境同步到RDE环境，因此对于一个开发人员而言，在给定时间自行使用代码是最自然的事情。

但是，通过仔细的协调，多个开发人员可以验证特定功能或调试特定问题。 关键是每个开发人员都会保持其本地项目的同步，以便特定开发人员所做的代码更改被其他开发人员吸收，否则，一个开发人员可能会无意中覆盖另一个开发人员的代码。 推荐的策略是，每个开发人员在同步到RDE之前将其更改提交到共享git分支，以便其他开发人员在做出自己的更改之前提取更改。

## RDE命令行工具命令 {#rde-cli-commands}

### 帮助/一般信息 {#help}

* 要获取命令列表，请键入：

  `aio aem:rde`

* 有关命令的详细帮助，请键入：

  `aio aem rde <command> --help`

### 全局标志 {#global-flags}

* 对于不太详细的输出，请使用quiet标志：

  `aio aem rde <command> --quiet`

  这会删除某些元素，例如旋转器和进度条，并限制对用户输入的需求。

* 对于JSON，请使用json标记，而不是控制台日志输出：

  `aio aem rde <command> --json`

  在抑制任何控制台输出时，这将返回有效的JSON。 请参阅下面的JSON示例。

* 要避免使用setup命令或任何aio配置创建来配置RDE连接信息，请使用组织、程序和环境的三个标志：

  `aio aem rde <command> --organizationId=<value> --programId=<value> --environmentId=<value>`

  这仍需要执行```aio login```。

### 部署到RDE {#deploying-to-rde}

本节介绍如何使用RDE CLI部署、安装或更新包、OSGI配置、内容包、单个内容文件以及Apache或Dispatcher配置。

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

默认情况下，工件会同时部署到创作层和发布层，但“ — s”标记可用于定位特定层。

可以部署任何AEM包，例如包含代码、内容或[容器包](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages)的包（也称为“所有”包）。

>[!IMPORTANT]
>
>WKND项目的Dispatcher配置不会通过上述内容包安装进行部署。 按照“部署Apache/Dispatcher配置”步骤单独部署它。

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

#### 部署与配置管道相关的配置（yaml配置） {#deploy-config-pipeline}

可以按如下方式部署项目[使用配置管道](/help/operations/config-pipeline.md)中描述的特定于环境的配置（一个或多个yaml文件）：

`aio aem:rde:install -t env-config ./my-config-folder`
其中，my-config-folder是包含yaml配置的父文件夹。

或者，也可以安装包含配置文件夹树的zip文件：

`aio aem:rde:install -t env-config config.zip`

请注意，yaml文件的envTypes数组应包含值&#x200B;*rde*，如以下示例所示：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["rde"]
```

### 根据站点主题和站点模板部署前端代码 {#deploying-themes-to-rde}

RDE支持基于[站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)和[站点模板](/help/sites-cloud/administering/site-creation/site-templates.md)的前端代码。 对于RDE，这是使用命令行指令来部署前端包完成的，而不是使用用于其他环境类型的Cloud Manager [前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)。

与往常一样，使用npm构建前端软件包：

`npm run build`

它应生成`dist/`文件夹，因此您的前端包文件夹应包含`package.json`文件和`dist`文件夹：

```
ls ./path-to-frontend-pkg-folder/
...
dist
package.json
```
现在，您可以通过指向前端包文件夹将前端包部署到RDE：

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
> * “dist”文件夹，对于npm build输出包文件夹
> * “package.json”文件，用于npm依赖关系包

>[!TIP]
>
> 如果您在2023年4月之前创建了RDE，并在首次尝试前端功能时遇到错误“UNEXPECTED_API_ERROR”，请尝试删除环境并再次创建它。

### 检查RDE的状态 {#checking-rde-status}

您可以使用RDE CLI检查环境是否已准备好部署到，以及通过RDE插件进行了哪些部署。

正在运行：

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

### 从RDE删除 {#deleting-from-rde}

您可以通过CLI工具删除以前部署到RDE的配置和捆绑包。 使用`status`命令可获取可删除内容的列表，其中包括要在delete命令中引用的包的`bsn`和配置的`pid`。

例如，如果已安装`com.adobe.granite.demo.MyServlet.cfg.json`，则`bsn`只是`com.adobe.granite.demo.MyServlet`，不带&#x200B;**cfg.json**&#x200B;后缀。

不支持删除内容包或内容文件。 要删除它们，应重置RDE，以使其返回到默认状态。

有关更多详细信息，请参阅以下示例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

有关更多信息和演示，请参阅视频教程[如何使用RDE命令(10:01)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)。

## 日志 {#rde-logging}

与其他环境类型类似，可以通过修改OSGi配置来设置日志级别，但如上所述，RDE的部署模型涉及命令行而不是Cloud Manager部署。 查看[日志记录文档](/help/implementing/developing/introduction/logging.md)以了解有关如何查看、下载和解释日志的详细信息。

RDE CLI还有其自己的日志命令，可用于快速配置应该记录哪些类和包以及在什么日志级别。 这些配置可以视为临时配置，因为它们不会修改版本控制中的OSGI属性。 此功能侧重于实时跟踪日志，而不是查找很久以前的日志。

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


## 重置 {#reset-rde}

重置RDE会同时从创作实例和发布实例中删除所有自定义代码、配置和内容。 例如，如果已经使用RDE测试特定功能，并且希望将其重置为默认状态，以便测试其他功能，则这种重置非常有用。

重置会将RDE设置为最新可用的AEM版本。

可通过[Cloud Manager](#reset-the-rde-cloud-manager)或通过[命令行](#reset-the-rde-command-line)进行重置。 重置需要几分钟时间，并且所有现有内容和代码都将从RDE中删除。

>[注释！]
>
>您必须分配了Cloud Manager开发人员角色，才能使用重置功能。 如果不能，则重置操作会导致错误。

### 通过命令行重置RDE {#reset-the-rde-command-line}

您可以通过运行以下命令来重置RDE并将其返回到默认状态：

`aio aem:rde:reset`

这通常需要几分钟的时间，并在成功时报告```Environment reset.```或报告错误```Failed to reset the environment.```。 有关结构化输出，请参阅下面有关```--json```输出的章节。

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

RDE重置过程启动后，通常需要几分钟才能完成，并使环境恢复到默认状态。 可以随时在&#x200B;**环境**&#x200B;信息卡的&#x200B;**状态**&#x200B;列或&#x200B;**环境**&#x200B;窗口中查看重置过程的状态。

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

RDE不同于其他环境，因为RDE中的内容可以安装在/apps下的install.rde文件夹（或install.author.rde或install.publish.rde）中。 这样，您就可以使用命令行工具将内容提交到Git并将其交付到RDE。

## 填充内容 {#populating-content}

重置RDE时，将删除所有内容，因此如果需要，必须执行显式操作以添加内容。 作为最佳实践，请考虑汇编一组内容以用作测试内容，以便在RDE中验证或调试功能。 可以使用以下几种策略来使用该内容填充RDE：

1. 使用命令行工具将内容包显式同步到RDE

1. 将示例内容放置在git中的/apps下的install.rde文件夹内并提交它，然后使用命令行工具将总体内容包同步到RDE。

1. 使用[内容复制工具](/help/implementing/developing/tools/content-copy.md)从生产、暂存或开发环境或其他RDE中复制定义的内容集。

1. 使用包管理器

同步内容包时，您的限制为1 GB。


## RDE与云开发环境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

虽然RDE在许多方面与云开发环境类似，但在体系结构上有一些细微的差异，可用于快速同步代码。 将代码获取到RDE的机制不同 — 对于RDE，一个代码与本地开发环境同步，而对于Cloud Development Environments，一个代码通过Cloud Manager进行部署。

因此，建议在RDE环境中验证代码后，使用非生产管道将代码部署到云开发环境。 最后，在使用生产管道进行部署之前测试代码。

另请注意以下注意事项：

* RDE不包含预览层
* RDE当前不支持预发行版渠道。


## 我需要多少个RDE？ {#how-many-rds-do-i-need}

RDE可用于每个已许可的解决方案，Adobe还提供了其他RDE，这些RDE可以被许可用于生产（非沙盒）程序。

所需的RDE数量取决于组织的组成和流程。 最灵活的模型是组织为每个AEM Cloud Service开发人员购买专用RDE。 在此模型中，每个开发人员都可以在RDE上测试其代码，而无需与其他团队成员就RDE环境是否可用进行协调。

在另一个极端情况下，具有单个RDE的团队可以使用内部流程来协调哪些开发人员可以在给定时间使用环境。 这可能发生在开发人员达到中间功能里程碑并准备好在云环境中进行验证时，开发人员可以在其中快速做出所需的更改。

中间模型是指一个组织购买多个RDE，因此存在更大可能未使用的RDE的模型。 一种策略可以是为每个Scrum团队或主要功能分配RDE。 内部进程可用于协调环境的使用。

## AEM FormsCloud Service快速开发环境(RDE)与其他环境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms开发人员可以使用AEM FormsCloud Service快速开发环境快速开发自适应Forms、工作流和自定义项，如自定义核心组件、与第三方系统的集成等。 AEM FormsCloud Service快速开发环境(RDE)不支持通信API。 它还不支持需要记录文档的功能，例如在提交自适应表单时生成记录文档。 下面列出的AEM Forms功能在快速开发环境(RDE)中不可用：

* 为自适应表单配置记录文档
* 在提交自适应表单时生成记录文档或执行工作流步骤
* 使用电子邮件提交操作或工作流中的电子邮件步骤将记录文档作为附件发送
* 在自适应表单或工作流步骤中使用Adobe Sign
* 通信API

>[!NOTE]
>
> 快速开发环境(RDE)的UI与Forms的其他Cloud Service环境之间没有区别。 所有与记录文档相关的选项（如为自适应表单选择记录文档模板）将继续显示在UI中。 这些环境没有通信API和记录文档功能来测试这些选项。 因此，当您选择需要通信API或记录文档功能的任何选项时，不会执行任何操作，并且会显示错误消息。

## rde教程

要了解AEM as a Cloud Service中的RDE，请参阅视频教程，其中演示了[如何设置它、如何使用它以及开发生命周期(01:25)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)。

# 疑难解答 {#troubleshooting}

## RDE故障排除(#rde-troublehooting)

### 如何获取现有RDE的最新AEM版本 {#get-latest-aem-version}

创建后，会将RDE设置为最新可用的Adobe Experience Manager (AEM)版本。 可以使用Cloud Manager或`aio aem:rde:reset`命令执行的[RDE重置](#reset-rde)会循环RDE并将其设置为最新可用的AEM版本。

## aio RDE插件故障排除 {#aio-rde-plugin-troubleshooting}

### 权限不足错误 {#insufficient-permissions}

要使用RDE插件，它要求您是Cloud Manager **开发人员 — Cloud Service**&#x200B;产品配置文件的成员。 有关更多详细信息，请参阅[将团队成员分配给Cloud Manager产品配置文件 — 分配开发人员产品配置文件](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer)。

或者，如果可以通过运行此命令登录到开发人员控制台，则可以确认您具有此开发人员角色：

`aio cloudmanager:environment:open-developer-console`

>[!TIP]
>
>如果看到`Warning: cloudmanager:* is not a aio command.`错误，则必须通过运行以下命令来安装[aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager)：
>
>```
>aio plugins:install @adobe/aio-cli-plugin-cloudmanager
>```

通过运行验证登录是否成功完成

`aio cloudmanager:list-programs`

这应列出您配置的组织下的所有程序，并确认您分配了正确的角色。

### 使用已弃用的上下文“aio-cli-plugin-cloudmanager” {#aio-rde-plugin-troubleshooting-deprecatedcontext}

由于“aio-cli-plugin-aem-rde”的历史记录，上下文名称“aio-cli-plugin-cloudmanager”使用了一段时间。 现在，rde插件使用IMS方式处理上下文信息，这意味着可以选择全局或本地存储上下文信息，并且如果愿意，可将所有aio调用默认到一个已配置的默认值。 配置的默认上下文存储在本地，使开发人员能够跟踪和使用文件夹中的各个上下文及其信息。 有关更多详细信息，请阅读[以上设置本地上下文的示例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)。

同时使用aio-cli-plugin-cloudmanager和aio-cli-plugin-aem-rde这两个插件，并希望将所有信息保存在同一上下文中的开发人员，现在可以选择以下选项：

#### 继续使用上下文“aio-cli-plugin-cloudmanager”

仍可以使用上下文，RDE插件中将显示弃用警告。 可以使用```--quiet```模式忽略此警告。 更新版本的RDE插件将不再提供用于读取上下文“aio-cli-plugin-cloudmanager”的回退。 若要继续使用它，只需将默认上下文配置为“aio-cli-plugin-cloudmanager”，请参阅上面的[设置本地上下文的示例](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)。

#### 还为Cloud Manager插件使用任何其他上下文名称

cloud manager插件提供了一个参数来定义要使用的上下文。 它目前尚不支持IMS默认上下文配置。 为此，请使用[示例配置RDE插件以设置本地上下文](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools)，并告知Cloud Manager插件在每次调用它时都使用“myContext”，如```--imsContextName=myContext```。
