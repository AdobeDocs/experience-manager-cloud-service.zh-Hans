---
title: 在發佈執行個體上執行內容轉移工具（舊版）
description: 在发布实例上运行内容转移工具
hide: true
hidefromtoc: true
exl-id: 0a699dc1-9977-4cf9-a1b0-7b503ea2fc69
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%

---

# 在發佈執行個體上執行內容轉移工具（舊版） {#run-content-transfer-tool-publish-instance}

## 简介 {#introduction}

內容轉移工具(CTT)在將內容從來源例項轉移到目標例項之前，不會執行任何型別的內容分析。 例如，將內容擷取至發佈環境時，CTT不會區分已發佈和未發佈的內容。 移轉集中指定的任何內容都將擷取到所選的目標執行個體。 使用者能將移轉集內嵌至「作者」執行個體或「發佈」執行個體（或兩者）。

>[!NOTE]
>建議在將內容移至生產執行個體時，在來源製作執行個體上安裝「內容轉移工具」，以將內容移至目標製作執行個體，同樣地，在來源發佈執行個體上安裝「內容轉移工具」，以將內容移至目標發佈執行個體。 另請參閱 [建議做法](#recommended-approach) 區段以取得更多詳細資訊。

## 推荐的方法 {#recommended-approach}

請遵循下列建議做法：

* 使用與Author例項上使用的相同版本「內容轉移工具」。

* 只需移轉單一發佈節點。 在開始提取之前，應將其從負載平衡器中移除。

* 建立移轉集時，請使用作者AEMas a Cloud Service環境的URL。

* 在擷取至發佈期間，發佈層級將不會縮小（不像作者）。

   >[!IMPORTANT]
   >為了防患於未然，請避免任何使用者啟動的寫入操作，例如：
   > * 從AEMas a Cloud Service作者發佈內容至該環境中的發佈
   > * 使用者在發佈執行個體之間同步

