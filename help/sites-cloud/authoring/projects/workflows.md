---
title: 使用项目工作流
description: 各種專案工作流程都可立即使用。
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 46%

---

# 使用项目工作流 {#working-with-project-workflows}

現成可用的專案工作流程包括下列專案：

* **项目审批工作流** – 此工作流允许您将内容分配给用户进行审查和批准。
* **请求启动项** – 此工作流用于请求启动项。
* **请求登陆页面** – 此工作流用于请求登陆页面。
* **请求电子邮件** – 此工作流用于请求电子邮件。
* **DAM建立和翻譯副本及DAM建立語言副本**  — 為資產和資料夾建立翻譯的二進位檔案、中繼資料和標籤。

根據您選取的專案範本，您有特定的工作流程可用：

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
>&amp;ast;这些工作流不会从项目中的&#x200B;**工作流**&#x200B;拼贴启动。另請參閱 [建立資產的語言副本。](/help/sites-cloud/administering/translation/managing-projects.md)

無論您選擇哪個工作流程，開始和完成工作流程的步驟都相同。 只有步驟會變更。

您直接在「專案」中啟動工作流程（「DAM建立語言副本」或「DAM建立和翻譯語言副本」除外）。 專案中任何未完成任務的資訊會列在 **任務** 圖磚。 使用者圖示旁會顯示需要完成之工作的通知。

有关在 AEM 中使用工作流的更多信息，请参阅以下内容：

* [参与工作流](/help/sites-cloud/authoring/workflows/participating.md)
* [将工作流应用于页面](/help/sites-cloud/authoring/workflows/applying.md)
* [配置工作流](/help/sites-cloud/administering/workflows-administering.md)

此部分介绍了可用于项目的工作流。

## 專案核准工作流程 {#project-approval-workflow}

在「專案核准」工作流程中，您可以將內容指派給使用者、檢閱，然後核准內容。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **`+`** 符号，然后选择&#x200B;**项目审批工作流**。
1. 輸入標題，並從「專案團隊」清單中選取指派給誰。 如果適用，請輸入說明、內容路徑、工作優先順序和到期日。

   ![请求审批](/help/sites-cloud/authoring/assets/projects-approval.png)

1. 单击&#x200B;**创建**。工作流程隨即開始。 任務會出現在 **任務** 圖磚。

## 請求啟動工作流程 {#request-launch-workflow}

此工作流程可讓您請求啟動。

1. 在您的简单项目中，选择&#x200B;**工作流**&#x200B;拼贴中的 **+** 符号，然后选择&#x200B;**请求启动工作流**。
1. 輸入啟動項的標題並提供啟動項來源路徑。 您也可以新增說明和上線日期（如適用）。 選取繼承來源頁面即時資料或排除子頁面（取決於您希望啟動項的行為）。

   ![请求启动项](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. 单击&#x200B;**创建**。工作流程隨即開始。 该工作流会显示在&#x200B;**工作流**&#x200B;列表中（单击&#x200B;**工作流**&#x200B;拼贴中的省略号 **...** 可访问此列表）。

## 为资产创建（和翻译）语言副本工作流 {#create-and-translate-language-copy-workflow-for-assets}

[为资产创建语言副本](/help/assets/translate-assets.md)中详细介绍了&#x200B;**创建语言副本**&#x200B;和&#x200B;**创建和翻译语言副本**&#x200B;工作流。
