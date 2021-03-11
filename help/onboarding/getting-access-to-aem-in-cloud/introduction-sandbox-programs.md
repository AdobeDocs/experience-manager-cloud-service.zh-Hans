---
title: '沙箱项目简介 '
description: '沙箱项目简介 '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 沙箱项目{#sandbox-programs}简介

## 简介 {#introduction}

沙箱项目是AEM Cloud Service中可用的两种项目类型之一，另一种是生产项目。

通常，创建沙箱是为了满足培训、运行演示、启用或概念验证(POC)的目的。他们不能载着实时的交通。 它们不受[AEM作为Cloud Service承诺的约束](https://www.adobe.com/legal/service-commitments.html)。

在沙箱中创建的环境未配置为自动缩放。 因此，这些环境不适合用于性能或负载测试。

沙箱项目包括“站点”和“资产”，并自动填充Git存储库、开发环境和非生产渠道。  Git存储库会填充基于AEM Project原型的示例项目。

请参阅[了解项目和项目类型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)，进一步了解项目类型。

### 沙箱项目{#attributes-sandbox}的属性

沙箱项目具有以下属性：

1. **项目创建：** 沙箱项目创建包括自动：
   * 使用示例代码和内容设置项目
   * 开发环境
   * 创建非生产管道部署到开发环境(部署到开发环境的主控分支)

1. **解决方案：** 沙箱项目包括AEM Sites和资产。

1. **AEM更新：** AEM更新可以手动应用于沙箱项目中的环境，且不会自动推送。有关详细信息，请参阅[AEM沙箱环境的更新](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox)。

1. **休眠：** 如果在某段时间内未检测到活动，沙箱项目中的环境将自动休眠。冬眠环境可以手动解除冬眠。
有关详细信息，请参阅[冬眠和脱冬沙箱环境](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)。