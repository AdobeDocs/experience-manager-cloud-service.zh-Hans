---
title: 在多个站点中使用目标内容
description: 如果您需要在多个站点间管理目标内容（例如活动、体验和优惠），则可以利用 AEM 中内置的目标内容多站点支持功能
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '2844'
ht-degree: 90%

---

# 在多个站点中使用目标内容 {#working-with-targeted-content-in-multisites}

如果您需要在多个站点间管理目标内容（例如活动、体验和优惠），则可以利用 AEM 中内置的目标内容多站点支持功能。

>[!NOTE]
>
>对目标内容提供多站点支持是一项高级功能。要使用此功能，您应该熟悉[多站点管理器](/help/sites-cloud/administering/msm/overview.md)以及 [Adobe Target 与 AEM 的集成](/help/sites-cloud/integrating/integrating-adobe-target.md)。

本文档将介绍以下内容：

* 简要概述 AEM 的目标内容多站点支持功能。
* 针对如何链接站点（在一个品牌中）介绍一些可能的使用情景。
* 提供一个示例来演练营销人员如何使用此功能。
* 详细说明如何实施目标内容的多站点支持功能。

要设置您的站点共享个性化内容的方式，您需要执行以下步骤：

1. [创建新区域](#creating-new-areas) 或 [创建区域作为live copy](#creating-new-areas). 区域包含可供页面的某个“区域”**&#x200B;使用的所有活动；也就是，页面上该组件所定位的位置。创建新区域会创建一个空区域，而创建区域作为Live Copy允许您跨站点结构继承内容。

1. [将您的站点或页面链接](#linking-sites-to-an-area)到区域。

您可以随时暂停或恢复继承。此外，如果您不希望暂停继承，则还可以创建本地体验。默认情况下，除非另有指定，否则所有页面都会使用主区域。

## 目标内容的多站点支持功能简介 {#introduction-to-multisite-support-for-targeted-content}

目标内容的多站点支持功能是开箱即用式功能，利用此功能，您可以将目标内容从通过 MSM 管理的主页面推送到本地 Live Copy，还可以管理对此类内容的全局修改和本地修改。

可以在&#x200B;**区域**&#x200B;中管理目标内容。区域可将在不同站点中使用的目标内容（活动、体验和优惠）分隔开来，并提供基于 MSM 的机制，以创建并管理目标内容的继承以及站点继承。这可让您无需在继承的站点中重新创建目标内容。

在某个区域中，只有链接到该区域的活动才会被推送到 Live Copy。默认情况下，主区域将处于选定状态。创建其他区域后，您可以将这些区域链接到站点或页面，以指示要推送的目标内容。

站点或 Live Copy 链接到的区域包含需要在该站点或 Live Copy 上提供的活动。默认情况下，站点或 Live Copy 会链接到主区域，但您也可以链接主区域之外的其他区域。

>[!NOTE]
>
>使用目标内容的多站点支持功能时，您应该注意以下两点：
>
>* 使用转出或 Live Copy 时，需要获得 MSM 许可。
>* 使用同步到 Adobe Target 的功能时，需要获得 Adobe Target 许可。
>

## 用例 {#use-cases}

您可以通过多种方式为目标内容设置多站点支持，具体取决于您的用例。 此部分从理论上介绍了如何在一个品牌中使用多种方式设置此功能。此外，在[示例：根据地域定位内容](#example-targeting-content-based-on-geography)中，您可以了解在多个站点中定位内容的实际应用。

目标内容打包在所谓的可定义站点或页面范围的区域中。这些区域在品牌级别进行定义。一个品牌可以包含多个区域。不同品牌的区域可以有所不同。一个品牌可能只包含主区域，从而在所有品牌之间共享；而另一个品牌可能包含多个品牌（例如，按地区划分的品牌）。因此，品牌之间不需要相互映射区域集。

例如，通过目标内容的多站点支持功能，您的&#x200B;**一个**&#x200B;品牌可以拥有两个（或更多）站点，这些站点具有以下某种内容：

* 完全&#x200B;*不同*&#x200B;的目标内容集 – 在一个站点中编辑目标内容不会影响其他站点。链接到不同区域的站点将读取并写入其自身的配置区域。例如：
   * 站点 A 链接到区域 X
   * 站点 B 链接到区域 Y
* *共享*&#x200B;的目标内容集 – 在一个站点中编辑会直接影响两个站点；通过让两个站点引用同一区域，可以实现此设置。链接到同一区域的站点共享该区域内的目标内容。例如：
   * 站点 A 链接到区域 X
   * 站点 B 也链接到区域 X
* 通过 MSM 从其他站点&#x200B;*继承*&#x200B;的不同目标内容集 – 内容可从主区域单向转出到 Live Copy。例如：
   * 站点 A 链接到区域 X
   * 站点 B 链接到区域 Y（该区域是区域 X 的 Live Copy）

您也可能有&#x200B;**多个**&#x200B;品牌在一个站点中使用，具体情况可能比此示例更加复杂。

![多站点示例](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>要从技术层面更详细地了解此功能，请参阅[如何构建目标内容的多站点管理](/help/sites-cloud/authoring/personalization/multisite-structure.md)。

## 示例：根据地域定位内容 {#example-targeting-content-based-on-geography}

使用目标内容的多站点支持功能，您可以共享、转出个性化内容，或将个性化内容单独分离出来。为了更好地说明如何使用此功能，请设想一个您想要控制如何根据地域转出目标内容的情景，如下所述：

同一个站点具有四个按地域划分的版本：

* **美国**&#x200B;站点位于左上角，它是主站点。在此示例中，该站点在“定位”模式下打开。
* 此站点的其他三个版本分别是&#x200B;**加拿大**、**英国**&#x200B;和&#x200B;**澳大利亚**，它们均为 Live Copy。这三个站点在“预览”模式下打开。

![多站点版本](/help/sites-cloud/authoring/assets/multisite-versions.png)

每个站点均共享地理区域中的个性化内容：

* 加拿大站点与美国站点共享主区域。
* 英国站点链接到欧洲区域，并从主区域继承内容。
* 澳大利亚站点由于位于南半球，季节性产品不适用，因此会有自己的个性化内容。

![多站点图表](/help/sites-cloud/authoring/assets/multisite-diagram.png)

对于北半球，我们创建了一个冬季活动，不过是针对男性受众创建的，北美的营销人员想要为冬季活动启用一幅新图像，因此他们在美国站点中更改了原有图像。

![美国版本](/help/sites-cloud/authoring/assets/multisite-us.png)

刷新选项卡后，我们无需执行任何操作，加拿大站点即会变更为新的图像。之所以会这样，是因为加拿大站点与美国站点共享主区域。而英国和澳大利亚站点中的图像不会发生改变。

![更改版本](/help/sites-cloud/authoring/assets/multisite-us-change.png)

营销人员希望将所做的这些更改转出到欧洲区域，因此通过点按或单击&#x200B;**转出页面**，[转出了 Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md)。刷新选项卡后，英国站点即会显示新的图像，因为欧洲区域从主区域继承内容（转出后继承）。

![转出 Live Copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

澳大利亚站点中的图像仍会保持不变，这是营销人员所期望的行为，因为澳大利亚此时是夏季，所以营销人员不希望变更此内容。澳大利亚站点之所以不会发生改变，是因为它没有与其他任何地区共享区域，它也不是其他地区的 Live Copy。营销人员绝不必担心澳大利亚站点的目标内容会被覆盖。

此外，对于英国站点，由于其区域是主区域的 Live Copy，因此您可以在活动名称旁边看到由绿色指示符标记的继承状态。如果活动是继承的，您将无法对其进行修改，除非暂停或分离 Live Copy。

您随时可以暂停继承或将继承完全分离出来。您还始终可以在不暂停继承的情况下，添加仅适用于该体验的本地体验。

>[!NOTE]
>
>要从技术层面更详细地了解此功能，请参阅[如何构建目标内容的多站点管理](/help/sites-cloud/authoring/personalization/multisite-structure.md)。

### 创建新区域与创建新区域作为 Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

在 AEM 中，您可以选择创建新区域，或创建新区域作为 Live Copy。创建新区域可将活动以及属于这些活动的任何内容（例如优惠、体验等）组合到一起。当您要创建完全不同的目标内容集或共享目标内容集时，您可以创建一个区域。

但是，如果您已经通过 MSM 在两个站点之间设置了继承，则您可能希望继承活动。在这种情况下，您将创建一个区域作为Live Copy，其中Y是X的Live Copy，因此也会继承所有活动。

>[!NOTE]
>
>当页面是链接到某个区域的 Live Copy，而该区域本身又是链接到页面 Blueprint 的区域的 Live Copy 时，默认转出会触发后续的目标内容转出。

例如，下图中有四个站点，其中两个站点共享主区域（以及该区域中的所有活动）；还有一个站点的区域是其他区域的 Live Copy，因此会在转出后共享活动；最后一个站点完全独立（因此其活动需要一个单独的区域）。

![图表详细信息](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

要在 AEM 中实现这种设置，您需要执行以下操作：

* 站点 A 链接到主区域 - 无需创建任何区域。在 AEM 中，默认情况下主区域将处于选定状态。站点 A 和 B 共享活动及其他内容。
* 站点 B 链接到主区域 - 无需创建任何区域。在 AEM 中，默认情况下主区域将处于选定状态。站点 A 和 B 共享活动及其他内容。
* 站点 C 链接到继承的区域，该区域是主区域的 Live Copy - 创建区域作为 Live Copy，即创建基于主区域的 Live Copy。转出后，继承的区域会从主区域继承活动。
* 站点 D 链接到其自身的独立区域 - 创建区域，即创建尚未定义任何活动的全新区域。独立区域不会与其他任何站点共享活动。

## 创建新区域 {#creating-new-areas}

区域可以跨活动和优惠使用。在任何一种内容（如活动）中创建区域后，您也可以将该区域用于另一种内容（如优惠）。

>[!NOTE]
>
>默认情况下，当您选择品牌名称时，名为“主区域”的默认区域会折叠 **直到** 创建另一个区域。 然后，在“活动”或“优惠”控制台中选 **择品牌****时，您会看到“区** 域 **** ”控制台。

要创建区域，请执行以下操作：

1. 导航到&#x200B;**个性化** > **活动**&#x200B;或&#x200B;**优惠**，然后导航到您的品牌。
1. 选择 **创建区域**.

   ![创建区域](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. 单击&#x200B;**区域**&#x200B;图标，然后单击&#x200B;**下一步**。
1. 在&#x200B;**标题**&#x200B;字段中，输入新区域的名称。（可选）选择标记。
1. 选择&#x200B;**创建**。

   AEM 随即会重定向到品牌窗口，其中列出了所有已创建的区域。如果除主区域之外还有其他区域，则您可以直接在“品牌”控制台中创建区域。

   ![创建](/help/sites-cloud/authoring/assets/multisite-create.png)

## 创建区域作为 Live Copy {#creating-areas-as-live-copies}

您可以创建区域作为 Live Copy，以便跨站点结构继承目标内容。

要创建区域作为 Live Copy，请执行以下操作：

1. 导航到&#x200B;**个性化** > **活动**&#x200B;或&#x200B;**优惠**，然后导航到您的品牌。
1. 选择 **创建区域作为Live Copy**.

   ![创建区域作为 Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. 选择要为其创建 Live Copy 的区域，然后单击&#x200B;**下一步**。

   ![创建 Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. 在“名 **称** ”字段中，输入Live copy的名称。默认情况下，包含子页面；通过选中“排除子页 **面”复选框** ，排除它们。

   ![创建 Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. 在&#x200B;**转出配置**&#x200B;下拉菜单中，选择相应的配置。

   有关每个选项的说明，请参阅[安装的转出配置](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations)。

   有关 Live Copy 的更多信息，请参阅[创建和同步 Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md)。

   >[!NOTE]
   >
   >如果将页面转出到 Live Copy，并且为 Blueprint 页面配置的区域同时也是为页面 Live Copy 配置的区域的 Blueprint，则 LiveAction **personalizationContentRollout** 会触发同步的 subRollout，它是&#x200B;**标准转出配置**&#x200B;的一部分。

1. 选择&#x200B;**创建**。

   AEM 随即会重定向到品牌窗口，其中列出了所有已创建的区域。如果除主区域之外还有其他区域，则您可以直接从品牌窗口中创建区域。

   ![创建区域](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## 将站点链接到区域 {#linking-sites-to-an-area}

您可以将区域链接到页面或站点。所有子页面都会继承区域，除非子页面上的映射覆盖了这些页面。不过，通常而言，您需要在站点级别建立链接。

建立链接后，只能使用选定区域中的活动、体验和优惠。这样可以防止意外搞混单独管理的内容。如果没有配置任何其他区域，则会使用每个品牌的主区域。

>[!NOTE]
>
>引用了同一区域的页面或站点使用的是&#x200B;*相同*&#x200B;的共享活动、体验和优惠集。编辑由多个站点共享的活动、体验或优惠会影响所有站点。

要将站点链接到区域，请执行以下操作：

1. 导航到要将其链接到区域的站点（或页面）。
1. 选择站点或页面，然后选择 **查看属性**.
1. 选择 **个性化** 选项卡。
1. 在&#x200B;**品牌**&#x200B;菜单中，选择要将您的区域链接到的品牌。选择品牌后，可用区域会显示在&#x200B;**区域引用**&#x200B;菜单中。

   ![链接站点](/help/sites-cloud/authoring/assets/multisite-english.png)

1. 从中选择区域 **区域引用** 下拉菜单并选择 **保存**.

   ![区域引用](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## 分离 Live Copy 或暂停目标内容的继承 {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

您可能想要暂停或分离目标内容的继承。需按活动暂停或分离 Live Copy。例如，您可能想要修改活动中的体验，但是如果该活动仍然链接到继承的副本，便无法修改体验或该活动的任何属性。

暂停 Live Copy 会暂时中断继承，但之后可以恢复继承。而分离 Live Copy 则会永久中断继承。

要暂停或分离目标内容的继承，需要先在活动中恢复继承。如果页面或站点链接到的区域是 Live Copy，则可以查看活动的继承状态。

从其他站点继承的活动的名称旁边显示有绿色标记。暂停的继承标记为红色，本地创建的活动没有图标。

>[!NOTE]
>
>* 您只能在活动中暂停或分离 Live Copy。
>* 要扩展继承的活动，无需暂停或分离 Live Copy。您始终可以为该活动创建&#x200B;**新的**&#x200B;本地体验和优惠。如果您想要修改现有活动，则需要暂停继承。
>

### 暂停继承 {#suspending-inheritance}

要在活动中暂停或分离目标内容的继承，请执行以下操作：

1. 导航到要在其中分离或暂停继承的页面，然后选择 **定位** 模式下拉菜单中。
1. 如果您的页面链接到的区域是 Live Copy，则可以看到继承状态。选择&#x200B;**开始定位**。
1. 要在活动中暂停继承，请执行以下操作之一：

   1. 选择活动的某个元素，例如受众。AEM 随即会自动显示“暂停 Live Copy”确认对话框。（在整个定位过程中，您都可以通过点按或单击任何元素来暂停 Live Copy。）
   1. 从工具栏的下拉菜单中选择&#x200B;**暂停 Live Copy**。

   ![暂停 Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. 选择 **暂停** 以暂停活动。 暂停继承的活动会标记为红色。

   ![暂停的 Live Copy](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### 中断继承 {#breaking-inheritance}

在活动中，要中断目标内容的继承，请执行以下操作：

1. 导航到要将Live Copy从母版分离的页面，然后选择 **定位** 模式下拉菜单中。
1. 如果您的页面链接到的区域是 Live Copy，则可以看到继承状态。选择&#x200B;**开始定位**。
1. 从工 **具栏的下拉菜单中选择** “分离Live Copy”。AEM会确认您是否要分离Live Copy。
1. 选择 **分离** 以从活动分离live copy。 分离之后，与继承有关的下拉菜单将不再显示。此时活动会变成本地活动。

   ![当地活动](/help/sites-cloud/authoring/assets/multisite-winter.png)

## 恢复目标内容的继承 {#restoring-inheritance-of-targeted-content}

如果在活动中暂停了目标内容的继承，则可以随时恢复继承。但是，如果分离了 Live Copy，则无法恢复继承。

要在活动中恢复目标内容的继承，请执行以下操作：

1. 导航到要在其中恢复继承的页面，然后选择 **定位** 模式下拉菜单中。
1. 选择&#x200B;**开始定位**。
1. 从工具栏的下拉菜单中选择&#x200B;**恢复 Live Copy**。

   ![恢复 Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. 选择 **继续** 以确认您要恢复Live Copy继承。 如果恢复继承，对当前活动所做的任何修改都会丢失。

## 删除区域 {#deleting-areas}

删除区域时，也会删除该区域中的所有活动。在您删除区域之前，AEM 会向您发出警告。如果您删除了站点链接到的区域，则此品牌的映射会自动重新映射到主区域。

要删除区域，请执行以下操作：

1. 导航到&#x200B;**个性化** > **活动**&#x200B;或&#x200B;**优惠**，然后导航到您的品牌。
1. 选择要删除的区域旁边的图标。
1. 选择 **删除** 并确认要删除该区域。
