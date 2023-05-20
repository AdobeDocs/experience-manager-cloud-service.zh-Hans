---
title: 管理发布
description: 將資產發佈或取消發佈至Experience Manager Assets、Dynamic Media和Brand Portal
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 10%

---

# 在Experience Manager Assets中管理發布 {#manage-publication-in-aem}

作為 [!DNL Adobe Experience Manager Assets] 管理員，您可以將包含資產的資產和資料夾從作者執行個體發佈到 [!DNL Experience Manager Assets]， [!DNL Dynamic Media]、和 [!DNL Brand Portal]. 此外，您还可以安排在稍后的日期或时间执行资产或文件夹的发布工作流。發佈後，使用者可以存取資產，並進一步將資產發佈給其他使用者。 依預設，您可以將資產和資料夾發佈到 [!DNL Experience Manager Assets]. 不過，您可以設定 [!DNL Experience Manager Assets] 啟用發佈至 [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) 和 [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

您可以使用以下其中一種方式，在資產或資料夾層級發佈或取消發佈資產 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理發布]** 中可用的選項 [!DNL Experience Manager Assets] 介面。 如果您對中的原始資產或資料夾進行後續修改 [!DNL Experience Manager Assets]，在您從重新發佈前，變更不會反映在發佈執行個體中 [!DNL Experience Manager Assets]. 它可確保進行中的變更不會出現在發佈執行個體中。 發佈執行個體中只能使用管理員發佈的已核准變更。

