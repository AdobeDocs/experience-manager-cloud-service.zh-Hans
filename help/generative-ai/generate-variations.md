---
title: 生成变体
description: 了解可从 AEM as a Cloud Service 和 Edge Delivery Services 的 Sidekick 访问的生成变体功能
exl-id: 9114037f-37b9-4b2f-a714-10933f69b2c3
feature: Generate Variations
role: Admin, Architect, Developer
source-git-commit: bbc51796c610af02b5260c063213cde2ef610ba2
workflow-type: ht
source-wordcount: '3262'
ht-degree: 100%

---


# 生成变体 {#generate-variations}

如果您正在寻找一种方法来优化您的数字渠道并加速内容创作，您可以使用“生成变体”功能。生成变体功能使用生成式人工智能 (AI) 根据提示创建内容变体；这些提示由 Adobe 提供或由用户创建和管理。创建变体后，您可以在您的网站上使用这些内容，并使用 [Edge Delivery Services](/help/edge/overview.md) 的[实验](https://www.aem.live/docs/experimentation)功能衡量它们的成功。

您可以从以下位置[访问生成变体](#access-generate-variations)功能：

* [在 Adobe Experience Manager (AEM) as a Cloud Service 中](#access-aemaacs)
* [AEM Edge Delivery Services 的 Sidekick](#access-aem-sidekick)
* [在内容片段编辑器中](/help/sites-cloud/administering/content-fragments/authoring.md#generate-variations-ai)

>[!NOTE]
>
>在所有情况下，要使用生成变体功能，您必须确保满足[访问权限方面的先决条件](#access-prerequisites)。

之后您可以：

* [开始使用](#get-started) Adobe 为特定用例创建的提示模板。
* 您可以[编辑现有提示](#edit-the-prompt)
* 或者[创建并使用您自己的提示](#create-prompt)：
   * [保存您的提示](#save-prompt)以供将来使用
   * [访问并使用整个组织的共享提示](#select-prompt)
* 在[生成针对特定受众的个性化内容时](#generate-copy)，请定义提示中使用的[受众](#audiences)区段。
* 在进行修改和优化结果（如有必要）之前，请根据提示预览输出。
* 使用 [Adobe Express 根据副本变体生成图像](#generate-image)；这使用了 Firefly 的生成式 AI 功能。
* 选择您想要在您的网站或试验中使用的内容。

## 法律和使用说明 {#legal-usage-note}

AEM 的生成式 AI 和生成变体是强大的工具，但对输出结果的使用责任在于&#x200B;**您**。

您对服务的输入应该与上下文相关。此上下文可以是您的品牌材料、网站内容、数据、此类数据的架构、模板或其他受信任的文档。

您必须根据您的用例评估任何输出内容的准确性。

在使用“生成变体”之前，您需要同意 [Adobe Generative AI 用户指南](https://www.adobe.com/cn/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

[生成变体的使用](#generative-action-usage)与生成式操作的消耗相关。

## 概述 {#overview}

当您打开“生成变体”（并展开左侧面板）时，您会看到：

![生成变体 - 主面板](assets/generate-variations-main-panel.png)

* 右面板
   * 这取决于您在左侧导航中做出的选择。
   * 默认情况下显示&#x200B;**提示模板**。
* 左侧导航
   * 在&#x200B;**生成变体**&#x200B;的左侧，有一个选项（三明治菜单）可以展开或隐藏左侧导航面板。
   * **提示模板**：
      * 显示各种提示的链接；这些可以包括提示：
         * 由 Adobe 提供，帮助您生成内容；带有 Adobe 图标标记。
         * 您自己创建的。
         * 在您的 IMS 组织内创建的；用显示多个头像的图标标记。
      * 包括用于创建您自己的提示的[新提示](#create-prompt)链接。
      * 您可以&#x200B;**删除**&#x200B;您自己或在 IMS 组织内创建的提示。这是通过在相应信息卡上使用椭圆按钮进入菜单来完成的。
   * [收藏夹](#favorites)：显示您已标记为收藏夹的前几代结果。
   * [最近](#recents)：提供您最近使用过的提示及其输入的链接。
   * **帮助和常见问题解答**：文档链接，包括常见问题解答。
   * **用户指南**：法律指南的链接。

## 开始使用 {#get-started}

该界面将引导您完成生成内容的过程。打开界面之后，第一步就是选择要使用的提示。

### 选择提示 {#select-prompt}

从主面板上，您可以选择：

* 用于开始生成内容的由 Adobe 提供的提示模板，
* 用于创建您自己的提示的[新建提示](#create-prompt)，
* 您创建的仅供您使用的模板，
* 您或您组织中的某人创建的模板。

区分方法：

* Adobe 提供的提示带有 Adobe 图标
* 在您的 IMS 组织中，可用的提示会用多头像图标进行标记。
* 您的私人提示没有特别标记。

![生成变体 - 提示模板](assets/generate-variations-prompt-templates.png)

### 提供输入 {#provide-inputs}

每个提示都需要您提供某些信息，以便生成式 AI 能够返回适当的内容。

输入字段会引导您了解所需的信息。为了提供帮助，某些字段提供了默认值，您可以根据需要使用或修改，同时还有解释这些要求的具体描述。

有几个关键输入字段是多个提示所共有的（某些字段并不总是可用）：

* ****&#x200B;计数/****&#x200B;数量
   * 您可以选择在一代中创建多少个内容变体。
   * 根据提示，这可能带有各种标签之一；例如计数、变体数量、创意数量等。
* **受众来源**/**目标受众**
   * 有助于向特定受众生成个性化内容。
   * Adobe 提供默认受众；或者您可以指定其他受众；请参阅[受众](#audiences)。
* **其他背景信息**
   * 插入相关内容以帮助生成式 AI 根据输入做出更好的响应。例如，如果您正在为特定页面或产品创建 Web 横幅，您可能希望包含有关该页面/产品的信息。
* **温度**
用于修改 Adobe Generative AI 的温度：
   * 更高的温度会偏离提示，导致出现更多的变化、随机性和创造性。
   * 较低的温度更具确定性，并且更接近提示中的内容。
   * 默认情况下，温度设置为 1。如果生成的结果不符合您的喜好，您可以尝试不同的温度。
* **编辑提示**
   * 可以[编辑底层提示](#edit-the-prompt)以优化生成的结果。

### 生成副本 {#generate-copy}

填写输入字段和/或修改提示后，您就可以生成内容并查看响应了。

选择&#x200B;**生成**，查看生成式 AI 生成的响应。所生成的内容变体会显示在生成它们的提示下方。

![生成变体 - 生成副本](assets/generate-variations-generate-content.png)

>[!NOTE]
>
>大多数 Adobe 提示模板在变体响应中都包含一个 **AI 原理说明**。这提供了透明度，解释了为什么生成式 AI 会产生那个特定的变体。

当您选择单个变体时，可以执行以下操作：

* **收藏**
   * 标记为&#x200B;**收藏**，以供将来使用（将显示在[收藏夹](#favorites)）。
* 赞同/反对
   * 使用赞同/反对指示器来告知 Adobe 响应的质量。
* **复制**
   * 复制到剪贴板，以便在您的网站上创作内容时或在[试验](https://www.aem.live/docs/experimentation)中使用。
* **移除**

如果您需要优化输入或提示，可以进行调整，并再次选择&#x200B;**生成**&#x200B;以获取一组新的响应。新的提示和响应显示在初始提示和响应的下方；您可以上下滚动以查看不同的内容集。

在每组变体上方是创建它们的提示，以及一个&#x200B;**重复使用**&#x200B;选项。如果您需要重新运行一个带有输入的提示，请选择&#x200B;**重新使用**，以便在&#x200B;**输入**&#x200B;中重新加载它们。

### 生成图像 {#generate-image}

在生成文本变体之后，您可以使用 Firefly 的生成式 AI 功能在 Adobe Express 中生成图像。

>[!NOTE]
>
>**生成图像**&#x200B;仅在您拥有作为 IMS 组织一部分的 Adobe Express 授权，并在 Admin Console 中授予您访问权限时可用。

选择一个变体，然后执行&#x200B;**生成图像**&#x200B;操作，直接在 [Adobe Express](https://www.adobe.com/cn/express/) 中打开&#x200B;**文本转图像**&#x200B;功能。提示是根据您的变体选择预先填充的，并且图像会根据该提示自动生成。

![生成变体 - Express 图像](assets/generate-variations-express-images.png)

您可以做进一步的更改：

* [在 Adobe Express 中编写自己的提示](https://helpx.adobe.com/cn/firefly/using/tips-and-tricks.html)，描述您希望看到的内容，
* 调整&#x200B;**文本转图像**&#x200B;选项，
* 然后&#x200B;**刷新**&#x200B;生成的图像。

您还可以使用&#x200B;**探索更多**&#x200B;来发掘更多可能性。

完成后，选择所需的图像并点击&#x200B;**保存**&#x200B;以关闭 Adobe Express。返回图像，并随变体一同保存。

![生成变体 - Express 图像已保存](assets/generate-variations-express-image-saved.png)

在这里，您可以将鼠标悬停在图像上，以显示以下操作项：

* **复制**：[将图像复制到剪贴板以供其他地方使用](#use-content)
* **编辑**：打开 Adobe Express，以便您可以对图像进行修改
* **下载**：将图像下载到本地机器
* **删除**：从变体中移除图像

>[!NOTE]
>
>[Content Credentials](https://helpx.adobe.com/cn/creative-cloud/help/content-credentials.html) 在基于文档的创作中使用时不会被持久化。

### 使用内容  {#use-content}

要使用生成式 AI 生成的内容，您必须将内容复制到剪贴板以便在其他地方使用。

这是通过使用复制图标来完成的：

* 对于文本：使用变体面板上可见的复制图标
* 对于图片：将鼠标移至图像上方以查看复制图标

复制到剪贴板后，您就可以粘贴这些信息，以便在为您的网站创作内容时使用。您还可以运行[试验](https://www.aem.live/docs/experimentation)。

## 收藏夹 {#favorites}

在查看内容后，您可以将选定的变体保存为收藏夹。

保存后，它们就会显示在左侧导航栏中的&#x200B;**收藏夹**&#x200B;下。收藏夹会被保留（直到您选择&#x200B;**删除**&#x200B;它们，或清除浏览器缓存）。

* 收藏夹和变体可以复制/粘贴到剪贴板，以便在您的网站内容中使用。
* 收藏夹可以被&#x200B;**移除**。

## 最近项目 {#recents}

此部分提供您最近活动的链接。在您选择&#x200B;**生成**&#x200B;后，会添加一个&#x200B;**最近**&#x200B;条目。其中有提示的名称和时间戳。如果您选择一个链接，它会加载提示，根据需要填充输入字段，并显示生成的变体。

## 编辑提示 {#edit-the-prompt}

底层提示可以进行编辑。建议您这样做：

* 如果您得到的生成结果需要进一步优化
* 建议您修改并[保存提示](#save-prompt)，以供将来使用

选择&#x200B;**编辑提示**：

![生成变体 - 编辑提示](assets/generate-variations-prompt-edit.png)

这将会打开提示编辑器，您可以在其中进行更改：

![生成变体 - 提示编辑器](assets/generate-variations-prompt-editor.png)

### 添加提示输入 {#add-prompt-inputs}

创建或编辑提示时，您可能需要添加输入字段。输入字段在提示中充当变量，并提供了在各种场景中使用相同提示的灵活性。它们允许用户定义提示中的特定元素，而无需编写整个提示。

* 字段定义为双花括号 `{{ }}` 包围一个占位符名称。
例如：`{{tone_of_voice}}`。

  >[!NOTE]
  >
  >双花括号之间不允许有空格。

* 它还在 `METADATA` 下定义，并具有以下参数：
   * `label`
   * `description`
   * `default`
   * `type`

#### 示例：添加新文本字段 - 语调 {#example-add-new-text-field-tone-of-voice}

要在提示中使用以下语法添加一个名为&#x200B;**语调**&#x200B;的新文本字段：

```prompt
{{@tone_of_voice, 
  label="Tone of voice",
  description="Indicate the desired tone of voice",
  default="optimistic, smart, engaging, human, and creative",
  type=text
}}
```

![生成变体 - 用语调编辑提示](assets/generate-variations-prompt-edited.png)

<!--
#### Example: Add new dropdown field - Page Type {#example-add-new-dropdown-field-page-type}

To create an input field Page Type providing a dropdown selection:

1. Create a spreadsheet named `pagetype.xls` in the top-level directory of your folder structure.
1. Edit the spreadsheet:

   1. Create two columns: **Key** and **Value**.
   1. In the **Key** column, enter labels that will appear in the dropdown.
   1. In the **Value** column, describe the key value so the generative AI has context.

1. In your prompt, refer to the title of the spreadsheet along with the appropriate type. 

   ```prompt
   {{@page_type, 
     label="Page Type",
     description="Describes the type of page",
     spreadsheet=pagetype
   }}
   ```
-->

## 创建提示 {#create-prompt}

当您从&#x200B;**提示模板**&#x200B;中选择&#x200B;**新提示**&#x200B;时，一个新的面板将会允许您输入新的提示。然后，您可以指定它们，并连同&#x200B;**温度**，一同来&#x200B;**生成**&#x200B;内容。

请参阅[保存提示](#save-prompt)，了解保存提示以备后用的详细信息。

请参阅[添加提示输入](#add-prompt-inputs)，了解有关添加您自己的提示输入的详细信息。

如果您希望在用户界面中以及在复制和粘贴到基于文档的创作流程时保留格式，请在提示中包含以下内容：

<!-- CHECK - are the double-quotes needed? -->

* `"Format the response as an array of valid, iterable RFC8259 compliant JSON"`

下图显示了这样做的好处：

* 在第一个例子中，`Title`和`Description`被组合在一起
* 在第二个示例中，它们被分别格式化：这是通过在提示中包含 JSON 请求来实现的。

![生成变体 - 标题和描述分别格式化的提示](assets/generate-variations-prompt-formatted.png)

## 保存提示 {#save-prompt}

编辑或创建提示后，建议您将其保存以备将来使用；无论是为您的 IMS 组织还是仅为您个人，均是如此。已保存的提示将会显示为&#x200B;**提示模板**&#x200B;卡片。

当编辑完提示后，在“输入”部分的底部，左侧的&#x200B;**生成**&#x200B;按钮旁边，会出现&#x200B;**保存**&#x200B;选项。

当被选中时，会打开&#x200B;**保存提示**&#x200B;对话框：

![生成变体 - 保存提示对话框](assets/generate-variations-prompt-save-dialog.png)

1. 添加一个独特的&#x200B;**提示名称**；用于识别&#x200B;**提示模板**&#x200B;中的提示。
   1. 一个新颖且独特的名称会创建一个新的提示模板。
   1. 一个已存在的名称会覆盖该提示；此时会显示一条消息。
1. （可选）添加描述。
1. 根据提示是否应仅对您个人保密，还是应在您的 IMS 组织内公开，激活或停用&#x200B;**组织内共享**&#x200B;选项。此状态显示在[“提示模板”中展示的结果卡片中](#select-prompt)。
1. **保存**&#x200B;提示；或&#x200B;**取消**&#x200B;操作。

>[!NOTE]
>
>如果正在覆盖/更新现有提示，您会收到通知（警告）。

>[!NOTE]
>
>在&#x200B;**提示模板**&#x200B;中，您可以删除自己或在 IMS 组织内创建的提示（使用通过省略号访问的菜单）。

## 受众 {#audiences}

为了生成个性化的内容，生成式 AI 必须对受众有所了解。Adobe 提供了多个默认受众，您也可以添加自己的受众。

添加受众时，您应该使用自然语言描述受众。例如：

* 若要创建受众
   * `Student`
* 您可以说：
   * `The audience consists of students, typically individuals who are pursuing education at various academic levels, such as primary, secondary, or tertiary education. They are engaged in learning and acquiring knowledge in diverse subjects, seeking academic growth, and preparing for future careers or personal development.`

支持两种受众来源：

* [Adobe Target](#audience-adobe-target)
* [CSV 文件](#audience-csv-file)

![生成变体 - 受众来源](assets/generate-variations-audiences.png)

### 受众 - Adobe Target {#audience-adobe-target}

在提示中选择一个 **Adobe Target** 受众，可以生成针对该受众进行个性化的内容。

>[!NOTE]
>
>要使用此选项，您的 IMS 组织必须有权访问 Adobe Target。

1. 选择 **Adobe Target**。
1. 然后从提供的列表中选择所需的&#x200B;**目标受众**。

   >[!NOTE]
   >
   >要使用 **Adobe Target** 受众，必须填写描述字段。如果不填写，下拉列表中会显示该受众不可用。要添加描述，请转到 Target，然后[添加受众描述](https://experienceleague.adobe.com/zh-hans/docs/target-learn/tutorials/audiences/create-audiences)。

   ![生成变体 - 受众来源 - Adobe Target](assets/generate-variations-audiences-adobe-target.png)

#### 添加 Adobe Target 受众 {#add-adobe-target-audience}

请参阅[创建受众](https://experienceleague.adobe.com/zh-hans/docs/target-learn/tutorials/audiences/create-audiences)，以在 Adobe Target 中创建受众。

### 受众 - CSV 文件 {#audience-csv-file}

在提示中选择一个 **CSV 文件**&#x200B;受众，可以生成针对所选&#x200B;**目标受众**&#x200B;进行个性化定制的内容。

Adobe 提供了多种受众可以使用。

1. 选择 **CSV 文件**。
1. 然后从提供的列表中选择所需的&#x200B;**目标受众**。

   ![生成变体 - 受众来源 - CSV 文件](assets/generate-variations-audiences-csv-file.png)

#### 添加受众 CSV 文件 {#add-audience-csv-file}

您可以从各种平台（例如，Google Drive、DropBox、Sharepoint）添加 CSV 文件，这些平台可以在文件公开后提供该文件的 URL。

>[!NOTE]
>
>在共享平台中，您&#x200B;*必须*&#x200B;有能力使该文件可公开访问。

例如，要从 Google Drive 上的文件添加受众：

1. 在 Google Drive 中，创建一个包含两列的电子表格文件：
   1. 第一列将显示在下拉菜单中。
   1. 第二列是受众描述。
1. 发布该文件：
   1. 文件 -> 共享 -> 发布到网络 -> CSV
1. 将 URL 复制到已发布的文件。
1. 前往“生成变体”。
1. 打开提示编辑器。
1. 在元数据中找到 **Adobe Target** 受众，并替换 URL。

   >[!NOTE]
   >
   >确保 URL 两端均保留双引号 (&quot;) 。

   例如：

   ![生成变体 - 添加受众 CSV 文件](assets/generate-variations-audiences-csv-save.png)

## 生成式操作的使用 {#generative-action-usage}

使用管理取决于所采取的操作：

* 生成变体

  一个复制变体的生成等同于一个生成式操作。作为客户，您的 AEM 许可证附带了一定数量的生成式操作。一旦基本权限消耗完毕，您可以购买额外的操作。

  >[!NOTE]
  >
  >请参阅 [Adobe Experience Manager：Cloud Service | 产品描述](https://helpx.adobe.com/cn/legal/product-descriptions/aem-cloud-service.html)，了解有关基本权限的更多详细信息，如果您想购买更多生成式操作，请联系您的帐户团队。

* Adobe Express

  图像生成的使用是通过 Adobe Express 权限和[生成式积分](https://helpx.adobe.com/cn/firefly/using/generative-credits-faq.html)来管理的。

## 访问“生成变体” {#access-generate-variations}

满足先决条件后，您可以通过 AEM as a Cloud Service 或 Edge Delivery Services 的 Sidekick 访问“生成变体”功能。

### 访问权限方面的先决条件 {#access-prerequisites}

要使用“生成变体”功能，您必须确保满足先决条件：

* [访问带有 Edge Delivery Services 的 Experience Manager as a Cloud Service](#access-to-aemaacs-with-edge-delivery-services)

#### 访问带有 Edge Delivery Services 的 Experience Manager as a Cloud Service{#access-to-aemaacs-with-edge-delivery-services}

需要访问“生成变体”功能的用户必须有权使用带有 Edge Delivery Services 的 Experience Manager as a Cloud Service 环境。

>[!NOTE]
>
>如果您的 AEM Sites as a Cloud Service 合同中未包含 Edge Delivery Services，您将需要签署一份新合同以获取访问权限。
>
>您应该联系您的客户团队，讨论如何迁移至带有 Edge Delivery Services 的 AEM Sites as a Cloud Service。

为了授予特定用户访问权限，请将他们的用户帐户分配到相应的产品配置文件中。请参阅[分配 AEM 产品配置文件，以了解更多详细信息](/help/journey-onboarding/assign-profiles-cloud-manager.md)。

### 从 AEM as a Cloud Service 访问 {#access-aemaacs}

“生成变体”功能可以通过 AEM as a Cloud Service 的[导航面板](/help/sites-cloud/authoring/basic-handling.md#navigation-panel)进行访问：

![导航面板](/help/sites-cloud/authoring/assets/basic-handling-navigation.png)

### 从 AEM Sidekick 访问 {#access-aem-sidekick}

在访问 Edge Delivery Services 的 Sidekick 的“生成变体”功能之前，需要进行一些配置。

1. 请参阅文档[安装 AEM Sidekick](https://www.aem.live/docs/sidekick-extension)，了解有关如何安装和配置 Sidekick 的信息。

1. 要在 Edge Delivery Services 的 Sidekick 中使用“生成变体”功能，请在 Edge Delivery Services 项目中的以下位置包含以下配置：

   * `tools/sidekick/config.json`

   这必须合并到您现有的配置中，然后进行部署。

   例如：

   ```prompt
   {
     // ...
     "plugins": [
       // ...
       {
         "id": "generate-variations",
         "title": "Generate Variations",
         "url": "https://experience.adobe.com/aem/generate-variations",
         "passConfig": true,
         "environments": ["preview","live", "edit"],
         "includePaths": ["**.docx**"]
       }
       // ...
     ]
   }
   ```

1. 您可能需要确保用户具有对带有 [Edge Delivery Services 的 Experience Manager as a Cloud Service 的访问权限](#access-to-aemaacs-with-edge-delivery-services)。

1. 然后，您可以通过在 Sidekick 的工具栏中选择&#x200B;**生成变体**&#x200B;来访问该功能：

   ![生成变体 - 从 AEM Sidekicj 访问](assets/generate-variations-sidekick-toolbar.png)

## 更多信息 {#further-information}

若要了解更多信息，您还可以阅读：

* [GenAI 在 GitHub 上生成变体](https://github.com/adobe/aem-genai-assistant#setting-up-aem-genai-assistant)
* [Edge Delivery Services 试验](https://www.aem.live/docs/experimentation)

## 常见问题解答 {#faqs}

### 格式化输出 {#formatted-outpu}

**生成的回复没有提供我需要的格式化输出。我该如何修改格式？例如：我需要一个标题和一个副标题，但是回复只有标题**

1. 以编辑模式打开实际提示。
1. 转到要求部分。
1. 您会发现一些关于输出的要求。
   1. 示例：“文本必须由三部分组成，即标题、正文和按钮标签。”或者“将响应格式化为一个包含属性“标题”、“正文”和“按钮标签”的有效 JSON 对象数组”。
1. 根据您的需求调整这些要求。

   >[!NOTE]
   >
   >如果您在输入的新输出上有单词/字符数限制，那么请创建一项要求。

   示例：“标题文本不得超过 10 个单词或 50 个字符，包括空格。”
1. 保存提示以供将来使用。

### 响应长度 {#length-of-response}

**生成的响应太长或太短。我如何改变其长度？**

1. 以编辑模式打开实际提示。
1. 转到要求部分。
1. 您会发现每个输出都有相应的单词/字符限制。
   1. 示例：“标题文本不得超过 10 个单词或 50 个字符（包括空格）。”
1. 根据您的需求修改这些要求。
1. 保存提示以供将来使用。

### 改善响应 {#improve-responses}

**我所得到的响应并不完全是我想要的。我能做些什么来改善它们？**

1. 尝试更改“高级”设置下的“温度”。
   1. 温度升高会偏离提示，导致出现更多的变化、随机性和创造性。
   1. 较低的温度更具确定性，且符合提示中的要求。
1. 在编辑模式下打开实际提示并查看提示。特别注意描述语调和其他重要标准的要求部分。

### 提示中的注释 {#comments-in-prompt}

**如何在提示中使用注释？**

提示中的注释用于包含不构成实际输出部分的备注、解释或指令。这些注释封装在特定的语法中：它们以双花括号开始和结束，并以一个哈希符号（例如，`{{# Comment Here }}`）开头。注释有助于明确提示的结构或意图，而不会影响生成的响应。

### 查找共享的提示 {#find-a-shared-prompt}

**如果我找不到别人共享的提示模板，我该怎么办？**

在这种情况下，需要检查各种细节：

1. 使用适合您环境的 URL。
例如，https://experience.adobe.com/#/aem/generate-variations
1. 确保选择正确的 IMS 组织。
1. 确认提示已保存为共享状态。

### v2.0.0 中的自定义提示 {#custom-prompts-v200}

**在 v.2.0.0 中，我的自定义提示消失了 - 我该怎么办？**

迁移到 v2.0.0 版本将会导致自定义提示模板损坏，因此它们将不可用。

要检索它们：

1. 转到 Sharepoint 中的 prompt-template 文件夹。
1. 复制提示。
1. 打开“生成变体”应用程序。
1. 选择“新建提示”卡片。
1. 粘贴该提示。
1. 验证提示是否有效。
1. 保存提示。

## 版本历史记录 {#release-history}

有关当前版本和之前版本的详细信息，请参阅[生成变体的发行说明](/help/generative-ai/release-notes-generate-variations.md)
