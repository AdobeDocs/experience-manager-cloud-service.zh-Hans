---
title: 如何設定Azure儲存體？
description: 瞭解如何將表單與Azure儲存伺服器整合。
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 10284b1ac6fbad2e7f6231603c3dd60b6e404299
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# 配置[!DNL Azure]存储 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md) 提供 [!DNL Azure] 整合表單的儲存設定 [!DNL Azure] 儲存服務。 表單資料模型可用來建立最適化Forms，並與互動 [!DNL Azure] 伺服器以啟用業務工作流程。 例如：

* 將資料寫入 [!DNL Azure] 於最適化表單提交時。
* 將資料寫入 [!DNL Azure] 透過「表單資料模型」中定義的自訂實體傳遞，反之亦然。
* 查詢 [!DNL Azure] 伺服器以取得資料並預先填入Adaptive Forms。
* 讀取資料來源 [!DNL Azure] 伺服器。

## 建立 [!DNL Azure] 儲存設定 {#create-azure-storage-configuration}

執行這些步驟之前，請確定您已 [!DNL Azure] 存放裝置帳戶與存取金鑰，用於授權存取 [!DNL Azure] 儲存體帳戶。

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure儲存體]**.
1. 選取資料夾以建立設定並點選 **[!UICONTROL 建立]**.
1. 在中指定設定的標題 **[!UICONTROL 標題]** 欄位。
1. 指定 [!DNL Azure] 中的儲存體帳戶 **[!UICONTROL Azure儲存體帳戶]** 欄位。
1. 指定用來存取Azure儲存體帳戶的金鑰 **[!UICONTROL Azure存取金鑰]** 欄位並點選 **[!UICONTROL 儲存]**.

## 创建表单数据模型 {#create-azure-form-data-model}

建立之後 [!DNL Azure] 儲存設定，您可以 [建立表單資料模型](create-form-data-models.md). 指定包含 [!DNL Azure] 中的設定 **[!UICONTROL 資料來源組態]** 建立表單資料模型時的欄位。 然後，您可以從存在於指定資料夾名稱中的設定清單中選取設定。

### 新增 [!DNL Azure] 表單資料模型的服務 {#add-azure-services}

建立表單資料模型和資料模型物件後，您可以新增 [!DNL Azure] 表單資料模型的服務。

若要新增 [!DNL Azure] 服務：

1. 在「編輯」模式中，從 **[!UICONTROL 服務]** 區段並點選 **[!UICONTROL 新增選取專案]**. 選取的服務會顯示在 **[!UICONTROL 服務]** 表單資料模型的索引標籤。

   ![新增選取的服務](assets/select-services.png)

1. 在 **[!UICONTROL 服務]** 索引標籤中，選取服務並 **[!UICONTROL 編輯屬性]**. 根據服務，定義服務的輸入或輸出模型物件。

1. 點選 **[!UICONTROL 儲存]** 以儲存表單資料模型。

   下表說明可用的 [!DNL Azure] 服務：

   <table>
    <tbody>
     <tr>
      <th><strong>服务名称</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>從Azure取得Blob</td>
      <td>使用ID或名稱擷取在Azure儲存空間中儲存為Blob的資料</td>
     </tr>
     <tr>
      <td>從Azure取得具有二進位檔URL的Blob</td>
      <td>使用ID或名稱，針對Azure儲存體中的二進位檔案，擷取以URL儲存為Blob的資料</td>
     </tr>
     <tr>
      <td>在Azure中儲存Blob</td>
      <td>使用Blob ID在Azure儲存空間中儲存資料</td>
     </tr>
     <tr>
      <td>在Azure中更新Blob</td>
      <td>使用Blob ID更新Azure儲存體中的資料</td>
     </tr>
     <tr>
      <td>從Azure擷取Blob ID清單</td>
      <td>根據輸入請求中定義的數字從Azure擷取Blob ID清單。</td>
     </tr>
     <tr>
      <td>從Azure擷取Blob的SAS URL</td>
      <td>根據輸入請求中的Blob ID從Azure擷取Blob的SAS URL。</td>
     </tr>
     <tr>
      <td>從Azure刪除Blob</td>
      <td>使用Blob ID從Azure儲存體刪除資料</td>
     </tr>
    </tbody>
   </table>

### 將資料模型物件屬性定義為搜尋索引鍵 {#define-data-model-object-as-metadata}

若要將資料模型物件屬性定義為搜尋索引鍵，請執行下列動作：

1. 在 **[!UICONTROL 模型]** 索引標籤中，選取資料模型物件屬性並點選 **[!UICONTROL 編輯屬性]**.
1. 切換 **[!UICONTROL 搜尋索引鍵]** 切換選項至「開啟」狀態。 此選項僅適用於主要資料型別。
1. 點選 **[!UICONTROL 完成]** 然後點選 **[!UICONTROL 儲存]** 以儲存表單資料模型。

將資料模型物件屬性定義為搜尋索引鍵後，雜湊值會儲存在Azure索引標籤中，而Base64編碼值會儲存在Azure中繼資料中。

>[!NOTE]
>
>每個Azure實體僅允許10個搜尋索引鍵，因為Azure僅允許每個Blob有10個標籤，而且標籤為搜尋索引鍵的屬性值會在雜湊後儲存在Azure索引標籤中。
