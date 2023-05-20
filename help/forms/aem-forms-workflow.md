---
title: OSGi上以Forms為中心的工作流程
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用 [!DNL AEM Forms] 自動化並快速建立稽核和核准的工作流程，以啟動檔案服務
seo-description: Use [!DNL AEM Forms] Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# OSGi上以Forms為中心的工作流程{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企業會從數以百計與數以千計的表單、各種後端系統，以及線上或離線資料來源收集資料。 他們還擁有一組動態的使用者，可就資料做出決策，其中涉及反複的稽核和核准流程。

除了內部和外部對象的檢閱和核准工作流程，大型組織和企業也有重複性的任務。 例如，將PDF檔案轉換為另一種格式。 以手動方式完成這些工作會花費許多時間與資源。 企業也有法律要求以數位方式簽署檔案並封存表單資料，以供日後以預先定義的格式使用。

## OSGi上以Forms為中心的工作流程簡介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM工作流程快速建立最適化Forms型工作流程。 這些工作流程可用於審查和核准、業務流程流、啟動檔案服務、與Adobe Sign簽名工作流程整合以及類似操作。 例如，信用卡申請處理、員工休假核准工作流程、將表單儲存為PDF檔案。 此外，這些工作流程也可在組織內或跨網路防火牆使用。

透過OSGi上的Forms工作流程，您可以快速在OSGi棧疊上建置和部署各種任務的工作流程，而不需要在JEE棧疊上安裝完整的流程管理功能。 工作流程的開發和管理使用熟悉的AEM Workflow和AEM Inbox功能。 工作流程構成了自動化跨越多個軟體系統、網路、部門甚至組織的真實業務流程的基礎。

設定後，這些工作流程可以手動觸發，以完成定義的流程，或在使用者提交表單時以程式設計方式執行 <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

OSGi以Forms為中心的工作流程延伸 [AEM收件匣](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) 並提供額外的元件（步驟）供AEM Workflow編輯器新增支援 [!DNL AEM Forms] — 以工作流程為中心。 <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

全部 [!DNL AEM Forms] 工作流程步驟支援使用變數。 變數可讓工作流程步驟在執行階段跨步驟保留和傳遞中繼資料。 您可以建立不同型別的變數來儲存不同型別的資料。 您也可以建立變數集合（陣列）來儲存多個相關、相同型別資料的執行個體。 通常情況下，當您需要根據其持有的值做出決定或儲存您稍後在程式中需要的資訊時，會使用變數或變數集合。 如需有關在這些以Forms為中心的工作流程元件中使用變數的詳細資訊（步驟），請參閱 [OSGi上以Forms為中心的工作流程 — 步驟參考](aem-forms-workflow-step-reference.md). 如需建立和管理變數的詳細資訊，請參閱 [AEM工作流程中的變數](variable-in-aem-workflows.md).

