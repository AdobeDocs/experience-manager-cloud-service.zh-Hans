---
title: 使用项目工作流
description: 各种项目工作流都可开箱即用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 41%

---

# 使用项目工作流 {#working-with-project-workflows}

现成可用的项目工作流包括以下内容：

* **项目审批工作流** – 此工作流允许您将内容分配给用户进行审查和批准。
* **请求启动项** – 此工作流用于请求启动项。
* **请求登陆页面** – 此工作流用于请求登陆页面。
* **请求电子邮件** – 此工作流用于请求电子邮件。
* **DAM创建和翻译副本和DAM创建语言副本**  — 为资源和文件夹创建已翻译的二进制文件、元数据和标记。

根据您选择的项目模板，您具有某些可用的工作流：

|   | **简单项目** | **翻译项目** |
|---|:-:|:-:|
| 项目审批工作流 | x |  |
| 请求启动项 | x |  |
| 请求登陆页面 | x |  |
| 请求电子邮件 | x | |
| DAM 创建语言副本&amp;ast; |  | x |
| DAM 创建和翻译语言副本&amp;ast; |   | x |

>[!NOTE]
>
>&amp;ast;这些工作流不会从项目中的&#x200B;**工作流**&#x200B;拼贴启动。参见 [创建资产的语言副本](/help/sites-cloud/administering/translation/managing-projects.md).

无论您选择哪个工作流，启动和完成工作流的步骤都是相同的。 只有步骤会更改。

直接在项目中启动工作流（DAM创建语言副本或DAM创建和翻译语言副本除外）。 有关项目中任何未完成任务的信息，请参见 **任务** 图块。 需要完成的任务的通知显示在用户图标旁边。

有关在 AEM 中使用工作流的更多信息，请参阅以下内容：

* [参与工作流](/help/sites-cloud/authoring/workflows/participating.md)
* [将工作流应用于页面](/help/sites-cloud/authoring/workflows/applying.md)
* [配置工作流](/help/sites-cloud/administering/workflows-administering.md)

此部分介绍了可用于项目的工作流。

## 项目审批工作流 {#project-approval-workflow}

在“项目审批”工作流中，您可以将内容分配给用户，审查并审批内容。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **`+`** 符号，然后选择&#x200B;**项目审批工作流**。
1. 输入标题，然后从“团队”列表中选择将其分配给的人员。 如果适用，请输入描述、内容路径、任务优先级和截止日期。

   ![请求审批](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 单击&#x200B;**创建**。工作流随即启动。 该任务出现在 **任务** 图块。

## 请求启动项工作流程 {#request-launch-workflow}

利用此工作流，可请求启动项。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **+** 符号，然后选择&#x200B;**请求启动工作流**。
1. 输入启动项的标题并提供启动项源路径。 您还可以添加描述和上线日期（如果适用）。 选择继承源页面活动数据或排除子页面，具体取决于您希望启动项的行为方式。

   ![请求启动项](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 单击&#x200B;**创建**。工作流随即启动。 该工作流会显示在&#x200B;**工作流**&#x200B;列表中（单击&#x200B;**工作流**&#x200B;拼贴中的省略号 **...** 可访问此列表）。

## 为资产创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

此 **创建语言副本** 和 **创建和翻译语言副本** 中详细介绍了这些工作流 [为资源创建语言副本](/help/assets/translate-assets.md).
