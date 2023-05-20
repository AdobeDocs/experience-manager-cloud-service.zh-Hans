---
title: 建立和使用主題
description: 您可以使用主題來風格化最適化表單，並使用核心元件提供視覺身分。 您可以在任何數量的Adaptive Forms中共用主題。
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 5%

---

# Adaptive Forms中的主題（核心元件） {#themes-for-af-using-core-components}

您可以建立並套用主題，以使用核心元件將最適化表單風格化。 主題包含元件和面板的樣式詳細資訊。 樣式包含背景顏色、狀態顏色、透明度、對齊方式及大小等屬性。 套用主題時，指定的樣式會反映在相應的元件上。 主題可獨立管理，不需參考最適化表單。

當您 [建立最適化表單](/help/forms/creating-adaptive-form.md) 使用核心元件時，現成可用的主題會顯示在 **樣式** 標籤。 依預設，僅 **畫布** 主題已推出。

>[!NOTE]
>
>最適化表單主題不應與 [最適化表單範本。](/help/forms/template-editor.md) 最適化表單主題僅包含最適化表單的樣式資訊。 最適化表單範本定義表單結構和初始內容，並包含主題以允許建立新的 [最適化表單。](/help/forms/creating-adaptive-form.md)

## 使用核心元件在Adaptive Forms中使用畫布主題 {#using-theme-in-adaptive-form}

將主題套用至最適化表單的步驟如下：

1. 登入您的AEM Forms作者執行個體。

1. 點選 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.

1. 按一下 **建立** > **最適化Forms**. 建立最適化表單的精靈隨即開啟。

1. 選取中的核心元件範本 **來源** 標籤。

   >[!NOTE]
   >
   > 使用核心元件建立最適化表單時，會在「樣式」標籤下看到畫布主題。 這是目前唯一可用的現成佈景主題。 但您可以透過設定前端管道將主題變更為喜歡並儲存以供未來使用。

1. 選取中的畫布主題 **樣式** 標籤。
1. 单击&#x200B;**创建**。

最適化表單主題用作最適化表單範本的一部分，以便在建立最適化表單時定義樣式。

## 自訂主題 {#customizing-theme}

若要自訂佈景主題，

