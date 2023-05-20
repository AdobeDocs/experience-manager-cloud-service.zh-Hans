---
title: 為Adobe InDesign產生僅供放置的轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 869c1c34-6287-4d62-bb7a-aa4df580ac0e
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 7%

---

# 為Adobe InDesign產生僅供放置的轉譯 {#fpo-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/configure-fpo-renditions.html?lang=en) |
| AEM as a Cloud Service | 本文 |

將大型資產從Experience Manager放入Adobe InDesign檔案時，創意專業人士必須等待相當長的時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，使用者會被封鎖而無法使用InDesign。 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe功能可讓您從InDesign檔案開始暫時放置小型轉譯。 當需要最終輸出時（例如對於列印和發佈工作流程），原始的全解析度資產會在背景中取代暫時轉譯。 這種背景的非同步更新可加快設計流程以提高生產力，且不會阻礙創作流程。

Assets提供僅用於放置的轉譯(FPO)。 這些FPO轉譯檔案大小雖小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程順利進行，而不會出現任何中斷情形。

Experience Manageras a Cloud Service提供雲端原生資產處理功能，可產生FPO轉譯。 使用資產微服務來產生轉譯。 您可以設定新上傳資產及Experience Manager中現有資產的轉譯產生。

以下是產生FPO轉譯的步驟：

1. [建立處理設定檔](#create-processing-profile).

1. 設定Experience Manager以使用此設定檔 [處理新資產](#generate-renditions-of-new-assets).
1. 使用設定檔來 [處理現有資產](#generate-renditions-of-existing-assets).

## 建立處理設定檔 {#create-processing-profile}

若要產生FPO轉譯，請建立 **[!UICONTROL 處理設定檔]**. 設定檔使用雲端原生資產微服務進行處理。 如需指示，請參閱 [建立資產微服務的處理設定檔](asset-microservices-configure-and-use.md).

選取 **[!UICONTROL 建立FPO轉譯]** 以產生FPO轉譯。 或者，按一下 **[!UICONTROL 新增]** 將另一個轉譯設定新增至相同設定檔。

![create-processing-profile-fpo-renditions](assets/create-processing-profile-fpo-renditions.png)

## 產生新資產的轉譯 {#generate-renditions-of-new-assets}

若要產生新資產的FPO轉譯，請套用 **[!UICONTROL 處理設定檔]** 至資料夾屬性中的資料夾。 在資料夾的「屬性」頁面中，按一下 **[!UICONTROL 資產處理]** 索引標籤中，選取 **[!UICONTROL FPO設定檔]** as a **[!UICONTROL 處理設定檔]**，並儲存變更。 所有上傳至資料夾的新資產都會使用此設定檔進行處理。

![add-fpo-rendition](assets/add-fpo-rendition.png)


## 產生現有資產的轉譯 {#generate-renditions-of-existing-assets}

若要產生轉譯，請選取資產並依照下列步驟操作。

![fpo-existing-asset-reprocess](assets/fpo-existing-asset-reprocess.gif)


## 檢視FPO轉譯 {#view-fpo-renditions}

您可以在工作流程完成後檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄並選取 **[!UICONTROL 轉譯]**. 或者，使用鍵盤快速鍵 `Alt + 3` 開啟預覽時。

按一下 **[!UICONTROL FPO轉譯]** 以載入其預覽。 或者，您也可以用滑鼠右鍵按一下轉譯，並將其儲存至您的檔案系統。 檢查左側邊欄中是否有可用的轉譯。

![rendition_list](assets/list-renditions.png)

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
