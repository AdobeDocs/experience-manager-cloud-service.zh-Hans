---
title: 预览资源
description: 瞭解如何在Dynamic Media中預覽資產。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 3928798d-352a-42a8-a544-7104fc9b3cf1
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 2%

---

# 预览资源{#previewing-assets}

當客戶在自己的網頁瀏覽器中檢視您上傳的數位資產時，您可以使用「預覽」來檢視該資產的外觀。 系統會使用指派給資產的預設內嵌式跨裝置檢視器進行預覽。

檢視器是各種設定或「預設集」的集合。 例如，檢視器會顯示大小、縮放行為、色彩配置、邊框和字型，以決定使用者在其電腦熒幕和行動裝置上檢視多媒體資產的方式。

除了對視訊、迴轉集和影像集使用專用的預覽功能外，您還可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/dynamic-media/image-presets.md)
* [套用檢視器預設集](/help/assets/dynamic-media/viewer-presets.md)

>[!NOTE]
>
>當您位於Adobe Experience Manager的網頁（網站）上時，無法預覽資產 **[!UICONTROL 編輯]** 模式。 請改為選取「 」，前往「預覽」模式 **[!UICONTROL 預覽]** 在頁面的右上角。

若要在使用者介面中啟用或停用檢視器預設集，請參閱 [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md).

**若要預覽資產：**

1. 從 **[!UICONTROL Experience Manager]**，位於 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]**，則 **[!UICONTROL 檔案]** 以存取資產。
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉式清單，選取 **[!UICONTROL 清單檢視]**.
1. （可選）使用 **[!UICONTROL 型別]** 欄，依您要預覽的型別排序資產。
1. 在 **[!UICONTROL 標題]** 欄中，選取您要預覽之資產的標題名稱（而非縮圖影像）。
1. 請根據您選取的資產型別，執行下列任一項作業：

   <table>
    <tbody>
      <tr>
      <td><strong>您選取的資產型別</strong><br /> </td>
      <td><strong>是否能夠預覽特定轉譯中的資產？</strong></td>
      <td><strong>是否可以在特定檢視器中預覽資產？</strong></td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在維度檢視器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取維度檢視器。</li>
      <li>若要將影像還原為原始的縮放地圖，請選取 <strong>重設</strong>.</li>
      <li>若要最大化顯示裝置上的檢視器，請選取 <strong>全熒幕</strong>.</li>
      </ul>
      <p><strong>導覽3D場景</strong></p>
      <ul>
      <li><p><strong>轉動您的3D攝影機</strong>  — 使檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按一下滑鼠左鍵+拖曳。</p> 觸控熒幕：按下+拖曳。</p></li>
      <li><p><strong>平移相機</strong>  — 向左、向右、向上和向下平移檢視。</p> 滑鼠：按一下滑鼠右鍵+拖曳。</p> 觸控熒幕：雙指按下+拖曳。</p></li>
      <li><p><strong>縮放相機</strong>  — 如果要在3D場景中移入和移出區域，請縮放相機。</p> 滑鼠：捲動滾輪。</p> 觸控熒幕：手指捏合。</p></li>
      <li><p><strong>重新將相機置中</strong>  — 使檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按兩下。</p> 觸控熒幕：點兩下。</li></ul></td>
      </tr>
      <tr>
      <td><p>图像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>若要預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>轉譯</strong> 從清單中，選取您要預覽的特定轉譯。</li>
        </ul> <p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>-</strong>圖示分別增加或減少選取影像的縮放。 若要將影像恢復為原始縮放，請選取 <strong>重設</strong>.<br>如果您在觸控熒幕上，請點兩下影像以按步驟放大。 當您達到最大縮放時，請再次點兩下影像以重設縮放狀態。 拖曳越過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒体</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>若要預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>轉譯</strong> 從清單中，選取您要預覽的特定轉譯。</li>
        </ul><p>選取較高解析度的視訊轉譯進行預覽，可能會導致視訊顯示遭到截斷。 原因是因為轉譯預覽會顯示客戶看到的確切解析度，所有這些都在用於預覽的內嵌檢視器的內容中進行。</p><p>在資產層級預覽最適化視訊集時，轉譯會分組到一個播放體驗中。 也就是說，最適化視訊的大小適合檢視，而且會在您的檢視裝置和連線速度環境下使用最佳解析度進行播放。<br /></p><p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>图像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示分別增加或減少選取影像的縮放。 若要將影像恢復為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請點兩下影像以按步驟放大。 當您達到最大縮放時，請再次點兩下影像以重設縮放狀態。 拖曳越過影像以平移。</p></td>
      </tr>
      <tr>
      <td>迴轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>- </strong>圖示分別增加或減少選取影像的縮放。 若要將影像恢復為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請點兩下影像以按步驟放大。 當您達到最大縮放時，請再次點兩下影像以重設縮放狀態。 拖曳越過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示分別增加或減少選取影像的縮放。 若要將影像恢復為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請點兩下影像以按步驟放大。 當您達到最大縮放時，請再次點兩下影像以重設縮放狀態。 拖曳越過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>傳送集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>若要預覽特定檢視器中的資產</strong>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取您要套用至資產的檢視器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360度影片<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>若要預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>轉譯</strong>，然後選取您要預覽的轉譯。</li>
        </ul> <p><strong>若要預覽特定檢視器中的資產</strong></p>
        <ul>
        <li>在頁面的左上角附近，選取圖示，下拉式清單隨即顯示。 選取 <strong>檢視者</strong>，然後選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示分別增加或減少選取影像的縮放。 若要將影像恢復為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請點兩下影像以按步驟放大。 當您達到最大縮放時，請再次點兩下影像以重設縮放狀態。 拖曳越過影像以平移。</p> </td>
      </tr>
    </tbody>
    </table>
