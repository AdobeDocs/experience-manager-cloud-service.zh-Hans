---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service架構
description: 瞭解 [!DNL AEM Forms] as a Cloud Service瞭解平台的可擴充性、可復原性和效能。
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 4%

---

# [!DNL AEM] Formsas a Cloud Service架構 {#architecture}

[!DNL Adobe Experience Manager Forms] as a Cloud Service是雲端原生解決方案，適用於建立、管理、發佈和更新複雜數位表格和通訊，同時將提交的資料與後端程式、商業規則整合，並將資料儲存在外部資料存放區。 它延伸了 [!DNL Adobe Experience Manager as a Cloud Service]. 若要進一步瞭解擴充、部署、環境和其他基礎結構，請參閱 [的架構簡介 [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html).

AEM Formsas a Cloud Service支援兩個主要使用案例：數位註冊和客戶通訊。 下圖說明這兩個使用案例的架構。

## Forms數位註冊

![Forms — 數位註冊](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Forms通訊

![Forms-Communication](assets/forms-cloud-service-architecture-forms-communications.svg)

## 组件

Formsas a Cloud Service包含多個元件：

### CDN （內容傳遞網路）

每個AEM Formsas a Cloud Service程式都可以存取 [內建CDN服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html). 它包含在Forms as a Cloud Services的授權中。

### 创作

Author是在標準Author執行模式中執行的AEM Formsas a Cloud Service例項。 此範本適用於內部使用者、表單設計人員和開發人員。 「作者」環境會啟用下列功能：

* 製作和管理表單。
* 連線到Automated forms conversion服務以將PDF或XDP表單轉換為最適化表單。
* 建立及執行以Forms為中心的工作流程。
* 管理最適化表單資產。
* 管理通訊資產。
* 同步RESTful API (Real-time API)和Batch API，以建立、組合和提供品牌導向和個人化的通訊。
* 用於組合、重新排列和驗證PDF檔案的同步API。

### 发布

發佈執行個體是在標準發佈執行模式下執行的AEM Formsas a Cloud Service。 發佈例項適用於表單式應用程式的一般使用者，例如存取公共網站和提交表單的使用者。 可啟用下列功能：

* 呈現和提交表單給一般使用者。
* 傳輸原始提交的表單資料，以便在最終記錄系統中進一步處理和儲存。
* 正在連線至客戶管理的儲存裝置以儲存資料。
* 連結Adobe Sign以電子簽章最適化表單提交記錄。
* 同步API以建立、組合和提供品牌導向和個人化的通訊。
* 同步API以組合、重新排列和驗證PDF檔案。

AEMas a Cloud Service上無法使用反向復寫，無法將內容/資料從發佈服務傳送至作者服務。 不過，您可以設定在發佈上執行的最適化Forms，將資料提交到作者上的工作流程（工作流程只能對作者執行）。 這在核准使用案例中很有幫助。

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) 是Adobe Experience Manager的快取及/或負載平衡工具，可與企業級Web伺服器搭配使用。

### Adobe服務

**自动化表单转换服务**

[automated forms conversion服務](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=zh-Hans) 自動將您的PDF和XFA表單轉換為適合裝置、回應式且HTML5型的最適化表單。

**Adobe Sign**

Adobe Sign是雲端型電子簽章服務，可讓使用者使用瀏覽器或行動裝置傳送、簽署、追蹤及管理簽名程式。 您可以整合Adobe Sign與最適化表單，以自動化簽署工作流程、簡化單一和多重簽名流程，並以電子方式簽署最適化表單。

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### 客戶管理的儲存裝置

Formsas a Cloud Service提供將內容儲存在外部儲存系統（例如Blob存放區、資料庫或儲存服務）中的選項。 您也可以將包含敏感個人資料(SPD)元素的程式內工作流程資料(AEM工作流程變數資料)儲存在客戶管理的存放庫中，以便安全處理。 Adobe建議僅將敏感資料儲存在客戶管理的儲存裝置上。

您可以使用 **統一的儲存聯結器** 以連線至Blob儲存體和 **表單資料模型** 以連線至資料庫或後端服務（RESTful、SOAP、Azure Blob儲存體等）。

### 文档服务

檔案服務由下列專案組成：

* **輸出服務（通訊 — Document Generation API）** 協助建立品牌核准、個人化和標準化的檔案，例如業務往來函、報表、索賠處理信函、福利通知、每月帳單或歡迎套件。

* **組合器服務（通訊 — Document Manipulation API）** 協助合併、重新排列和驗證PDF檔案。

* **記錄檔案(DoR)服務** 協助產生記錄檔案(DoR)。 此服務會在其Pod中執行，且獨立於Formsas a Cloud Service的Author和Publish例項。 它有助於提供更好的效能，並依據負載獨立調整Pod。

### Cloud Manager

Cloud Manager是 [AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html). 這是我們客戶營運與開發人員角色的單一入口點。 這是可管理AEM計畫和環境的地方。 Cloud Manager已經演變成為自助服務入口網站，可以在這裡建立和設定AEMas a Cloud Service的主要元件：

* 建立和管理方案
* 在程式內建立和管理AEM環境
* 建立和管理將客戶程式碼和設定部署到特定環境的管道
* 取得這些元件的重要生命週期事件（例如產品更新）的通知。如需Cloud Manager的詳細資訊，請參閱 [瞭解Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) 和 [Cloud Manager簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hans).

### 开发人员控制台

開發人員控制檯提供每個執行Forms as a Cloud Service環境的各種細節。 這些詳細資訊有助於對環境進行偵錯。 如需詳細資訊，請參閱 [使用開發人員控制檯除錯AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by leveraging multiple integrations with Adobe Sign, Document Services, Form Data Model, Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While leveraging the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (for example, product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can leverage a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (for example, folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### 最適化表單製作 {#local-development}

當您設定並設定 [!DNL AEM Forms] as a Cloud Service於環境，您可以設定開發、測試和生產環境。 此外，設定並設定本機開發環境，以進行快速反複和開發。 您可以下載及設定AEM SDK，以及 [!DNL AEM Forms] 附加功能封存，用於設定本機 [!DNL Forms] as a Cloud Service開發環境。  如需詳細指示，請參閱 [設定本機開發環境](setup-local-development-environment.md).

## 调试 {#debugging}

AEMas a Cloud Service在自助式、可擴充的雲端基礎結構上執行。 它要求AEM開發人員瞭解並偵錯AEMas a Cloud Service的各個層面，從建置和部署，到取得執行AEM應用程式的詳細資訊。 如需詳細資訊，請參閱 [偵錯AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html).
