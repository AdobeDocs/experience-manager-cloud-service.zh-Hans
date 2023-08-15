---
title: 使用方法 [!DNL Adobe Sign] 在自适应表单中？
description: 您可以启用电子签名([!DNL Adobe Sign])自适应表单的工作流，用于自动执行签名工作流、简化单个和多签名流程，以及通过移动设备以电子方式签名表单。
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 3%

---


# 使用 [!DNL Adobe Sign] 在自适应表单中 {#using-adobe-sign-in-an-adaptive-form}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html) |
| AEM as a Cloud Service | 本文 |


[!DNL Adobe Sign] 支持自适应表单的电子签名工作流。电子签名可改进法律、销售、工资单、人力资源管理和其他领域的文档处理工作流。

在典型的 [!DNL Adobe Sign] 和自适应Forms场景中，用户填写自适应表单以申请需要一个或多个参与方签名的服务。 例如，抵押贷款和信用卡申请需要所有借款人和共同申请人的合法签名。 要为类似方案启用电子签名工作流，您可以集成 [!DNL Adobe Sign] 和自适应表单。 还有几个示例是，您可以使用 [!DNL Adobe Sign] 至：

* 使用完全自动化的计划书、报价和合同流程从任何设备完成交易。
* 更快地完成人力资源流程，并为员工提供数字体验。
* 缩短合同周期，更快地吸引供应商。
* 创建可自动执行常用流程的数字工作流。

[!DNL Adobe Sign] 与集成 [!DNL AEM Forms] 支持：

