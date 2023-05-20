---
title: 探索Adobe Experience Manager Formsas a Cloud Service的最新創新。
description: 「探索 [!DNL AEM Forms] as a Cloud Service建立、管理和發佈企業級表單與業務流程。」
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: 4279b4a880429f535cf341d35ac38c9b4dc55ae2
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 7%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->


# 顶级 Adobe Experience Manager Forms 创新 {#latest-innovations}

Adobe Experience Manager Forms中的一些主要創新包括：

| 創新 | 详细信息 |
|---|---|
| Headless最適化Forms | 建立和管理 [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 在Adobe Experience Manager平台內。 讓您的開發人員能夠建立、發佈和管理互動式表單，這些表單可透過API存取和互動，而不是透過傳統的圖形使用者介面。 <br/> <br/> 這些表單的提交方式不需使用傳統的HTML表單介面。 換言之，它們可讓您透過API或後端程式碼以程式設計方式提交表單資料，無論前端是否有任何可見的表單元素。 <br/> ![](https://experienceleagueadobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?)<br/> Headless表單適用於各種情況，例如建置單頁應用程式、漸進式網頁應用程式或行動應用程式時，而其中傳統HTML表單介面可能不是必要或不實用。 Headless表單可讓開發人員直接透過API或後端程式碼提交表單資料，有助於簡化工作流程，並改善網頁應用程式的整體效能。 |
| 核心组件 | 此 [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 是一組24個開放原始碼、符合BEM規範的元件，建立在Adobe Experience Manager WCM核心元件的基礎上。 這些表單專為建立最適化Forms而設計，這些表單可適應使用者的裝置、瀏覽器和熒幕大小。 <br/> <br/>利用这些组件，可提供一系列广泛的表单字段选项（包括文本字段、复选框、下拉菜单等）来创建卓越的数据捕获和注册体验。此外也包含驗證、條件式邏輯和回應式設計等功能，這些功能可用來建立方便使用者且易於使用的表單。 <br/> ![](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?)<br/>此外，由于这些组件是开源的，因此，开发人员能够轻松定制和扩展组件以满足其组织的特定需求。而且，这些组件基于 BEM 方法而构建，这确保了它们可扩展且可维护。 |
| Microsoft PowerAutomate聯結器 | AEM Forms Power Automate聯結器可讓您將Adobe Experience Manager (AEM) Forms與Microsoft Power Automate (先前稱為Microsoft Flow)整合。 Power Automate是雲端型服務，可讓您在不同的應用程式和服務之間建立自動化工作流程。  <br/> <br/> 使用AEM Form Power Automate聯結器，您可以建立根據提交最適化表單自動觸發的工作流程。 例如，您可以建立工作流程，以在使用者提交表單時自動傳送電子郵件通知給特定人員，或在使用者完成表單時在Microsoft Planner中建立任務。  <br/> ![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999) <br/> AEM Forms Power Automate聯結器是一款功能強大的工具，可讓您將Adaptive Forms與連結Microsoft Power Automate的其他應用程式和服務自動化及整合，讓您使用更廣泛的工具。 您可以建立符合您特定需求的工作流程，並有能力新增自訂動作、條件和觸發器。 此外，Power Automate提供詳細的分析和報告，讓您能夠隨著時間監視和最佳化工作流程。 |
| Microsoft儲存聯結器 | 適用於的AEM Forms Microsoft儲存聯結器 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-sharedrive">OneDrive</a>， <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-sharedrive"> SharePoint， </a> 和 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?#submit-to-azure-blob-storage"> Azure Blob儲存體 </a> 聯結器可讓您將Adobe Experience Manager (AEM) Forms與Microsoft OneDrive和SharePoint整合。 透過此聯結器，您可以直接從Adaptive Forms將資料檔案和附件上傳到OneDrive和SharePoint。 <br/> ![](/help/forms/assets/onedrive-and-sharepoint.jpg) <br/>OneDrive和SharePoint可與其他商務應用程式整合，例如CRM系統、會計軟體和專案管理工具。 這可讓您簡化業務流程、減少手動資料輸入，並改善整體效率。 |
| 精靈UI | 最適化Forms精靈UI是快速輕鬆建立最適化表單的強大工具。 其簡單易用的介面和自訂選項可讓所有使用者存取，無論其技術專業水準為何。 <br/> <br/> 精靈UI透過引導使用者逐步完成表單建立過程來簡化最適化表單的建立過程。 精靈UI分成多個標籤，每個標籤清楚提供設定最適化表單的選項。 表單作者會以線性方式在標籤中前進，以選取範本、提交動作和表單元件的資料來源等選項。 <br/> ![](/help/release-notes/assets/wizard.png) <br/>精靈介面可簡化尋找最適化表單所有基本選項的流程，並使表單建立更容易，即使是不熟悉此技術的使用者也能做到。 |
| Adobe Analytics與Forms的Experience Cloud設定自動化  [!BADGE 即將推出]{type=Informative tooltip="Adobe Analytics即將推出適用於Forms的Experience Cloud設定自動化"} | 表單分析可透過測量使用者參與度、最佳化轉換率、監控表單效能和改善使用者體驗，為表單效能提供有價值的深入分析。  透過追蹤使用者行為和回饋，分析可以識別表單中造成挫折或困惑的區域，並指引改進表單的設計和功能。 <br/> <br/> 透過使用，您可以透過幾個按鈕來啟用Adobe Analytics和Experience Cloud設定自動化。 它可讓您將AEM Formsas a Cloud Service與Experience Platform標籤和Adobe Analytics連線起來，以擷取和追蹤您發佈之表單的績效量度。 <br/> <br/> ![](/help/forms/assets/forms-analytics-report.png) <br/><br/> Formsas a Cloud Service提供Adobe Analytics報表OOTB。 它可協助您輕鬆瞭解表單的效能。 表單層級量度可讓您深入瞭解表單在多個關鍵績效指標(KPI)上的執行情形，例如，轉譯、訪客、提交、平均填滿時間。 <br/> <br/> 它還提供使用者存取面板中欄位內容說明的平均次數詳細資訊，以協助您確定在提供資訊之前讓使用者停止並尋找資訊的欄位。 您可以進一步簡化這類欄位，或協助內容改善轉換。 |
| 新一代可組合性 | 透過新一代可撰寫性，企業內的員工都可以在他們偏好的工具(例如Microsoft Excel和Google Sheets)中建立表單，而無需進行有關新UI工作流程的廣泛培訓。 <br/> <br/> 此外，新一代可撰寫性專為以無與倫比的速度載入表單而設計，在即時頁面上獲得近乎完美的Google Lighthouse分數，從而確保最佳效能和使用者體驗。<br/> <br/> ![](/help/forms/assets/web-vitals.jpeg) 此外，由於Next Gen Composability提供的簡單工具，部署表單變得前所未有的簡單或快速。 只需最短的開發時間，您就可以輕鬆簡化上線的路徑，並為客戶提供卓越的外觀體驗。 |
