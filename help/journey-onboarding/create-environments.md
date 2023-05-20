---
title: 创建环境
description: 了解如何使用 Cloud Manager 创建您的首批环境。
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 53%

---

# 创建环境 {#create-environments}

在這部分中 [入門歷程，](overview.md) 您將瞭解如何使用Cloud Manager建立您的首批環境。

## 目标 {#objective}

在阅读了本次入门培训历程的前一篇文档[创建程序](create-program.md)后，您现在拥有了自己的 Cloud Manager 程序。 现在您可以了解如何使用 Cloud Manager 为该程序创建您的首批环境。

阅读本文档后，您将：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

## 什么是环境？ {#environments}

环境位于 Cloud Manager 层次结构中程序的下方。 虽然程序允许您组织解决方案并授予特定团队成员访问这些程序的权限，但环境属于特定程序，是这些程序中 Adobe 解决方案的单个实例。环境用于特定目的，如创作内容或测试新开发。 Cloud Manager 的 CI/CD 管道便于将代码从 Git 存储库部署到这些环境。

如果您回想一下理論上的WKND Travel and Adventure Enterprises的範例，他們是一家專注於旅遊相關媒體的租使用者，他們可能有兩個計畫。 亦即，WKND Magazine部門的Sites計畫，以及WKND Media部門的Assets計畫。 每个程序可能都有两个环境，例如一个生产环境（为站点的实际流量提供服务）和一个开发环境（用于测试新的应用程序代码）。

有四種不同型別的環境：

* **生产和暂存** – 生产和暂存环境成对可用，分别用于生产和测试目的。
* **開發**  — 可以為開發和測試目的建立開發環境，並且只能與非生產管道相關聯。
* **快速開發**  — 快速開發環境(RDE)可讓開發人員快速部署和檢閱變更，將測試經證實可在本機開發環境中運作的功能的時間減到最少。

出於此上線歷程的目的，為了讓您以最低程度開始，您可以建立一個可用來探索AEMas a Cloud Service功能的開發環境。

## 创建环境 {#creating-environments}

1. 登入雲端管理員，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 選取您要新增環境的計畫。

1. 若要新增環境，請從 **計畫總覽** 頁面，在 **環境** 卡片，選取 **新增環境**.

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

      ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 选择&#x200B;**环境类型**。
      * 可用/使用的环境数显示在开发环境类型后面的括号中。
   * 提供&#x200B;**环境名称**。
   * 提供&#x200B;**环境描述**。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

环境可用后，分配给&#x200B;**开发人员**&#x200B;的组织成员可以登录 Cloud Manager 并管理 Cloud Manager Git 存储库。

## 后续内容 {#whats-next}

既然您已经阅读了入门培训历程的这一部分，您应该：

* 了解什么是环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

您的云资源已创建，可以由您的团队访问。 作為系統管理員，您必須先將您的團隊成員指派給AEM中與Adobe Admin Consoleas a Cloud Service的產品設定檔，以便他們能夠存取這些資源。

因此，您應該透過下一次檢視檔案來繼續您的入門歷程 [將團隊成員指派給AEMas a Cloud Service產品設定檔](assign-profiles-aem.md). 在該檔案中，您將瞭解如何授予團隊成員存取新環境的許可權。

## 其他资源 {#additional-resources}

如果您想要超越入門歷程的內容，以下是額外的選用資源。

* [管理環境](/help/implementing/cloud-manager/manage-environments.md)  — 瞭解您可以建立的環境型別，以及如何為您的Cloud Manager專案建立環境型別
* [使用Adobe Cloud Manager — 環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager環境由AEM編寫、發佈和Dispatcher服務組成。 了解不同的环境如何支持角色，以及如何使用不同的 CI/CD 管道互动。
* [快速開發環境](/help/implementing/developing/introduction/rapid-development-environments.md)  — 請參閱本檔案以瞭解如何使用RDE的詳細資訊

<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