* [在Cloud Manager中設定管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* 設定使用者 [投稿人角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* 您應擁有 [Git基本知識](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) 和Cloud ServiceGit存放庫。

若要自訂畫布主題：
1. [原地複製畫布主題](#1-download-canvas-theme-download-canvas-theme)
1. [瞭解主題的結構](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [變更package.json和package_lock.json中的名稱](#changename-packagelock-packagelockjson)
1. [建立 ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [啟動本機proxy伺服器](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [自訂主題](#customize-the-theme-customizing-theme)
1. [認可變更](#6-committing-the-changes-committing-the-changes)
1. [部署管道](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1.複製畫布主題 {#download-canvas-theme}

開啟命令提示字元並執行下列命令以複製畫布主題：

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> 「表單建立精靈」的「樣式」標籤會顯示與package.json檔案相同的主題名稱。

### 2.瞭解主題的結構 {#structure-of-canvas-theme}

最適化表單主題是包含CSS、JavaScript和靜態資源的套件，這些資源定義表單的樣式並符合最適化表單主題的結構。 最適化表單主題具有下列前端專案的典型結構：

* `src/components`：AEM核心元件專屬的JavaScript和CSS檔案
* `src/resources`：图标、徽标和字体等静态文件
* `src/site`：套用至整個AEM Sites頁面的JavaScript和CSS檔案
* `src/theme.ts`：JavaScript &amp; CSS主題的主要進入點
* `src\theme.scss`：套用至整個主題的JavaScript和CSS檔案

此 `src/components` 資料夾中有專用於所有AEM核心元件（例如按鈕、核取方塊、容器、頁尾等）的JavaScript和CSS檔案。 您可以編輯AEM元件專屬的CSS檔案，以設定按鈕或核取方塊的樣式。

![编辑主题](/help/forms/assets/theme_structure.png)

若要自訂主題，您可以啟動本機Proxy伺服器，根據實際AEM內容即時檢視主題自訂。

### 3.變更畫布主題的package.json和package_lock.json中的名稱 {#changename-packagelock-packagelockjson}

更新中畫布主題的名稱和版本 `package.json` 和 `package_lock.json` 檔案。

>[!NOTE]
>
> 名稱不應包含 `@aemforms` 標籤之間。 它應該是簡單文字，作為使用者提供的名稱。

![畫布主題圖片](/help/forms/assets/changename_canvastheme.png)

### 4.在主題資料夾中建立.env檔案 {#creating-env-file-theme-folder}

建立 `.env` 檔案並新增下列引數：

* **AEM url**
AEM_URL=https://[author-instance]

* **AEM網站名稱**
AEM_ADAPTIVE_FORM=Form_name

* **AEM Proxy連線埠**
AEM_PROXY_PORT=7000


![畫布布主題結構](/help/forms/assets/env-file-canvas-theme.png)

### 5.啟動本機proxy伺服器 {#starting-a-local-proxy-server}

1. 从命令行中，导航到本地计算机上主题的根。
1. 执行 `npm install`，npm 将检索依赖项并安装项目。
1. 执行 `npm run live`，代理服务器将启动。

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. 點選或按一下 **本機登入（僅限管理員工作）** 並使用AEM管理員提供給您的Proxy使用者認證登入。

   ![本地登录](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * 建立本機使用者以登入本機。 為主題設計者提供投稿人角色。
   > * 如果您將AEM URL指定為 `http://localhost:[port]/` 在 `.env` 畫布布主題的檔案，系統會將您直接重新導向至瀏覽器。


1. 登录后，将浏览器中的 URL 更改为指向 AEM 管理员提供给您的示例内容的路径。

   * 例如，如果提供的路径为 `/content/formname.html?wcmmode=disabled`，將URL變更為 `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![代理的示例内容](/help/forms/assets/sample_af.png)

導覽至最適化表單，檢視套用至最適化表單的畫布主題。

### 6.自訂主題 {#customize-theme}

1. 在编辑器中，打开文件 `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > 您可以編輯「 」，直接設定網站中所有最適化表單元件的樣式。 `site/_variables.scss` 檔案。

1. 編輯的變數 `font colour` 至 `red`.

   ![编辑主题](/help/forms/assets/edit_theme.png)

   **設定不同AEM元件的樣式**

   您可以在編輯器中變更最適化表單的CSS檔案，以設定其不同元件的樣式。 Canvas Theme資料夾中的每個Adaptive Form核心元件都有不同的CSS資料夾。

   ![核心元件](/help/forms/assets/theme-component.png)

   若要在主題編輯器中指定特定元件的樣式，您可以在主題資料夾中編輯CSS。 例如，如果您想要變更文字方塊欄位的邊框顏色，請在編輯器中開啟CSS檔案並變更其邊框顏色。

   ![編輯文字方塊CSS](/help/forms/assets/edit_color_textbox.png)

1. 當您儲存檔案時，Proxy伺服器會透過行來辨識變更 `[Browsersync] File event [change]`.

   ![代理浏览器同步](/help/forms/assets/browser_sync.png)

1. 切換回本機Proxy伺服器的瀏覽器時，變更會立即顯示。

   ![變更AF主題](/help/forms/assets/edit_theme_af.png)

主題設計人員會預覽本機Proxy伺服器中的變更，並根據不同AEM元件的需求自訂主題。

將變更提交至AEM Git存放庫之前，您需要存取 [Git存放庫資訊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7.確認變更 {#committing-the-changes}

變更主題並使用本機Proxy伺服器測試主題後，請將變更提交至AEM FormsCloud Service的Git存放庫。 它讓自訂主題可在您的FormsCloud Service環境中提供給Adaptive Forms作者使用。

在將變更提交至AEM FormsCloud Service的Git存放庫之前，您需要在本機電腦上複製存放庫。 複製存放庫：

1. 按一下「 」，建立新的主題存放庫 **[!UICONTROL 存放庫]** 選項。

   ![建立新的主題存放庫](/help/forms/assets/createrepo_canvastheme.png)

1. 按一下 **[!UICONTROL 新增存放庫]** 並指定 **存放庫名稱** 在 **新增存放庫** 對話方塊。 单击“**[!UICONTROL 保存]**”。

   ![新增畫布主題存放庫](/help/forms/assets/addcanvasthemerepo.png)

1. 按一下 **[!UICONTROL 複製存放庫URL]** 複製已建立存放庫的URL。

   ![畫布布主題URL](/help/forms/assets/copyurl_canvastheme.png)

1. 開啟命令提示字元並複製上述建立的雲端存放庫。

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. 使用類似於的命令將您正在編輯的主題存放庫檔案移動到雲端存放庫中
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
例如，使用此命令 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. 在雲端存放庫的目錄中，使用下列命令提交您移動到的主題檔案。

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. 自訂會推送至Git存放庫。

   ![已提交更改](/help/forms/assets/cmd_git_push.png)

您的自訂內容現在會安全地儲存在Git存放庫中。


### 8.執行前端管道 {#deploy-pipeline}

1. 建立前端管道以部署自訂主題。 瞭解 [如何設定一線管道以部署自訂主題](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. 執行已建立的前端管道，以部署下方的自訂主題資料夾 **[!UICONTROL 樣式]** 最適化表單建立精靈的索引標籤。

>[!NOTE]
>
>如果您在畫布主題資料夾中進行任何修改，未來需要重新執行上述管道。 因此，必須記住管道的名稱。

## 自訂主題的範例 {#example-to-customize-a-theme}

1. 登入您的AEM Forms作者執行個體。
1. 開啟使用核心元件建立的最適化表單。
1. 使用命令提示字元啟動本機Proxy伺服器，然後按一下 **本機登入（僅限管理員工作）**.
1. 登入後，系統會將您重新導向至瀏覽器，並檢視套用的主題。
1. 下載 [畫布主題](https://github.com/adobe/aem-forms-theme-canvas) 並解壓縮下載的zip資料夾。
1. 在偏好的編輯器中開啟解壓縮的zip資料夾。
1. 建立 `.env` 檔案主題資料夾並新增引數： **AEM URL**， **AEM_ADAPTIVE_FORM** 和 **AEM_PROXY_PORT**.
1. 開啟Canvas主題資料夾中文字方塊的CSS檔案，並變更其邊框顏色以顯示 `red` 顏色並儲存變更。
1. 再次重新開啟瀏覽器，您會看到變更立即反映在最適化表單中。
1. 移動複製存放庫中的畫布主題資料夾。
1. 提交變更並執行前端管道。

執行管道後，該主題便可在「樣式」標籤下使用。

## 最佳實務 {#best-practices}

* **避免使用其他主題的資產**

   編輯主題時，您可以瀏覽並新增其他主題中的資產（例如影像）。 例如，您正在編輯頁面的背景。 例如，當您選取 **[!UICONTROL 頁面]** ![編輯按鈕](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 新增]** > **[!UICONTROL 影像]**，您會看到對話方塊，可讓您瀏覽並新增其他主題中的影像。

   如果從其他主題新增資產，而另一個主題被移動或刪除，則您可能會遇到目前主題的問題。 建議您避免瀏覽和新增其他主題中的資產。

* **變更容器面板配置寬度**

   不建議變更容器面板配置寬度。 當您指定容器面板的寬度時，它會變成靜態，不會適應不同的顯示。

* **使用表單編輯器或主題編輯器來處理頁首和頁尾**

   如果要使用字型樣式、背景和透明度等樣式選項來設定頁首和頁尾的樣式，請使用主題編輯器。
如果您想在頁尾中提供標誌影像、公司名稱和版權資訊等資訊，請使用表單編輯器選項。