下圖說明在OSGi上建立、執行及監控Forms工作流程的端對端程式。

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 开始之前 {#before-you-start}

* 工作流程是真實世界業務流程的表示法。 讓您的真實商業程式與商業程式參與者清單隨時待命。 此外，在開始建立工作流程之前，請準備好宣傳品(最適化Forms、PDF檔案等)。
* 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並協助報告工作流程的進度。 將您的業務流程劃分為邏輯階段。
* 您可以設定AEM Workflows的指派工作步驟，以傳送電子郵件通知給使用者或受指派人。 所以， [啟用電子郵件通知](#configure-email-service).
* 工作流程也可以使用Adobe符號進行數位簽名。 如果您打算在工作流程中使用Adobe Sign，請 [設定Adobe Sign用於 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 將其用於工作流程之前。

## 建立工作流程模型 {#create-a-workflow-model}

工作流程模型包含商業流程的邏輯和流程。 它由一系列步驟組成。 這些步驟是AEM元件。 您可以視需要使用引數和指令碼來擴充工作流程步驟，以提供更多功能和控制。 [!DNL AEM Forms] 除了開箱即用的AEM步驟外，還提供一些步驟。 如需AEM和 [!DNL AEM Forms] 步驟，請參閱 [AEM工作流程步驟參考](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) 和 [OSGi上以Forms為中心的工作流程 — 步驟參考](aem-forms-workflow.md).

AEM提供直覺式使用者介面，可使用提供的工作流程步驟建立工作流程模型。 如需建立工作流程模型的逐步指示，請參閱 [建立工作流程模型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows). 下列範例提供逐步指示，讓您為核准與複查工作流程建立工作流程模型：

>[!NOTE]
>
>您必須是工作流程編輯器群組的成員，才能建立或編輯工作流程模型。

### 建立核准和稽核工作流程的模型 {#create-a-model-for-an-approval-and-review-workflow}

核准和稽核工作流程適用於需要人為干預才能做出決定的任務。 下列範例會建立由前台銀行代理填寫的按揭貸款申請的工作流程模型。 填妥應用程式後，就會傳送以進行核准。 稍後會使用Adobe Sign將核准的申請傳送給申請人以取得電子簽章。

此範例可作為以下附加的套件提供。 使用封裝管理程式匯入並安裝範例。 您也可以執行下列步驟，手動建立應用程式的工作流程模型：

此範例會建立工作流程模型，作為前台銀行代理商填寫的抵押應用程式。 填寫完畢後，就會傳送應用程式以供核准。 稍後，核准的應用程式會傳送給客戶，以使用Adobe Sign進行電子簽章。 您可以使用封裝管理程式匯入及安裝範例。

[获取文件](assets/example-mortgage-loan-application.zip)

1. 開啟「工作流程模型」主控台。 預設URL為 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 選取 **建立**，則 **建立模型**. 「新增工作流程模型」對話方塊隨即顯示。
1. 輸入 **標題** 和 **名稱** （選擇性）。 例如，抵押貸款應用程式。 點選 **完成**.
1. 選取新建立的工作流程模型並點選 **編輯**. 現在，您可以新增工作流程步驟以建立商業邏輯。 第一次建立工作流程模型時，模型會包含：

   * 步驟：流程開始與流程結束。 這些步驟代表工作流程的開始和結束。 這些步驟為必要步驟，無法編輯或移除。
   * 名為步驟1的參與者步驟範例。 此步驟已設定為指派工作專案給管理員使用者。 移除此步驟。

1. 啟用電子郵件通知。 您可以在OSGi上設定以Forms為中心的工作流程，以傳送電子郵件通知給使用者或受指派人。 執行以下設定以啟用電子郵件通知：

   1. 前往AEM設定管理員，網址為 `https://[server]:[port]/system/console/configMgr`.
   1. 開啟 **[!UICONTROL Day CQ郵件服務]** 設定。 指定 **[!UICONTROL smtp伺服器主機名稱]**， **[!UICONTROL SMTP伺服器連線埠、]** 和 **[!UICONTROL 「寄件者」地址]** 欄位。 单击“**[!UICONTROL 保存]**”。
   1. 開啟 **[!UICONTROL Day CQ連結外部化器]** 設定。 在 **[!UICONTROL 網域]** 欄位中，指定本機、作者和發佈執行個體的實際主機名稱/IP位址和連線埠號碼。 单击“**[!UICONTROL 保存]**”。

1. 建立工作流程階段。 一個工作流程可以有多個階段。 這些階段會顯示在AEM收件匣中，並報告工作流程的進度。

   若要定義階段，請點選 ![資訊圈](assets/info-circle.png) 圖示若要開啟工作流程模型屬性，請開啟 **階段** 標籤，為工作流程模型新增階段，然後點選 **儲存並關閉**. 以抵押貸款申請為例，建立階段：貸款請求、貸款請求狀態、要簽署的檔案，以及已簽署的貸款檔案。

1. 拖放 **指派任務** 步驟瀏覽器至工作流程模型。 使其成為模型的第一步。

   指派任務元件會將工作流程建立的任務指派給使用者或群組。 除了指派工作之外，您也可以使用元件來指定工作的最適化表單或非互動式PDF。 最適化表單必須接受使用者的輸入，且非互動式PDF或使用唯讀最適化表單進行僅稽核工作流程。

   您也可以使用步驟來控制工作的行為。 例如，建立自動記錄檔案、將任務指派給特定使用者或群組、提交資料的路徑、要預先填入的資料路徑以及預設動作。 如需指派工作步驟選項的詳細資訊，請參閱 [OSGi上以Forms為中心的工作流程 — 步驟參考](aem-forms-workflow.md) 檔案。

   ![工作流程編輯器](assets/workflow-editor.png)

   以按揭應用程式為例，設定指派工作步驟以使用唯讀最適化表單，並在工作完成後顯示PDF檔案。 此外，選取可核准貸款請求的使用者群組。 於 **動作** 標籤，停用 **提交** 選項。 建立 **actionTaken** 字串資料型別的變數，並將變數指定為 **路由變數**. 例如，actionTaken。 此外，請新增「核准」和「拒絕」路由。 路由在AEM收件匣中會顯示為個別的動作（按鈕）。 工作流程會根據使用者點選的動作（按鈕）選取分支。

   您可以針對設定為例如Mortgage Application之指派工作步驟的所有欄位整組值，匯入範例套件（可在區段開頭下載）。

1. 將OR拆分元件從步驟瀏覽器拖放至工作流程模型。 「OR分割」會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您在工作流程中匯入條件式處理路徑。 您可視需要將工作流程步驟新增至每個分支。

   您可以使用規則定義、ECMA指令集或外部指令集來定義分支的路由表示式。

   使用運算式編輯器建立Branch 1和Branch 2的路由運算式。 這些路由運算式可協助您根據AEM收件匣中的使用者動作選擇分支。

   **分支1的路由運算式**

   使用者點選時 **核准** 在AEM收件匣中，會啟用分支1。

   ![OR分割範例](assets/orsplit_branch1_active_new.png)

   **分支2的路由運算式**

   使用者點選時 **拒絕** 在AEM收件匣中，會啟用分支2。

   ![OR分割範例](assets/orsplit_branch2_active_new.png)

   如需使用變數建立路由運算式的詳細資訊，請參閱 [中的變數 [!DNL AEM Forms] 工作流程](variable-in-aem-workflows.md).

1. 新增其他工作流程步驟以建立商業邏輯。

   在抵押範例中，新增產生「記錄檔案」、兩個指派工作步驟，以及一個簽署檔案步驟至模型的「分支1」，如下圖所示。 一個指派任務步驟是顯示和傳送 **將簽署給申請者的貸款檔案** 另一個指派任務元件為 **顯示已簽署的檔案**. 此外，新增指派工作元件至分支2。 當使用者點選AEM收件匣中的拒絕時，它會啟動。

   針對指派任務步驟、記錄檔案步驟和簽署檔案步驟的所有欄位之完整值集（例如按揭應用程式），匯入範例套件，可在本節開頭下載。

   工作流程模型已準備就緒。 您可以透過各種方法啟動工作流程。 如需詳細資訊，請參閱 [在OSGi上啟動以Forms為中心的工作流程](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## 建立以Forms為中心的工作流程應用程式 {#create-a-forms-centric-workflow-application}

應用程式是與工作流程關聯的最適化表單。 透過「收件匣」提交應用程式時，它會啟動相關的工作流程。 若要讓Forms工作流程可作為AEM收件匣中的應用程式，以及 [!DNL AEM Forms] 應用程式，請執行以下動作以建立工作流程應用程式：

>[!NOTE]
>
>您必須是fd-administrator群組的成員，才能建立和管理工作流程應用程式。

1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流程應用程式]** 和點選 **[!UICONTROL 建立]**.
1. 在「建立工作流程應用程式」視窗中，為下列欄位提供輸入，然後點選 **建立**. 隨即會建立新應用程式，並列在「工作流程應用程式」畫面中。

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>標題會顯示在AEM收件匣中，並協助使用者選擇應用程式。 保持其描述性。 例如，儲蓄帳戶開立應用程式。<br /> </td>
  </tr>
  <tr>
   <td>名称 </td>
   <td>指定應用程式的名稱。 除字母、數字、連字型大小和底線以外的所有字元都會取代為連字型大小。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>說明會顯示在AEM收件匣中。 在說明欄位中提供應用程式的詳細資訊。 例如，應用程式的用途。<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td><p>指定自適應表單的路徑。 當使用者啟動應用程式時，會顯示指定的最適化表單。</p> <p><strong>注意</strong>：工作流程應用程式不支援超過一頁的表單和PDF檔案，或需要在Apple iPad上捲動。 在Apple iPad上開啟應用程式，且最適化表單或PDF檔案長於頁面時，表單欄位和第二頁的內容會遺失。</p> </td>
  </tr>
  <tr>
   <td>访问组</td>
   <td><p>選取群組。 只有選取群組的成員才能在AEM收件匣中看到應用程式。 存取群組選項可讓所有的 [!DNL workflow-users] 群組可供選取。 </p> <br /> </td>
  </tr>
  <tr>
   <td>预填服务</td>
   <td>選取 <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">預填服務</a> 最適化表單的預設值。<br /> </td>
  </tr>
  <tr>
   <td>工作流模型</td>
   <td>選取 <a href="aem-forms-workflow.md#create-a-workflow-model">工作流程模型</a> 應用程式的。 工作流程模型包含業務處理的邏輯和流程。 </td>
  </tr>
  <tr>
   <td>数据文件路径</td>
   <td>指定crx-repository中資料檔案的路徑。 路徑是相對於最適化表單有效負載的，並包含資料檔案的名稱。 一律包含檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路径</td>
   <td>指定crx-repository中附件資料夾的路徑。 附件路徑是相對於承載位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>记录文档路径</td>
   <td>指定crx-repository中記錄檔案的路徑。 此路徑是相對於最適化表單裝載位置。 一律包含檔案的完整名稱，包括副檔名（如適用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上啟動以Forms為中心的工作流程 {#launch}

您可以透過以下方式啟動或觸發以Forms為中心的工作流程：

* [從AEM收件匣提交應用程式](#inbox)
* [從以下位置提交應用程式： [!DNL AEM Forms] 應用程式](#afa)

* [提交最適化表單](#af)
* [使用watched資料夾](#watched)

* [提互動動式通訊或信件](#letter)

### 從AEM收件匣提交應用程式 {#inbox}

您建立的工作流程應用程式可在「收件匣」中作為應用程式使用。 屬於下列成員的使用者： [!DNL workflow-users] 群組可以填寫並提交觸發相關工作流程的應用程式。 如需使用AEM收件匣提交應用程式和管理工作的相關資訊，請參閱 [在AEM收件匣中管理Forms應用程式和工作](manage-applications-inbox.md).

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and allows you to make changes to the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### 提交最適化表單 {#af}

您可以設定最適化表單的提交動作，以在提交最適化表單時啟動工作流程。 最適化Forms提供 **叫用AEM工作流程** 提交動作，在提交最適化表單時啟動工作流程。 如需提交動作的詳細資訊，請參閱 [設定提交動作](configuring-submit-actions.md). 若要提交最適化表單，請透過 [!DNL AEM Forms] 應用程式，啟用同步處理 [!DNL AEM Forms] 最適化表單屬性中的應用程式。

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Tap **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Tap **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### 清除工作流程例項 {#purge-workflow-instances}

最大限度地减少工作流实例的数量可以提高工作流引擎的性能，因此，您可以定期从存储库中清除已完成或正在运行的工作流实例。如需詳細資訊，請參閱 [定期清除工作流程例項](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html) 清除工作流程例項
