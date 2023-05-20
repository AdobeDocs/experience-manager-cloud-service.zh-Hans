---
title: 整合最適化表單與Microsoft® Power Automate
description: 整合最適化表單與Microsoft® Power Automate。
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 5%

---

# 連線最適化表單與Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

您可以設定最適化表單，在提交時執行Microsoft® Power Automate Cloud Flow。 配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automation Cloud Flow 进行处理。 它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。以下範例說明將最適化表單與Microsoft® Power Automate整合後可執行的操作：

* 在Power Automate業務流程中使用最適化Forms資料
* 使用Power Automate將擷取的資料傳送至500多個資料來源或任何公開可用的API
* 對擷取的資料執行複雜的計算
* 依照預先定義的排程將最適化Forms資料儲存至儲存系統

最適化Forms編輯器提供 **叫用Microsoft® Power Automate流程** 傳送最適化表單資料、附件和記錄檔案的提交動作會傳送到Power Automate Cloud Flow。 若要使用提交動作將擷取的資料傳送至Microsoft®Power Automate， [使用Microsoft® Power Automate連線您的Formsas a Cloud Service執行個體](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## 前提条件

以下為連線最適化表單與Microsoft® Power Automate的必要條件：

* Microsoft® Power Automate Premium授權。
* Microsoft® [Power Automate流程](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) 使用 `When an HTTP request is received` 觸發以接受最適化表單提交資料。


* 具有Forms作者和Forms管理員許可權的Experience Manager使用者。
* 確保用於連線到Power Automate的帳戶是Power Automate流程的所有者。


## 使用Microsoft® Power Automate連線您的Formsas a Cloud Service執行個體 {#connect-forms-server-with-power-automate}

執行下列動作，將您的Formsas a Cloud Service執行個體與Microsoft® Power Automate連線：

1. 建立Microsoft® Azure Active Directory應用程式
1. 建立Microsoft® Power Automate Dataverse雲端設定。
1. 建立Microsoft® Power Automate Flow Service雲端設定
1. 發佈Microsoft® Power Automate Dataverse雲端設定。

### 建立Microsoft® Azure Active Directory應用程式 {#ms-power-automate-application}

1. 登入 [Azure入口網站](https://portal.azure.com/).
1. 選取 [!UICONTROL Azure Active Directory] 從左側導覽列中。
1. 在「預設目錄」頁面上，選取 [!UICONTROL 應用程式註冊] 從左側面板。
1. 在「應用程式註冊」頁面上，按一下「新註冊」 。
1. 在頁面上指定名稱、支援的帳戶型別和重新導向URI。 在「重新導向URI」中，指定下列專案，然後按一下「儲存」。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![註冊Azure Active Directory應用程式](assets/power-automate-application.png)

   >[!NOTE]
   >如有需要，您也可以從「驗證」頁面指定其他重新導向URI。
   > 對於支援的帳戶型別，請根據您的使用案例選取單一租使用者、多個租使用者或個人Microsoft帳戶


1. 在「驗證」頁面上，啟用下列選項，然後按一下「儲存」。


   * 存取權杖（用於隱含流程）
   * ID權杖（用於隱含和混合流量）

1. 在API許可權頁面上，按一下新增許可權。
1. 在Microsoft® API底下，選取「流量服務」，然後選取下列許可權。
   * Flows.Manage.All
   * Flows.Read.All

   按一下「新增許可權」以儲存許可權。
1. 在API許可權頁面上，按一下新增許可權。 選取我的組織使用的API並搜尋 `DataVerse`.
1. 啟用user_impersonation ，然後按一下新增許可權。
1. （可選）在「憑證和密碼」頁面上，按一下「新增使用者端密碼」。 在新增使用者端密碼畫面上，提供密碼到期的說明和時段，然後按一下新增。 產生秘密字串。
1. 記錄您組織的特定資訊 [動態環境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### 建立Microsoft® Power Automate Dataverse雲端設定 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms作者執行個體上，導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**.
1. 於 **[!UICONTROL 設定瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定 **[!UICONTROL 標題]** 針對設定，啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 並開啟您在上一步建立的設定容器。

   >[!NOTE]
   >
   >建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。
1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] AEM Forms中的設定。
1. 於 **[!UICONTROL 設定Microsoft® Power Automate的Dataverse服務]** 頁面，指定 **[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、 **[!UICONTROL 使用者端密碼]**， **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用的使用者端ID、使用者端密碼、OAuth URL和動態環境URL [Microsoft® Azure Active Directory應用程式](#ms-power-automate-application) 您在上一節中建立。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL

![使用Microsoft Power Automate應用程式UI中的「端點」選項來尋找OAuth URL](assets/endpoints.png)
使用Microsoft® Power Automate應用程式UI中的「端點」選項來尋找OAuth URL

1. 點選 **[!UICONTROL Connect]** . 如有要求，請登入您的Microsoft® Azure帳戶。 點選 **[!UICONTROL 儲存]**.

### 建立Microsoft® Power Automate Flow Service雲端設定。

1. 導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate流程服務]** 並開啟您在上一節中建立的設定容器。

   >[!NOTE]
   >
   >建立最適化表單時，請在 **[!UICONTROL 設定容器]** 欄位。
1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] AEM Forms中的設定。
1. 於 **[!UICONTROL 設定Microsoft® Power Automate的Dataverse]** 頁面，指定 **[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、 **[!UICONTROL 使用者端密碼]**， **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用使用者端ID、使用者端密碼、OAuth URL和Dynamics環境ID。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL。 開啟 [我的流程](https://us.flow.microsoft.com) 連結並點選「我的流程」，使用URL中列出的ID作為「動態環境ID」。
1. 點選 **[!UICONTROL Connect]**. 如有要求，請登入您的Microsoft® Azure帳戶。 點選 **[!UICONTROL 儲存]**.

### 發佈Microsoft® Power Automate Dataverse和Microsoft® Power Automate Flow Service雲端設定 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 導覽至 **[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 並開啟您之前建立的設定容器 [建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration) 區段。
1. 選取 `dataverse` 設定並點選 **[!UICONTROL 發佈]**.
1. 在發佈頁面上，選取 **[!UICONTROL 所有設定]** 並點選 **[!UICONTROL 發佈]**. 發佈Power Automate Dataverse和Power Automate Flow Service雲端設定。

您的Formsas a Cloud Service執行個體現在已與Microsoft® Power Automate連線。 您現在可以將Adaptive Forms資料傳送至Power Automate流程。

## 使用叫用Microsoft® Power Automate流程提交動作將資料傳送至Power Automate流程 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在您之後 [使用Microsoft® Power Automate連線您的Formsas a Cloud Service執行個體](#connect-forms-server-with-power-automate)，請執行下列動作來設定最適化表單，以在表單提交時傳送擷取的資料至Microsoft®流程。

1. 登入您的Author例項，選取您的Adaptive Form並按一下 **[!UICONTROL 屬性]**.
1. 在設定容器中，瀏覽並選取在區段中建立的容器 [建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)，然後點選 **[!UICONTROL 儲存並關閉]**.
1. 開啟最適化表單進行編輯，並導覽至 **[!UICONTROL 提交]** 最適化表單容器屬性的區段。
1. 在屬性容器中，針對 **[!UICONTROL 提交動作]** 選取 **[!UICONTROL 叫用Power Automate流程]** 選項。 可用的電源自動化流程清單隨即顯示 **[!UICONTROL Power Automate流程]** 選項。 選取所需的流程，Adaptive Forms資料在提交時就會提交給它。

![設定提交動作](assets/submission.png)

>[!NOTE]
>
> 在提交最適化表單之前，請確定 `When an HTTP Request is received` 使用以下JSON結構描述的觸發程式已新增到您的Power Automate流程。

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

