---
title: 使用 ContextHub 配置分段
description: 了解如何使用ContextHub配置分段。
exl-id: fbc38611-dbee-426e-b823-df64b6730c45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 5%

---

# 使用 ContextHub 配置分段{#configuring-segmentation-with-contexthub}

分段是创建营销活动时的主要考虑事项。请参阅 [了解分段](segmentation.md) 有关分段工作方式和关键术语的信息。

根据您已收集的有关网站访客的信息以及要实现的目标，您需要定义目标内容所需的区段和策略。

然后，这些区段用于向访客提供具体目标内容。 [活动](activities.md) 此处定义的内容可以包含在任何页面中，并定义专用内容适用的访客区段。

AEM使您能够轻松地个性化用户体验。 它还允许您验证区段定义的结果。

## 访问区段 {#accessing-segments}

的 [受众](audiences.md) 控制台用于管理ContextHub的区段以及Adobe Target帐户的受众。 本文档介绍如何管理ContextHub的区段。

要访问您的区段，请在全局导航中选择 **导航>个性化>受众**.

![管理受众](../assets/contexthub-segmentation-audiences.png)

## 区段编辑器 {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
的 **区段编辑器** 允许您轻松修改区段。 要编辑区段，请在区段列表中选择一个区段，然后单击 **编辑** 按钮。

![区段编辑器](../assets/contexthub-segment-editor.png)

