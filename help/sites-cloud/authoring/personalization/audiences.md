---
title: 管理受众
description: 通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 的区段
exl-id: dff72c15-afcd-4b16-a711-e9ca3010e3ec
source-git-commit: f5f2c7c4dfacc113994c380e8caa37508030ee92
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 64%

---

# 管理受众{#managing-audiences}

通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 的区段：

* 新增對象 — Adobe Target對象或ContextHub區段。
* 管理對象。

ContextHub 中称为&#x200B;*区段*&#x200B;的受众是由特定标准定义的一类访客，可确定哪些人会看到目标活动。鎖定目標活動時，您可以直接在鎖定目標程式中選取對象，或在「對象」主控台中建立新對象。

在「對象」主控台中，對象會依品牌組織。

在“定位”模式下，可以使用受众来[创作目标内容](/help/sites-cloud/authoring/personalization/targeted-content.md)，您也可以在该模式下创建受众（但您需要在“受众”控制台中创建 Adobe Target 受众）。您在「鎖定目標」模式中建立的對象會出現在「對象」主控台中。

對象會以標籤顯示，說明所定義的對象型別：

* CH - ContextHub區段
* AT - Adobe Target對象

## 在受眾主控台中建立ContextHub區段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在「對象」主控台中或在鎖定過程中建立ContextHub區段。

要在“受众”控制台中创建 ContextHub 区段，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。单击或点按&#x200B;**受众**。
1. 点按或单击&#x200B;**创建 ContextHub 区段**。

   ![创建区段](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. 在&#x200B;**新 ContextHub 区段**&#x200B;对话框中，输入标题并调整提升，然后单击&#x200B;**创建**。新 ContextHub 区段随即会显示在受众列表中。

   >[!NOTE]
   >
   >您可以通过点按或单击&#x200B;**已修改**&#x200B;来对修改列表进行降序排序，以查看任何新创建的受众。

有关使用 ContextHub 创建区段的更多详细信息，请参阅“使用 ContextHub 配置分段”文档。<!--For further detail about creating segments using ContextHub, please see the [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) documentation.-->

## 使用Audience Console建立Adobe Target對象 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以使用受眾主控台，直接在AEM中建立Adobe Target受眾。

對象是由可決定要包含在目標活動中的規則所定義。 對象定義可包含多個規則，而每個規則均可包含多個引數。

當您使用多個規則時，這些規則會由布林運運算元AND組合，這表示任何可能的對象成員都必須符合要包含在活動中的所有已定義條件。 例如，如果您定義作業系統規則和瀏覽器規則，則活動中只會包含同時使用已定義作業系統和已定義瀏覽器的訪客。

>[!NOTE]
>
>如果“创建”菜 **单中未显示** “创建 **** 目标受众”，则您没有创建受众的必要权限。 您需要下面的写 `/etc/segmentation` 入权限才能创建受众。 默认情况下，组内容作者具有写权限。

要创建 Adobe Target 受众，请执行以下操作：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。单击或点按&#x200B;**受众**。

   ![导航到受众](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. 在“受众”控制台中，依次点按或单击&#x200B;**创建**&#x200B;和&#x200B;**创建目标受众**。

   ![创建目标受众](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. 在 **Adobe Target設定** 對話方塊中，選取目標組態，然後點選或按一下 **確定**.
1. 在「規則#1」區域中，點選或按一下屬性型別，然後在可用的欄位中輸入任何屬性資訊。 完成後，選取屬性右側的核取記號以儲存它。 另請參閱 [屬性及其選項](#attributes-and-their-options) 以取得所有屬性的相關資訊。
1. 单击 **添加规则** ，以添加其他规则。 根据需要输入任意数量的规则。 规则与布尔运算符AND相结合，这意味着受众必须满足每个规则的所有要求才能符合活动条件。
1. 点按或单击&#x200B;**下一步**。
1. 輸入對象名稱，然後點選或按一下 **儲存**.
1. 点按或单击&#x200B;**保存**。您的對象會列在「對象」清單中。

### 屬性及其選項 {#attributes-and-their-options}

您可以為下列每個屬性建立鎖定目標規則：

| **属性** | **描述** | **有关更多信息** |
|---|---|---|
| **移动设备** | 根据移动设备、设备类型、设备供应商、屏幕尺寸（按像素）等参数定位移动设备。 | 请参阅 Adobe Target 上的[移动设备文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html)。 |
| **自定义** | 自定义参数都是 mbox 参数。如果您将任何 mbox 参数传递给 mbox，或者使用 targetPageParams 函数，这些参数将会显示在此处以供在受众中使用。 | 请参阅 Adobe Target 上的[自定义参数文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html)。 |
| **操作系统** | 您可以定位使用特定操作系统的访客。 | 定位使用 Linux、Macintosh 或 Windows 的用户。 |
| **站点页面** | 定位特定页面的访客或具有特定 mbox 参数的访客。 | 请参阅 Adobe Target 上的[站点页面文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html)。 |
| **浏览器** | 您可以定位在访问您的页面时使用特定浏览器或特定浏览器选项的用户。 | 请参阅 Adobe Target 上的[浏览器选项文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html)。 |
| **访客配置文件** | 定位满足特定配置文件参数的访客。 | 请参阅 Adobe Target 上的[访客配置文件文档](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html)。 |
| **流量源** | 根据将访客转至您的站点的搜索引擎或登陆页来定位访客。 | 请参阅 Adobe Target 上的[流量源文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html)。 |

## 在對象主控台中修改對象 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能編輯在您編輯的相同AEM例項中建立的Adobe Target對象。 無法編輯在不同的AEM環境中建立的Target對象。

您可以从“受众”控制台中编辑任何 ContextHub 受众。您也可以编辑 Adobe Target 受众，但只能编辑在 AEM 中创建的受众：

1. 在“导航”控制台中，单击或点按&#x200B;**个性化**。单击或点按&#x200B;**受众**。
1. 点按或单击要编辑的 ContextHub 区段旁边的图标，然后点按或单击&#x200B;**编辑**。
1. 在区段编辑器中进行任何编辑。有关更多信息，请参阅 ContextHub 文档。<!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
