---
title: 如何为自适应Forms自定义自动生成的记录文档模板？
description: 了解如何使用Adobe Forms Designer下载、自定义和重新上传为自适应Forms自动生成的记录文档(DoR)模板。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
source-git-commit: 51ec9ef76a8f3f9b7bf2cdc25b03f72e286f586f
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---


# 自定义自动生成的记录文档模板

<span class="preview">本文适用于基于&#x200B;**核心组件**&#x200B;和&#x200B;**基础组件**&#x200B;的自适应Forms。</span>

在为自适应表单自动生成记录文档(DoR)时，AEM Forms会根据表单结构创建一个默认模板。 您可以自定义此自动生成的模板，以符合贵组织的品牌和布局要求。

自定义工作流包含三个步骤：

1. 从Forms Manager下载自动生成的DoR模板。
1. 使用Adobe Forms Designer修改模板。
1. 将自定义模板重新上传到AEM Forms并将其配置为自定义模板。

## 先决条件 {#prerequisites}

在开始之前，请确保您具备以下条件：

* 有权下载和上传模板以访问AEM Forms Manager。
* 已在本地计算机上安装Adobe Forms Designer。
* 已启用&#x200B;**[!UICONTROL 生成记录文档]**&#x200B;的自适应表单。

## 步骤1：下载自动生成的DoR模板 {#download-auto-generated-dor-template}

要为您的自适应表单下载自动生成的DoR模板（XDP文件），请执行以下操作：

1. 登录到您的AEM Forms创作实例。
1. 导航到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择要为其下载DoR模板的自适应表单。
1. 打开所选自适应表单的属性。
1. 在属性面板中，选择&#x200B;**[!UICONTROL 下载记录文档]**&#x200B;选项以下载自动生成的DoR模板（XDP文件）。
1. 将下载的XDP文件保存到本地计算机。


## 步骤2：使用Adobe Forms Designer自定义模板 {#customize-template-using-designer}

在Adobe Forms Designer中打开下载的XDP模板，并根据您组织的需求对其进行修改。

1. 在&#x200B;**Adobe Forms Designer**&#x200B;中打开下载的XDP文件。
1. 根据需要自定义模板。 自定义项的示例包括：

   * **多个母版页**：添加其他母版页以便为记录文档的特定页面定义不同的布局。 例如，使用带有公司抬头的独特第一页和布局更简单的后续页。
   * **字体颜色和字体系列**：更改字体颜色、大小和字体系列，以符合您的公司品牌准则。
   * **自定义元素**：添加公司徽标、页眉、页脚和免责声明文本等元素以建立一致的品牌标识。
   * **页面布局和样式**：调整边距、间距和整个页面结构以提高可读性。
   * **字段样式和位置**：修改表单字段的外观和位置以匹配您的首选布局。

1. 保存自定义的XDP模板。

>[!NOTE]
>
> 请勿删除或修改模板中存在的任何脚本。 修改脚本可能会影响数据绑定和记录文档的生成。

## 步骤3：将自定义模板重新上传到AEM {#reupload-customized-template}

自定义模板后，请将其上传到AEM Forms并配置自适应表单以使用它。

1. 将自定义XDP模板上传到您的AEM Forms实例：
   * 导航到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
   * 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 文件上传]**&#x200B;并上传自定义的XDP文件。

然后配置表单以使用自定义模板。 根据您的表单是基于核心组件还是基于基础组件，步骤会有所不同。

>[!BEGINTABS]

>[!TAB 核心组件]

对于基于核心组件的自适应Forms：

1. 在要应用自定义模板的编辑器中打开自适应表单。
1. 在内容树中，选择&#x200B;**[!UICONTROL 指南容器]** （根面板）。
1. 打开&#x200B;**[!UICONTROL 属性]**&#x200B;并单击&#x200B;**[!UICONTROL 记录文档]** (DoR)图标以打开记录文档属性。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，打开&#x200B;**[!UICONTROL 模板]**&#x200B;下拉菜单并选择&#x200B;**[!UICONTROL 自定义]**。
1. 浏览并选择上传的自定义XDP模板。
1. 选择要保存的复选标记。

   ![记录文档属性 — 模板设置为自定义（核心组件）](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB 基础组件]

对于基于基础组件的自适应Forms：

1. 在要应用自定义模板的编辑器中打开自适应表单。
1. 选择根面板（表单容器）。
1. 打开&#x200B;**[!UICONTROL 记录文档属性]**（从属性面板或DoR选项卡）。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，打开&#x200B;**[!UICONTROL 模板]**&#x200B;下拉菜单并选择&#x200B;**[!UICONTROL 自定义]**。
1. 浏览并选择上传的自定义XDP模板。
1. 选择要保存的&#x200B;**[!UICONTROL 完成]**。

   ![记录文档属性 — 模板设置为自定义（基础组件）](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

现在，自适应表单在生成记录文档时使用自定义模板。

## 验证自定义模板 {#verify-customized-template}

要确认已正确应用自定义模板，请执行以下操作：

1. 提交自适应表单的测试条目。
1. 生成记录文档。
1. 验证生成的PDF是否反映了您的自定义设置，包括徽标、字体、布局更改和其他品牌元素。

## 疑难解答 {#troubleshooting}

| 问题 | 解决方法 |
|---|---|
| 自定义模板未上传。 | 确保XDP文件有效且未损坏。 确认您具有将文件上传到AEM Forms所需的权限。 |
| 自定义项不会显示在生成的记录文档中。 | 确认您在表单属性的&#x200B;**[!UICONTROL 记录文档模板配置]**&#x200B;部分中选择了正确的自定义模板。 |
| 生成的PDF中存在布局或格式问题。 | 验证Adobe Forms Designer中的自定义是否遵循[基本模板约定](/help/forms/generate-document-of-record-core-components.md#base-template-conventions)。 确保所有元素都在模板结构中正确定位。 |

## 另请参阅 {#see-also}

* [生成自适应Forms记录文档（核心组件）](/help/forms/generate-document-of-record-core-components.md)
* [生成自适应Forms记录文档（基础组件）](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [记录文档的基础模板](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [自定义记录文档中的品牌信息](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)

