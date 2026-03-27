---
title: 使用主题编辑器自定义自适应表单主题
description: 了解如何使用主题编辑器在Adobe Experience Manager中为基于核心组件的自适应Forms创建和自定义可视化主题。
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: f1b318803b9b854ec2ce800670f6484799113599
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---


# 自定义表单主题 {#customizing-form-themes}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

Adobe Experience Manager (AEM) Forms中的主题编辑器是一个可视化界面，您可以通过它创建和自定义自适应Forms的主题，而无需手动编写代码。 主题定义表单组件和面板的外观，包括背景颜色、字体样式、边框、维度和间距。 应用主题时，指定的样式会反映在相应的组件上，并且您可以在多个自适应Forms中重用相同的主题。

主题编辑器无需专门的开发人员角色来设置基本表单样式。 只需CSS的相关知识，您就可以使用可视侧边栏为表单设置样式，或直接在编辑器中编写高级CSS覆盖。

## 先决条件 {#prerequisites}

* Adobe Experience Manager Forms中的作者级别权限。
* 对CSS样式设置原则的基本了解。 有关完整的CSS引用，请参阅[MDN Web文档CSS引用](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)。

## 导航到主题目录 {#navigate-to-themes}

1. 登录到您的AEM创作实例。
1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主题]**。

   Themes目录显示所有可用的主题，包括AEM Canvas提供的任何标准主题，以及您或您的组织创建的自定义主题。

### 创建新主题 {#create-a-new-theme}

1. 在Themes目录中，选择要存储新主题的文件夹。
1. 单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 主题]**。

   ![创建新主题](/help/forms/assets/custom-theme-create.png)

1. 在&#x200B;**[!UICONTROL 创建主题]**&#x200B;对话框中，指定以下详细信息：
   * **[!UICONTROL 标题]**：主题的描述性标题。
   * **[!UICONTROL 名称]**：主题的节点名称。
   * **[!UICONTROL 要预览主题的自适应表单]**：对于核心组件主题，请选择基于核心组件的自适应表单。 **[!UICONTROL 使用默认自适应表单]**&#x200B;使用基础自适应表单，而不是核心组件。 所选表单会显示在主题编辑器画布中，以在编辑时实时预览。
   * **[!UICONTROL 描述]** *（可选）*：主题的简短描述。
   * **[!UICONTROL 配置容器]** *（可选）*：包含Adobe字体配置详细信息的配置容器。
   * **[!UICONTROL 标记]** *（可选）*：附加到主题的标记用于标识和搜索。
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![配置自定义主题](/help/forms/assets/custom-theme-name.png)

   创建主题。 您现在可以单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以在主题编辑器中打开它。

### 编辑现有主题 {#edit-an-existing-theme}

1. 在&#x200B;**主题**&#x200B;目录中，选择要修改的主题。
1. 单击操作栏中的&#x200B;**[!UICONTROL 编辑]**&#x200B;以在主题编辑器中打开主题。

   ![编辑主题](/help/forms/assets/custom-theme-edit.png)

### 上传主题 {#upload-a-theme}

您可以将主题包（例如，从另一个环境导出的主题包）导入到Themes目录中：

1. 在&#x200B;**主题**&#x200B;目录中，单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**。
1. 浏览选择计算机上的主题包（ZIP文件），然后单击&#x200B;**[!UICONTROL 上传]**。

   ![上载主题 — 使用“文件上载”选项创建“菜单”](/help/forms/assets/custom-theme-upload.png)

上传的主题将显示在Themes目录中，可以像其他任何主题一样进行编辑。

### 下载主题 {#download-a-theme}

您可以将主题导出为包（ZIP文件），以便在另一个AEM Forms环境中重复使用或对其进行备份：

1. 在&#x200B;**主题**&#x200B;目录中，选择一个或多个主题（使用主题卡上的复选框）。
1. 在操作栏中单击&#x200B;**[!UICONTROL 下载]**。 将出现一个对话框，其中包含所选主题的详细信息。
1. 在对话框中确认或单击&#x200B;**[!UICONTROL 下载]**。 主题包将作为ZIP文件下载到您的计算机。

   ![下载主题 — 选择主题并单击“下载”](/help/forms/assets/custom-theme-download.png)

