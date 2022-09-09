---
title: 使用项目工作流
description: 提供了多种开箱即用的项目工作流。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 100%

---

# 使用项目工作流 {#working-with-project-workflows}

现成可用的项目工作流包括：

* **项目审批工作流** – 此工作流允许您将内容分配给用户进行审查和批准。
* **请求启动项** – 此工作流用于请求启动项。
* **请求登陆页面** – 此工作流用于请求登陆页面。
* **请求电子邮件** – 此工作流用于请求电子邮件。
* **DAM 创建和翻译副本以及 DAM 创建语言副本** - 为资产和文件夹创建已翻译的二进制文件、元数据和标记。

根据您选择的项目模板，您可以使用特定工作流：

|  | **简单项目** | **翻译项目** |
|---|:-:|:-:|
| 项目审批工作流 | x |  |
| 请求启动项 | x |  |
| 请求登陆页面 | x |  |
| 请求电子邮件 | x |  |
| DAM 创建语言副本&amp;ast; |  | x |
| DAM 创建和翻译语言副本&amp;ast; |  | x |

>[!NOTE]
>
>&amp;ast;这些工作流不会从项目中的&#x200B;**工作流**&#x200B;拼贴启动。请参阅[为资产创建语言副本](/help/sites-cloud/administering/translation/managing-projects.md)。

无论您选择哪个工作流，启动和完成工作流的步骤都是相同的。只是具体的实施步骤有所不同。

您可以直接在项目中启动工作流（DAM 创建语言副本或 DAM 创建和翻译语言副本除外）。项目中任何未完成任务的信息会在&#x200B;**任务**&#x200B;拼贴中列出。用户图标旁边会显示需要完成的任务通知。

有关在 AEM 中使用工作流的更多信息，请参阅以下内容：

* [参与工作流](/help/sites-cloud/authoring/workflows/participating.md)
* [将工作流应用于页面](/help/sites-cloud/authoring/workflows/applying.md)
* [配置工作流](/help/sites-cloud/administering/workflows-administering.md)

此部分介绍了可用于项目的工作流。

## 项目批准工作流 {#project-approval-workflow}

在项目批准工作流中，您可以将内容分配给用户进行审核，然后批准内容。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **`+`** 符号，然后选择&#x200B;**项目审批工作流**。
1. 输入标题并从“团队”列表中选择要将其分配给的对象。在适用的情况下，输入描述、内容路径、任务优先级和到期日期。

   ![请求审批](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。相应任务会显示在&#x200B;**任务**&#x200B;拼贴中。

## 请求启动项工作流 {#request-launch-workflow}

使用此工作流，您可以请求启动项。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **+** 符号，然后选择&#x200B;**请求启动工作流**。
1. 输入启动项的标题并提供启动项源路径。在适用的情况下，您还可以添加描述和起始日期。根据您希望启动项具备的行为方式，选择“继承源页面活动数据”或“不包括子页面”。

   ![请求启动项](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 单击&#x200B;**创建**。该工作流随即会启动。该工作流会显示在&#x200B;**工作流**&#x200B;列表中（单击&#x200B;**工作流**&#x200B;拼贴中的省略号 **...** 可访问此列表）。

## 为资产创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

[为资产创建语言副本](/help/assets/translate-assets.md)中详细介绍了&#x200B;**创建语言副本**&#x200B;和&#x200B;**创建和翻译语言副本**&#x200B;工作流。
