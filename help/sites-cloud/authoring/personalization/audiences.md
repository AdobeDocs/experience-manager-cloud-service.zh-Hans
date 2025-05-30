---
title: 管理受众
description: 通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 的区段
exl-id: dff72c15-afcd-4b16-a711-e9ca3010e3ec
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 86%

---

# 管理受众{#managing-audiences}

通过“受众”控制台，您可以创建、组织和管理 Adobe Target 帐户的受众，或管理 ContextHub 的区段：

* 添加受众 - Adobe Target 受众或 ContextHub 区段。
* 管理受众。

ContextHub 中称为&#x200B;*区段*&#x200B;的受众是由特定标准定义的一类访客，可确定哪些人会看到目标活动。定位活动时，您可以直接在“定位”过程中选择受众，也可以在“受众”控制台中创建新受众。

在“受众”控制台中，各受众按品牌进行组织。

在“定位”模式下，可以使用受众来[创作目标内容](/help/sites-cloud/authoring/personalization/targeted-content.md)，您也可以在该模式下创建受众（但您需要在“受众”控制台中创建 Adobe Target 受众）。在“定位”模式下创建的受众会显示在“受众”控制台中。

受众显示有相应的标签，用于说明定义的受众类型：

* CH - ContextHub 区段
* AT - Adobe Target 受众

## 在“受众”控制台中创建 ContextHub 区段 {#creating-a-contexthub-segment-in-the-audiences-console}

您可以在“受众”控制台中或在定位过程中创建 ContextHub 区段。

要在“受众”控制台中创建 ContextHub 区段，请执行以下操作：

1. 在导航控制台中，选择&#x200B;**Personalization**。 选择&#x200B;**受众**。
1. 选择&#x200B;**创建ContextHub区段**。

   ![创建区段](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. 在&#x200B;**新 ContextHub 区段**&#x200B;对话框中，输入标题并调整提升，然后单击&#x200B;**创建**。新 ContextHub 区段随即会显示在受众列表中。

   >[!NOTE]
   >
   >您可以通过点按或单击&#x200B;**已修改**&#x200B;来对修改列表进行排序，按降序排序，以查看任何创建的受众。

有关使用 ContextHub 创建区段的更多详细信息，请参阅“使用 ContextHub 配置分段”文档。<!--For further detail about creating segments using ContextHub, see [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md).-->

## 使用“受众”控制台创建 Adobe Target 受众 {#creating-an-adobe-target-audience-using-the-audience-console}

您可以直接在 AEM 中使用“受众”控制台创建 Adobe Target 受众。

受众由确定目标活动中包含哪些人的规则进行定义。受众定义可以包含多个规则，每个规则可以包含多个参数。

使用多个规则时，这些规则会通过布尔运算符 AND 进行组合，这意味着任何潜在的受众成员必须满足所有定义的条件才能包含在活动中。例如，如果您定义了操作系统规则和浏览器规则，则只有同时使用定义的操作系统和定义的浏览器的访客才会包含在活动中。

>[!NOTE]
>
>如果“创建”菜 **单中未显示** “创建 **&#x200B;**&#x200B;目标受众”，则您没有创建受众的必要权限。您需要下面的写 `/etc/segmentation` 入权限才能创建受众。默认情况下，组内容作者具有写权限。

要创建 Adobe Target 受众，请执行以下操作：

1. 在导航控制台中，选择&#x200B;**Personalization**。 选择&#x200B;**受众**。

   ![导航到受众](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. 在“受众”控制台中，选择&#x200B;**创建**，然后选择&#x200B;**创建目标受众**。

   ![创建目标受众](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. 在&#x200B;**Adobe Target配置**&#x200B;对话框中，选择Target配置并选择&#x200B;**确定**。
1. 在“规则#1”区域，选择属性类型，并在可用的字段中输入任何属性信息。 完成后，选中该属性右侧的复选标记以保存该属性。有关所有属性的信息，请参阅[属性及其选项](#attributes-and-their-options)。
1. 单击 **添加规则** ，以添加其他规则。根据需要输入任意数量的规则。规则与布尔运算符AND相结合，这意味着受众必须满足每个规则的所有要求才能符合活动条件。
1. 选择&#x200B;**下一步**。
1. 输入受众的名称，然后选择&#x200B;**保存**。
1. 选择&#x200B;**保存**。受众随即会列在“受众”列表中。

### 属性及其选项 {#attributes-and-their-options}

您可以为以下每个属性创建定位规则。

| **属性** | **描述** | **有关更多信息** |
|---|---|---|
| **移动设备** | 根据移动设备、设备类型、设备供应商、屏幕尺寸（按像素）等参数定位移动设备。 | 请参阅 Adobe Target 上的[移动设备文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=zh-Hans)。 |
| **自定义** | 自定义参数都是 mbox 参数。如果您将任何 mbox 参数传递给 mbox，或者使用 targetPageParams 函数，这些参数将会显示在此处以供在受众中使用。 | 请参阅 Adobe Target 上的[自定义参数文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=zh-Hans)。 |
| **操作系统** | 您可以定位使用特定操作系统的访客。 | 定位使用 Linux、Macintosh 或 Windows 的用户。 |
| **站点页面** | 定位特定页面的访客或具有特定 mbox 参数的访客。 | 请参阅 Adobe Target 上的[站点页面文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=zh-Hans)。 |
| **浏览器** | 您可以定位在访问您的页面时使用特定浏览器或特定浏览器选项的用户。 | 请参阅 Adobe Target 上的[浏览器选项文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=zh-Hans)。 |
| **访客配置文件** | 定位满足特定配置文件参数的访客。 | 请参阅 Adobe Target 上的[访客配置文件文档](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=zh-Hans)。 |
| **流量源** | 根据将访客转至您的站点的搜索引擎或登陆页来定位访客。 | 请参阅 Adobe Target 上的[流量源文档](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=zh-Hans)。 |

## 在“受众”控制台中修改受众 {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>您只能编辑在当前所编辑的相同 AEM 实例中创建的 Adobe Target 受众。无法编辑在不同的 AEM 环境中创建的目标受众。

您可以从“受众”控制台中编辑任何 ContextHub 受众。您也可以编辑 Adobe Target 受众，但只能编辑在 AEM 中创建的受众：

1. 在导航控制台中，选择&#x200B;**Personalization**。 选择&#x200B;**受众**。
1. 选择要编辑的ContextHub区段旁边的图标，然后选择&#x200B;**编辑**。
1. 在区段编辑器中进行任何编辑。有关更多信息，请参阅 ContextHub 文档。<!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