您稍后可以使用[在同一环境或其他环境中上载主题](#upload-a-theme)来上载此ZIP。

## 了解主题编辑器界面 {#understand-the-theme-editor}

在主题编辑器中打开主题时，您会看到两个主要区域：

![主题编辑器](/help/forms/assets/custom-theme-editor.png)

* **画布**（右侧）：显示链接到主题的自适应表单预览。 所有样式更改都会立即反映在此处，因此您可以实时查看编辑的影响。
* **侧栏**（左侧）：包含&#x200B;**选择器**&#x200B;面板，该面板以树结构列出了所有可样式化的表单组件，如页面、表单、字段、按钮、面板、图像、hCaptcha和reCaptcha。

### 画布工具栏 {#canvas-toolbar}

![带有切换侧面板、“撤消”、“重做”、“模拟器”、“编辑/预览”和“主题”选项的主题编辑器画布工具栏](/help/forms/assets/custom-theme-toolbar-utilities.png)

从左到右，工具栏提供：
* **A：切换侧面板**：显示或隐藏选择器侧栏。 当您想要专注于画布时，使用此选项可最大化表单预览区域，或者在您需要选择组件或设置组件样式时再次显示侧栏。
* **B：主题选项**（下拉列表）：打开包含四个选项的菜单。 在需要更改预览表单、查看CSS、管理保存的样式或获取编辑器内帮助时单击它。 在打开主题选项下拉列表时，您会看到：

  ![显示“配置”、“查看主题CSS”、“管理样式”和“帮助”的“主题选项”下拉列表](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL 配置]**：将画布中显示的表单切换到其他自适应表单。 使用此选项检查您的主题在其他表单上的显示方式，而无需离开编辑器。
     ![为主题预览配置自适应表单](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL 查看主题CSS]**：打开一个对话框，其中包含主题的完整编译CSS。 要仅查看当前选定组件的CSS，请改用侧边栏中的&#x200B;**[!UICONTROL 查看CSS]**（便于调试或复制规则）。
     ![查看最终CSS](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL 管理样式]**：打开对话框以保存、命名并重用文本和图像样式。 保存的样式可以应用于其他组件；最近使用的样式也可以显示以便快速重用。
   * **[!UICONTROL 帮助]**：开始主题编辑器的图像引导式教程。
* **C：撤消/重做**：还原或重新应用上次样式更改。 如果您尝试某种样式，并且希望回退而不丢失其他编辑，则此功能非常有用。
* **D：模拟器**：选择设备或断点（例如，台式机、平板电脑或移动设备）以预览该屏幕大小的表单。 表单预览会调整大小以匹配所选的断点。 您在选择断点时设置的任何样式仅应用于该断点，因此您可以定义响应式样式。 有关详细信息，请参阅[不同屏幕大小的样式](#styling-for-different-screen-sizes)。
* **E：编辑/预览**：在两种模式之间切换。 **编辑**&#x200B;为默认设置：您可以单击画布上的组件以将其选中并在侧栏中更改其样式。 **预览**&#x200B;将表单显示为最终用户会看到它而没有选择边框、组件标签或样式边栏，因此您可以在发布之前检查主题表单的外观和行为。

<!--**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).-->

### 为组件设置样式

可通过两种方式选取要造型的组件：
* **从画布**：直接单击表单中的组件（例如，文本字段、按钮或下拉列表）。 所选元素使用边框突出显示，其上方会显示组件标签（例如“文本输入小组件”）。 该组件的样式选项会显示在侧栏中。

  ![从画布编辑主题](/help/forms/assets/custom-theme-field-level.png)

* **从“选择器”面板**：使用左侧边栏中的树结构可向下钻取到特定组件。 例如，展开&#x200B;**[!UICONTROL 字段]** > **[!UICONTROL 小组件]** > **[!UICONTROL 文本输入]**&#x200B;以专门针对文本框小组件。

  ![从选择器面板编辑主题](/help/forms/assets/custom-theme-selector.png)

#### 将样式应用于组件 {#apply-styles-to-a-component}

选择组件后，侧栏会显示可用的样式属性，这些属性分为以下类别：

* **[!UICONTROL 维度和位置]**：控件对齐、大小、边距、边距、宽度、高度和Z索引。
* **[!UICONTROL 文本]**：配置字体系列、粗细、颜色、大小、行高、对齐方式、字母间距、文本修饰和转换。 有关支持的CSS文本属性的完整列表，请参阅[MDN CSS文本文档](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text)。
* **[!UICONTROL 背景]**：设置背景颜色、图像或渐变。 请参阅[MDN CSS背景文档](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders)。
* **[!UICONTROL 边框]**：定义边框宽度、样式、半径和颜色。
* **[!UICONTROL 效果]**：添加不透明度、混合模式和阴影。

要应用样式，请执行以下操作：

1. 从画布或“选择器”面板中选择组件。
1. 在侧栏中设置所需的可视属性。 例如，选择&#x200B;**[!UICONTROL 背景颜色]**&#x200B;并调整&#x200B;**[!UICONTROL 字体颜色]**。
1. 单击复选标记图标&#x200B;**[!UICONTROL 确定]**&#x200B;以确认属性更改。

   ![应用样式](/help/forms/assets/custom-theme-applying-style.png)

<!--#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.-->

### 表单级样式 {#form-level-styling}

表单级样式将样式广泛应用到同一类型的所有组件。 例如，如果在&#x200B;**[!UICONTROL 选择器]**&#x200B;面板中选择&#x200B;**字段**&#x200B;并将背景颜色设置为蓝色，则表单中的每个字段（文本框、数字框、日期选取器和下拉列表）都会继承该蓝色背景。

**示例：**&#x200B;要在表单中的所有字段上设置统一的背景颜色：

1. 在&#x200B;**选择器**&#x200B;面板中选择&#x200B;**[!UICONTROL 字段]**。
1. 在侧栏中，将&#x200B;**[!UICONTROL 背景颜色]**&#x200B;设置为蓝色。
1. 单击&#x200B;**[!UICONTROL 确定]**。

   ![表单级样式](/help/forms/assets/custom-theme-form-level-styling.png)

表单中的所有字段组件现在都显示蓝色背景。

### 组件级样式 {#component-level-styling}

组件级样式定位特定的组件类型，覆盖任何更广泛的表单级样式。 例如，如果只希望文本框小组件具有不同的背景颜色，而所有其他字段均保持蓝色，则可以专门定位文本框小组件。

**示例：**&#x200B;要仅对文本框小组件设置绿色背景和紫色字体：

1. 在“选择器”面板中，展开&#x200B;**[!UICONTROL 字段]** > **[!UICONTROL 小组件]** > **[!UICONTROL 文本输入]**。
1. 将&#x200B;**[!UICONTROL 字体颜色]**&#x200B;设置为紫色。
   ![字段级样式](/help/forms/assets/custom-theme-field-level-styling1.png)
1. 将&#x200B;**[!UICONTROL 背景颜色]**&#x200B;设置为绿色。
   ![字段级样式](/help/forms/assets/custom-theme-field-level-styling2.png)
1. 单击&#x200B;**[!UICONTROL 确定]**。

文本框小组件现在显示带有紫色文本的绿色背景，而所有其他字段从表单级样式中保持为蓝色。

>[!NOTE]
>
> **组件级样式始终优先于表单级样式。**&#x200B;在两个级别上定义样式时，更具体的组件级选择器将覆盖更广泛的表单级选择器。 这遵循标准[CSS特殊性规则](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)。 例如，如果在所有字段（表单级别）上设置了蓝色背景，在文本框小组件（组件级别）上设置了绿色背景，则文本框将显示绿色背景。

## 不同屏幕大小的样式 {#styling-for-different-screen-sizes}

您可以为不同的设备大小定义不同的样式，以便您的主题具有响应性。 主题编辑器工具栏显示&#x200B;**设备选项**（例如，iPhone 5、iPad、Desktop、Tablet、Tablet、Small Screen），以便预览该屏幕大小的表单并设置其样式。

1. 在画布工具栏中，使用&#x200B;**设备模拟器**：单击其中一个设备标签（例如，**[!UICONTROL 桌面]**、**[!UICONTROL 平板电脑]**、**[!UICONTROL iPad]**、**[!UICONTROL 小屏幕]**）。 表单上方的标尺显示选定设备的像素宽度。
1. 选择该设备后，可使用侧栏设置或调整样式。 样式仅适用于选定的设备视图。
1. 切换到另一台设备并根据需要为其定义样式。
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;并在完成后保存主题。

   ![主题编辑器中的设备模拟器 — 标尺和设备选项（桌面、平板电脑、iPad、小屏幕）](/help/forms/assets/custom-theme-emulator.png)

因此，同一主题在每个设备上可以有不同的间距、字体大小或与布局相关的样式，这与响应式样式的[AEM 6.5主题编辑器行为](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=zh-Hans)相匹配。

## 使用高级CSS覆盖 {#use-advanced-css-overrides}

对于无法通过可视侧边栏使用的样式，您可以直接在编辑器中编写自定义CSS。

1. 选择组件。
1. 在侧边栏中，展开&#x200B;**[!UICONTROL 高级]**&#x200B;部分。
1. 将自定义CSS规则写入&#x200B;**[!UICONTROL CSS覆盖]**&#x200B;区域。 如果存在冲突，这些规则将覆盖通过可视控件设置的任何属性。

有关完整的CSS属性引用，请参阅[MDN Web文档CSS引用](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)。

### 添加CSS伪元素 {#add-css-pseudo-elements}

**[!UICONTROL 高级]**&#x200B;部分还支持CSS伪元素，如`::before`和`::after`。 利用这些功能，可在组件周围注入内容或装饰样式，而无需修改表单结构。 例如，要在文本框组件之前添加一个视觉指示器：

1. 选择组件（例如，`CMP Textbox`）。
1. 展开&#x200B;**[!UICONTROL 高级]**&#x200B;部分。
1. 在`::before`伪元素字段中，添加CSS属性，例如：

   ```css
   color: #B10DC9;
   ```

   ![在CSS之前](/help/forms/assets/custom-theme-before-css.png)

1. 在`::after`伪元素字段中，添加CSS属性，例如：

   ```css
   color: #006400;
   ```

   在CSS之后![](/help/forms/assets/custom-theme-after-css.png)


这些伪元素遵循标准CSS行为。 有关完整引用，请参阅[MDN CSS Pseudo元素](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)。

## 最佳实践 {#best-practices}

* **使用“选择器”面板进行精确定位**：在样式化嵌套元素（如字段标签或长说明）时，请使用左侧的“选择器”面板，而不是单击画布。 这将确保以适当的特定方式生成正确的CSS选择器。
* **避免使用其他主题中的资产**：编辑主题时，请勿浏览并添加其他主题中的资产（如图像）。 如果移动或删除源主题，则当前主题将中断。
* **不更改容器面板布局宽度**：在容器面板上指定固定宽度会使其成为静态状态并阻止其适应不同的屏幕大小。

## 另请参阅 {#see-also}

{{see-also}}