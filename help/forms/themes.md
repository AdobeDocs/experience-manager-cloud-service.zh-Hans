---
title: 创建和使用主题
description: 您可以使用主题来风格化自适应表单并提供可视标识。 您可以在任意数量的自适应Forms中共享主题。
exl-id: 99c3d1f7-5756-49d2-98ee-72dd62063110
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '5494'
ht-degree: 1%

---

# 创建和使用主题 {#creating-and-using-themes}

您可以创建并应用主题以风格化自适应表单<!-- or an interactive communication-->. 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式将反映在相应的组件上。 主题是独立管理的，不引用自适应表单<!-- or interactive communication -->.

您可以下载并安装 [!DNL AEM Forms] 引用内容包 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 用于将引用主题和模板导入环境的门户。

## 创建、下载或上传主题 {#creating-downloading-or-uploading-a-theme}

主题将创建并另存为单独的实体，以及诸如自适应Forms之类的元属性。 它允许在多个自适应Forms中重用主题<!-- or  and interactive communications-->. 您还可以将主题移动到其他实例并重复使用。

### 创建主题 {#creating-a-theme}

要创建主题，请执行以下操作：

1. 单击 **[!UICONTROL Adobe Experience Manager]**，单击 **[!UICONTROL Forms]**，然后单击 **[!UICONTROL 主题]**.

1. 在“主题”页面中，单击 **[!UICONTROL 创建]** > **[!UICONTROL 主题]**.
将启动创建主题的向导。

1. 指定 **[!UICONTROL 名称]** 主题。

1. 指定用于预览 **[!UICONTROL 此主题的默认预览]** 字段。 单击 **[!UICONTROL 使用默认值]** 以使用默认表单预览主题。

