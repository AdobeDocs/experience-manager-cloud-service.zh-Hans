---
title: 快速开发环境
description: 了解如何在云环境中利用快速开发环境进行快速开发迭代。
hidefromtoc: true
source-git-commit: 983901387d059a98942b4f7c533770a55dd4ff4a
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 7%

---


# 快速开发环境 {#rapid-development-environments}

>[!AVAILABILITY]
>
>此功能尚不可用。

为了部署更改，当前的云开发环境需要使用一种流程，该流程采用称为CI/CD管道的广泛代码安全和质量规则。 对于需要快速、迭代更改的情况，Adobe引入了快速开发环境（简称RDE）。

RDE允许开发人员快速部署和审查更改，从而最大限度地减少测试经证明可在本地开发环境中工作的功能所需的时间。

在RDE中测试了更改后，即可通过Cloud Manager管道将其部署到常规的云开发环境。

## 简介 {#introduction}

RDE可用于代码、内容以及Apache或Dispatcher配置。 与常规的云开发环境不同，开发人员可以使用本地命令行工具将本地构建的代码同步到RDE。

每个程序都配置了RDE。 对于沙盒帐户，它们将在数小时未使用后休眠。

通常，单个开发人员在给定时间使用RDE来测试和调试特定功能。 开发会话完成后，RDE可重置为默认状态，以供下次使用。

<!-- Temporarily hiding this. See CQDOC-19795 for more details

Additional RDEs may be purchased for Production programs -->

## 在程序中启用RDE {#enabling-rde-in-a-program}

