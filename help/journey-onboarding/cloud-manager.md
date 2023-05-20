---
title: 访问 Cloud Manager
description: 了解如何访问 Cloud Manager，以便您可以设置项目资源。
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# 访问 Cloud Manager {#cloud-resources}

在這部分中 [入門歷程，](overview.md) 您將瞭解如何存取Cloud Manager，以便您可以設定專案資源。

## 目标 {#objective}

在本次入门培训历程的前一篇文章[将团队成员分配给 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md)中，您已授予 AEMaaCS 团队适当的角色。 現在瞭解如何存取Cloud Manager，以便您可以設定團隊使用的專案資源。

由于您完成了本次历程的前一步，您的团队可以访问 Cloud Manager。 Cloud Manager 用于创建和管理项目资源，如程序和环境。

閱讀本檔案後，您應瞭解下列事項：

* 系統管理員指派給 **業務負責人** 角色必須是組織中第一個登入和存取Cloud Manager的角色。
* 如何登录 Cloud Manager。

## Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要组成部分，是您团队的单一入口点。 它通过其专门构建的 CI/CD 管道为具有企业开发设置的客户提供支持，这些管道可确保全面测试和最佳代码质量，从而提供卓越的体验。 Cloud Manager 提供以自助方式启动所需的一切，包括创建云资源和环境的能力。

通常，分配给&#x200B;**业务负责人**&#x200B;产品配置文件的团队成员负责添加您的云资源，如程序和环境。 此人了解业务需求，并了解由谁完成初始 Cloud Manager 设置。

出於此入門歷程的目的，您作為系統管理員已經將自己指派給 **業務負責人** 產品設定檔，並可設定雲端資源。 根據實際專案需求，業務負責人可能與系統管理員相同，也可能不同。

## 作为系统管理员和业务负责人访问 Cloud Manager {#access-sysadmin-bo}

在您指派給的專案團隊成員之前 **業務負責人** 角色可以存取cloud manager並開始建立cloud資源，必須為系統管理員指派 **業務負責人** 角色。 他們還必須登入Cloud Manager，就像您在本次入門歷程的上一步中所做的那樣。

1. 确保您作为系统管理员已分配&#x200B;**业务负责人**&#x200B;角色。

   * 回到這個歷程的上一步， [將團隊成員指派給Cloud Manager產品設定檔，](assign-profiles-cloud-manager.md) 有關指派 **業務負責人** 角色給系統管理員。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并显示正常登陆页面。

通过使用&#x200B;**业务负责人**&#x200B;角色以系统管理员身份成功登录，您可以通过&#x200B;**业务负责人**&#x200B;角色初始化 Cloud Manager，以供其他用户使用。 您不會收到確認或任何訊息。 只要登入就足夠了。

直到您使用以系統管理員身份登入Cloud Manager **業務負責人** 角色，具有此角色的其他使用者 **業務負責人** 角色無法在Cloud Manager中建立計畫。 即使指派了正確的角色，此規則仍為真。

## 导航到 Cloud Manager {#navigate-cloud-manager}

使用者具有 **業務負責人** 角色會收到一封歡迎電子郵件，其中包含開始使用的連結。 按照以下步骤使用此欢迎电子邮件导航到 Cloud Manager。

1. 在歡迎電子郵件中，按一下 **開始使用**，如下圖所示。
   ![电子邮件示例](/help/journey-onboarding/assets/get-started-email.png)

1. 導覽至Cloud Manager的 **程式與產品** 頁面。

   >[!TIP]
   >
   >您还可以直接从 `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)` 导航到 Cloud Manager 的登录页面。 將此頁面加入書籤以供日後參考。

1. 您會被導向到Cloud Manager的登陸頁面。

或者，您也可以按照以下步骤从 Adobe Experience Cloud 主页导航到 Cloud Manager 的&#x200B;**程序和产品**&#x200B;页面

1. 直接导航到 [Adobe Experience Cloud](https://experience.adobe.com) 并使用 Adobe ID 登录。

1. 從Adobe Experience Cloud首頁，選取 **Experience Manager** 以開啟AEM首頁。

   ![Experience Cloud 主页](/help/journey-onboarding/assets/setup-resources2.png)

1. 於 **Cloud Manager** 圖磚，選取 **Launch**.

   ![AEM 主页](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登入後，您會被導向至Cloud Manager登陸頁面。 另請參閱 [檢視Cloud Manager的程式](#viewing-programs) 以取得更多詳細資料。

如何通过 Cloud Manager 访问您的程序和产品取决于您，并且不影响您如何使用 Cloud Manager 或如何管理您的程序。

>[!NOTE]
>
>根據Cloud Manager中指派的角色和應用程式的狀態，您在使用Cloud Manager使用者介面時會看到不同的畫面。

## 查看程序 {#viewing-programs}

成功存取Cloud Manager後，您所看到的將取決於程式的狀態，如以下部分所述。

### 当没有程序存在时 {#no-programs}

如果您的组织中不存在任何程序，则登陆页面会指示您创建第一个程序。

![无程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### 当程序已经存在时 {#programs-exist}

如果您的組織中存在程式，那麼您的登入頁面會顯示您現有的程式，並提供一個按鈕來新增其他程式。

![程序存在](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### 当程序存在且您是系统管理员时 {#programs-exist-sysadmin}

如果您的組織中存在程式並且您是系統管理員，則會顯示您的登入頁面 **管理存取權** 按鈕以及 **新增計畫** 選項。

![系统管理员视图](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## 正在验证您的用户角色 {#verify-user-roles}

成功登录 Cloud Manager 后，您可以验证您是否已被分配&#x200B;**业务负责人**&#x200B;产品配置文件。

1. 从窗口的右上角选择您的个人资料。

   ![用户配置文件](/help/journey-onboarding/assets/setup-resources5.png)

1. 若要顯示指派給使用者的角色，請選取 **使用者角色**.

   ![用户角色](/help/journey-onboarding/assets/setup-resources6.png)

1. 该对话框应确认您的用户具有&#x200B;**业务负责人**&#x200B;角色。

   ![用户角色列表](/help/journey-onboarding/assets/setup-resources7.png)

您已作为业务负责人成功登录 Cloud Manager！ 如果您未被分配&#x200B;**业务负责人**&#x200B;角色，请联系您的系统管理员。

## 后续内容 {#whats-next}

现在您可以作为系统管理员访问 Cloud Manager，您已经准备好创建第一个程序了。

透過下一次檢視檔案來繼續您的上線之旅 [建立計畫](create-program.md) 您可在何處學習如何執行此作業。

## 其他资源 {#additional-resources}

如果您想要超越入門歷程的內容，以下是額外的選用資源。

* [Cloud Manager 简介](/help/onboarding/cloud-manager-introduction.md) –
了解 Cloud Manager、Cloud Manager 程序和环境。
* [AEM as a Cloud Service 团队和生产简介](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
