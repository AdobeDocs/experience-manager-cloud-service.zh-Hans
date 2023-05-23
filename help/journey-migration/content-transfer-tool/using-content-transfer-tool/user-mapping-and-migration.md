---
title: 用户映射和主体迁移
description: 使用者對應和主體移轉概要
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 25bfcd521e9bbc54bff3b87d17cdeb0f99a68511
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 21%

---

# 用户映射和主体迁移 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射"
>abstract="内容传输工具可帮助您将用户和组从现有 AEM 系统移动到 AEM as a Cloud Service。必须将现有用户映射到其 IMS ID，以免用户在云服务创作实例上重复。"

>[!NOTE]
>如需舊版的使用者對應工具，請參閱 [舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 简介 {#introduction}

在过渡到 Adobe Experience Manager (AEM) as a Cloud Service 的历程中，您需要将用户和组从现有 AEM 系统移至 AEM as a Cloud Service。此操作由内容传输工具完成。

对 AEM as a Cloud Service 的一项重大更改是完全集成使用 Adobe ID 来访问创作层。这需要使用 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 来管理用户和用户组。用户配置文件信息集中存储在 Adobe Identity Management System (IMS) 中，该系统在所有 Adobe 云应用程序之间提供单点登录。有关更多详细信息，请参阅 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management)。由於此變更，現有使用者需要對映至其IMS ID，以避免Cloud Service作者執行個體上的重複使用者。 由於傳統AEM中的群組與IMS中的群組完全不同，群組不會對應，但在移轉完成後必須協調兩組群組。

## 使用者對應和移轉細節 {#user-mapping-detail}

內容轉移工具和Cloud Acceleration Manager將會移轉與正在移轉的內容相關聯的任何使用者。 此對應會自動完成，並且可以在提取開始前透過切換控制是否完成。 使用者在開始擷取時，可覆寫切換的預設設定。

* 如果來源系統是Author例項，則預設情況下，執行對應的選擇為 _於_，因為這是建議的程式。
* 如果來源系統是發佈執行個體，則預設情況下，執行對應的選擇為 _關閉_，因為使用者通常不會移轉或用於發佈執行個體。

## 映射和迁移用户时的重要注意事项 {#important-considerations}


### 例外情況 {#exceptional-cases}

會記錄下列特定案例：

1. 如果使用者在電子郵件中沒有電子郵件地址 `profile/email` 的欄位 *jcr* 節點可能移轉有問題的使用者或群組，但不會進行對應。 即使電子郵件地址用作登入使用者名稱，也是如此。

1. 如果使用者已停用，則會被視為與未停用時相同。 它會正常對應和移轉，並在雲端例項上維持停用。

1. 如果使用者存在於目標AEM Cloud Service執行個體上，且具有與來源AEM執行個體上使用者相同的使用者名稱(rep：principalName)，則不會移轉有問題的使用者或群組。

1. 如果移轉使用者時未先透過使用者對應進行對應，或其電子郵件地址與用來登入IMS的電子郵件地址不符，則他們將無法在目標雲端系統上使用IMS ID登入。 他們或許可以使用傳統AEM方法登入，但請記住，這通常不是所需或期望的。


## 其他考量 {#additional-considerations}

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 設定，Cloud Service執行個體上已轉移的使用者將與整個現有存放庫一起刪除，並將建立新存放庫以將內容擷取到。 這也會重設所有設定，包括目標Cloud Service執行個體的許可權，新增至的管理員使用者則為true **管理員** 群組。 管理員使用者必須重新新增至 **管理員** 群組以擷取CTT的存取權杖。
* 執行內容追加時，如果內容由於自上次轉移以來未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移，即使使用者和群組在此期間已變更。 這是因為使用者和群組會隨著相關聯的內容一起移轉。
* 如果目標AEM Cloud Service執行個體中的使用者與來源AEM執行個體上的其中一位使用者擁有不同的使用者名稱，但電子郵件地址相同，並且已啟用「使用者對應」，則會在記錄中寫入錯誤訊息，且不會傳輸來源AEM使用者，因為目標系統上只允許一位具有指定電子郵件地址的使用者。

## 最終摘要與報告 {#final-report}

成功完成擷取和內嵌後，就會產生一份報表，顯示主要移轉詳細資訊。 另請參閱 [如何驗證主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 以取得詳細資訊。