使用组件浏览器，您可以添加 **和** 和 **或** 容器以定义区段逻辑，然后添加其他组件以比较属性和值，或引用脚本和其他区段以定义选择标准(请参阅 [创建新区段](#creating-a-new-segment))以定义选择区段的确切方案。

当整个语句的计算结果为true时，区段即已解析。 如果有多个区段适用，则 **提升** 因素。 请参阅 [创建新区段](#creating-a-new-segment) 有关提升因子的详细信息。

>[!CAUTION]
>
>区段编辑器不检查是否有任何循环引用。 例如，区段A引用了另一个区段B，而这反过来又引用了区段A。您必须确保区段不包含任何循环引用。

### 容器 {#containers}

以下容器现成可用，允许您将比较和引用分组在一起进行布尔值评估。 可将组件从组件浏览器拖至编辑器。 请参阅以下部分 [使用AND和OR容器](#using-and-and-or-containers) 以了解更多信息。

|  |  |
|---|---|
| 容器 AND | 布尔AND运算符 |
| 容器 OR | 布尔OR运算符 |

### 比较 {#comparisons}

以下区段比较功能现成可用，可用于评估区段属性。 可将组件从组件浏览器拖至编辑器。

|  |  |
|---|---|
| Property-Value | 将存储的属性与定义的值进行比较 |
| Property-Property | 将存储的一个属性与另一个属性进行比较 |
| 属性区段引用 | 将存储的属性与另一个引用区段进行比较 |
| 属性脚本引用 | 将存储的属性与脚本的结果进行比较 |
| 区段引用脚本参考 | 将引用的区段与脚本结果进行比较 |

>[!NOTE]
>
>在比较值时，如果未设置比较的数据类型（即设置为自动检测），则ContextHub的分段引擎将只比较Javascript所示的值。 它不会将值转换为其预期类型，这可能会导致误导性结果。 例如：
>
>`null < 30 // will return true`
>
>因此，当 [创建区段](#creating-a-new-segment)，则您应该 **数据类型** 只要已知比较值的类型。 例如：
>
>比较属性时 `profile/age`，您已经知道比较类型将 **数字**，因此即使 `profile/age` 未设置，比较 `profile/age` 少于30的将返回 **false**，如您预期的。

### 引用 {#references}

以下引用现成可用，可直接链接到脚本或其他区段。 可将组件从组件浏览器拖至编辑器。

|  |  |
|---|---|
| 段引用 | 评估引用的区段 |
| 脚本引用 | 评估引用的脚本。 请参阅以下部分 [使用脚本引用](#using-script-references) 以了解更多信息。 |

## 创建新区段 {#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 之后 [访问区段](#accessing-segments), [导航到文件夹](#organizing-segments) 要创建区段的位置，或将其保留在根目录中。

1. 点按或单击 **创建** 按钮，选择 **创建ContextHub区段**.

   ![添加区段](../assets/contexthub-create-segment.png)

1. 在 **新的ContextHub区段**，根据需要输入区段的标题以及提升值，然后点按或单击 **创建**.

   ![新区段](../assets/contexthub-new-segment.png)

   每个区段都有一个提升参数，用作加权因子。 数值越大，表示将优先选择该区段，以在多个区段有效的情况下选择数量较低的区段。

   * 最小值： `0`
   * 最大值： `1000000`

1. 从区段控制台中，编辑新创建的区段，以在区段编辑器中将其打开。
1. 将比较或引用拖到区段编辑器中，该编辑器将显示在默认的AND容器中。
1. 双击或点按新引用或区段的配置选项，以编辑特定参数。 在本例中，我们正在测试巴塞尔的人员。

   ![测试巴塞尔人员](../assets/contexthub-comparing-property-value.png)

   始终设置 **数据类型** 以确保正确评估比较。 请参阅 [比较](#comparisons) 以了解更多信息。

1. 单击 **完成** 要保存定义，请执行以下操作：
1. 根据需要添加更多组件。您可以使用用于“与”和“或”比较的容器组件来构建布尔表达式(请参阅 [使用AND和Or容器](#using-and-and-or-containers) )。 使用区段编辑器，您可以删除不再需要的组件，或将它们拖动到语句中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

使用AND和OR容器组件，您可以在AEM中构建复杂的区段。 执行此操作时，了解一些基本要点：

* 定义的顶级始终是最初创建的AND容器。 无法更改，但对区段定义的其余部分没有影响。
* 确保对容器进行嵌套是合理的。 容器可以作为布尔表达式的括号查看。

以下示例用于选择在我们的瑞士目标组中被视为的访客：

```text
 People in Basel

 OR

 People in Zürich
```

首先，在默认的AND容器中放置OR容器组件。 在OR容器中，您可以添加属性或引用组件。

![使用OR运算符的区段](../assets/contexthub-or-operator.png)

您可以根据需要嵌套多个AND和OR运算符。

### 使用脚本引用 {#using-script-references}

通过使用脚本引用组件，可以将区段属性的评估委派给外部脚本。 正确配置脚本后，即可将其用作区段条件的任何其他组件。

#### 定义要引用的脚本 {#defining-a-script-to-reference}

1. 将文件添加到 `contexthub.segment-engine.scripts` clientlib。
1. 实施返回值的函数。 例如：

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. 使用注册脚本 `ContextHub.SegmentEngine.ScriptManager.register`.

如果脚本依赖于其他属性，则脚本应调用 `this.dependOn()`. 例如，如果脚本依赖于 `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用脚本 {#referencing-a-script}

1. 创建ContextHub区段。
1. 添加 **脚本参考** 组件。
1. 打开 **脚本参考** 组件。 如果 [正确配置](#defining-a-script-to-reference)，则脚本应在 **脚本名称** 下拉菜单。

## 组织区段 {#organizing-segments}

如果您有多个区段，它们可能会变得难以作为平面列表进行管理。 在这种情况下，创建文件夹以管理区段会非常有用。

### 创建新文件夹 {#create-folder}

1. 之后 [访问区段](#accessing-segments)，单击或点按 **创建** 按钮，选择 **文件夹**.

   ![添加文件夹](../assets/contexthub-create-segment.png)

1. 提供文件夹的&#x200B;**标题**&#x200B;和&#x200B;**名称**。
   * **标题**&#x200B;应为描述性的。
   * **名称**&#x200B;将成为存储库中的节点名称。
      * 它会根据标题自动生成，并根据 [AEM 命名约定](/help/implementing/developing/introduction/naming-conventions.md)进行调整。
      * 如有必要可以调整。

   ![创建文件夹](../assets/contexthub-create-folder.png)

1. 点击或单击&#x200B;**创建**。

   ![确认文件夹](../assets/contexthub-confirm-folder.png)

1. 文件夹将显示在区段列表中。
   * 对列的排序方式将影响新文件夹在列表中显示的位置。
   * 您可以点按或单击列标题以调整排序。
      ![新文件夹](../assets/contexthub-folder.png)

### 修改现有文件夹 {#modify-folders}

1. 之后 [访问区段](#accessing-segments)，单击或点按要修改的文件夹以将其选中。

   ![选择文件夹](../assets/contexthub-select-folder.png)

1. 点按或单击 **重命名** 来重命名文件夹。

1. 提供 **文件夹标题** 单击 **保存**.

   ![重命名文件夹](../assets/contexthub-rename-folder.png)

>[!NOTE]
>
>重命名文件夹时，只能更改标题。 名称无法更改。

### 删除文件夹

1. 之后 [访问区段](#accessing-segments)，单击或点按要修改的文件夹以将其选中。

   ![选择文件夹](../assets/contexthub-select-folder.png)

1. 点按或单击 **删除** 删除文件夹。

1. 出现一个对话框，其中显示了选定要删除的文件夹的列表。

   ![确认删除](../assets/contexthub-confirm-segment-delete.png)

   * 点按或单击 **删除** 确认。
   * 点按或单击 **取消** 中止。

1. 如果任何选定的文件夹包含子文件夹或区段，则必须确认删除这些文件夹或区段。

   ![确认删除子项](../assets/contexthub-confirm-segment-child-delete.png)

   * 点按或单击 **强制删除** 确认。
   * 点按或单击 **取消** 中止。

>[!NOTE]
>
> 无法将区段从一个文件夹移动到另一个文件夹。

## 测试区段的应用 {#testing-the-application-of-a-segment}

定义区段后，可借助 **[ContextHub](contexthub.md).**

1. 预览页面
1. 单击ContextHub图标以显示ContextHub工具栏
1. 选择与您创建的区段匹配的角色
1. ContextHub将解析选定角色的适用区段

例如，我们为在巴塞尔中识别用户而制定的简单区段定义基于用户的位置。 加载与这些条件匹配的特定角色时，会显示区段是否成功解析：

![解析的区段](../assets/contexthub-segment-resolve.png)

或者，如果它未得到解决：

![未解析的区段](../assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征仅在重新加载页面时发生更改。

此类测试也可在内容页面上执行，并与目标内容及相关内容结合使用 **活动** 和 **体验**.

如果您设置了活动和体验，则可以使用活动轻松测试区段。 有关设置活动的详细信息，请参阅相关 [关于创作目标内容的文档](targeted-content.md).

1. 在已设置目标内容的页面的编辑模式下，您可以通过内容上的箭头图标来查看内容是否已定位。
1. 切换到预览模式并使用ContextHub，切换到与为体验配置的分段不匹配的人物。
1. 切换到与为体验配置的区段匹配的角色，并查看体验是否会相应地发生更改。

## 使用区段 {#using-your-segment}

区段用于控制特定目标受众看到的实际内容。 请参阅 [管理受众](audiences.md) 以详细了解受众和区段， [创作目标内容](targeted-content.md) 关于使用受众和区段来定位内容。
