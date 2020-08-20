---
title: 代码质量测试-Cloud Services
description: 代码质量测试-Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---


# 代码质量测试 {#code-quality-testing}

代码质量测试会评估应用程序代码的质量。 它是仅代码质量管道的核心目标，在所有非生产和生产管道中立即执行构建步骤。

请参阅 [配置CI-CD管道](/help/implementing/cloud-manager/configure-pipeline.md) ，进一步了解不同类型的管道。

## Understanding Code Quality Rules {#understanding-code-quality-rules}

在“代码质量测试”中，将扫描源代码，确保它满足某些质量标准。 目前，这是通过SonarQube和使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则，这些规则结合了通用Java规则和AEM特定规则。 某些AEM特定规则是根据AEM工程部门的最佳实践创建的，称为“自定 [义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)”。

>[!NOTE]
>您可以在此处下载规则的完整 [列表](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx)。

**三层门**

此代码质量测试步骤中有三层结构，用于解决已发现的问题：

* **关键**:这些问题由门确定，导致管道立即失效。

* **重要说明**:这些是由门标识的问题，导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以改写问题，在这种情况下，管道将继续，或者他们可以接受问题，在这种情况下，管道会因故障而停止。

* **信息**:这些问题由网关确定，它们仅用于提供信息，对管道执行没有影响

此步骤的结果将作为评 *级提供*。

下表总结了每个“严重”、“重要”和“信息”类别的等级和故障阈值：

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全等级 | A = 0漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性等级 | A = 0错误 <br/>B =至少1个次要错误 <br/>C =至少1个主要错误 <br/>D =至少1个关键错误E =至少1个阻止程序错误 | 重要信息 | &lt; C |
| 可维护性等级 | 代码气味的未平仓修复成本为： <br/><ul><li>&lt;=5%已进入应用程序的时间，评级为A </li><li>评级在6%到10%之间是B </li><li>11%到20%的评级是C </li><li>21%到50%的评级是D</li><li>超过50%的东西</li></ul> | 重要信息 | &lt; A |
| 范围 | 单位测试线覆盖和条件覆盖的混合使用以下公式： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>其中：CT =运行单元测试时已至少评估为“true”的条件 <br/>CF =运行单元测试时已至少评估为“false”的条件 <br/>LC =覆盖行=行=到覆盖——未覆盖行 <br/><br/> B =条件总数 <br/>EL =可执行行（lines到覆盖）总数 | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数。 | 信息 | > 1 |
| 未解决问题 | 总体问题类型——漏洞、错误和代码气味 | 信息 | > 0 |
| 复制行 | 重复块中涉及的行数。 <br/>对于要视为重复的代码块： <br/><ul><li>**非Java项目：**</li><li>至少应有100个连续令牌和重复令牌。</li><li>这些令牌至少应在以下位置传播： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，适用于其他语言</li><li>**Java项目：**</li><li> 无论令牌和行的数量如何，都至少应有10个连续和重复的语句。</li></ul> <br/>在检测重复时，会忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的Cloud Service兼容性问题数。 | 信息 | > 0 |

>[!NOTE]
>
>有关更 [详细的定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，请参阅度量定义。


>[!NOTE]
>
>要进一步了解Cloud Manager执行的自定义代码质 [!UICONTROL 量规则]，请参阅 [自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

## 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际上没有问题的问题。 这称为“假阳性”。

在这些情况下，可以使用标准Java注释对源代 `@SuppressWarnings` 码进行注释，该注释将规则ID指定为注释属性。 例如，一个常见问题是，用于检测硬编码密码的SonarQube规则在如何识别硬编码密码方面可能具有攻击性。

要查看特定示例，此代码在AEM项目中很常见，该项目具有连接到某些外部服务的代码：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然后，SonarQube将引发阻止程序漏洞。 查看代码后，您会发现这不是漏洞，并可以使用相应的规则ID对此进行注释。

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

然后，正确的解决方案是删除硬编码密码。

>[!NOTE]
>
>尽管最好尽量使注释具 `@SuppressWarnings` 体，即仅注释导致问题的特定语句或块，但也可以在类级别添加注释。

>[!NOTE]
>虽然没有明确的安全测试步骤，但在代码质量步骤中仍会评估与安全相关的代码质量规则。 请参阅AEM [的安全概述作为Cloud Service](/help/security/cloud-service-security-overview.md) ，进一步了解Cloud Service中的安全性。
