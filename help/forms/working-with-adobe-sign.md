---
title: 使用方法 [!DNL Adobe Sign] 在自适应表单中？
description: 您可以启用电子签名([!DNL Adobe Sign])自适应表单的工作流程，以自动执行签名工作流程，简化单个和多签名流程，以及从移动设备以电子方式对表单进行签名。
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '3100'
ht-degree: 0%

---


# 使用 [!DNL Adobe Sign] 在自适应表单中 {#using-adobe-sign-in-an-adaptive-form}


>[!NOTE]
>
>在自适应表单中使用Adobe Sign角色的功能在2021年8月的预发行渠道中提供。 该功能将在2021年9月版中正式发布。


[!DNL Adobe Sign] 为自适应Forms启用电子签名工作流。 电子签名可改进工作流程，以处理法律、销售、工资、人力资源管理等领域的文档。

在 [!DNL Adobe Sign] 和自适应Forms方案中，用户填写自适应表单以申请需要一个或多个方签名的服务。 例如，抵押贷款和信用卡申请要求所有借款人和共同申请人签名。 要为类似情景启用电子签名工作流，您可以集成 [!DNL Adobe Sign] 自适应表单。 例如，您可以使用 [!DNL Adobe Sign] 至：

* 通过完全自动化的建议书、报价和合同流程，与任何设备达成交易。
* 更快地完成人力资源流程，并为员工提供数字体验。
* 缩短合同周期并更快地载入您的供应商。
* 创建可自动处理常见流程的数字工作流。

[!DNL Adobe Sign] 集成 [!DNL AEM Forms] 支持：

