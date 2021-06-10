---
title: 代码质量测试 — Cloud Services
description: 代码质量测试 — Cloud Services
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: 64023bbdccd8d173b15e3984d0af5bb59a2c1447
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 1%

---

# 代码质量测试{#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="代码质量测试"
>abstract="代码质量测试会评估应用程序代码的质量。 它是仅代码质量管道的核心目标，将在所有非生产和生产管道中的构建步骤之后立即执行。"

代码质量测试会评估应用程序代码的质量。 它是仅代码质量管道的核心目标，将在所有非生产和生产管道中的构建步骤之后立即执行。

请参阅[配置CI-CD管线](/help/implementing/cloud-manager/configure-pipeline.md) ，了解有关不同类型管线的更多信息。

## 了解代码质量规则{#understanding-code-quality-rules}

在“代码质量测试”中，会扫描源代码以确保其符合特定质量标准。 目前，这是通过SonarQube与使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则可组合通用Java规则和特定于AEM的规则。 某些特定于AEM的规则是根据AEM Engineering中的最佳实践创建的，称为[Custom Code Quality Rules](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

>[!NOTE]
>您可以在此处[下载规则的完整列表。](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

**三层门**

此代码质量测试步骤中有一个三层结构，用于测试已识别的问题：

* **关键**:这些是由门确定的问题，会导致管道立即失败。

* **重要信息**:这些是门标识的问题，会导致管道进入暂停状态。部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下管道会继续），也可以接受问题（在这种情况下，管道会因故障而停止）。

* **信息**:这些是门标识的问题，这些问题仅供参考，对管道执行没有影响

此步骤的结果将作为&#x200B;*Ratings*&#x200B;提供。

下表汇总了每个“关键”、“重要”和“信息”类别的评级和故障阈值：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全评级 | A = 0漏洞<br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞<br/>D =至少1个关键漏洞<br/>E =至少1个拦截器漏洞 | 关键 | &lt; B |
| 可靠性评级 | A = 0错误<br/>B =至少1个次要错误<br/>C =至少1个主要错误<br/>D =至少1个关键错误E =至少1个拦截器错误 | 重要信息 | &lt; C |
| 可维护性评级 | 代码气味的未解决补救成本是：<br/><ul><li>&lt;> </li><li>评级在6%到10%之间为a B </li><li>11%到20%的评级为C </li><li>评级在21%到50%之间为D</li><li>超过50%的都是E</li></ul> | 重要信息 | &lt; A |
| 范围 | 使用以下公式的单位测试线覆盖率和条件覆盖率的混合：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>其中：CT =运行单元测试时已至少评估为“true”的条件，运行单元测试时测试<br/>CF =已评估为“false”的条件，运行单元测试时运行单元测试时至少评估一次，而运行单元测试时LC =覆盖行= linestocover — 未覆盖行<br/><br/>B =条件总数<br/>EL =可执行行(linestocover)的总数<br/> | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | > 1 |
| 未决问题 | 总体问题类型 — 漏洞、错误和代码气味 | 信息 | > 0 |
| 复制的行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块：  <br/><ul><li>**非Java项目：**</li><li>应至少有100个连续令牌和重复令牌。</li><li>这些令牌应至少在以下位置分布： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，用于其他语言</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都应至少有10个连续和重复的语句。</li></ul> <br/>在检测重复项时，将忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的Cloud Service兼容性问题的数量。 | 信息 | > 0 |

>[!NOTE]
>
>有关更多详细定义，请参阅[量度定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)。


>[!NOTE]
>
>要详细了解由[!UICONTROL Cloud Manager]执行的自定义代码质量规则，请参阅[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 处理误报{#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际上没有问题的问题。 这称为&#x200B;*false positive*。

在这些情况下，可以使用标准Java `@SuppressWarnings`注释对源代码进行注释，该注释指定规则ID作为注释属性。 例如，一个常见的问题是，用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能过于激进。

要查看特定示例，此代码在AEM项目中相当常见，该项目具有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube随后将引发拦截器漏洞。 查看代码后，您会发现这不是一个漏洞，并可以使用相应的规则ID对此进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代码是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那么，正确的解决方案就是删除硬编码密码。

>[!NOTE]
>
>尽管最好尽量使`@SuppressWarnings`注释具体（即仅对导致问题的特定语句或块添加注释），但可以在类级别添加注释。

>[!NOTE]
>虽然没有明确的安全测试步骤，但在代码质量步骤中仍会评估与安全相关的代码质量规则。 请参阅[AEM as a Cloud Service的安全概述](/help/security/cloud-service-security-overview.md) ，了解有关Cloud Service安全性的更多信息。
