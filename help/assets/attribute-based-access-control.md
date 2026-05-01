---
title: 基于属性的访问控制
description: 了解如何启用基于属性的访问控制来定义基于元数据的规则，以定义对Content Hub中可用资源的访问级别
role: Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="适用于AEM Assets)。"
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: b736af556c8580d005097c27cceba050b21a57c9
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 2%

---


# 基于属性的访问控制 {#attribute-based-access-control}

基于属性的访问控制(ABAC)允许Content Hub管理员定义基于元数据的规则，以控制对Content Hub中可用资源的访问级别。

组织的管理员为用户组定义规则，这些规则将映射到组ID。 规则是[逻辑运算符和比较运算符](#supported-rule-constructs)的组合，管理员可以根据需要定义任意数量的规则，以管理Content Hub中的资源访问。

规则基于元数据。 如果规则中定义的条件与资源元数据匹配，则会向用户组显示资源。 Content Hub扫描&#x200B;**所有Assets**&#x200B;和&#x200B;**收藏集**&#x200B;内所有可用资源的资源元数据（包括自定义元数据），向用户组显示结果。

例如，当资产元数据与“Brand = Brand X”和“Region = EMEA或美洲”匹配时，允许访问组ID = 1011的用户组。 Content Hub只向ID = 1011的用户组显示这些资产，其中“Brand = Brand X”和“Region = EMEA或美洲”。

可以使用以下方法配置Content Hub中的ABAC规则：

* **自助配置**&#x200B;使用Content Hub中的[AI助手](#configure-abac-using-ai-assistant-in-content-hub)，由AEM治理代理提供支持
* **基于电子表格的配置**&#x200B;到[Adobe支持](#configure-abac-using-spreadsheet)

借助Content Hub中的AI助手，管理员可以使用元数据和自然语言定义和管理ABAC规则。 这可以加快规则配置速度并减少对手动支持工作流程的依赖性。

基于属性的访问控制的一些主要优势包括：

* 消除了权限对文件夹结构的依赖
* 允许管理员上传资产并追溯确定权限结构
* 减少重复项的数量并提高资产完整性。 当与不同组共享相同的资产时，基于文件夹的权限需要重复项。
* 实现基于规则的粒度访问
* 支持跨品牌和区域的可扩展治理
* 改进资产管理

>[!VIDEO](https://video.tv.adobe.com/v/3475413/?learn=on&enablevpops){transcript=true}

## 如何启用基于属性的访问控制 {#enable-attribute-based-access-control}

可以使用以下方法配置Content Hub中的ABAC规则：

* **在Content Hub中使用AI助手（由AEM治理代理提供支持）进行自助配置**\
  管理员可以使用Content Hub中的自然语言直接定义和管理ABAC规则。

* 通过Adobe支持&#x200B;**基于电子表格的配置**\
  管理员可以在电子表格中定义ABAC规则，并通过Adobe支持部门提交以进行配置。

## 在Content Hub中使用AI助手配置ABAC

借助由AEM治理代理提供支持的Content Hub中的AI Assistant，您可以使用自然语言直接在Content Hub中创建和管理ABAC规则。

您可以：
* 搜索现有规则
* 创建规则
* 更新规则
* 删除规则

这使管理员能够创建和管理访问规则，而无需依赖支持工作流。

### 开始之前 {#before-you-begin-ai-assistant}

在为ABAC规则配置使用Content Hub中的AI助手之前，请确保以下各项：

* 您已获得AEM as a Cloud Service的许可
* 由AEM治理代理提供支持的AI助手适用于您的组织
* 如果您还没有访问权限，请联系您的Adobe代表并完成所需的许可步骤
* try-buy程序不需要GenAI乘客

### 使用AI Assistant配置ABAC规则的步骤 {#steps-ai-assistant}

1. 在Content Hub中打开AI助手。

1. 从简单的说明开始。

   例如：

   `Create a new rule in Content Hub`

   AI Assistant将指导您了解创建规则所需的信息。

1. 用自然语言定义规则。

   例如：

   `Frescopa Web Marketers user group should have access to assets where product equals Frescopa`

1. 选择必须应用ABAC规则的环境。

1. 在应用规则之前对其进行检查。

   AI Assistant生成规则的结构化预览。 不会自动应用任何内容。 您可以查看生成的规则，根据需要对其进行调整，或者在应用它之前取消操作。

1. 保存并应用规则。

   保存后，将根据元数据动态强制实施规则。

此审核步骤有助于确保应用规则之前的准确性。

### 使用提示管理ABAC规则 {#manage-abac-rules-using-prompts}

开始使用AI Assistant后，您可以通过对话方式管理ABAC规则。

**发现规则**

* 显示所有现有的Content Hub ABAC规则

**创建规则**

* 创建规则以授予产品营销组访问所有资产的权限
* 授予销售组访问地区等于EMEA的资产的权限

**更新规则**

* 更新要包含APAC的EMEA营销组的规则

**删除规则**

* 删除产品营销组的规则

**浏览元数据和组**

* 显示可用组和元数据属性以设置规则

## 使用电子表格配置ABAC

如果贵组织未启用AI助手，则可以使用基于电子表格的工作流配置ABAC规则。

单击&#x200B;**下载电子表格**&#x200B;下载并在电子表格中定义规则。 创建Adobe支持工单并将电子表格中定义的规则提供给Adobe。

[!BADGE 下载电子表格]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}

使用本文所述的准则在电子表格中定义规则。

>[!IMPORTANT]
>
>定义规则后，导航到电子表格的&#x200B;**验证错误**&#x200B;选项卡，然后单击&#x200B;**运行ABAC验证**。 通过&#x200B;**所有验证**&#x200B;消息确认您可以向Adobe提供定义的规则。

### 使用电子表格配置ABAC规则的步骤 {#steps-spreadsheet}

1. 下载ABAC电子表格模板。
1. 使用基于元数据的条件在电子表格中定义规则。
1. 将每个规则映射到相应的IMS组ID。
1. 在注释中捕获规则的业务意图。
1. 提交Adobe支持工单并与Adobe共享已完成的电子表格。
1. Adobe为您的组织配置规则。

## 基于属性的访问控制用例示例 {#example-metadata-based-rules}

为了支持大规模的营销推广，地区和品牌的不同团队成员需要访问数字资产。 每个角色都有一个基于地区和品牌的特定范围。 ABAC使用资源元数据自动实施这些规则。 下表说明了此用例的角色以及应用的规则：

| 用户画像 | 角色 | 角色描述 | 组标识 | ABAC规则 |
|---|---|---|---|---|
| John | EMEA营销主管 | 监督EMEA地区所有品牌的营销执行。 需要访问所有面向EMEA市场的品牌的已批准资产。 | 集团欧洲、中东和非洲地区营销 | 区域=“EMEA” |
| 迈克 | APAC营销主管 | 监督APAC中所有品牌的营销执行。 需要访问所有面向APAC市场的品牌的已批准资产。 | 群营销(apac) | 区域=“APAC” |
| 苏菲 | 品牌X管理器(EMEA) | 管理EMEA地区的Brand X标识。 只需要看到针对EMEA市场定制的Brand X认可的内容。 | group-emea-brandx | 地区= “EMEA”和&amp;品牌= “品牌X” |
| Tom | Brand Y Manager (APAC) | 在APAC中管理品牌Y标识。 只需查看针对APAC市场定制的Brand Y认可内容。 | 群 — apac — 白兰地 | 地区=“APAC”和&amp;品牌=“Brand Y” |

利用这些规则，Content Hub管理员可以：

* **基于规则的粒度访问**：用户只能查看与其区域和品牌相关的资产，而无需手动分配权限。
* **无缝的全球协作**：区域和品牌团队并行工作，无访问冲突。
* **可扩展和未来验证的权限**：随着新区域或品牌的添加，可以根据元数据更新规则。

### ABAC有用的其他方案 {#additional-scenarios-abac}

ABAC还可以帮助解决以下情况：

* **全球品牌和区域访问**：团队只能看到与其品牌和市场相关的资产。
* **代理和合作伙伴协作**：外部代理和合作伙伴只能访问与其相关的营销活动资产。
* **不同团队基于角色的访问权限**：营销、销售和法律等团队可以访问与其职能相关的资产。
* **特定于区域的法律合规性**：可以将用户限制为仅使用针对特定法规或区域要求批准的资产。

>[!IMPORTANT]
>
>默认情况下，[电子表格](#configure-abac-spreadsheet)中未使用任何规则指定的所有其他用户组将被拒绝访问。 如果用户不属于为其定义了ABAC规则的任何组，则他们无法访问任何资产。 如果某些用户必须对所有资源（例如管理员）拥有访问权限，请在电子表格中包含一个具有组ID的组，并指定该组需要访问所有资源，以便Adobe可以对其进行相应配置。

## 支持的规则结构 {#supported-rule-constructs}

* **逻辑运算符**：
   * AND：所有条件都必须为true
   * 或：必须至少有一个条件为true

* **比较运算符**：
   * 等于(=)：检查用户或资产属性是否与某个值匹配
   * 不等于(!=)：检查用户或资产属性是否与值不匹配

当资源元数据字段包含数组（例如多个区域或标记）时，等于表示包含逻辑，不等于表示不包含逻辑。

这使您能够编写简单而富于表达力的规则，例如ALLOW if region = emea AND assetType != prototype AND tags != confidential。

## 准则 {#guidelines-attribute-based-access-control}

以下准则适用于基于AI Assistant和基于电子表格的配置：

* ABAC规则仅适用于已批准用于Content Hub的资产。 有关详细信息，请参阅[批准适用于Content Hub的Assets](/help/assets/approve-assets-content-hub.md)。
* 不要定义DENY规则。 始终将DENY规则转换为ALLOW规则。 例如，如果assetType = prototype AND confidential = yes，则ALLOW if region = user-region AND（如果assetType != prototype OR confidential != yes），则可以转换为ALLOW。
* ABAC规则使用IMS组ID应用于用户组，该ID可在Admin Console中使用。
* 您可以使用AEM as a Cloud Service创作环境为资源设置[批准目标](/help/assets/approve-assets-content-hub.md#set-approval-target)。 ABAC规则应用于通过审批目标= Content Hub审批的资产，因为审批目标=交付适用于可用于交付+ Content Hub的资产。 Assets标记为批准目标=投放对Content Hub中的所有人可见。
* 确保ABAC规则中使用的元数据架构已正确定义，并且在AEM中可用。 提供AEM中用于定义ABAC规则中所引用属性的元数据架构或架构的完整路径。 您可以选择创建包含与ABAC条件匹配的示例资产的测试文件夹，以帮助验证规则行为并准确评估访问权限。
* 在注释中捕获规则的业务意图，即使条件已正确写入，因为意图有助于验证和更正逻辑（如果需要）。
* 确保跨资产一致地维护用于访问规则的元数据值，如品牌、区域和产品。
* 从基于品牌或基于区域的访问等关键用例开始。
* 使用AI Assistant定义规则时，使用清除提示。 用商业语言描述意图，以便AI Assistant可以将其转换为结构化规则。
* 为DRM设置的PDF许可证文件必须对所有用户可见，以便他们在下载带许可证的资源时查看许可证信息。

## 常见问题解答 {#faqs-attribute-based-access-control-content-hub}

### AEM Assets Content Hub中基于属性的访问控制(ABAC)是什么？

AEM Assets Content Hub中基于属性的访问控制(ABAC)允许管理员定义基于元数据的规则，以控制不同用户组对数字资源的访问级别。 访问权限由资源元数据是否与规则中指定的条件匹配来确定，从而允许对资源可见性进行精细的动态管理。

### 管理员如何在AEM Assets Content Hub中使用ABAC定义访问规则？

管理员通过基于资产元数据（例如品牌或区域）创建条件并将这些条件链接到特定用户组ID来定义访问规则。 这些规则使用逻辑运算符和比较运算符来准确地指定哪些资产对哪些用户组可见。

### 在AEM Assets Content Hub中使用ABAC与传统基于文件夹的权限相比有何主要好处？

ABAC消除了对权限文件夹结构的依赖性，允许管理员上传资产和追溯分配权限，并减少所需的重复资产数量。 这提高了资产完整性并简化了权限管理，尤其是在资产需要与多个组共享时。

### 管理员能否直接在AEM Assets Content Hub界面中设置ABAC规则？

管理员可以使用Content Hub中的AI助手配置ABAC规则（如果为其组织启用了）。 他们还可以通过Adobe支持继续使用基于电子表格的工作流。

### 在AEM Assets Content Hub中设置ABAC规则时，可以使用哪些类型的元数据条件？

AEM Assets Content Hub中的ABAC规则可以使用逻辑运算符（例如AND和OR）以及比较运算符（例如，等于和不等于）。 必须在规则中使用的元数据属性进行正确定义，并且可在AEM元数据架构中使用，这些元数据属性可以包含区域、品牌、产品、营销活动、资源类型或发布状态等字段。

### 为什么AEM Assets Content Hub ABAC对于拥有大型团队和多种资源需求的组织特别有用？

ABAC对于拥有大型团队的组织非常有用，因为它可以根据用户角色、区域、品牌或业务需求实现基于规则的细粒度资产访问。 它确保用户只能看到与其职责相关的资产，而无需手动分配权限或过度重复资产。

### 在将ABAC电子表格提交到AEM Assets Content Hub支持之前，管理员应该如何为Adobe准备该电子表格？

管理员应在Adobe Admin Console中创建用户组，记下其组ID，明确定义电子表格中每个组的权限和条件，确保所有元数据属性正确映射到相应的架构，并使用注释列阐明每个规则的业务意图。