* 单用户和多用户签名工作流
* 顺序和同时的签名工作流
* 以匿名或已登录用户的身份对表单进行签名
* 动态签名流程(与 [!DNL AEM Forms] 工作流)
* 通过知识库、电话、社交用户档案和政府ID进行身份验证
* 为每个协议收件人分配角色。 Adobe Sign的业务和企业服务级别可以选择 [协议收件人的角色](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## 前提条件 {#prerequisites}

使用之前 [!DNL Adobe Sign] 在自适应表单中：

* 确保 [!DNL AEM Forms] as a Cloud Service已配置为使用Adobe Sign。 有关详细信息，请参阅 [将Adobe Sign与 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* 保持收件人列表就绪。 您至少需要每个收件人的电子邮件地址。

## 配置 [!DNL Adobe Sign] 自适应表单 {#configure-adobe-sign-for-an-adaptive-form}

配置 [!DNL Adobe Sign] 对于自适应表单：

1. [启用 [!DNL Adobe Sign] 自适应表单](#enableadobsignforanadaptiveform)
1. [添加 [!DNL Adobe Sign] 自适应表单的字段](#addadobesignfieldstoanadaptiveform)
1. [选择 [!DNL Adobe Sign] Cloud Service自适应表单](#select-adobe-sign-cloud-service-and-signing-order)

1. [添加 [!DNL Adobe Sign] 自适应表单的收件人](#addsignerstoanadaptiveform)
1. [为自适应表单选择提交操作](#selectsubmitactionforanadaptiveform)

![收件人详细信息](assets/signer_details_new.png)

### 启用 [!DNL Adobe Sign] 自适应表单  {#enableadobesign}

您可以启用 [!DNL Adobe Sign] 或创建 [!DNL Adobe Sign] 启用了自适应表单。 选择以下选项之一：

* [创建 [!DNL Adobe Sign] 启用自适应表单](#create-an-adaptive-form-for-adobe-sign)
* [启用 [!DNL Adobe Sign] （对于现有自适应表单）](#editafsign).

#### 为Adobe Sign创建自适应表单 {#create-an-adaptive-form-for-adobe-sign}

要创建启用符号的自适应表单，请执行以下操作：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **[!UICONTROL 创建]** 选择 **[!UICONTROL 自适应表单]**. 此时将显示模板列表。 选择模板并点按 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 基本]** 选项卡：

   1. 指定 **[!UICONTROL 名称]** 和 **[!UICONTROL 标题]** （在自适应表单中）。

   1. 选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 创建时间 [集成 [!DNL Adobe Sign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   配置容器包含 [!DNL Adobe Sign] Cloud Services。 这些服务可在自适应表单编辑器中进行选择。

1. 在 **[!UICONTROL 表单模型]** 选项卡，选择以下选项之一：

   * 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项，然后选择记录文档模板。 使用选项时，发送进行签名的文档将仅显示基于关联表单模板的那些字段。 它不会显示自适应表单的所有字段。

   * 如果没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档将显示自适应表单的所有字段。

1. 点按&#x200B;**[!UICONTROL 创建。]** 将创建启用符号的自适应表单。 您可以将 [!DNL Adobe Sign] 字段并将其发送以进行签名。

#### 启用 [!DNL Adobe Sign] 自适应表单 {#editafsign}

使用 [!DNL Adobe Sign] 在现有自适应表单中：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择自适应表单并点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，选择 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 集成时创建 [!DNL Adobe Sign] with [!DNL AEM Forms].
1. 在 **[!UICONTROL 表单模式]** 选项卡，选择以下选项之一：

   * 如果您有自定义表单模板，并且需要基于表单模板的记录文档，请选择 **[!UICONTROL 将表单模板关联为记录文档模板]** 选项，然后选择记录文档模板。 使用选项时，发送进行签名的文档将仅显示基于关联表单模板的那些字段。 它不会显示自适应表单的所有字段。

   * 如果没有自定义表单模板，请选择 **[!UICONTROL 生成记录文档]** 选项。 使用选项时，发送以供签名的文档将显示自适应表单的所有字段。

1. 点按 **[!UICONTROL 保存并关闭]**. 自适应表单已启用 [!DNL Adobe Sign]. 现在，您可以将 [!DNL Adobe Sign] 字段并将其发送以进行签名。

### 添加 [!DNL Adobe Sign] 自适应表单的字段 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 具有可置于自适应表单上的各种字段。 这些字段接受各种类型的数据（如签名、缩写、公司或标题），并帮助在签名期间收集额外信息以及签名。 您可以使用 [!DNL Adobe Sign] 要放置的块组件 [!DNL Adobe Sign] 自适应表单中不同位置的字段。

要向自适应表单添加字段并自定义与这些字段相关的各种选项，请执行以下操作：

1. 拖放 **[!UICONTROL Adobe Sign块]** 组件从组件浏览器转换到自适应表单。 的 [!DNL Adobe Sign] 块组件支持所有 [!DNL Adobe Sign] 字段。 默认情况下，它会添加 **[!UICONTROL 签名]** 字段。

   ![符号块](assets/sign_block_new.png)

   默认情况下， [!DNL Adobe Sign] 块在已发布的自适应表单中不可见。 它仅在签名文档中可见。 您可以更改 [!DNL Adobe Sign] 阻止 [!DNL Adobe Sign] 块组件。

   >[!NOTE]
   >
   >  * 使用 [!DNL Adobe Sign] 块不必使用 [!DNL Adobe Sign] 在自适应表单中。 如果您不使用 [!DNL Adobe Sign] 阻止并添加收件人的字段，则默认签名字段会显示在签名文档的底部。
   >  * 使用 [!DNL Adobe Sign] 仅对那些自动生成记录文档的自适应Forms进行块。 如果您使用自定义XDP来生成记录文档或基于表单模板的自适应表单， [!DNL Adobe Sign] 不支持块。



1. 选择 **[!UICONTROL Adobe Sign块]** 组件，然后点按 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** 选择并添加 [!DNL Adobe Sign] 字段。 **B.** 展开 [!DNL Adobe Sign] 阻止全屏视图

1. 点按 **[!UICONTROL Adobe Sign]** 字段 ![Adobe Sign](assets/adobesign.png) 图标。 它会显示用于选择和添加的选项 [!DNL Adobe Sign] 字段。

   展开 **[!UICONTROL 类型]** 用于选择 [!DNL Adobe Sign] 字段，然后点按完成 ![保存](assets/save_icon.svg) 图标以将选定字段添加到 [!DNL Adobe Sign] 块。 的 **[!UICONTROL 类型]** 下拉字段包括“签名”、“收件人信息”和“数据”字段类型。 [!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 中列出的支持字段 [!UICONTROL 类型] 下拉框。 有关 [!DNL Adobe Sign] 字段，请参阅 [Adobe Sign文档](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必须为字段提供唯一的名称。 您还可以选择必需选项来将字段标记为必填。 除 **[!UICONTROL 名称]** 和 **[!UICONTROL 必需]** 选项，某些 [!DNL Adobe Sign] 字段。 例如，蒙版和多行。 此外，还为每个 [!DNL Adobe Sign] 字段是否位于相同或不同的位置 [!DNL Adobe Sign] 块。

   如果您选择 **[!UICONTROL 数字签名]** 从下拉列表中，您可以将数字签名应用到自适应表单：

   * 在线使用云签名使用 [数字ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服务提供商托管。
   * 通过使用智能卡、USB令牌或基于文件的数字ID下载包含Adobe Acrobat或Reader的文档，从本地进行。

### 启用 [!DNL Adobe Sign] 自适应表单 {#enableadobsignforanadaptiveform}

开箱即用， [!DNL Adobe Sign] 未为自适应表单启用。 要启用该功能：

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它会打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它使 [!DNL Adobe Sign] 自适应表单。

### 选择 [!DNL Adobe Sign] Cloud Service和签名顺序 {#select-adobe-sign-cloud-service-and-signing-order}

您可以配置多个 [!DNL Adobe Sign] 服务实例的AEM [!DNL Forms]. 建议为每个功能（人力资源、财务等）单独提供一组服务。 它使跟踪和报告已签名文档变得更轻松。 例如，银行有多个部门。 您可以为每个部门单独配置以更好地跟踪文档。

文档还可以有多个收件人。 例如，信用卡申请可以有多个申请人。 银行在开始处理申请之前需要所有申请人的签名。 对于多收件人方案，您可以选择按顺序或同时按顺序对文档进行签名。

要选择Cloud Service和签名顺序，请执行以下操作：

![云服务](assets/cloud-service.png)

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它会打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它使 [!DNL Adobe Sign] 自适应表单。
1. 从已配置的列表中选择Cloud Service [!DNL Adobe Sign] Cloud Services。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 列表为空，请遵循 [配置 [!DNL Adobe Sign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 配置服务的文章。

   下拉列表列出了 `global` 工具>中的文件夹 **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 此外，该下拉列表还列出了您在 **[!UICONTROL 配置容器]** 字段。

1. 从 **[!UICONTROL 收件人可以完成]** 对话框。 收件人可以签署自适应表单 **[!UICONTROL 按顺序]**  — 一个接一个收件人，或 **[!UICONTROL 同时]**  — 按任意顺序排列。

   按顺序，一个收件人每次接收Adobe Sign协议。 收件人完成分配的操作后，协议将发送给下一个收件人，等等。

   所有收件人同时收到Adobe Sign协议，并可以彼此并行执行操作。

1. 使用协议ID字段将二进制文件与协议ID(agreementId)关联。 它会将协议ID添加到基于架构的表单的提交数据的afBoundData部分。 协议ID还会添加到所有启用Adobe Sign的表单的已提交数据中的afSubmissionInfo部分。 您可以使用协议ID来使用自定义代码跟踪协议状态（需要自定义实施）。

1. [将收件人添加到自适应表单](working-with-adobe-sign.md#addsignerstoanadaptiveform) 并点按完成 ![保存](assets/save_icon.svg) 图标以保存更改。

### 将收件人添加到自适应表单 {#addsignerstoanadaptiveform}

您可以拥有一个或多个Adobe Sign协议的收件人。 添加收件人时，您还可以为收件人配置身份验证详细信息，并选择表单填充者和收件人是否是同一人。 执行以下步骤以添加和提供有关收件人的各种详细信息：

1. 在内容浏览器中，点按 **[!UICONTROL 表单容器]**，然后点按 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它会打开具有自适应表单容器属性的属性浏览器。
1. 在属性浏览器中，展开 **[!UICONTROL 电子签名]** 折叠面板，然后选择 **[!UICONTROL 启用Adobe Sign]** 选项。 它使 [!DNL Adobe Sign] 自适应表单。
1. 点按 **[!UICONTROL 添加收件人]**. 它会向自适应表单中添加收件人。 您可以向自适应表单中添加多个收件人。 所有收件人都将收到一份提交自适应表单的Adobe Sign协议。
   ![电话详细信息](assets/recipient-settings.png)

1. 单击 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标以指定有关收件人的以下信息：

   * **[!UICONTROL 标题]:** 指定标题以唯一标识收件人。

   * **[!UICONTROL 收件人与填表人是否相同？]:** 选择 **[!UICONTROL 是]**，如果表单填写者和第一个收件人是同一人。 <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL 收件人角色]:** 选择收件人的角色。 Adobe Sign的业务和企业服务级别可以选择 [协议收件人的角色](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html)，而不仅仅是 **签名者**，以更好地匹配其工作流要求。

   * **[!UICONTROL 收件人电子邮件地址]:** 指定收件人的电子邮件地址。 收件人将收到关于指定电子邮件地址的Adobe Sign协议。 您可以选择使用在表单字段中提供的电子邮件地址、在登录用户的Experience Manager用户配置文件中，或手动输入电子邮件地址。 这是强制性步骤。

      >[!NOTE]
      >
      >确保第一个收件人或唯一收件人（如果有单个收件人）的电子邮件地址与 [!DNL Adobe Sign] 用于配置AEM云服务的帐户。

   * **[!UICONTROL 收件人身份验证方法]:** 指定在打开Adobe Sign协议之前验证收件人的方法。 您可以在电话、知识库、基于社交身份的身份验证和 [政府ID](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html).
   >[!NOTE]
   >
   >    * 默认情况下，基于社交身份的身份验证提供了使用Facebook、Google和LinkedIn进行身份验证的选项。 您可以联系 [!DNL Adobe Sign] 支持启用其他社交身份验证提供程序。


   * **[!DNL Adobe Sign]要填写或签名的字段：** 选择 [!DNL Adobe Sign] 字段。 自适应表单可以具有多个 [!DNL Adobe Sign] 字段。 您可以选择为收件人启用特定字段。 字段会显示所有可用的 [!DNL Adobe Sign] 阻止。 选择块时，该块的所有字段都将被选中。 您可以使用X图标取消选择字段。

   ![recipient-details](assets/signer-details.png)

   上图有两个示例 [!DNL Adobe Sign] 块：个人信息和办公室详细信息

   点按 ![保存](assets/save_icon.svg) 图标。 将添加收件人。

### 为自适应表单选择提交操作 {#selectsubmitactionforanadaptiveform}

在之后，添加 [!DNL Adobe Sign] 字段，启用 [!DNL Adobe Sign] 从表单容器中，选择 [!DNL Adobe Sign] Cloud Service并添加Adobe Sign协议收件人，为自适应表单选择相应的提交操作。 有关自适应Forms提交操作的详细信息，请参阅 [配置提交操作](configuring-submit-actions.md).

签署和提交表单是相互独立的。 在用户提交表单后，一旦创建Adobe Sign协议，就会立即提交自适应表单。 [!DNL AEM Forms] as a Cloud Service不会等待收件人签名或完成其他操作以提交自适应表单。 用户单击“提交”按钮或“摘要”步骤显示表单摘要后，即会立即提交表单。

此外， [!DNL Adobe Sign] 启用的自适应表单嵌入了Adobe Sign协议ID以提交数据。 您可以使用协议ID来使用自定义代码跟踪协议状态（需要自定义实施）。

Adobe Sign协议ID(agreementId)包含在自适应表单的提交数据中。 默认情况下，协议ID位于 `afSubmissionInfo` 已提交数据的节点。

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

或者，您也可以将绑定与协议ID(agreementId)关联。 它会将协议ID添加到已提交数据的afBoundData部分。 例如，在以下提交的数据中，协议ID绑定到 `<userName>` 节点：

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
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

您的表单签名体验已准备就绪。 您可以预览表单以验证签名体验。 在已发布的表单上， [!DNL Adobe Sign] 当收件人收到通过电子邮件签名的表单时，将显示块字段。 当 **[!UICONTROL 何时收件人与填写表单的人员相同？]** 选项被标记为“是”且满足条件时，用户在提交后将被重定向到Adobe Sign协议，用户可以立即对文档进行签名，而无需等待协议在电子邮件中显示。

## 为自适应表单配置云签名 {#configure-cloud-signatures-for-an-adaptive-form}

基于云的数字签名或远程签名是新一代的数字签名，可跨桌面、移动设备和Web使用，并满足对收件人身份验证的最高级别合规性和保证。 您可以使用基于云的数字签名对自适应表单进行签名。

之后 [编辑自适应表单属性Adobe Sign](working-with-adobe-sign.md#enableadobesign)，请执行以下步骤以将云签名字段添加到自适应表单：

1. 拖放 **[!UICONTROL Adobe Sign块]** 组件从组件浏览器转换到自适应表单。 的 [!UICONTROL Adobe Sign块] 组件具有所有受支持的 [!DNL Adobe Sign] 字段。 默认情况下，它会添加 **[!UICONTROL 签名]** 字段。

   ![符号块](assets/sign-block-new.png)

1. 选择 **[!UICONTROL Adobe Sign块]** 组件，然后点按 **[!UICONTROL 编辑]** ![编辑](assets/Smock_Edit_18_N.svg) 图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** 选择并添加 [!DNL Adobe Sign] 字段。 **B.** 展开 [!DNL Adobe Sign] 阻止全屏视图

1. 点按 **[!UICONTROL Adobe Sign字段]** ![Adobe Sign](assets/adobesign.png) 图标。 它会显示用于选择和添加的选项 [!DNL Adobe Sign] 字段。

   展开 **[!UICONTROL 类型]** 要选择的下拉字段 **[!UICONTROL 数字签名]** 并点按 **[!UICONTROL 完成]** 图标以将选定字段添加到 [!DNL Adobe Sign] 块。

   ![数字签名](assets/digital_signatures_new.png)

   必须为字段提供唯一的名称。

   使用以下方法将数字签名应用到自适应表单：

   * 云签名：使用 [数字ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服务提供商托管。
   * Adobe Acrobat或Reader:使用Adobe Acrobat或Reader下载并打开文档，以使用智能卡、USB令牌或基于文件的数字ID进行签名。

   将云签名字段添加到自适应表单后，请执行以下步骤以完成配置过程：

   * [为自适应表单启用Adobe Sign](#enableadobsignforanadaptiveform)
   * [为自适应表单选择Adobe Sign Cloud Service](#selectadobesigncloudserviceforanadaptiveform)
   * [将收件人添加到自适应表单](#addsignerstoanadaptiveform)
   * [为自适应表单选择提交操作](#selectsubmitactionforanadaptiveform)


### 配置感谢页面或摘要步骤组件 {#configure-the-thank-you-page-or-summary-step-component}

的 **[!UICONTROL 摘要步骤]** 组件会自动提交表单，在自定义的“摘要”页面中填充信息，并显示已提交表单的摘要。 摘要步骤组件具有可用于表单的全宽。 建议在包含摘要步骤组件的部分上不要包含任何其他组件。

## 常见问题 {#frequently-asked-questions}

**问：** 您可以在另一个自适应表单中嵌入自适应表单。 嵌入式自适应表单是否 [!DNL Adobe Sign] 已启用？
**答：** 否，Experience Manager Forms不支持使用嵌入了 [!DNL Adobe Sign] 启用了用于签名的自适应表单

**问：** 当我使用高级模板创建自适应表单并将其打开进行编辑时，会显示一条错误消息“电子签名或收件人的配置不正确”。 中。 如何解决错误消息？
**答：** 使用高级模板创建的自适应表单配置为使用 [!DNL Adobe Sign]. 要解决错误，请创建并选择 [!DNL Adobe Sign] 云配置和配置 [!DNL Adobe Sign] 自适应表单的收件人。

**问：** 我能用一下吗 [!DNL Adobe Sign] 自适应表单的静态文本组件中的文本标记？
**答：** 是，您可以在文本组件中使用文本标记来添加 [!DNL Adobe Sign] “记录文档”（仅“自动生成的记录文档”选项）的字段。 要了解创建文本标记的过程和规则，请参阅 [Adobe Sign文档](https://helpx.adobe.com/sign/using/text-tag.html). 另请注意，自适应Forms对文本标记的支持有限。 您可以使用文本标记仅创建那些满足以下条件的字段 [Adobe Sign块](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支持。

## 故障诊断 {#troubleshoot}

### [!DNL Adobe Sign] 协议失败 {#adobe-sign-agreement-failures}

**问题**
When [!DNL Adobe Sign] 为自适应表单配置了服务，则服务无法创建 [!DNL Adobe Sign] 基础自适应表单的协议。

**解决方法**

* 检查 [Adobe Sign Cloud Service配置](adobe-sign-integration-adaptive-forms.md) 在自适应表单中使用。
* 确保API应用程序位于 [!DNL Adobe Sign] 用于配置的服务器 [!DNL Adobe Sign] Cloud Service具有所需的权限。
* 如果您使用多个 [!DNL Adobe Sign] Cloud Services，指向 **[!UICONTROL oAuth URL]** 所有服务都提供 **[!UICONTROL Adobe Sign·沙德]**.

* 使用单独的电子邮件地址来配置 [!DNL Adobe Sign] 帐户和第一个或单个收件人的帐户。 第一个收件人或唯一收件人（如果有单个收件人）的电子邮件地址不能与 [!DNL Adobe Sign] 用于配置AEM云服务的帐户。

## 相关文章 {#related-articles}

* [集成 [!DNL Adobe Sign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [使用的最佳实践 [!DNL Adobe Sign] 带自适应Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
