---
title: 使用ContextHub配置分段
description: 了解如何使用ContextHub配置分段。
translation-type: tm+mt
source-git-commit: 82ad2cda70dd664ac9456a04f34e2d5831687fc1
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# 使用ContextHub配置分段{#configuring-segmentation-with-contexthub}

分段是创建营销活动时的主要考虑事项。请参 [阅了解细分](segmentation.md) ，以了解有关细分工作方式和关键术语的信息。

根据您已收集的有关网站访客和您要实现的目标的信息，您需要定义目标内容所需的细分和策略。

然后，这些区段用于为访客提供具体目标内容。 [此处](activities.md) 定义的活动可以包含在任何页面上，并定义专用内容适用的访客区段。

AEM允许您轻松个性化用户体验。 它还允许您验证区段定义的结果。

## 访问区段 {#accessing-segments}

受众 [控制台](audiences.md) ，用于管理ContextHub的区段以及您的Adobe Target帐户的受众。 本文档涵盖管理ContextHub的区段。

要访问您的区段，请在全局导航中选 **择导航>个性化>受众**。

![管理受众](/help/sites-cloud/authoring/assets/contexthub-segmentation-audiences.png)

## 区段编辑器 {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
段 **编辑器** 允许您轻松修改段。 要编辑区段，请在区段列表中选择区段，然后单击编 **辑** 按钮。

![细分编辑器](/help/sites-cloud/authoring/assets/contexthub-segment-editor.png)