1. 指定 **[!UICONTROL 配置容器]**. 您可以选择 **[!UICONTROL 配置容器]** ，其中包含帐户Adobe字体的配置详细信息。 您还可以将选项暂时留空，然后在 [主题属性](#metadata-of-a-theme).

1. 单击 **[!UICONTROL 创建]** 然后单击 **[!UICONTROL 编辑]** 要在主题编辑器中打开主题，或单击 **[!UICONTROL 完成]** ，以返回到主题页面。

### 与Experience Manager6.5 Forms和先前版本中的主题不同 {#difference-in-themes}

在Cloud Service实例上创建的主题：

* 具有版本号2。

* 存储在 `/content/dam/formsanddocuments-themes/<theme-name>/`

* 不提供客户端库选项。 您无法指定客户端库类别和路径。

* 对/apps位置没有写入和更新权限(Forms用户组对/apps位置没有写入和更新权限)。

* 在上传创建的主题之前 [!DNL Experience Manager Forms] 6.5或更早版本到Cloud Service实例，请确保将客户端库位置设置为 `etc/clientlibs/fd/themes`. 如果 `etc` 文件夹，手动将位置更新为 `etc/clientlibs/fd/themes`.  您可以在 [!DNL Experience Manager Forms] 6.5或更早版本的实例。 在设置客户端库的位置后，管理员可以将主题上传到Cloud Service实例，或使用内容传输工具将主题从6.5或以前的版本实例迁移到Cloud Service实例。

   此外，更改类别的名称。 如果名称未更改，则会出现错误 `theme with same category name exists` 可能会发生。 更改类别名称时，不会影响使用该主题的自适应Forms。

### 下载主题 {#downloading-a-theme}

您可以将主题导出为zip文件，并在其他项目或Experience Manager实例中使用这些主题。 要下载主题，请执行以下操作：

1. 单击 **[!UICONTROL Adobe Experience Manager]**，单击 **[!UICONTROL Forms]**，然后单击 **[!UICONTROL 主题]**.

1. 在“主题”页面中， **[!UICONTROL 选择]** 主题，然后单击 **[!UICONTROL 下载]**. 将显示一个包含主题详细信息的对话框。

1. 单击 **[!UICONTROL 下载]**. 主题将下载为zip文件。

>[!NOTE]
>
>如果您下载的主题与自适应表单相关联且关联的自适应表单基于自定义模板，则还应下载自定义模板。 在上传下载的主题和自适应表单时，还应上传相关的自定义模板。

### 上传主题 {#uploading-a-theme}

具有管理员权限的用户可以上传在中创建的主题 [!DNL Experience Manager Forms] 6.5或更早版本。

要上传主题，请执行以下操作：

1. 单击 **[!UICONTROL Adobe Experience Manager]**，单击 **[!UICONTROL Forms]**，然后单击 **[!UICONTROL 主题]**.

1. 在“主题”页面中，单击 **[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**.
1. 在“文件上载”提示中，浏览并选择您计算机上的主题包，然后单击 **[!UICONTROL 上传]**.
已上传的主题可在主题页面中使用。

## 主题的元数据 {#metadata-of-a-theme}

主题的元属性列表（可在主题的属性页面中找到）。

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>名称</strong></th>
   <th><strong>可以编辑</strong></th>
   <th><strong>属性描述</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>标题</td>
   <td>是</td>
   <td>显示主题的名称。</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>描述</td>
   <td>是</td>
   <td>有关主题的描述。</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>类型</td>
   <td>否</td>
   <td>
    <ul>
     <li>资产类型。</li>
     <li>值始终为主题。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>创建时间</td>
   <td>否</td>
   <td>主题创建日期</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>作者名称</td>
   <td>是</td>
   <td>主题的作者。 在主题创建时计算。</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>上次修改日期</td>
   <td>否</td>
   <td>上次修改主题的日期。</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>状态</td>
   <td>否</td>
   <td>主题的状态（已修改/已发布）。</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>按时发布</td>
   <td>是</td>
   <td>自动发布主题的时间。</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>发布关闭时间</td>
   <td>是</td>
   <td>该自动取消发布主题了。</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>标记</td>
   <td>是</td>
   <td>附加到主题的标签，用于标识，用于改进搜索。</td>
  </tr>
  <!-- <tr>
   <td>11.</td>
   <td>References</td>
   <td>Links</td>
   <td>
    <ul>
     <li>Contains 'Referred by' section. Lists forms that use the theme.</li>
     <li>Since the theme does not refer to any other asset, there is no 'Refers' section.</li>
    </ul> </td>
  </tr>
   <tr>
   <td>12.</td>
   <td>Clientlib Location</td>
   <td>Yes</td>
   <td>
    <ul>
     <li>The user-defined repository path within '/etc' where the clientlibs corresponding to this theme are stored.</li>
     <li>Default value - '/etc/clientlibs/fd/themes' + relative path of theme asset.</li>
     <li>If the location does not exist, the folder hierarchy is auto-generated.</li>
     <li>When this value is changed, the clientlib node structure is moved to the new location entered.<br /> <em><strong>Note:</strong> If you change default clientlib location, in the CRXDE repository assign <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>to <code>forms-users</code> and <code>crx:replicate</code>, <code>jcr:read </code>to <code>fd-service</code> in the new location. Also attach another ACL by adding <code>deny jcr:addChildNodes</code> for <code>forms-user</code></em></li>
    </ul> </td>
  </tr> 
  <tr>
   <td>13.</td>
   <td>Clientlib Category Name</td>
   <td>Yes</td>
   <td>
    <ul>
     <li>The user-defined clientlib category name for this theme.</li>
     <li>An error is displayed if the name is already in use by some other existing theme.</li>
     <li>Default value - computed using theme location.</li>
     <li>When this value is changed, the category name is updated on the corresponding clientlib node. Updating Clientlib Category Name in the jsp files is not required because clientlib category name is used by reference.</li>
    </ul> </td>
  </tr> -->
 </tbody>
</table>

## 关于主题编辑器 {#about-the-theme-editor}

主题编辑器是企业用户和Web设计人员/开发人员友好界面，提供指定各种自适应表单样式所需的功能 <!-- and interactive communication --> 元素。 在创建主题时，该主题将作为单独的实体（如表单）存储 <!--  , interactive communications, letters, document fragments, and data dictionaries-->.

通过主题编辑器，您可以自定义在主题中设置样式的组件的样式。 您可以自定义表单的方式 <!-- or interactive communication --> 在设备上查看。

主题编辑器分为两个面板：

* **画布**  — 显示在右侧。 它显示了自适应表单的示例 <!--  or interactive communication --> 所有样式变化都能即时反映。 您还可以直接从画布中选择对象，以查找与其关联的样式，并编辑这些样式。 顶部的设备分辨率标尺控制画布。 从标尺中选择分辨率断点会显示示例表单的预览 <!--  or interactive communication --> 以获得相关决议。 画布将详细讨论 [下面](themes.md#using-canvas).

* **侧栏** — 显示在左侧。 具有以下项目：

   * **选择器：** 显示为样式选择的组件及其可设置样式的属性。 选择器表示类型的所有组件。 如果选择主题中的文本框组件来进行样式设置，则表单中的所有文本框都将 <!-- or interactive communication --> 继承样式。 选择器允许您选择通用组件或特定组件以进行样式设置。 例如，字段组件是通用组件，而文本框是特定组件。

      **为通用组件设置样式：**
字段可以是数字框字段（如年龄）或文本框字段（如地址）。
设置字段样式时，所有字段（如年龄、名称、地址）都会设置样式。

      **为特定组件设置样式**:特定组件会影响特定类别的对象。 设置主题中数字框组件的样式时，只有中的数字框对象会继承该样式。

      例如，文本框字段（如地址）越长，数字框字段（如年龄）越短。 您可以选择数字框字段、缩短其长度并应用于表单。 表单中所有数字框字段的宽度都会减小。

      使用特定背景颜色自定义所有字段组件时，所有字段（如年龄、名称和地址）都会继承背景颜色。 当您选择数字框（如年龄）并减小其宽度时，所有数字框（如年龄）的宽度会减少，家庭中的人数也会减少。 文本框的宽度不会更改。

   * **州：** 用于自定义处于特定状态的对象的样式。 例如，您可以指定对象处于默认、集中、禁用、悬停或错误状态时的外观。
   * **属性类别：** 样式属性分为不同的类别。 例如Dimension和位置、文本、背景、边框和效果。 在每个类别下，提供样式信息。 例如，在“背景”下，您可以提供“背景颜色”和“图像和渐变”。

   * **高级：** 允许您向对象添加自定义CSS，该对象将覆盖在存在重叠时定义的可视化控件属性。

   * **查看CSS**:允许您查看所选组件的CSS。
   此外，在侧栏中，底部还显示一个箭头。 单击箭头时，您会再获得两个选项： **模拟成功** 和 **模拟错误。** 这些选项以及上述选项将进行详细讨论 [下面](themes.md#using-rail).

[ ![主题编辑器](assets/themes.png)](assets/themes-1.png) **A.** 侧栏 **B.** 画布

### 设置组件样式 {#styling-components}

您可以在多个自适应Forms中使用主题<!-- and interactive communications -->，可导入您在主题中指定的组件格式。 您可以设置各种组件的样式，如标题、描述、面板、字段、图标和文本框。 使用小组件在主题中配置组件属性。 虽然“CSS覆盖”部分允许您编写CSS代码或提供自定义选择器，但并非要求您事先了解CSS或LESS。 在侧栏中选择组件时，将显示“CSS覆盖”部分。

![侧栏中的可样式组件](assets/stylable-components.png)

允许您选择和设置不同组件样式的侧栏中的选项。

单击侧栏中某个组件所对应的编辑按钮，将在画布中选择该组件，并允许您使用侧栏中的选项来设置组件样式。

某些组件（如文本框、数字框、单选按钮和复选框）被分类到“字段”等通用组件下。 例如，您要自定义单选按钮的样式。 要选择用于样式设置的单选按钮，请选择 **[!UICONTROL 字段]** > **[!UICONTROL 构件]** > **[!UICONTROL 单选按钮]**.

### 样式面板布局 {#styling-panel-layouts-br}

主题 [!DNL AEM Forms] 支持表单中面板布局中元素的样式<!-- and  interactive communications -->. 支持现成布局和自定义布局中元素的样式。

现成面板包括：

* 左侧选项卡
* 顶部选项卡
* 折叠
* 响应
* 向导
* 移动设备布局

   * 标题中的面板标题
   * 标题中没有面板标题

每种布局的选择器各不相同。
主题编辑器中的自定义布局样式涉及：

* 为可设置样式的布局定义组件，以及CSS选择器，用于唯一标识这些组件。
* 定义可应用于这些组件的CSS属性。
* 从用户界面以交互方式定义这些组件的样式。

### 不同屏幕大小的不同样式 {#different-styles-for-different-screen-sizes-br}

桌面和移动设备布局的样式可能略有不同或完全不同。 对于移动设备，平板电脑和手机共享相似的布局，但组件大小除外。

使用主题编辑器断点为不同屏幕大小定义替代样式。 您可以选择开始构建主题的基本设备或分辨率，并且系统会自动生成其他分辨率的样式变体。 您可以明确修改所有分辨率的样式。

>[!NOTE]
>
>首先使用表单创建主题<!-- or interactive communication-->，然后应用于不同的表单<!-- or interactive communications-->. 主题创建中使用的断点可能与表单不同 <!-- or interactive communication --> 主题。 CSS媒体查询基于表单 <!-- or interactive communication --> 在主题创建中使用，而不是表单 <!-- or interactive communication --> 主题。

### 选择对象时，侧栏中的样式属性上下文会发生更改 {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

在画布中选择组件时，其样式属性会列在侧栏中。 选择对象类型及其状态，然后提供其样式。

### 主题编辑器中最近使用的样式 {#recently-used-styles-in-theme-editor}

主题编辑器最多可缓存应用于组件的十种样式。 您可以将缓存的样式与主题的其他组件一起使用。 最近使用的样式将作为列表框显示在侧栏中选定组件的正下方。 最初，最近使用的样式列表为空。

![资产库](assets/asset-library.png)

在设置组件样式时，将在列表框中缓存并列出样式。 在本例中，文本框的标签已设置样式以更改字体大小和颜色。 您可以按照类似的步骤选择图像或更改颜色以设置组件样式。 观察更改字段标签样式时如何在列表框中缓存和列出样式。

![为可供其他组件使用的组件缓存的字体样式](assets/font-style-cached1.png)

在此示例中，字段标签的样式已更改，为样式选择响应面板描述时，资产库中会添加一个列表条目。 资产库中的条目可用于更改响应式面板描述的样式。

在资产库中添加样式后，该样式可用于其他主题和 [样式模式](inline-style-adaptive-forms.md) 表单编辑器UI的URL中。 同样，当您使用表单编辑器的样式模式时 <!-- or interactive communication editor --> 为组件设置样式的UI，会缓存样式，并在主题中可用。

利用资产库对应的加号按钮，可使用您提供的名称永久保存样式。 即使您未单击侧栏中的“保存”按钮以将样式应用于组件，加号按钮仍会保存样式。 样式模式中不提供用于保存样式以供日后使用的加号按钮。

![为资产库提供自定义样式名称](assets/custom-style-name.png)

当您为样式提供自定义名称时，该样式将绑定到主题，不再可用于其他主题。 要删除保存的样式，请执行以下操作：

1. 在“画布”工具栏上，单击 **[!UICONTROL 主题选项]** ![主题选项](assets/theme-options.png) > **[!UICONTROL 管理样式]**.
1. 在“管理样式”对话框中，选择保存的样式，单击 **[!UICONTROL 删除]**.

   ![删除保存的样式](assets/manage-styles.png)

### 实时预览、保存和放弃更改 {#live-preview-save-and-discard-changes}

对样式所做的修改会立即反映在表单中 <!-- or interactive communication --> 加载到画布中。 实时预览允许您以交互方式定义并查看样式的影响。 更改组件的样式时， **[!UICONTROL 完成]** 按钮。 要保留更改，请使用 **[!UICONTROL 完成]** 按钮。

>[!NOTE]
>
>在字段中输入无效字符时，字段边界颜色将变为红色，屏幕左上角会显示一条错误消息。 例如，如果在接受数字字符作为输入的文本框中输入字母，则输入框边界颜色将更改为红色。 如果不解决屏幕中心底部显示的错误，则无法保存此类主题。

### 包含其他自适应表单的主题 {#theme-with-another-adaptive-form}

创建主题时，会使用主题编辑器附带的表单进行创建。 您可以在此表单中为组件提供样式。 您可以选择表单，而不是主题编辑器附带的表单 <!-- or interactive communication --> 提供样式并预览其结果。

替换当前表单或 <!-- interactive communication --> 在主题编辑器画布中：

1. 在“主题编辑器”面板中，单击 **[!UICONTROL 主题选项]** ![主题选项](assets/theme-options.png) > **[!UICONTROL 配置]**.

1. 在“常规”选项卡中，浏览并选择表单 <!-- or interactive communication --> 对于 **[!UICONTROL 自适应表单]** 字段。

### 重做/撤消 {#redo-undo}

您可以撤消或重做意外发生的不需要的更改。 在画布中使用重做/撤消按钮。

![重做和撤消操作](assets/redo_undo_new.png)

在主题编辑器中设置组件样式时，会显示重做/撤消按钮。

## 使用主题编辑器 {#using-the-theme-editor}

利用主题编辑器，可编辑您创建或上传的主题。 导航到 **[!UICONTROL Forms和文档]** > **[!UICONTROL 主题]**，然后选择一个主题并将其打开。 主题在主题编辑器中打开。

如上所述，主题编辑器有两个面板：侧栏和画布。
![主题编辑器](assets/theme-editor.png)

在主题编辑器中自定义文本框小组件的成功状态样式。 组件在画布中处于选中状态，并在侧栏中处于选中状态。 侧栏中可用的样式选项用于自定义组件的外观。

### 使用画布 {#using-canvas}

主题是使用现成表单创建的，还是使用表单创建的 <!-- or interactive communication --> 你选的。 画布显示表单或 <!-- interactive communication --> 用于通过主题中指定的自定义创建主题。 表格上方的标尺用于根据设备的显示大小确定布局。

在“画布”工具栏中，您会看到：

* **[!UICONTROL 切换侧面板]** ![切换侧面板](assets/toggle-side-panel.png):允许您显示或隐藏侧栏。
* **[!UICONTROL 主题选项]** ![主题选项](assets/theme-options.png):提供三个选项

   * 配置：提供用于选择预览表单的选项 <!-- or interactive communication , base clientlib, -->和Adobe Fonts配置。
   * 查看主题CSS:为所选主题生成CSS。
   * 管理样式：提供用于管理文本和图像样式的选项
   * 帮助：运行主题编辑器的图像指导教程。

* **[!UICONTROL 模拟器]** ![标尺](assets/ruler.png):模拟不同显示大小的主题外观。 在模拟器中，显示大小被视为断点。 您可以选择断点并为其指定样式。 例如，台式机和平板电脑是两个断点。 您可以为每个断点指定不同的样式。

在画布中选择组件时，您会在其顶部看到组件工具栏。 组件工具栏允许您选择组件或切换到通用组件。 例如，在面板中选择一个数字文本框。 您会在组件工具栏中看到以下选项：

* **[!UICONTROL 数字框小组件]**:允许您选择组件以自定义其在侧栏中的外观。
* **[!UICONTROL 字段小组件]**:允许您选择用于样式的通用组件。 在此示例中，将选择所有文本输入组件（文本框/数字框/数字步进器/日期输入）以进行样式设置。

* ![字段级别](assets/select_parent_icon.svg):允许您选择父组件以进行样式设置。 如果选择数字框并点按此图标，则会选择字段组件。 如果选择字段组件并点按此图标，则会选择面板。 如果您继续点按此图标进行选择，则最终会选择样式布局。

>[!NOTE]
>
>组件工具栏中可用的选项因您选择的组件而异。

### 使用侧栏 {#using-rail}

主题编辑器中的侧栏提供了用于自定义主题中组件样式和使用选择器的选项。 选择器允许您选择一组组件或单个组件，并且您可以在侧栏中搜索选择器。 您可以为自定义组件编写选择器。

当您从侧栏的画布或选择器中选择组件时，侧栏会显示允许您为其自定义样式的所有选项。
以下是您在选择组件时在侧栏中看到的选项：

* 状态
* 属性表
* 模拟错误/成功

#### 状态 {#state}

状态是用户与组件交互的指标。 例如，当用户在文本框中输入错误数据时，文本框的状态将变为错误状态。 主题编辑器允许您指定特定状态的样式。

自定义状态样式的选项因组件而异。

#### 属性表 {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>用法</strong></td>
  </tr>
  <tr>
   <td><p>尺寸及位置</p> </td>
   <td><p>允许您设置主题中组件的对齐方式、大小、位置和放置样式。 </p> <p>您的选项包括显示设置、内边距、边距、宽度、高度和Z索引。</p> <p>您还可以使用布局模式通过简单的拖放界面定义组件的宽度。 有关更多信息，请参阅 <a href="resize-using-layout-mode.md">使用布局模式调整组件大小</a>.</p> </td>
  </tr>
  <tr>
   <td><p>文本</p> </td>
   <td><p>用于自定义主题组件中的文本样式。</p> <p>例如，您希望更改在文本框中输入文本的外观。</p> <p>您的选项包括字体系列、粗细、颜色、大小、行高、文本对齐、字母间距、文本缩进、下划线、斜体、文本转换、垂直对齐、基线和方向。 </p> </td>
  </tr>
  <tr>
   <td><p>背景 </p> </td>
   <td><p>用于使用图像或颜色填充组件的背景。 </p> </td>
  </tr>
  <tr>
   <td><p>边框</p> </td>
   <td><p>允许您选择组件边框的外观。 例如，您希望文本框具有深红色的粗边框，边框带虚线。 </p> <p>您的选项包括边框的宽度、样式、半径和颜色。</p> </td>
  </tr>
  <tr>
   <td><p>效果</p> </td>
   <td><p>允许您为组件添加特殊效果，如不透明度、混合模式和阴影。 </p> </td>
  </tr>
  <tr>
   <td><p>高级</p> </td>
   <td><p>允许您添加：</p>
    <ul>
     <li>属性 <code>::before</code> 和 <code>::after</code> 用于在选择器中默认内容之后或之前添加内容的伪元素，并设置其样式。<br /> 请参阅 <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">CSS伪元素</a>.</li>
     <li>组件内联的自定义CSS代码。</li>
    </ul> <p>添加自定义CSS代码时，它会覆盖您使用侧栏中的选项添加的自定义设置。 </p> </td>
  </tr>
 </tbody>
</table>

#### 模拟错误/成功 {#simulate-error-success}

“模拟错误”和“成功”选项在侧栏底部可用。 您可以使用侧栏底部显示的显示/隐藏箭头来查看它们。 使用主题编辑器，您可以设置组件的各种状态样式。

例如，在表单中添加一个数字字段，并在主题编辑器中指定其样式。 当用户在字段中键入字母数字值时，您希望文本框的背景颜色发生更改。 在主题中选择数字字段，然后使用侧栏中的状态选项。 在侧栏中选择“错误”状态，然后将背景颜色更改为红色。 要预览行为，您可以使用侧栏中提供的“模拟错误”选项。 “模拟错误”和“成功”选项的详细描述如下：

* **模拟成功**:如果为成功状态指定组件的样式，则可让您查看组件的外观。 例如，在表单中，客户设置了密码。 用户可以根据您提供的准则设置密码。 如果用户键入密码时遵循您提供的所有准则，文本框将变为绿色。 当文本框变为绿色时，它处于成功状态。 您可以为处于成功状态的组件指定样式，并使用模拟成功选项模拟其外观。

* **模拟错误**:如果为错误状态指定组件的样式，则允许您查看组件的外观。 例如，在表单中，客户设置了密码。 用户可以根据您提供的准则设置密码。 当用户键入的密码不符合您提供的所有准则时，文本框将变为红色。 当文本框变为红色时，它处于错误状态。 您可以为处于错误状态的组件指定样式，并使用“模拟错误”选项模拟其外观。

### 为组件设置样式 {#styling-a-component}

例如，在您的表单中，您有两种类型的文本框：仅接受数字值的，或接受字母数字值的。 您可以为仅接受数值（数字框）的文本框自定义样式。

要自定义特定组件的样式（此示例中的数字框），请执行以下步骤：

1. 在主题编辑器中，在画布中选择数字框。
1. 选择数字框时，您可以看到包含三个选项的组件工具栏：

   * **[!UICONTROL 数值框小组件]**
   * **[!UICONTROL 字段小工具]**

1. 选择 **[!UICONTROL 数字框小组件]**.
1. 侧栏标题会更改为数字框小组件，并显示用于自定义其外观的选项。
使用 **[!UICONTROL Dimension和位置]** 选项来自定义组件的大小。 确保国家 **[!UICONTROL 默认]**.

而不是选择 **[!UICONTROL 数字框小组件]**，选择 **[!UICONTROL 字段小组件]** ，然后执行上述步骤。 在为 **[!UICONTROL 字段小组件]** 选项，除数字框外，所有文本框的大小都相同。

### 给定状态的样式字段 {#styling-fields-given-state}

通过组件工具栏，您还可以为组件的不同状态指定组件样式。 例如，如果某个组件处于禁用状态，则该组件将处于禁用状态。 可在主题编辑器中设置样式的组件的常用状态包括：默认、集中、禁用、错误、成功和悬停。 您可以在画布中选择组件，然后使用侧栏中的状态选项来自定义其外观。

要自定义组件在特定状态中的样式，请执行以下步骤：

1. 在画布中选择一个组件，然后从组件工具栏中选择相应的选项。
侧栏显示用于自定义组件样式的选项。
1. 在侧栏中选择状态。 例如，错误状态。
1. 使用选项，例如 **[!UICONTROL 边框、背景]** 自定义组件的外观。
1. 使用 **[!UICONTROL 模拟错误]** 选项来查看编辑样式的外观。

在指定组件状态后自定义组件的样式时，仅针对指定状态显示组件的自定义设置。 例如，如果在选择悬停状态时自定义组件的样式。 当您在呈现的表单中的组件上移动指针时，会为组件显示自定义设置 <!-- or interactive communication --> 将主题应用到其中。

要模拟除错误和成功以外的状态行为，请使用预览模式。 要使用预览模式，请单击 **[!UICONTROL 预览]** 中。

### 小显示器的样式布局 {#styling-layouts-for-smaller-displays}

在画布中使用标尺为显示屏较小的设备选择断点。 单击模拟器 ![标尺](assets/emulator-icon.svg) 在画布中查看标尺和断点。 断点允许您预览表单 <!-- or interactive communication --> 用于与不同设备（如手机和平板电脑）相关的显示大小。 主题编辑器支持多种显示大小。

要为不同断点设置组件样式，请执行以下操作：

1. 在画布中，选择标尺上方的断点。
断点表示移动设备及其显示大小。
1. 使用侧栏自定义表单的样式 <!-- or interactive communication --> 主题中的组件，显示选定的显示大小。
1. 确保保存自定义设置。

您可以设置表单样式 <!-- or interactive communication --> 组件。 表单 <!-- and interactive communication --> 适用于台式机和移动设备的组件可能具有完全不同的样式。

### 在主题中使用Web Fonts {#using-web-fonts-in-a-theme}

现在，您可以在自适应表单中使用Web服务中提供的字体 <!-- or interactive communication -->. 现成， [Adobe Fonts](https://fonts.adobe.com/),Adobe的web字体服务可用作配置。 要使用Adobe Fonts，请创建一个工具包，在其中添加字体，然后从 [Adobe Fonts](https://fonts.adobe.com/).

要在Experience Manager中配置Adobe Fonts，请执行以下步骤：

1. 在创作实例中，单击 ![Adobe Experience Manager](assets/adobeexperiencemanager.png)**[!UICONTROL Adobe Experience Manager ]**>**[!UICONTROL &#x200B;工具&#x200B;]**![锤子](assets/hammer.png) >**[!UICONTROL &#x200B;部署&#x200B;]**>**[!UICONTROL  Cloud Services ]**.
1. 在 **[!UICONTROL Cloud Services]** 页面，导航到并打开 **[!UICONTROL Adobe Fonts]** 选项。 打开配置文件夹，然后单击 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，指定配置的标题，然后单击 **[!UICONTROL 创建]**.

   系统会将您重定向到配置页面。

1. 在显示的编辑组件对话框中，提供您的工具包ID并单击 **[!UICONTROL 确定]**.

要配置主题以使用Adobe Fonts配置，请执行以下步骤：

1. 在创作实例中，在主题编辑器中打开一个主题。
1. 在主题编辑器中，导航到 **[!UICONTROL 主题选项]** ![主题选项](assets/theme-options.png) > **[!UICONTROL 配置]**.
1. 在 **[!UICONTROL Adobe Fonts配置]** 字段，选择工具包，然后单击 **[!UICONTROL 保存]**.

   现在，您可以看到这些字体已添加到主题的font-family属性中。

<!-- >
### Listing and selecting fonts in theme editor {#listing-and-selecting-fonts-in-theme-editor}

You can use the theme configuration service to add more fonts to the theme editor. Perform the following steps to add fonts:

1. Log in to Experience Manager Web Console with administrative privileges. URL for the Experience Manager Web Console is `https://'[server]:[port]'/system/console/configMgr`.
1. Open **[!UICONTROL Adaptive Form Theme Configuration Service]**.

   ![theme-config](assets/theme-config.png)

1. Click +, specify the name of the font, and click **Save**. The font is added and available in theme editor. -->

#### 在主题编辑器中选择字体 {#selecting-fonts-in-theme-editor}

您可以使用+按钮添加字体。 添加字体时，该字体会列在侧栏中。

![主题编辑器中列出的新字体](assets/theme-font.png)

除了主题配置选项之外，您还可以从主题编辑器本身添加字体。 在侧栏下的字体系列字段中键入要使用的字体，然后按键盘上的返回键。

![在主题编辑器中键入和选择字体](assets/font-selection.png)

选择字体时，该字体会添加到字体系列列表下。 您可以使用主题编辑器中的“蒙版”选项来禁用或启用列出的字体。

![多字体](assets/multi-fonts.jpg)

您可以看到组件字体更改。

“字体系列”字段支持多种字体。 键入字体时，浏览器会查找该字体并将其应用于选定的组件。 如果浏览器找不到字体，则会在系列中查找该字体旁边的字体。 您可以首先键入要查找的特定字体。 如果找不到要使用的字体，可以在族中键入通用字体并使用该字体。

#### 在主题编辑器中应用的蒙版样式 {#mask-styles-applied-in-theme-editor}

您可以掩盖在主题中应用的样式。 在主题编辑器侧栏中，您可以使用 ![toggle_eye](assets/toggle_eye.png)图标来禁用应用的样式。 例如，如果在表单中更改组件的维度 <!-- or interactive communication -->，则可以使用属性左侧的蒙版按钮来禁用该功能。 保存主题时，将保留选定的掩码选项。

![主题编辑器侧栏中可用的掩码选项](assets/mask-styles.png)

以下示例显示了主题中已蒙版和未蒙版的样式。

![蒙版和未蒙版的样式](assets/mask2.png)

## 将主题应用于表单 {#applying-a-theme-to-a-form-or-interactive-communication-br}

要将主题应用到自适应表单，请执行以下操作：

1. 在编辑模式下打开您的表单。 要在编辑模式下打开表单，请选择一个表单，然后单击 **[!UICONTROL 打开]**.
1. 在编辑模式下，选择一个组件，然后单击 ![字段级别](assets/select_parent_icon.svg) > **[!UICONTROL 自适应表单容器]**，然后单击 ![cppr](assets/cmppr.png).

   您可以在侧栏中编辑表单的属性。

1. 在侧栏中，单击 **[!UICONTROL 样式]**.
1. 从 **[!UICONTROL 自适应表单主题]** 下拉菜单并单击 **[!UICONTROL 完成]** ![check-button](assets/check-button.png).

您还可以在创建自适应表单时为其定义主题。

<!-- To apply a theme to an interactive communication:

1. Open your interactive communication in edit mode. To open a interactive communication in edit mode, select a form and click **Open**.
1. In the edit mode, select a component, then click ![field-level](assets/field-level.png) &gt;**Document Container**, and then click ![cmppr](assets/cmppr.png).

   You can edit properties of your form in the sidebar.

1. In the sidebar, under **Basic**, select your theme from the **Theme** drop-down and click **Done** ![check-button](assets/check-button.png) -->

### 在运行时更改表单的主题 {#change-theme-of-a-form-at-runtime}

主题样式表单中的不同组件。 您可以使用 `themeOverride` 属性来动态更改表单的主题。 表单的典型URL是：

`https://<server>:<port>/content/forms/af/test.html`

您可以使用themeOverride参数在运行时应用主题。

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

的 `themeOverride` 选项可让您提供主题的路径。 它会更改表单的主题，并使用更新的样式刷新表单。

## 使用主题获取特定外观 {#specific-af-appearance}

使用 [!DNL AEM Forms]，以及默认的现成画布主题，还有许多其他主题。 如果要设计表单 <!-- or interactive communication --> 使用其他主题以及更多更改，从主题库文件夹复制主题。 将复制的主题粘贴到“主题库”文件夹之外，然后根据所需的更改编辑复制的主题。

要复制主题，请执行以下步骤：

1. 在创作实例中，导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主题]**.
1. 打开主题库文件夹。
1. 在“主题库”文件夹中，将指针悬停在相应的现成主题上，然后点按 **[!UICONTROL 复制]**.
1. 将复制的主题粘贴到“主题库”文件夹之外。
1. 自定义复制的主题。

自定义主题后，将其应用于表单 <!-- or interactive communication -->.

>[!NOTE]
>
>请勿修改“主题库”文件夹中可用的主题。 此文件夹包含系统主题。 在安装的 [!DNL AEM Forms].

## 对其他自适应表单用例的影响 {#impact-on-other-adaptive-form-use-cases}

* **发布/取消发布表单：** 在发布表单时，也会发布应用于的主题（如果尚未发布）
* **导入/导出表单：** 导入或导出表单时，其关联的主题也会自动导入或导出。
* **表单的引用：** 表单引用中的引用部分包含主题的额外条目。
* **表单的上次修改时间：** 更新了关联的主题。
<!-- * **A/B Testing:** You can apply a different theme to two versions of the form in A/B testing. The information of the two themes is individually stored on the two guide containers. -->

## CSS生成序列 {#css-generation-sequence}

选择查看CSS时，主题编辑器会收集所有样式信息并构建CSS。 它按以下顺序收集信息：

<!-- 1. Styling defined in the theme's base client library. -->
1. 用户定义的样式，使用侧栏中的属性指定。
1. 使用“CSS覆盖”选项提供的CSS样式。

例如，文本框的背景颜色为蓝色<!-- in the base client library-->. 您可以使用侧栏中的属性将其更改为粉红色。 生成CSS时，您会看到文本框的背景颜色为粉红色。 使用属性更改背景颜色后，另一位作者使用CSS覆盖选项将背景颜色文本框更改为白色。 生成CSS时，在生成的CSS中，背景颜色显示为白色。

## 调试样式 {#debugging-styles}

在主题编辑器中指定组件样式时，将生成一个CSS。 设置通用组件的样式时，其中包含的多个组件也会设置样式。 例如，当您设置字段样式时，其中的文本框和标签也会设置样式。 设置字段中文本框的样式时，它会获得自己的CSS。 如果要调试为字段和组件生成的CSS，主题编辑器会提供用于查看CSS的选项。

您可以使用以下选项查看生成的CSS:

* **查看CSS** 选项：在主题中选择组件后，您可以在侧栏中看到“查看CSS”选项。 它显示生成的CSS，包括的CSS `::before` 和 `::after` 伪元素。
* **查看主题CSS** 选项：在画布工具栏中，单击 ![主题选项](assets/theme-options.png) > **[!UICONTROL 查看主题CSS]**. 您可以查看从在主题编辑器中定义的属性生成的整个主题CSS。

## 疑难解答、建议和最佳实践 {#troubleshooting-recommendations-and-best-practices}

* **避免使用其他主题中的资产**

   编辑主题时，您可以浏览其他主题中的资产（如图像）并添加这些资产。 例如，您正在编辑页面的背景。 例如，当您选择 **[!UICONTROL 页面]** ![edit-button](assets/edit-button.png)> **[!UICONTROL 背景]** > **[!UICONTROL 添加]** > **[!UICONTROL 图像]**&#x200B;时，您会看到一个对话框，通过该对话框可以浏览并添加其他主题中的图像。

* 如果从其他主题添加资产，而另一个主题被移动或删除，则您可能会遇到当前主题的问题。 建议您避免从其他主题浏览和添加资产。

<!-- * **Using base clientlib, theme editor, and inline styling**

    * **Base clientlib**:

      Base client library contains styling information. To use styling information in client-side libraries in themes.

        1. Navigate to **[!UICONTROL Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Themes]**.
        1. In the Themes page, select a theme and click **[!UICONTROL Properties]**.
        1. In the Properties page that opens, click **[!UICONTROL Advanced]**.
        1. In the Advanced tab, in the Clientlib Location field, browse, and select the client-library you want to use.
        1. Click **[!UICONTROL Save]**.

      The styling you specify in client library is imported in the theme that uses it. For example, you specify styling for text box, numeric box, and switch in the client library. When you import your client library in the theme, styling for text box, numeric box, and switch is imported. You can then style other components using theme editor. -->
    您还可以创建主题、创建主题副本，然后修改复制的主题中为类似用例提供的样式。
    请参阅[使用主题获取特定外观](#specific-af-appearance)
    
    * **主题编辑器：**
    
    主题编辑器允许您创建主题以设置表单的样式 &lt;!> — 或交互式通信 — >。 您可以在主题中指定组件的样式，以便在多个表单之间保持一致的外观 &lt;!> — 或交互式通信 — >您开发。 建议在主题中指定样式信息，然后将该主题应用到表单中。
    
    * **内联样式：**
    
    您可以在表单中使用样式模式来设置组件的样式 &lt;!> — 或交互式通信 — >使用表单时的多渠道编辑器。 使用样式模式更改表单组件样式将覆盖主题中指定的样式。 如果要更改特定表单中某些组件的样式，请参阅[组件的内联样式](inline-style-adaptive-forms.md)。

<!-- * **Using client-side libraries**

  If you want to create client libraries to import styling information, see [Using Client-Side Libraries](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/clientlibs.html). After you create a client library, you can import it in your theme using the steps mentioned above. -->

* **更改容器面板布局宽度**

   不建议更改容器面板布局宽度。 指定容器面板的宽度时，该面板会变为静态，且不会适应不同的显示。

* **何时使用表单编辑器或主题编辑器来处理页眉和页脚**

   如果要使用字体样式、背景和透明度等样式选项来设置页眉和页脚的样式，请使用主题编辑器。
如果要提供徽标图像、页眉中的公司名称以及页脚中的版权信息等信息，请使用表单编辑器选项。
