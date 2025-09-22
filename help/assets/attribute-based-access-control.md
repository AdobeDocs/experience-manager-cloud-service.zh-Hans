---
title: 基于属性的访问控制
description: 了解如何启用基于属性的访问控制来定义基于元数据的规则，以定义对Content Hub中可用资源的访问级别
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: 0833e31d37c473d37e16ee037823e61611622322
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 4%

---

# 基于属性的访问控制 {#attribute-based-access-control}

基于属性的访问控制(ABAC)允许Content Hub管理员定义基于元数据的规则，以定义对Content Hub中可用资源的访问级别。

组织的管理员为用户组定义规则，这些规则将映射到组ID。 规则是[逻辑运算符和比较运算符的组合](#supported-rule-constructs)，管理员可以定义任意数量的规则，以便在Content Hub中管理资源访问。

这些规则基于元数据，如果规则中定义的条件与资源元数据匹配，则资源将向用户组显示。 Content Hub扫描&#x200B;**所有Assets**&#x200B;和&#x200B;**收藏集**&#x200B;内所有可用资源的资源元数据（包括自定义元数据）以向用户组显示结果。

例如，当资产元数据与“Brand = Brand X”和“Region = EMEA或美洲”匹配时，允许访问组ID = 1011的用户组。 Content Hub只向ID为1011的用户组显示品牌为`Brand X`且地区为`EMEA`或`Americas`的那些资源。

基于属性的访问控制的一些主要优势包括：

* 消除了权限对文件夹结构的依赖

* 允许管理员上传资产并追溯确定权限结构

* 减少重复数量 - 提高资产完整性。当同一资产被不同组共享时，基于文件夹的权限需要设置副本。

## 如何启用基于属性的访问控制？ {#enable-attribute-based-access-control}

截至目前，您无法使用Content Hub用户界面自行创建基于属性的访问控制规则。

单击&#x200B;**下载电子表格**&#x200B;下载并在电子表格中定义规则。 创建Adobe支持工单并将电子表格中定义的规则提供给Adobe。

[!BADGE 下载电子表格]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}


使用本文中定义的准则，在电子表格中定义规则。

>[!IMPORTANT]
>
> 定义规则后，导航到电子表格的&#x200B;**验证错误**&#x200B;选项卡，然后单击&#x200B;**运行ABAC验证**。 **所有验证均通过**&#x200B;消息，确认您可以向Adobe提供定义的规则。

## 基于属性的访问控制用例示例 {#example-metadata-based-rules}

为了支持大规模的营销推广，地区和品牌的不同团队成员需要访问数字资产。 每个角色都有一个基于地区和品牌的特定范围。 ABAC通过资产元数据自动实施这些规则。 下表说明了此用例的不同角色类型以及应用的规则：

| 角色 | 角色 | 角色描述 | 组标识 | ABAC规则 |
|---------------------|----------------|-----------------|------------|------------|
| John | EMEA营销主管 | 监督EMEA地区所有品牌的营销执行。 需要访问所有面向EMEA市场的品牌的已批准资产。 | 集团欧洲、中东和非洲地区营销 | 区域=“EMEA” |
| 迈克 | APAC营销主管 | 监督APAC中所有品牌的营销执行。 需要访问所有面向APAC市场的品牌的已批准资产。 | 群营销(apac) | 区域=“APAC” |
| 苏菲 | 品牌X管理器(EMEA) | 管理EMEA地区的Brand X标识。 只需要看到针对EMEA市场定制的Brand X认可的内容。 | group-emea-brandx | 地区= “EMEA”和&amp;品牌= “品牌X” |
| Tom | Brand Y Manager (APAC) | 在APAC中管理品牌Y标识。 只需查看针对APAC市场定制的Brand Y认可内容。 | 群 — apac — 白兰地 | 地区=“APAC”和&amp;品牌=“Brand Y” |

利用这些规则，Content Hub管理员可以：

* **基于规则的粒度访问**：用户只能看到与其区域和品牌相关的资产 — 没有手动权限分配。

* **无缝的全球协作**：区域和品牌团队并行工作，没有访问冲突。

* **可扩展和未来验证的权限**：随着新区域或品牌的添加，可以根据元数据更新规则。

>[!IMPORTANT]
>
> 默认情况下，[电子表格](#enable-attribute-based-access-control)中未使用任何规则指定的所有其他用户组将被拒绝访问。 如果用户不属于为其定义了ABAC规则的任何组，则他们无法访问任何资产。 如果您需要让一些用户拥有对所有资源的访问权限（例如，管理员），则必须在电子表格中提及具有组ID的组，其中包含该特定组需要访问所有资源的详细信息，并且Adobe会为您配置该组。


## 支持的规则结构 {#supported-rule-constructs}

* **逻辑运算符**：
   * AND：所有条件都必须为true
   * 或：必须至少有一个条件为true
* **比较运算符**：
   * 等于(=)：检查用户或资产属性是否与某个值匹配
   * 不等于(！=)：检查用户或资产属性是否与值不匹配

当资源元数据字段包含数组（例如，多个区域或标记）时，`Equals`引用`contains`逻辑，`Not Equals`引用`does not contain`逻辑。

这允许您编写简单而有表达性的规则，例如：如果区域= emea和assetType ，则允许！=原型和标记！=机密。

## 准则 {#guidelines-attribute-based-access-control}

* ABAC规则仅适用于已批准用于Content Hub的资产。 有关详细信息，请参阅[批准适用于Content Hub的Assets](/help/assets/approve-assets-content-hub.md)。

* 不提供DENY规则，而是始终将DENY转换为ALLOW规则。 例如，`ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes`可以转换为`ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`。

* ABAC规则使用IMS组ID应用于用户组，该ID可在Admin Console中使用。


* 您可以使用AEM as a Cloud Service创作环境为资源设置[批准目标](/help/assets/approve-assets-content-hub.md#set-approval-target)。 ABAC规则应用于审批目标= `Content Hub`的已审批资产，因为审批目标= `Delivery`适用于可用于`Delivery` + `Content Hub`的资产。 标记为批准目标= `Delivery`的Assets对内容中心中的所有人可见。

* 确保ABAC规则中使用的元数据架构已正确定义，并且在AEM中可用。 提供AEM中元数据架构的完整路径，这些架构定义ABAC规则中引用的属性。 您可以选择创建一个测试文件夹，其中包含一些元数据值与ABAC条件匹配的示例资源。 这有助于验证规则行为并准确评估访问权限。

* 捕获评论中规则的业务意图，无论条件是否正确写入，因为意图有助于我们验证并更正逻辑（如果需要）。

* 为DRM设置的许可证PDF文件需要对所有人可见，以便用户在使用许可证下载资源时能够看到这些文件。