使用组件浏览器，您可 **以添加AND** 和OR **容器来定义段逻辑，然后添加其他组件来比较属性和值，或引用脚本和其他段来定义选择条件(请参阅**[](#creating-a-new-segment)创建新段)以定义选择段的确切方案。

当整个语句的计算结果为true时，段即已解析。 在适用多个区段的事件下，还 **会使** 用提升因子。 有关 [提升因子的详细信息](#creating-a-new-segment) ，请参阅创建新区段。

>[!CAUTION]
>
>段编辑器不检查任何循环引用。 例如，区段A引用了另一个区段B，这反过来又引用了区段A。您必须确保您的区段不包含任何循环引用。

### 容器 {#containers}

以下容器是现成的，允许您将比较和引用分组在一起进行布尔评估。 可以将组件浏览器拖动到编辑器中。 有关详细信 [息，请参阅下一节](#using-and-and-or-containers) “使用AND和OR”。

|  |  |
|---|---|
| 容器 AND | 布尔AND运算符 |
| 容器 OR | 布尔OR运算符 |

### 比较 {#comparisons}

现成可使用以下细分比较来评估细分属性。 可以将组件浏览器拖动到编辑器中。

|  |  |
|---|---|
| 属性值 | 将存储的属性与定义的值进行比较 |
| 属性——属性 | 将存储的一个属性与另一个属性进行比较 |
| 属性段引用 | 将存储的属性与另一个引用的区段进行比较 |
| 属性——脚本参考 | 将存储的属性与脚本的结果进行比较 |
| 段引用脚本参考 | 将引用的段与脚本的结果进行比较 |

>[!NOTE]
>
>在比较值时，如果未设置比较的数据类型（即设置为自动检测）,ContextHub的分段引擎将简单地将值与javascript进行比较。 它不会将值转换为其预期类型，这会导致误导性结果。 例如：
>
>`null < 30 // will return true`
>
>因此， [在创建区段](#creating-a-new-segment)时，应当在已知 **比较值的类型时** ，选择数据类型。 例如：
>
>在比较属性 `profile/age`时，您已经知道比较类型将是 **数字**，因此即使未设置，小于30的 `profile/age` 比较也会返回 `profile/age` false ****，如您所期望的。

### 引用 {#references}

以下参考功能现成可用，可直接链接到脚本或其他段。 可以将组件浏览器拖动到编辑器中。

|  |  |
|---|---|
| 段引用 | 评估引用的区段 |
| 脚本引用 | 评估引用的脚本。 有关详细信息，请 [参阅下一节](#using-script-references) “使用脚本引用”。 |

## Creating a New Segment {#creating-a-new-segment}

要定义新区段，请执行以下操作：

1. 访问 [区段后](#accessing-segments)，单击或点按创建按钮，然后选择 **创建ContextHub区段**。

   ![添加区段](/help/sites-cloud/authoring/assets/contexthub-create-segment.png)

1. 在“新 **建ContextHub区段**”中，根据需要输入区段的标题以及提升值，然后点按或单击创 **建**。

   ![新细分](/help/sites-cloud/authoring/assets/contexthub-new-segment.png)

   每个区段都有一个提升参数，用作加权因子。 数值越大，表示在多个段有效的情况下，将优先选择数值越低的段。

   * Minimum value: `0`
   * Maximum value: `1000000`

1. 从“区段”控制台中，编辑新创建的区段，以在区段编辑器中将其打开。
1. 将比较或引用拖动到段编辑器，它将显示在默认的AND容器中。
1. 多次单击或点按新引用或区段的配置选项以编辑特定参数。 在这个例子中，我们正在测试巴塞尔的人员。

   ![巴塞尔人员测试](/help/sites-cloud/authoring/assets/contexthub-comparing-property-value.png)

   如果可能， **请始终设置** “数据类型”，以确保正确评估比较。 有关更 [多信息](#comparisons) ，请参阅比较。

1. Click **Done** to save your definition:
1. 根据需要添加更多组件。您可以使用AND和OR比较的容器组件来构建布尔表达式(请参 [阅使用AND和Or容器](#using-and-and-or-containers) )。 使用区段编辑器，您可以删除不再需要的组件，或将它们拖动到语句中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

使用AND和OR容器组件，您可以在AEM中构建复杂的细分。 这样做时，了解一些基本要点会有所帮助：

* 定义的顶级始终是最初创建的AND容器。 无法更改，但对区段定义的其余部分没有影响。
* 确保容器嵌套合理。 这些容器可以作为布尔表达式的括号进行查看。

以下示例用于选择在我们的瑞士访客中被视为的目标组:

```text
 People in Basel

 OR

 People in Zürich
```

通过将OR容器组件放置到默认的AND容器中来开始。 在OR容器中，您可以添加属性或引用组件。

![使用OR运算符进行段](/help/sites-cloud/authoring/assets/contexthub-or-operator.png)

您可以根据需要嵌套多个AND和OR运算符。

### 使用脚本引用 {#using-script-references}

通过使用“脚本引用”组件，可以将段属性的评估委派给外部脚本。 正确配置脚本后，该脚本即可用作段条件的任何其他组件。

#### 定义要引用的脚本 {#defining-a-script-to-reference}

1. 将文件添加 `contexthub.segment-engine.scripts` 到clientlib。
1. 实现返回值的函数。 例如：

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

1. 注册脚本 `ContextHub.SegmentEngine.ScriptManager.register`。

如果脚本依赖于其他属性，则脚本应调用 `this.dependOn()`。 例如，如果脚本取决于 `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### 引用脚本 {#referencing-a-script}

1. 创建ContextHub区段。
1. 在 **段的所** 需位置添加“脚本引用”组件。
1. 打开“脚本引用”组 **件的编辑** 对话框。 如果 [配置正确](#defining-a-script-to-reference)，脚本应显示在“脚本 **名称** ”下拉菜单中。

## 测试区段的应用 {#testing-the-application-of-a-segment}

定义区段后，可以借助ContextHub测试潜在 **[结果](contexthub.md)。**

1. 预览页面
1. 单击ContextHub图标以显示ContextHub工具栏
1. 选择与您创建的区段匹配的人物
1. ContextHub将解析所选角色的适用区段

例如，我们在巴塞尔识别用户的简单细分定义基于用户的位置。 加载符合这些条件的特定人物会显示区段是否成功解析：

![解析的段](/help/sites-cloud/authoring/assets/contexthub-segment-resolve.png)

或者，如果它未解决：

![无法解析的区段](/help/sites-cloud/authoring/assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>所有特征都会立即解析，但大多数特征只会在页面重新加载时发生更改。

此类测试还可以在内容页面上执行，并结合目标内容以及相关 **活动** 和 **体验**。

如果您已设置活动和体验，则可以使用活动轻松测试您的细分。 有关设置活动的详细信息，请参阅有关创 [作目标内容的相关文档](targeted-content.md)。

1. 在已设置目标内容的页面的编辑模式下，可以通过内容上的箭头图标来查看内容是否为目标。
1. 切换到预览模式并使用Context Hub，切换到与为体验配置的分段不匹配的人物。
1. 切换到与为体验配置的细分相匹配的人物，并查看体验是否会相应发生更改。

## 使用您的细分 {#using-your-segment}

区段用于控制特定目标受众看到的实际内容。 有关受众 [和](audiences.md) ，请参阅管理受众和区段，以及创 [作有关使用受众和区段来](targeted-content.md) 目标内容的目标内容。