* 单个和多用户签名工作流
* 顺序和同步签名工作流
* 以匿名或登录用户身份签署表单
* 动态签名流程（与集成） [!DNL AEM Forms] Workflow)
* 通过知识库、电话、社交个人资料和政府ID进行验证
* 为每个协议收件人分配角色。 用于商业和企业服务级别的Adobe Sign可以选择扩展 [协议收件人的角色](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## 前提条件 {#prerequisites}

使用前 [!DNL Adobe Sign] 在自适应表单中：

* 确保 [!DNL AEM Forms] as a Cloud Service配置为使用Adobe Sign。 有关详细信息，请参阅 [将Adobe Sign与集成 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* 保持收件人列表就绪。 您至少需要每个收件人的电子邮件地址。

## 配置 [!DNL Adobe Sign] 自适应表单 {#configure-adobe-sign-for-an-adaptive-form}

配置 [!DNL Adobe Sign] 对于自适应表单：

1. [启用 [!DNL Adobe Sign] 自适应表单](#enableadobsignforanadaptiveform)
1. [添加 [!DNL Adobe Sign] 自适应表单的字段](#addadobesignfieldstoanadaptiveform)
1. [选择 [!DNL Adobe Sign] 自适应表单Cloud Service](#select-adobe-sign-cloud-service-and-signing-order)

1. [添加 [!DNL Adobe Sign] 自适应表单的收件人](#addsignerstoanadaptiveform)
1. [为自适应表单选择提交操作](#selectsubmitactionforanadaptiveform)

![收件人详细信息](assets/signer_details_new.png)

### 启用 [!DNL Adobe Sign] 自适应表单  {#enableadobesign}

您可以启用 [!DNL Adobe Sign] 创建自适应表单或创建 [!DNL Adobe Sign] 已启用自适应表单。 选择下列选项之一：

* [创建 [!DNL Adobe Sign] 启用的自适应表单](#create-an-adaptive-form-for-adobe-sign)
* [启用 [!DNL Adobe Sign] 对于现有的自适应表单](#editafsign).

#### 创建Adobe Sign自适应表单 {#create-an-adaptive-form-for-adobe-sign}

要创建启用签名的自适应表单，请执行以下操作：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **[!UICONTROL 创建]** 并选择 **[!UICONTROL 自适应表单]**. 此时将显示模板列表。 选择模板并点按 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 基本]** 选项卡：

   1. 指定 **[!UICONTROL 名称]** 和 **[!UICONTROL 标题]** 用于自适应表单。

   1. 选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 创建时间 [集成 [!DNL Adobe Sign] 替换为 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   配置容器包含 [!DNL Adobe Sign] 为您的环境配置的Cloud Service。 这些服务可在自适应表单编辑器中选择。

1. 在 **[!UICONTROL 表单模型]** 选项卡，选择以下选项之一：

   * 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项并选择记录文档模板。 使用选项时，发送以供签名的文档仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   * 如果您没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档显示自适应表单的所有字段。

1. 点按&#x200B;**[!UICONTROL 创建。]** 将创建一个支持签名的自适应表单。 您可以添加 [!DNL Adobe Sign] 将字段发送到表单以供签名。

#### 启用 [!DNL Adobe Sign] 自适应表单 {#editafsign}

使用 [!DNL Adobe Sign] 在现有的自适应表单中：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 集成时创建 [!DNL Adobe Sign] 替换为 [!DNL AEM Forms].
1. 在 **[!UICONTROL 表单模式]** 选项卡，选择以下选项之一：

   * 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项并选择记录文档模板。 使用选项时，发送以供签名的文档仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   * 如果您没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档显示自适应表单的所有字段。

1. 点按 **[!UICONTROL 保存并关闭]**. 自适应表单已启用 [!DNL Adobe Sign]. 现在，您可以添加 [!DNL Adobe Sign] 将字段发送到表单以供签名。

### 添加 [!DNL Adobe Sign] 自适应表单的字段 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 提供了多个可放置在自适应表单上的字段。 这些字段接受各种类型的数据，如签名、首字母、公司或标题，并帮助收集签名期间的额外信息和签名。 您可以使用 [!DNL Adobe Sign] 要放置的块组件 [!DNL Adobe Sign] 自适应表单中不同位置的字段。

要将字段添加到自适应表单并自定义与这些字段相关的各种选项，请执行以下操作：

1. 拖放 **[!UICONTROL Adobe Sign块]** 组件从组件浏览器复制到自适应表单。 此 [!DNL Adobe Sign] 块组件具有所有受支持的 [!DNL Adobe Sign] 字段。 默认情况下，它添加 **[!UICONTROL 签名]** 字段至自适应表单。

   ![签名块](assets/sign_block_new.png)

   默认情况下， [!DNL Adobe Sign] 块在发布的自适应表单中不可见。 它仅在签名文档中可见。 您可以更改以下项的可见性 [!DNL Adobe Sign] 从的属性中阻止 [!DNL Adobe Sign] 块组件。

   >[!NOTE]
   >
   >  * 使用 [!DNL Adobe Sign] 块不是强制使用的 [!DNL Adobe Sign] 在自适应表单中。 如果您不使用 [!DNL Adobe Sign] 为收件人阻止并添加字段，则默认签名字段显示在签名文档的底部。
   >  * 使用 [!DNL Adobe Sign] 仅阻止自动生成记录文档的自适应Forms。 如果您使用自定义XDP生成记录文档或基于表单模板的自适应表单， [!DNL Adobe Sign] 不支持该块。


1. 选择 **[!UICONTROL Adobe Sign块]** 组件并点按 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 选择并添加 [!DNL Adobe Sign] 字段。 **B.** 展开 [!DNL Adobe Sign] 阻止到全屏视图

1. 点按 **[!UICONTROL Adobe Sign]** 字段 ![Adobe Sign](assets/adobesign.png) 图标。 它会显示要选择和添加的选项 [!DNL Adobe Sign] 字段。

   展开 **[!UICONTROL 类型]** 用于选择 [!DNL Adobe Sign] 字段，然后点按完成 ![保存](assets/save_icon.svg) 图标以将所选字段添加至 [!DNL Adobe Sign] 封锁。 此 **[!UICONTROL 类型]** 下拉字段包括签名、收件人信息和数据字段类型。 [!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 中列出的支持字段 [!UICONTROL 类型] 下拉框。 有关 [!DNL Adobe Sign] 字段，请参阅 [Adobe Sign文档](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必须为字段提供唯一名称。 您还可以选择必填选项来标记必填字段。 除了 **[!UICONTROL 名称]** 和 **[!UICONTROL 必填]** 选项，部分 [!DNL Adobe Sign] 字段具有更多选项。 例如，蒙版和多行。 此外，请为每个ID指定一个唯一的名称 [!DNL Adobe Sign] 字段是位于同一还是不同位置 [!DNL Adobe Sign] 块。

   如果您选择 **[!UICONTROL 数字签名]** 从下拉列表中，您可以将数字签名应用于自适应表单：

   * 在线使用云签名签名以签名 [数字标识](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服务提供商托管。
   * 使用Adobe Acrobat下载文档或使用智能卡、USB令牌或基于文件的数字IDReader，即可从本地下载文档。

### 启用 [!DNL Adobe Sign] 自适应表单 {#enableadobsignforanadaptiveform}

开箱即用， [!DNL Adobe Sign] 未为自适应表单启用。 要启用该功能：

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它可打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它支持 [!DNL Adobe Sign] 用于自适应表单。

### 选择 [!DNL Adobe Sign] Cloud Service和签名顺序 {#select-adobe-sign-cloud-service-and-signing-order}

您可以配置多个 [!DNL Adobe Sign] AEM实例的服务 [!DNL Forms]. 建议为每个职能（人力资源、财务等）提供单独的一组服务。 它使跟踪和报告已签署文档更加容易。 例如，银行具有多个部门。 您可以为各个部门设置单独的配置，以便更好地跟踪文档。

一个文档也可以有多个收件人。 例如，信用卡申请可以有多个申请人。 在开始处理申请之前，银行需要所有申请人的签名。 对于多收件人方案，您可以选择按顺序或同时顺序签署文档。

要选择Cloud Service和签名顺序，请执行以下操作：

![云服务](assets/cloud-service.png)

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它可打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它支持 [!DNL Adobe Sign] 用于自适应表单。
1. 从已配置的列表中选择Cloud Service [!DNL Adobe Sign] Cloud Service。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 列表为空，请按照 [配置 [!DNL Adobe Sign] 替换为 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 文章以配置服务。

   下拉列表中列出的Cloud Service `global` 文件夹(位于“工具”> **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. 此外，下拉列表还会列出您在中选择的文件夹中存在的Cloud Service。 **[!UICONTROL 配置容器]** 创建自适应表单时显示的字段。

1. 从中选择签名顺序 **[!UICONTROL 收件人可以填写]** 对话框。 收件人可以签署自适应表单 **[!UICONTROL 按顺序]**  — 一个接一个的收件人，或者 **[!UICONTROL 同时]**  — 按任意顺序。

   按顺序排列，每个收件人一次收到Adobe Sign协议。 收件人完成分配的操作后，协议将发送给下一个收件人，依此类推。

   所有收件人将同时按顺序接收Adobe Sign协议，并且可以相互并行执行操作。

1. 使用协议ID字段将绑定与协议ID (agreementId)相关联。 它会将协议ID添加到提交数据的基于架构的表单的afBoundData部分。 协议ID还会添加到所有启用Adobe Sign的表单的已提交数据的afSubmissionInfo部分。 您可以使用协议ID通过自定义代码跟踪协议状态（需要自定义实施）。

1. [将收件人添加到自适应表单](working-with-adobe-sign.md#addsignerstoanadaptiveform) 然后点击“完成” ![保存](assets/save_icon.svg) 图标以保存更改。

### 将收件人添加到自适应表单 {#addsignerstoanadaptiveform}

Adobe Sign协议可以有一个或多个收件人。 添加收件人时，您还可以配置收件人的身份验证详细信息，并选择表单填写者和收件人是否为同一个人。 执行以下步骤以添加并提供有关收件人的各种详细信息：

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它会打开具有自适应表单容器属性的属性浏览器。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它支持 [!DNL Adobe Sign] 用于自适应表单。
1. 点按 **[!UICONTROL 添加收件人]**. 它会向自适应表单添加收件人。 您可以将多个收件人添加到自适应表单。 所有接收者都会收到有关提交自适应表单的Adobe Sign协议。
   ![phone-details](assets/recipient-settings.png)

1. 单击 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标来指定有关收件人的以下信息：

   * **[!UICONTROL 标题]：** 指定标题以唯一标识收件人。

   * **[!UICONTROL 收件人与填表人是否相同？]：** 选择 **[!UICONTROL 是]**，如果表单填写者和第一个收件人为同一个人。 <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL 收件人角色]：** 选择收件人的角色。 用于商业和企业服务级别的Adobe Sign可以选择扩展 [协议收件人的角色](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html)，而不仅仅是 **签名者**，以更好地匹配他们的工作流要求。

   * **[!UICONTROL 收件人电子邮件地址]：** 指定收件人的电子邮件地址。 收件人通过指定的电子邮件地址接收Adobe Sign协议。 您可以选择使用表单字段、登录用户的Experience Manager用户配置文件中提供的电子邮件地址，或者手动输入电子邮件地址。 这是强制步骤。

     >[!NOTE]
     >
     >确保第一个收件人或唯一收件人（如果只有一个收件人）的电子邮件地址与 [!DNL Adobe Sign] 用于配置AEMCloud Service的帐户。

   * **[!UICONTROL 收件人身份验证方法]：** 指定在打开Adobe Sign协议之前对收件人进行身份验证的方法。 您可以在电话、知识库、基于社会身份的身份验证和 [政府ID](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html) 对象 [!DNL Adobe Acrobat Sign]. 对象 [!DNL Adobe Acrobat Sign for Government] 您可以在电话和基于知识的身份验证之间进行选择。

   >[!NOTE]
   >
   >    * 默认情况下，基于社交身份的身份验证提供使用Facebook、Google和LinkedIn进行身份验证的选项。 您可以联系 [!DNL Adobe Sign] 支持启用其他社交身份验证提供程序。
   >

   * **[!DNL Adobe Sign]要填写或签名的字段：** 选择 [!DNL Adobe Sign] 收件人字段。 自适应表单可以有多个 [!DNL Adobe Sign] 字段。 您可以选择为收件人启用特定字段。 字段显示所有可用的 [!DNL Adobe Sign] 块。 选择块时，将选择该块的所有字段。 您可以使用X图标取消选择字段。

   ![recipient-details](assets/signer-details.png)

   上图有两个例子 [!DNL Adobe Sign] 块：个人信息和办公室详细信息

   点按 ![保存](assets/save_icon.svg) 图标。 已添加收件人。

### 为自适应表单选择提交操作 {#selectsubmitactionforanadaptiveform}

在您之后，添加 [!DNL Adobe Sign] 字段到自适应表单，启用 [!DNL Adobe Sign] 在表单容器中，选择 [!DNL Adobe Sign] Cloud Service并添加Adobe Sign协议接收者，为自适应表单选择适当的提交操作。 有关自适应Forms提交操作的详细信息，请参阅 [配置提交操作](configuring-submit-actions.md).

签名和提交表单是相互独立的。 在用户提交表单后创建Adobe Sign协议后，会立即提交自适应表单。 [!DNL AEM Forms] as a Cloud Service不会等待收件人签名或完成其他操作以提交自适应表单。 用户单击“提交”按钮或“摘要”步骤显示表单摘要后，就会立即提交表单。

此外， [!DNL Adobe Sign] 已启用自适应表单嵌入Adobe Sign协议ID以提交数据。 您可以使用协议ID通过自定义代码跟踪协议状态（需要自定义实施）。

Adobe Sign协议ID (agreementId)包含在自适应表单的提交数据中。 默认情况下，协议ID显示在 `afSubmissionInfo` 已提交数据的节点。

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

或者，您也可以将绑定与协议ID (agreementId)相关联。 它会将协议ID添加到已提交数据的afBoundData部分。 例如，在以下提交的数据中，协议ID将绑定到 `<userName>` 节点：

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <userName>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</userName>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表单签名体验已准备就绪。 您可以预览表单以验证签名体验。 在已发布的表单上， [!DNL Adobe Sign] 当收件人收到通过电子邮件签名的表单时，会显示块字段。 当 **[!UICONTROL 什么时候收件人和填表人相同？]** 选项标记为“是”且满足条件，则在提交后用户将被重定向到Adobe Sign协议，用户可以立即签署文档，而不是等待协议出现在电子邮件中。

## 为自适应表单配置云签名 {#configure-cloud-signatures-for-an-adaptive-form}

基于云的数字签名或远程签名是新一代的数字签名，可在桌面、移动设备和Web上使用，并且满足收件人身份验证的最高合规性和保证要求。 您可以使用基于云的数字签名对自适应表单进行签名。

之后 [编辑Adobe Sign的自适应表单属性](working-with-adobe-sign.md#enableadobesign)，执行以下步骤以将云签名字段添加到自适应表单：

1. 拖放 **[!UICONTROL Adobe Sign块]** 组件从组件浏览器复制到自适应表单。 此 [!UICONTROL Adobe Sign块] 组件具有所有受支持的 [!DNL Adobe Sign] 字段。 默认情况下，它添加 **[!UICONTROL 签名]** 字段至自适应表单。

   ![签名块](assets/sign-block-new.png)

1. 选择 **[!UICONTROL Adobe Sign块]** 组件并点按 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 选择并添加 [!DNL Adobe Sign] 字段。 **B.** 展开 [!DNL Adobe Sign] 阻止到全屏视图

1. 点按 **[!UICONTROL Adobe Sign字段]** ![Adobe Sign](assets/adobesign.png) 图标。 它会显示要选择和添加的选项 [!DNL Adobe Sign] 字段。

   展开 **[!UICONTROL 类型]** 要选择的下拉字段 **[!UICONTROL 数字签名]** 然后点击 **[!UICONTROL 完成]** 图标以将所选字段添加至 [!DNL Adobe Sign] 封锁。

   ![数字签名](assets/digital_signatures_new.png)

   必须为字段提供唯一名称。

   使用以下方式将数字签名应用于自适应表单：

   * 云签名：使用签名 [数字标识](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服务提供商托管。
   * Adobe Acrobat或Reader：使用Adobe Acrobat或Reader下载并打开文档，以使用智能卡、USB令牌或基于文件的数字ID进行签名。

     >[!NOTE]
     >
     > 数字签名还适用于 [!DNL Adobe Acrobat Sign for Government] 但无法使用云签名应用它。

   将云签名字段添加到自适应表单后，执行以下步骤以完成配置过程：

   * [为自适应表单启用Adobe Sign](#enableadobsignforanadaptiveform)
   * [为自适应表单选择Adobe Sign Cloud Service](#selectadobesigncloudserviceforanadaptiveform)
   * [将收件人添加到自适应表单](#addsignerstoanadaptiveform)
   * [为自适应表单选择提交操作](#selectsubmitactionforanadaptiveform)

### 配置感谢页面或摘要步骤组件 {#configure-the-thank-you-page-or-summary-step-component}

此 **[!UICONTROL 摘要步骤]** 组件自动提交表单，填充自定义摘要页面中的信息，并显示已提交表单的摘要。 摘要步骤组件占据表单可用的完整宽度。 建议在包含摘要步骤组件的部分中没有任何其他组件。

## 常见问题 {#frequently-asked-questions}

**问：** 您可以将自适应表单嵌入到其他自适应表单中。 嵌入式自适应表单是否可以 [!DNL Adobe Sign] 已启用？
**Ans：** 否，Experience Manager Forms不支持使用嵌入 [!DNL Adobe Sign] 已启用自适应表单以供签名

**问：** 当我使用高级模板创建自适应表单并打开它进行编辑时，出现错误消息“电子签名或收件人配置不正确”。 显示。 如何解决错误消息？
**Ans：** 使用高级模板创建的自适应表单配置为使用 [!DNL Adobe Sign]. 要解决此错误，请创建并选择 [!DNL Adobe Sign] 云配置和配置 [!DNL Adobe Sign] 自适应表单的收件人。

**问：** 我可以使用 [!DNL Adobe Sign] 自适应表单的静态文本组件中的文本标记？
**Ans：** 可以，您可以在文本组件中使用文本标记来添加 [!DNL Adobe Sign] 字段到已启用自适应表单的记录文档（仅限自动生成的记录文档选项）。 要了解创建文本标记的过程和规则，请参阅 [Adobe Sign文档](https://helpx.adobe.com/sign/using/text-tag.html). 另请注意，自适应Forms对文本标记的支持有限。 您可以使用文本标记仅创建满足以下条件的字段 [Adobe Sign块](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支持。

## 疑难解答 {#troubleshoot}

### [!DNL Adobe Sign] 协议失败 {#adobe-sign-agreement-failures}

**问题**
时间 [!DNL Adobe Sign] 为自适应表单配置了服务，该服务无法创建 [!DNL Adobe Sign] 基础自适应表单的协议。

**解决方法**

* 查看 [Adobe Sign Cloud Service的配置](adobe-sign-integration-adaptive-forms.md) 在自适应表单中使用。
* 确保API应用程序位于 [!DNL Adobe Sign] 用于配置的服务器 [!DNL Adobe Sign] Cloud Service具有所需的权限。
* 如果您使用多个 [!DNL Adobe Sign] Cloud Service，指向 **[!UICONTROL oAuth URL]** 所有服务的总和 **[!UICONTROL Adobe Sign Shard]**.

* 使用单独的电子邮件地址进行配置 [!DNL Adobe Sign] 第一个或单个收件人的帐户和。 第一个收件人或唯一收件人（如果只有单个收件人）的电子邮件地址不能与 [!DNL Adobe Sign] 用于配置AEMCloud Service的帐户。

## 相关文章 {#related-articles}

* [集成 [!DNL Adobe Sign] 替换为 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [使用的最佳实践 [!DNL Adobe Sign] 使用自适应Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
