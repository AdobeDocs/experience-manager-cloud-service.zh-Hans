---
title: '沙盒程序简介 '
description: 沙盒程序简介
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 3b57acc47dd60d050ceebebb12bd9080b7fc5cf5
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 沙盒程序简介{#sandbox-programs}

## 简介 {#introduction}

沙盒程序是AEMCloud Service中可用的两种程序类型之一，另一种是生产程序。

通常创建沙盒是为了用于培训、运行演示、启用或概念验证(POC)。它们不能载上实时流量。 它们不受[AEM as a Cloud Service承诺的约束](https://www.adobe.com/legal/service-commitments.html)。

在沙盒中创建的环境未配置为自动缩放。 因此，这些环境不适合进行性能或负载测试。

沙盒程序包括站点和资产，并自动填充了Git存储库、开发环境和非生产管道。  Git存储库会使用基于AEM项目原型的示例项目填充。

请参阅[了解程序和程序类型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) ，了解有关程序类型的更多信息。

### 沙盒程序的属性{#attributes-sandbox}

沙盒程序具有以下属性：

1. **项目创建：** 沙盒项目创建包括自动：
   * 使用示例代码和内容设置项目
   * 开发环境的创造
   * 创建非生产管道部署到开发环境(主控的分支部署到开发环境)

1. **解决方案：** 沙盒项目包括AEM Sites和Assets。

1. **AEM更新：** AEM更新可以手动应用于沙盒项目中的环境，且不会自动推送。有关更多详细信息，请参阅[AEM对沙盒环境的更新](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) 。

1. **休眠：** 如果在特定时间段内未检测到任何活动，则沙盒项目中的环境将自动休眠。沙盒在处于非活动状态8小时后会进入休眠节点，在此之后，它们可以解除休眠。 可以手动解除休眠环境。
有关更多详细信息，请参阅[休眠和解除休眠沙盒环境](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)。

1. **删除**:沙箱在连续休眠模式下6个月后被删除，之后可以重新创建。
