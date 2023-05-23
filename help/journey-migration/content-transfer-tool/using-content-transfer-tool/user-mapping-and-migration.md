---
title: 用户映射和主体迁移
description: 使用者對應和主體移轉概要
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 9%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射"
>abstract="「內容轉移工具」可協助您將使用者和群組從您現有的Adobe Experience Manager (AEM)系統移至AEMas a Cloud Service。 必须将现有用户映射到其 IMS ID，以免用户在云服务创作实例上重复。"

>[!NOTE]
>如需舊版的使用者對應工具，請參閱 [舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在轉變到Adobe Experience Manager (AEM) as a Cloud Service的歷程中，您必須將使用者和群組從您現有的AEM系統移動到AEMas a Cloud Service。 此工作由「內容轉移工具」完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。此程式需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 使用者設定檔資訊集中在AdobeIdentity Management系統(IMS)中，可在所有Adobe雲端應用程式中提供單一登入。 有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。由於此變更，現有使用者必須對應至其IMS ID，以避免在Cloud Service作者執行個體上出現重複使用者。 由於傳統AEM中的群組與IMS中的群組完全不同，群組不會對應，但在移轉完成後必須協調兩組群組。

## 使用者對應和移轉細節 {#user-mapping-detail}

內容轉移工具和Cloud Acceleration Manager會移轉與正在移轉的內容相關聯的任何使用者。 此對應會自動完成，並且可以在提取開始前透過切換控制是否完成。 使用者在開始擷取時，可覆寫切換的預設設定。

* 如果來源系統是Author例項，則預設情況下，執行對應的選擇為 _於_，因為這是建議的流程。
* 如果來源系統是發佈執行個體，則預設情況下，執行對應的選擇為 _關閉_，因為使用者通常不會移轉或用於發佈執行個體。

## 映射和迁移用户时的重要注意事项 {#important-considerations}


### 例外情況 {#exceptional-cases}

會記錄下列特定案例：

1. 如果使用者在電子郵件中沒有電子郵件地址 `profile/email` 的欄位 *jcr* 節點，相關使用者或群組可能已移轉，但未對應。 即使使用電子郵件地址作為使用者名稱登入，也會發生這種情況。

1. 如果使用者已停用，則會被視為與未停用時相同。 它會正常對應和移轉，並在雲端例項上維持停用。

1. 如果使用者存在於目標AEM Cloud Service執行個體上，且具有與來源AEM執行個體上使用者相同的使用者名稱(rep：principalName)，則不會移轉有問題的使用者。

1. 如果使用者未透過使用者對應進行對應，就無法在目標雲端系統上使用其IMS ID登入。 或者，如果他們的電子郵件地址與用來登入IMS的電子郵件地址不符，則他們也無法使用其IMS ID在目標雲端系統上登入。 他們也許可以使用傳統的AEM方法登入，但此方法通常不是所需或期望的。


## 其他考量 {#additional-considerations}

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 設定，則Cloud Service執行個體上已轉移的使用者會與整個現有存放庫一起刪除。 而且，會建立一個新存放庫，並擷取其中的內容。 此程式也會重設所有設定，包括目標Cloud Service執行個體的許可權，若管理員使用者已新增至 **管理員** 群組。 管理員使用者必須重新導覽至 **管理員** 群組以擷取CTT的存取權杖。
* 執行內容追加時，如果內容由於在上次轉移後未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移。 即使使用者與群組在此期間已變更，此規則仍為真。 原因是使用者和群組會隨著相關聯的內容一起移轉。
* 如果目標AEM Cloud Service執行個體中的某個使用者與來源AEM執行個體上的某個使用者具有不同的使用者名稱，但電子郵件地址相同，並且已啟用「使用者對應」，則記錄會記錄一則錯誤訊息。 此外，不會轉移來源AEM使用者，因為目標系統上只允許一位擁有指定電子郵件地址的使用者。

## 最終摘要與報告 {#final-report}

成功完成擷取和內嵌後，就會產生一份報表，顯示主要移轉詳細資訊。 另請參閱 [如何驗證主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 以取得詳細資訊。