* [使用快速發佈功能發佈資產](#quick-publish)
* [使用管理發布功能發佈資產](#manage-publication)
* [稍后发布资产](#publish-assets-later)
* [將資產發佈至Dynamic Media](#publish-assets-to-dynamic-media)
* [将资产发布到 Brand Portal](#publish-assets-to-brand-portal)
* [限制與秘訣](#limitations-and-tips)

## 使用快速發佈功能發佈資產 {#quick-publish}

快速發佈可讓您將內容立即發佈至選取的目的地。 從 [!DNL Experience Manager Assets] 主控台，導覽至上層資料夾，並選取您要發佈的所有資產或資料夾。 按一下 **[!UICONTROL 快速發佈]** 工具列中的選項，然後從您要發佈資產的下拉式清單中選取目標。

![快速发布](assets/quick-publish-to-aem.png)

## 使用管理發布功能發佈資產 {#manage-publication}

管理出版物可讓您向所選目的地發佈內容或從中取消發佈內容。 [新增內容](#add-content) 至整個DAM存放庫的發佈清單， [包含資料夾設定](#include-folder-settings) 以發佈所選資料夾的內容並套用篩選器，以及 [排程發佈](#publish-assets-later) 到更晚的日期或時間。

從 [!DNL Experience Manager Assets] 主控台，導覽至上層資料夾，並選取您要發佈的所有資產或資料夾。 按一下 **[!UICONTROL 管理發布]** 工具列中的選項。 如果您沒有 [!DNL Dynamic Media] 和 [!DNL Brand Portal] 設定於 [!DNL Experience Manager Assets] 例項，您只能將資產和資料夾發佈到 [!DNL Experience Manager Assets].

![管理发布](assets/manage-publication-aem.png)

下列選項適用於 [!UICONTROL 管理發布] 介面：

* [!UICONTROL 操作]
   * `Publish`：將資產和資料夾發佈到所選目的地
   * `Unpublish`：從目的地取消發佈資產和資料夾

* [!UICONTROL 目标]
   * `Publish`：將資產和資料夾發佈至 [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: 将资源发布到 [!DNL Dynamic Media]
   * `Brand Portal`：將資產和資料夾發佈至 [!DNL Brand Portal]

* [!UICONTROL 计划]
   * `Now`：立即發佈資產
   * `Later`：根據以下基準發佈資產： `Activation` 日期或

若要繼續，請按一下 **[!UICONTROL 下一個]**. 根據選取範圍， **[!UICONTROL 範圍]** 標籤會反映不同的選項。 的選項 **[!UICONTROL 新增內容]** 和 **[!UICONTROL 包含資料夾設定]** 僅適用於將資產和資料夾發佈到 [!DNL Experience Manager Assets] (`Destination: Publish`)。

![管理发布范围](assets/manage-publication-aem-scope.png)

### 添加内容 {#add-content}

發佈至 [!DNL Experience Manager Assets] 可讓您進一步新增更多內容（資產和資料夾）至發佈清單。 您可以跨dam存放庫將更多資產或資料夾新增到清單中。 按一下 **[!UICONTROL 新增內容]** 按鈕以新增更多內容。

您可以從資料夾中新增多個資產，或一次新增多個資料夾。 但您無法一次從多個資料夾新增資產。

![添加内容](assets/manage-publication-add-content.png)

### 包括文件夹设置 {#include-folder-settings}

依預設，將資料夾發佈至 [!DNL Experience Manager Assets] 會發佈所有資產、子資料夾及其參考。

若要篩選您要發佈的資料夾內容，請按一下 **[!UICONTROL 包含資料夾設定]**：

* `Include folder contents`

   * 啟用：會發佈所選資料夾的所有資產、子資料夾（包括子資料夾的所有資產）和參考。
   * 停用：只會發佈選取的資料夾（空白）和參考。 所選資料夾的資產未發佈。

* `Include folder contents` 和 `Include only immediate folder contents`

   如果同時選取這兩個選項，則會發佈所選資料夾、子資料夾（空白）和參照的所有資產。 子資料夾的資產未發佈。

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![包括文件夹设置](assets/manage-publication-include-folder-settings.png)

套用篩選器後，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 發佈]**. 按一下發佈按鈕時，會顯示確認訊息 `Resource(s) have been scheduled for publication` 出現。 而且選取的資產和（或）資料夾會根據排程器(`Now` 或 `Later`)。 登入您的發佈執行個體，驗證資產和（或）資料夾是否已成功發佈。

![发布到 AEM](assets/manage-publication-publish-aem.png)

在上圖中，您可以看到 **[!UICONTROL 發佈目標]** 屬性。 讓我們回顧您選擇發佈到的事實 [!DNL Experience Manager Assets] (`Destination: Publish`)。 那麼，它為何只顯示資料夾和資產發佈至 `AEM`，而其他兩個資產會發佈至兩者 `AEM` 和 `Dynamic Media`？

在這裡，您必須瞭解資料夾屬性的角色。 資料夾的 **[!UICONTROL Dynamic Media發佈模式]** 屬性在發佈中會扮演重要角色。 若要檢視資料夾的屬性，請選取資料夾並按一下 **[!UICONTROL 屬性]** （從工具列）。 如需資產，請參閱其上層資料夾的屬性。

下表說明發佈作業如何根據所定義的 **[!UICONTROL 目的地]** 和 **[!UICONTROL Dynamic Media發佈模式]**：

| [!UICONTROL 目标] | [!UICONTROL Dynamic Media 发布模式] | [!UICONTROL 发布目标] | 允許的內容 |
| --- | --- | --- | --- |
| 发布 | 选择性发布 | `AEM` | 資產和（或）資料夾 |
| 发布 | 即时 | `AEM` 和 `Dynamic Media` | 資產和（或）資料夾 |
| 发布 | 激活后 | `AEM` 和 `Dynamic Media` | 資產和（或）資料夾 |
| Dynamic Media | 选择性发布 | `Dynamic Media` | Assets |
| Dynamic Media | 即时 | `None` | 無法發佈資產 |
| Dynamic Media | 激活后 | `None` | 無法發佈資產 |

>[!NOTE]
>
>僅資產發佈至 [!DNL Dynamic Media].
>
>發佈資料夾至 [!DNL Dynamic Media] 不受支援。
>
>如果您選取資料夾(`Selective Publish`)並選擇 [!DNL Dynamic Media] 目的地， [!UICONTROL 發佈目標] 屬性反映 `None`.


現在讓我們變更 **[!UICONTROL 目的地]** 在上述使用案例中 **[!UICONTROL Dynamic Media]** 並驗證結果。 如此一來，只有 `Selective Publish` 資料夾已發佈至 [!DNL Dynamic Media]. 的資產 `Immediate` 和 `Upon Activation` 資料夾不會發佈，且會反映 `None`.

![发布到 Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>若 [!DNL Dynamic Media] 未在您的電腦上設定 [!DNL Experience Manager Assets] 執行個體和 **[!UICONTROL 目的地]** 是 **[!UICONTROL 發佈]**，則資產與資料夾一律會發佈至 `AEM`.
>
>發佈至 [!DNL Brand Portal] 與資料夾屬性無關。 所有資產、資料夾和集合皆可發佈至Brand Portal。 另請參閱 [將資產發佈至Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>如果您已自訂 [!DNL Manage Publication] 精靈，您的自訂功能可繼續搭配現有功能使用。
>
>不過，您可以移除現有的自訂專案，以使用新的 [!DNL Manager Publication] 功能。


## 稍后发布资产 {#publish-assets-later}

若要將資產發佈工作流程排程至之後的日期或時間：

1. 從 [!UICONTROL Experience Manager Assets] 主控台，導覽至上層資料夾，並選取您要排程發佈的所有資產或資料夾。
1. 按一下 **[!UICONTROL 管理發布]** 工具列中的選項。
1. 按一下 **[!UICONTROL 發佈]** 從 **[!UICONTROL 動作]**，然後選取 **[!UICONTROL 目的地]** 您要發佈內容的位置。
1. 在&#x200B;**[!UICONTROL 计划]**&#x200B;中选择&#x200B;**[!UICONTROL 稍后]**。
1. 選取 **[!UICONTROL 啟用日期]** 並指定日期和時間。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![管理發布工作流程](assets/manage-publication-workflow.png)

1. 在 **[!UICONTROL 範圍]** 標籤， **[!UICONTROL 新增內容]** （如有需要）。 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在 **[!UICONTROL 工作流程]** 索引標籤中，指定工作流程標題。 单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![工作流标题](assets/manage-publication-workflow-title.png)

   登入目的地執行個體以驗證已發佈的資產（取決於排程的日期或時間）。

## 將資產發佈至Dynamic Media {#publish-assets-to-dynamic-media}

僅資產發佈至 [!DNL Dynamic Media]. 不過，發佈行為會因資料夾屬性而異。 資料夾可以具有 **[!UICONTROL Dynamic Media發佈模式]** 設定為選擇性發佈，可以是下列任一專案：

* `Selective Publish`
* `Immediate`
* `Upon Activation`

的發佈程式 **[!UICONTROL 立即]** 和 **[!UICONTROL 啟動時]** 模式是一致的，但不同 **[!UICONTROL 選擇性發佈]**. 另請參閱 [在Dynamic Media中設定檔案夾層級的選擇性發佈](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). 在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [使用管理發布選擇性將資產發佈到Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [使用管理發布選擇性從Dynamic Media或Experience Manager取消發佈資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [使用快速發佈將資產發佈到Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [透過搜尋結果選擇性地發佈或取消發佈資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## 将资产发布到 Brand Portal {#publish-assets-to-brand-portal}

您可以將資產、資料夾和集合發佈至 [!DNL Experience Manager Assets Brand Portal] 執行個體。

* [将资产发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [将文件夹发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [将收藏集发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## 限制與秘訣 {#limitations-and-tips}

* 的選項 [!UICONTROL 管理發布] 僅適用於具有復寫許可權的使用者帳戶。
* 未發佈空白資料夾。
* 如果您發佈正在處理的資產，只會發佈原始內容。 缺少轉譯。 請等候處理完成，然後在處理完成時發佈或重新發佈資產。
* 取消發佈複雜資產時，請僅取消發佈資產。 請避免取消發佈引用，因為它們可能會被其他已發佈的資產引用。

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
