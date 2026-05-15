---
title: Adobe Experience Manager as a Cloud Service的HIPAA准备工作
description: 了解Experience Manager as a Cloud Service对HIPAA法规的支持，以及如何在实施新的AEM as a Cloud Service项目时实现合规性。
feature: Compliance
role: Admin, Developer, Leader
exl-id: 9928811e-3487-430a-9e2f-04959460c95f
source-git-commit: c2b849ef25afd0809891a822a99ddd3059bf1919
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 8%

---

# Adobe Experience Manager as a Cloud Service的HIPAA准备工作 {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询您公司的法律部门，以获取有关HIPAA法规的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及这对于您这样的Adobe客户的意义的更多信息，请参阅：
>
>* Adobe信任中心中的[HIPAA和Adobe产品和服务](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)
>* [Adobe隐私中心](https://www.adobe.com/cn/privacy.html)

对于Adobe Experience Manager (AEM) as a Cloud Service，Adobe正在提供文档以帮助您了解HIPAA准备情况。 这些内容可帮助您符合相关法规。

## 健康保险流通与责任法案(HIPAA) {#health-insurance-portability-and-accountability-act-hipaa}

### 健康保险流通与责任法案(HIPAA) {#the-health-insurance-portability-and-accountability-act-hipaa}

HIPAA隐私、安全和违规通知规则为称为受保护健康信息(PHI)的单独可识别健康信息建立了重要的保护。

根据HIPAA，受保实体是医疗保健提供商、健康计划或医疗保健清算所。 业务联营公司乃向涉及存取PHI之受保实体提供服务之实体。 HIPAA隐私和安全规则要求被覆盖实体以商业伙伴协议(BAA)的形式从商业伙伴获得书面保证，该协议要求商业伙伴保护被覆盖实体的PHI的隐私和安全。

### 向Adobe提供PHI {#providing-phi-to-adobe}

Adobe充当其HIPAA就绪服务的业务联系人，该服务列在AEM as a Cloud Service中的[HIPAA就绪服务](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)下。

授权任何Adobe HIPAA就绪服务以处理PHI **的客户必须**&#x200B;具有正确的许可证以及与Adobe一起签名的访客BAA。

>[!IMPORTANT]
>
>客户不得在未指定为HIPAA就绪服务或未获得使用HIPAA就绪服务的相应许可证的Adobe产品和服务中创建、接收、维护或传输PHI。

### HIPAA共享责任 {#hipaa-shared-responsibilities}

Adobe HIPAA就绪服务依赖于共同责任安全模型，要求客户和Adobe各自在维护PHI安全方面承担不同的责任。 在此共享安全模型下，Adobe依赖客户使用和配置与HIPAA一致的适用于HIPAA的服务。

有关为支持HIPAA的服务执行Adobe BAA的更多信息，请联系您的Adobe销售代表或客户成功经理。

>[!IMPORTANT]
>
>**免责声明**：
>
>客户有责任使用Adobe HIPAA就绪服务，并负责确保Adobe HIPAA就绪服务满足其合规性要求。

有关详细信息，请参阅Adobe信任中心中的[HIPAA和Adobe产品和服务](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)。

## HIPAA术语 {#hipaa-terminology}

下表介绍了AEM服务如何根据HIPAA使用情况进行分类。

| HIPAA准备就绪 | 描述 |
| --- | --- |
| HIPAA就绪 | 旨在适当配置并与BAA一起使用时处理PHI。 |
| HIPAA未就绪 | 不能用于处理PHI，也不能用于与HIPAA相关的用例。 |

>[!NOTE]
>
>HIPAA就绪性分类基于每项服务的预期功能，并可能会随着时间的推移而改变。
>
>在规划与HIPAA相关的部署时，客户应该参考最新的文档和适用的合同条款。

## AEM as a Cloud Service中的HIPAA服务就绪性 {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

下表描述了哪些AEM服务可用于HIPAA，以及哪些服务可以与其一起使用。 符合HIPAA要求的服务需要为医疗保健购买扩展安全性，如[其他要求](#additional-requirements)中所述。

| 产品/功能 | 服务 | HIPAA准备就绪 |
| --- | --- | --- |
| AEM Sites | AEM Sites， AEM Publish， Edge Delivery Services | HIPAA就绪 |
| AEM Sites | 通用编辑器 | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |
| AEM Sites Optimizer | Sites Optimizer | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |
| AEM Assets | AEM Assets | HIPAA就绪 |
| AEM Assets | Content Hub | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |
| AEM Assets | Brand Portal | HIPAA未就绪 |
| AEM Assets | Dynamic Media OpenAPI | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |
| AEM Assets | Dynamic Media场景7 | HIPAA未就绪 |
| AEM Forms | AEM Forms、身份验证Facade服务、PDF实用工具服务 | HIPAA就绪 |
| AEM CIF | Commerce Integration Framework | HIPAA未就绪 |
| AEM Cloud Manager | AEM Cloud Manager、Release Orchestrator、版本切换、版本验证器 | HIPAA就绪 |
| AEM Cloud Manager | 软件分发 | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |
|   |   |   |
| AEM Guides  | AEM Guides  | HIPAA未就绪 |
|   |   |   |
| LLM Optimizer | LLM Optimizer | 未引入PHI时，无法将HIPAA就绪<br>[1]添加到扩展安全程序中。 |

>[!NOTE]
>
>[1]
>
>对于指明可以添加到扩展安全性计划中的HIPAA就绪型服务，客户必须确保不会将PHI路由到或存储在这些服务中。
>
>将PHI引入不符合HIPAA的服务可能会导致不合规的情况。

### 其他要求 {#additional-requirements}

[服务已列出](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)为HIPAA就绪，需要为医疗保健购买扩展安全性。

购买医疗保健扩展安全保护时，需要：

* 为该计划选择的产品已可使用HIPAA（如表中所列），
* 已为&#x200B;*每个*&#x200B;产品购买医疗保健扩展安全性；这将确保足够的Cloud Manager积分，
* 扩展的医疗保健安全保护在项目创建时应用。

如果满足要求，则可以在创建AEM程序时应用医疗保健的扩展安全性；有关详细信息，请参阅[设置](#setup)。

>[!NOTE]
>
>有关配置和定价的更多详细信息，请联系您的销售代表。

## 环境 {#environments}

*HIPAA就绪*&#x200B;不适用于RDE（快速开发环境）、开发或暂存环境，因为这些环境不允许使用PHI。

这意味着您必须：

* 将虚拟数据用于开发和测试目的
* 仅处理来自生产环境的PHI

下表显示了支持环境类型在HIPAA就绪时的位置。

| | RDE | 开发 | 暂存  | Prod |
| --- | --- | --- | --- | --- |
| 环境类型  | 否  | 否  | 否  | 是  |

## 设置 {#setup}

当您[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)时，[安全选项卡提供用于激活HIPAA保护](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)的选项。