请按照以下步骤使用Cloud Manager为您的项目创建RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要向其添加RDE的程序以显示其详细信息。

   * RDE可以添加到这两个 [沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [生产计划。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. 从&#x200B;**程序概述**&#x200B;页面，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**添加环境**&#x200B;以添加环境。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

      ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 选择 **快速开发** 下 **选择环境类型** 标题。
      * 可用/已使用的环境的数量显示在环境类型后面的括号中。
   * 提供 **名称** 来获取。
   * 提供可选 **描述** 来获取。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。 

有关使用Cloud Manager创建环境、管理谁有权访问环境以及分配自定义域的更多信息，请参阅 [Cloud Manager文档。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安装RDE命令行工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager为程序添加RDE后，您可以通过设置命令行工具与其进行交互，如以下步骤所述：

1. 按照以下过程安装Adobe I/OCLI工具 [此处](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安装Adobe I/OCLI tools cloud manager插件，并按照说明对其进行配置 [此处](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 通过运行以下命令来安装Adobe I/OCLI工具AEM RDE插件：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 为您的组织ID配置Cloud Manager插件：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   并将字母数字字符串替换为您自己的组织ID，您可以使用策略查找该ID [此处](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 接下来，配置您的项目ID:

   `aio config:set cloudmanager_programid 12345`

1. 然后，配置RDE要附加到的环境ID:

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

1. 通过运行

   `aio cloudmanager:list-programs`

   这应该会列出您配置的组织下的所有项目。

   请注意，上述要求您是Cloud Manager的成员 **开发人员 — Cloud Service** 产品配置文件。 请参阅 [本页](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 以了解更多详细信息。

   或者，如果您可以通过运行以下命令登录到开发人员控制台，则可以确认您具有此开发人员角色：

   `aio cloudmanager:environment:open-developer-console`

## 在开发新功能时使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建议使用以下工作流来开发新功能：

* 当通过AEMas a Cloud Service SDK到达中间里程碑并在本地成功验证该里程碑时，应将代码提交到尚未包含在主行中的git功能分支，尽管提交到git是可选的。 构成“中间里程碑”的内容因团队习惯而异。 示例包括几行新代码、半天工作或完成子功能。

* 如果RDE已被其他功能使用，并且您想要 [将其重置为默认状态](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重置将需要几分钟时间，并且所有现有内容和代码都将被删除。 您可以使用RDE状态命令确认RDE已准备就绪。

* 使用RDE命令行界面，将本地代码同步到RDE。 选项包括安装内容包、特定包、OSGi配置文件、内容文件和Apache/Dispatcher配置的zip文件。 也可以引用远程内容包。 请参阅 [RDE命令行工具](#rde-cli-commands) 的子菜单。 您可以使用status命令验证部署是否成功。 （可选）使用包管理器来安装内容包。

* 在RDE中测试代码。 Cloud Manager中提供了创作和发布URL。

* 如果代码未按预期运行，请使用标准调试技术来了解问题并进行适当的更改。 在不将代码修改提交到git（因为它们尚未验证）的情况下，使用本地CLI将代码同步到RDE。 继续迭代，直到问题得到解决。

* 在代码按预期行为后，将代码提交到git功能分支。

* 同步到RDE的代码不使用Cloud Manager管道，因此，现在您应该使用Cloud Manager非生产管道将git功能分支部署到云开发环境。 这将验证代码是否通过Cloud Manager质量门，并让您有信心在以后使用Cloud Manager生产管道成功部署代码。

* 对每个中间里程碑重复上述步骤，直到该功能的所有代码都准备就绪为止，并且在RDE和云开发环境中均运行良好。

* 通过Cloud Manager生产管道将代码部署到生产环境。

## 使用RDE调试现有功能 {#use-rde-to-debug-an-existing-feature}

工作流与开发新功能类似。 区别在于，同步到RDE的代码将反映任何被推送到已发现问题的环境的git标签。 此外，部署与上游环境匹配的内容可能会非常有用。 这可以通过导出和导入内容包来实现。

## 同一RDE上的多个开发人员协作 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支持单个项目。 由于代码是从本地开发环境同步到RDE环境，因此对于一个开发人员而言，在给定时间自行使用代码是最自然的。

但是，通过谨慎的协调，多个开发人员可以验证特定功能或调试特定问题。 关键是每个开发人员保持其本地项目同步，以便特定开发人员所做的更改会被其他开发人员吸收，否则，一个开发人员可能会无意中覆盖另一个开发人员的代码。 建议每个开发人员在同步到RDE之前将其更改提交到共享的git分支，以便其他开发人员在进行自己的更改之前先提取更改。

## RDE命令行工具命令 {#rde-cli-commands}

### 帮助/一般信息 {#help}

* 对于命令列表，请键入：

   `aio aem:rde`

* 有关命令的详细帮助，请键入：

   `aio aem rde <command> --help`

### 部署到RDE {#deploying-to-rde}

本节介绍如何使用RDE CLI部署、安装或更新包、OSGi配置、内容包、单个内容文件以及Apache或Dispatcher配置。

一般使用模式为 `aio aem:rde:install <artifact>`.

您可以找到以下一些示例：

<u>部署内容包</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的响应如下所示：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

或者，您也可以引用远程存储库：

`aio aem:rde:install 'https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip'`

<u>部署OSGI配置</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

其中，成功部署的响应如下所示：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署包</u>

要部署包，请使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

其中，成功部署的响应如下所示：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署内容文件</u>

要部署内容文件，请使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

其中，成功部署的响应如下所示：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher配置</u>

对于此类配置，整个文件夹结构需要采用zip文件的形式。 您可以通过从调度程序配置文件夹的根中运行此命令来压缩该文件：

`zip -y -r dispatcher.zip`

然后，使用以下命令部署配置：

`aio aem:rde:install -t dispatcher-config dispatcher-wknd-2.1.0.zip`

成功的部署将生成如下所示的响应：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的代码不会经历Cloud Manager管道及其关联的质量门，但代码会进行一些分析，这些分析会报告错误，如以下代码示例所示：

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

上述代码示例说明了捆绑包未解析时的行为，在这种情况下，捆绑包是“暂存”的，只有在通过安装其他代码满足其要求（在此例中，缺少导入）时，才会安装该捆绑包。

### 检查RDE的状态 {#checking-rde-status}

您可以使用RDE CLI检查环境是否准备好部署到，因为哪些部署是通过RDE插件进行的。

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

如果该命令返回有关实例部署的注释，您仍然可以继续并执行下次更新，但您的最后一个实例可能尚未显示在实例上。

### 显示部署历史记录 {#show-deployment-history}

您可以通过运行以下项来检查对RDE进行的部署的历史记录：

`aio aem:rde:history`

它会以以下形式返回响应：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 从RDE中删除 {#deleting-from-rde}

您可以通过CLI工具删除以前部署到RDE的配置和包。 使用 `status` 命令，其中包含可删除内容的列表 `bsn` 对于包和 `pid` 用于删除命令中引用的配置。

例如，如果 `com.adobe.granite.demo.MyServlet.cfg.json` 已安装， `bsn` 只是 `com.adobe.granite.demo.MyServlet`，而 **cfg.json** 后缀。

不支持删除内容包或内容文件。 要删除它们，应重置RDE，这会将其返回到默认状态。

有关更多详细信息，请参阅以下示例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

## 重置 {#reset-rde}

重置RDE会从创作实例和发布实例中删除所有自定义代码、配置和内容。 例如，如果RDE已用于测试特定功能，并且您希望将其重置为默认状态以测试其他功能，则此功能会非常有用。

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

您可以按照以下步骤使用Cloud Manager重置RDE:

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要重置RDE的程序。

1. 在&#x200B;**概述**&#x200B;页面中，单击屏幕顶部的&#x200B;**环境**&#x200B;选项卡。

   ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**全部显示**&#x200B;按钮，直接跳转到&#x200B;**环境**&#x200B;选项卡。

      ![显示所有选项](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 的 **环境** 窗口打开，并列出程序的所有环境。

   ![“环境”选项卡](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 单击要重置的RDE的省略号按钮，然后选择 **重置**.

   ![查看环境详细信息](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 通过单击 **重置** 中。

   ![确认重置](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager通过横幅通知确认已开始重置过程。

   ![重置横幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

启动RDE重置过程后，通常需要几分钟才能完成并将环境返回到其默认状态。 可以在 **状态** 列 **环境** 卡或 **环境** 窗口。

![RDE重置状态](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您还可以直接从 **环境** 卡 **概述** 页面。

![从环境卡重置RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有关如何使用Cloud Manager管理环境的更多信息，请参阅 [Cloud Manager文档。](/help/implementing/cloud-manager/manage-environments.md)

## 日志记录 {#logging}

可以通过修改OSGi配置来设置日志级别。 检查 [文档](/help/implementing/developing/introduction/logging.md) 以了解更多信息。

## RDE与云开发环境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

虽然RDE在许多方面与云开发环境类似，但为了允许快速同步代码，RDE存在一些较小的体系结构差异。 将代码传递到RDE的机制不同 — 对于RDE，一个会同步来自本地开发环境的代码，而对于云开发环境，一个会通过Cloud Manager部署代码。

出于这些原因，建议在RDE环境上验证代码后，使用非生产管道将代码部署到云开发环境。 最后，在使用生产管道部署之前，先测试代码。

<!-- Temporarily hiding this. See CQDOC-19795 for more details

## How many RDEs do I need? {#how-many-rds-do-i-need}

The purchase of additional RDEs for Production programs will be possible beginning with late January.

The number of RDEs needed depends on the make-up and processes of an organization. The most flexible model is where an organization purchases a dedicated RDE for each one of their AEM CS developers. In this model, each developer can test their code on the RDE without needing to coordinate with other team members around whether an RDE environment is available.

At the other extreme, a team with a single RDE may use internal processes to coordinate which developer can use the environment at a given time. This can possibly be whenever a developer has hit an intermediate feature milestone and is ready to validate in a Cloud environment where they can quickly make the changes they need.

An intermediate model is one where an organization purchases a number of RDEs that will create a situation in which not every developer will have a dedicated environment, but there is a greater likelihood of an unused RDE being available. One strategy could be to allocate an RDE per scrum team or major feature. Internal processes may be used to coordinate usage of the environments. -->
