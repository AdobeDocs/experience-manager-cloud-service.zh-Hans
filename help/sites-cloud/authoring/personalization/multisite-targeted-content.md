---
title: 在多个站点中使用目标内容
description: 如果您需要在多个站点间管理目标内容（例如活动、体验和选件），则可以利用 AEM 中内置的目标内容多站点支持功能
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 在多个站点中使用目标内容 {#working-with-targeted-content-in-multisites}

如果您需要在多个站点间管理目标内容（例如活动、体验和选件），则可以利用 AEM 中内置的目标内容多站点支持功能。

>[!NOTE]
>
>对目标内容提供多站点支持是一项高级功能。要使用此功能，您应熟悉多站点管理器以及Adobe Target与AEM的集成。
<!--
>Working with Multisite support for targeted content is an advanced feature. To use this feature, you should be familiar with [Multi Site Manager](/help/sites-administering/msm.md) and the [Adobe Target integration](/help/sites-administering/target.md) with AEM.
-->

本文档将介绍以下内容：

* 简要概述 AEM 的目标内容多站点支持功能。
* 针对如何链接站点（在一个品牌中）介绍一些可能的使用情景。
* 提供一个示例来演练营销人员如何使用此功能。
* 详细说明如何实施目标内容的多站点支持功能。

要设置您的站点共享个性化内容的方式，您需要执行以下步骤：

1. [创建新区域](#creating-new-areas)，或[创建新区域作为 Live Copy](#creating-new-areas)。区域包含可供页面的某个“区域”**&#x200B;使用的所有活动；也就是，页面上该组件所定位的位置。如果创建新区域，则会创建一个空的区域；然而，如果创建新区域作为 Live Copy，则您可以跨站点结构继承目标内容。

1. [将您的站点或页面链接](#linking-sites-to-an-area)到区域。

您可以随时暂停或恢复继承。此外，如果您不希望暂停继承，则还可以创建本地体验。默认情况下，除非另有指定，否则所有页面都会使用主区域。

## 目标内容的多站点支持功能简介 {#introduction-to-multisite-support-for-targeted-content}

目标内容的多站点支持功能是开箱即用式功能，利用此功能，您可以将目标内容从通过 MSM 管理的主页面推送到本地 Live Copy，还可以管理对此类内容的全局修改和本地修改。

You manage this in an **Area**. 区域可将在不同站点中使用的目标内容（活动、体验和选件）分隔开来，并提供基于 MSM 的机制，以创建并管理目标内容的继承以及站点继承。如此一来，您就不必按照 6.2 之前的 AEM 版本中的要求，在继承的站点中重新创建目标内容。

在某个区域中，只有链接到该区域的活动才会被推送到 Live Copy。默认情况下，主区域将处于选定状态。创建其他区域后，您可以将这些区域链接到站点或页面，以指示要推送的目标内容。

站点或 Live Copy 链接到的区域包含需要在该站点或 Live Copy 上提供的活动。默认情况下，站点或Live copy链接到主区域，但您可以很好地链接除主区域之外的其他区域。

>[!NOTE]
>
>使用目标内容的多站点支持功能时，您应该注意以下两点：
>
>* 使用转出或 Live Copy 时，需要获得 MSM 许可。
>* 使用同步到 Adobe Target 的功能时，需要获得 Adobe Target 许可。
>



## 用例 {#use-cases}

您可以使用多种方式设置目标内容的多站点支持功能，具体使用哪种方式取决于您的用例。此部分从理论上介绍了如何在一个品牌中使用多种方式设置此功能。In addition, in [Example: Targeting Content Based on Geography](#example-targeting-content-based-on-geography), you can see a real-world application of targeting content in multiple sites.

目标内容打包在所谓的可定义站点或页面范围的区域中。这些区域在品牌级别进行定义。一个品牌可以包含多个区域。不同品牌的区域可以有所不同。一个品牌可能只包含主区域，从而在所有品牌之间共享；而另一个品牌可能包含多个品牌（例如，按地区划分的品牌）。因此，品牌之间不需要相互映射区域集。

例如，通过目标内容的多站点支持功能，您的&#x200B;**一个**&#x200B;品牌可以拥有两个（或更多）站点，这些站点具有以下某种内容：

* 完全“不同”**&#x200B;的目标内容集 - 在一个站点中编辑目标内容不会影响其他站点。链接到不同区域的站点将读写到其自己配置的区域。 例如：
   * 站点 A 链接到区域 X
   * 站点 B 链接到区域 Y
* “共享”**&#x200B;的目标内容集 - 在一个站点中编辑会直接影响两个站点；通过让两个站点引用同一区域，可以实现此设置。链接到同一区域的站点共享此区域内的目标内容。 例如：
   * 站点 A 链接到区域 X
   * 站点 B 也链接到区域 X
* A distinct set of targeted content *inherited* from another site via MSM - Content can be unidirectionally rolled out from master to live copy. 例如：
   * 站点 A 链接到区域 X
   * 站点 B 链接到区域 Y（该区域是区域 X 的 Live Copy）

您也可能有&#x200B;**多个**&#x200B;品牌在一个站点中使用，具体情况可能比此示例更加复杂。

![多站点示例](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## 示例：根据地域定位内容 {#example-targeting-content-based-on-geography}

使用目标内容的多站点支持功能，您可以共享、转出个性化内容，或将个性化内容单独分离出来。为了更好地说明如何使用此功能，请设想一个您想要控制如何根据地域转出目标内容的情景，如下所述：

同一个站点具有四个按地域划分的版本：

* **美国**&#x200B;站点位于左上角，它是主站点。在此示例中，该站点在“定位”模式下打开。
* 此站点的其他三个版本分别是&#x200B;**加拿大**、**英国**&#x200B;和&#x200B;**澳大利亚**，它们均为 Live Copy。这三个站点在“预览”模式下打开。

![多站点版本](/help/sites-cloud/authoring/assets/multisite-versions.png)

每个站点均共享地理区域中的个性化内容：

* 加拿大站点与美国站点共享主区域。
* 大不列颠与欧洲区域链接，并从主区域继承。
* 澳大利亚站点由于位于南半球，季节性产品不适用，因此会有自己的个性化内容。

![多站点图](/help/sites-cloud/authoring/assets/multisite-diagram.png)

对于北半球，我们创建了一个冬季活动，不过是针对男性受众创建的，北美的营销人员想要为冬季活动启用一幅新图像，因此他们在美国站点中更改了原有图像。

![美国版本](/help/sites-cloud/authoring/assets/multisite-us.png)

刷新选项卡后，我们无需执行任何操作，加拿大站点即会变更为新的图像。之所以会这样，是因为加拿大站点与美国站点共享主区域。在大不列颠和澳大利亚的站点中，图像没有改变。

![更改版本](/help/sites-cloud/authoring/assets/multisite-us-change.png)

营销人员希望将所做的这些更改转出到欧洲区域，因此通过点按或单击&#x200B;**转出页面**，转出了 Live Copy。After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout). <!--The marketer would like to roll out these changes to the European region and [rolls out the live copy](/help/sites-administering/msm-livecopy.md) by tapping or clicking **Rollout Page**. After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout).-->

![转出Live Copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

澳大利亚站点中的图像仍会保持不变，这是营销人员所期望的行为，因为澳大利亚此时是夏季，所以营销人员不希望变更此内容。澳大利亚站点之所以不会发生改变，是因为它没有与其他任何地区共享区域，它也不是其他地区的 Live Copy。营销人员绝不必担心澳大利亚站点的目标内容会被覆盖。

此外，对于英国站点，由于其区域是主区域的 Live Copy，因此您可以在活动名称旁边看到由绿色指示符标记的继承状态。如果活动是继承的，您将无法对其进行修改，除非暂停或分离 Live Copy。

您随时可以暂停继承或将继承完全分离出来。您还始终可以在不暂停继承的情况下，添加仅适用于该体验的本地体验。

>[!NOTE]
>
>For a more technical look at this feature, see [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### 创建新区域与创建新区域作为 Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

在 AEM 中，您可以选择创建新区域，或创建新区域作为 Live Copy。创建新区域可将活动以及属于这些活动的任何内容（例如选件、体验等）组合到一起。如果您想要创建完全不同的目标内容集，或想要共享目标内容集，则应当创建新区域。

但是，如果您已经通过 MSM 在两个站点之间设置了继承，则您可能希望继承活动。在这种情况下，您应当创建新区域作为 Live Copy，让区域 Y 成为区域 X 的 Live Copy，从而可以继承所有活动。

>[!NOTE]
>
>当页面是链接到某个区域的Live Copy，而该区域本身是链接到页面Blueprint的区域的Live Copy时，默认转出将触发目标内容的后续转出。

例如，下图中有四个站点，其中两个站点共享主区域（以及该区域中的所有活动）；还有一个站点的区域是其他区域的 Live Copy，因此会在转出后共享活动；最后一个站点完全独立（因此其活动需要一个单独的区域）。

![图详细信息](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

要在 AEM 中实现这种设置，您需要执行以下操作：

* 站点 A 链接到主区域 - 无需创建任何区域。在 AEM 中，默认情况下主区域将处于选定状态。站点 A 和 B 共享活动及其他内容。
* 站点 B 链接到主区域 - 无需创建任何区域。在 AEM 中，默认情况下主区域将处于选定状态。站点 A 和 B 共享活动及其他内容。
* 站点 C 链接到继承的区域，该区域是主区域的 Live Copy - 创建区域作为 Live Copy，即创建基于主区域的 Live Copy。转出后，继承的区域会从主区域继承活动。
* 站点 D 链接到其自身的独立区域 - 创建区域，即创建尚未定义任何活动的全新区域。独立区域不会与其他任何站点共享活动。

## 创建新区域 {#creating-new-areas}

区域可以跨活动和选件使用。在任何一种内容（如活动）中创建区域后，您也可以将该区域用于另一种内容（如选件）。

>[!NOTE]
>
>默认区域称为主区域，点按或单击品牌名称时，此区域默认处于折叠状态，**直到**&#x200B;您创建其他区域。Then, when you select a brand in either the **Activity** or **Offers** console, you see the **Area** console.

要创建新区域，请执行以下操作：

1. Navigate to **Personalization** > **Activities** or **Offers** or and then to your brand.
1. 点按或单击&#x200B;**创建区域**。

   ![创建区域](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. 单击&#x200B;**区域**&#x200B;图标，然后单击&#x200B;**下一步**。
1. 在&#x200B;**标题**&#x200B;字段中，输入新区域的名称。（可选）选择标记。
1. 点按或单击&#x200B;**创建**。

   AEM 随即会重定向到品牌窗口，其中列出了所有已创建的区域。如果除主区域之外还有其他区域，则您可以直接在“品牌”控制台中创建区域。

   ![创建](/help/sites-cloud/authoring/assets/multisite-create.png)

## 创建区域作为 Live Copy {#creating-areas-as-live-copies}

您可以创建区域作为 Live Copy，以便跨站点结构继承目标内容。

要创建区域作为 Live Copy，请执行以下操作：

1. Navigate to **Personalization** > **Activities** or **Offers** and then to your brand.
1. 点按或单击&#x200B;**创建区域作为 Live Copy**。

   ![创建Live Copy区域](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. 选择要为其创建 Live Copy 的区域，然后单击&#x200B;**下一步**。

   ![创建Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. 在&#x200B;**名称**&#x200B;字段中，输入 Live Copy 的名称。默认情况下，会包括子页面；通过选中&#x200B;**不包括子页面**&#x200B;复选框，可将子页面排除。

   ![创建Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. 在&#x200B;**转出配置**&#x200B;下拉菜单中，选择相应的配置。

   See Installed Rollout Configurations for descriptions of each option. <!--See [Installed Rollout Configurations](/help/sites-administering/msm-sync.md#installed-rollout-configurations) for descriptions of each option.-->

   See Creating and Synchronizing Live Copies for more information on live copies. <!--See [Creating and Synchronizing Live Copies](/help/sites-administering/msm-livecopy.md) for more information on live copies.-->

   >[!NOTE]
   >
   >When a page is rolled out to a Live Copy and the area configured for the Blueprint page is also the Blueprint for the area configured for the Pages Live Copy, the LiveAction **personalizationContentRollout** triggers a synchronous subRollout, which is part of the **Standard rollout config**.

1. 点按或单击&#x200B;**创建**。

   AEM 随即会重定向到品牌窗口，其中列出了所有已创建的区域。如果除主区域之外还有其他区域，则您可以直接从品牌窗口中创建区域。

   ![创建区域](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## 将站点链接到区域 {#linking-sites-to-an-area}

您可以将区域链接到页面或站点。除非这些页面被子页面上的映射覆盖，否则所有子页面都会继承这些区域。 不过，通常而言，您需要在站点级别建立链接。

建立链接后，只能使用选定区域中的活动、体验和选件。这样可以防止意外搞混单独管理的内容。如果没有配置任何其他区域，则会使用每个品牌的主区域。

>[!NOTE]
>
>Pages or sites that reference the same area are using the *same* shared set of activities, experiences, and offers. 编辑由多个站点共享的活动、体验或选件会影响所有站点。

要将站点链接到区域，请执行以下操作：

1. 导航到要将其链接到区域的站点（或页面）。
1. 选择相应的站点或页面，然后点按或单击&#x200B;**查看属性**。
1. Tap or click the **Personalization** tab.
1. 在&#x200B;**品牌**&#x200B;菜单中，选择要将您的区域链接到的品牌。选择品牌后，可用区域会显示在&#x200B;**区域引用**&#x200B;菜单中。

   ![链接站点](/help/sites-cloud/authoring/assets/multisite-english.png)

1. 从&#x200B;**区域引用**&#x200B;下拉菜单中选择相应的区域，然后点按或单击&#x200B;**保存**。

   ![区域引用](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## 分离 Live Copy 或暂停目标内容的继承 {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

您可能想要暂停或分离目标内容的继承。需按活动暂停或分离 Live Copy。例如，您可能想要修改活动中的体验，但是如果该活动仍然链接到继承的副本，便无法修改体验或该活动的任何属性。

暂停 Live Copy 会暂时中断继承，但之后可以恢复继承。而分离 Live Copy 则会永久中断继承。

要暂停或分离目标内容的继承，需要先在活动中恢复继承。如果页面或站点链接到的区域是Live Copy，则可以查看活动的继承状态。

从其他站点继承的活动的名称旁边显示有绿色标记。暂停的继承标记为红色，本地创建的活动没有图标。

>[!NOTE]
>
>* 您只能在活动中暂停或分离 Live Copy。
>* 要扩展继承的活动，无需暂停或分离 Live Copy。您始终可以为该活动创建&#x200B;**新的**&#x200B;本地体验和选件。如果您想要修改现有活动，则需要暂停继承。
>



### 暂停继承 {#suspending-inheritance}

要在活动中暂停或分离目标内容的继承，请执行以下操作：

1. 导航到要在其中分离或暂停继承的页面，然后点按或单击“模式”下拉菜单中的&#x200B;**定位**。
1. 如果您的页面链接到的区域是 Live Copy，则可以看到继承状态。点按或单击&#x200B;**开始定位**。
1. 要在活动中暂停继承，请执行以下操作之一：

   1. 选择活动的某个元素，例如受众。AEM 随即会自动显示“暂停 Live Copy”确认对话框。（在整个定位过程中，您都可以通过点按或单击任何元素来暂停 Live Copy。）
   1. 从工具栏的下拉菜单中选择&#x200B;**暂停 Live Copy**。
   ![暂停Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Tap or click **Suspend** to suspend the activity. 暂停继承的活动会标记为红色。

   ![暂停的Live Copy](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### 中断继承 {#breaking-inheritance}

在活动中，要中断目标内容的继承，请执行以下操作：

1. 导航到要在其中将 Live Copy 从主区域中分离出来的页面，然后点按或单击“模式”下拉菜单中的&#x200B;**定位**。
1. 如果您的页面链接到的区域是 Live Copy，则可以看到继承状态。点按或单击&#x200B;**开始定位**。
1. 从工具栏的下拉菜单中选择&#x200B;**分离 Live Copy**。AEM 会向您确认是否要分离 Live Copy。
1. 点按或单击&#x200B;**分离**，以在活动中将 Live Copy 分离出来。分离之后，与继承有关的下拉菜单将不再显示。此时活动会变成本地活动。

   ![本地活动](/help/sites-cloud/authoring/assets/multisite-winter.png)

## 恢复目标内容的继承 {#restoring-inheritance-of-targeted-content}

如果在活动中暂停了目标内容的继承，则可以随时恢复继承。但是，如果分离了 Live Copy，则无法恢复继承。

要在活动中恢复目标内容的继承，请执行以下操作：

1. Navigate to the page where you want to restore inheritance and tap or click **Targeting** in the mode drop-down menu.
1. 点按或单击&#x200B;**开始定位**。
1. Select **Resume Live Copy** from the drop-down menu in the toolbar.

   ![恢复Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. 点按或单击&#x200B;**继续**，以确认您想要恢复 Live Copy 继承。如果恢复继承，对当前活动所做的任何修改都会丢失。

## 删除区域 {#deleting-areas}

删除区域时，也会删除该区域中的所有活动。在您删除区域之前，AEM 会向您发出警告。如果您确实删除了站点所链接的区域，则此品牌的映射将自动重新映射到主区域。

要删除区域，请执行以下操作：

1. Navigate to **Personalization** > **Activities** or **Offers** and then your brand.
1. 点按或单击要删除的区域旁边的图标。
1. 点按或单击&#x200B;**删除**，并确认要删除该区域。
