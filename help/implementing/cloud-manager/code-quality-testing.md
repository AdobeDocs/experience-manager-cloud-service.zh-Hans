---
title: 代码质量测试
description: 了解管道的代码质量测试的工作原理，以及它如何提高部署质量。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: ca3c1f255b8441a8d376a55a5353d58848384b8b
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 2%

---

# 代码质量测试 {#code-quality-testing}

了解管道的代码质量测试的工作原理，以及它如何提高部署质量。

>[!CONTEXTUALHELP]
>
>
## Communications API {#introduction}

代码质量测试根据一组质量规则来评估应用程序代码。 它是仅代码质量管道的主要目的，将在所有生产和非生产管道中的构建步骤之后立即执行。

请参阅文档 [配置CI-CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 了解有关不同类型管道的更多信息。

## 代码质量规则 {#understanding-code-quality-rules}

代码质量测试会扫描源代码，以确保它符合特定质量标准。 这是通过SonarQube与使用OakPAL的内容包级别检查的组合来实现的。 有100多个规则，这些规则组合了通用Java规则和特定于AEM的规则。 某些特定于AEM的规则是根据AEM Engineering中的最佳实践创建的，称为 [自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
You can download the complete list of rules [with this link.](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### Three-Tiered Ratings {#three-tiered-gate}

Issues identified by code quality testing are assigned to one of three categories.

* **Critical** - These are issues which cause an immediate failure of the pipeline.

* **重要信息**  — 这些问题导致管道进入暂停状态。 部署经理、项目经理或业务所有者可以覆盖问题（在这种情况下管道会继续），也可以接受问题（在这种情况下，管道会因故障而停止）。

* **信息**  — 这些问题仅供参考，对管道执行没有影响

此步骤的结果将作为 **评级**.

下表汇总了每个关键、重要和信息类别的评级和故障阈值。

| 名称 | 定义 | 类别 | 失败阈值 |
|--- |--- |--- |--- |
| 安全评级 | A =无漏洞 <br/>B =至少1个次要漏洞<br/> C =至少1个主要漏洞 <br/>D =至少1个关键漏洞 <br/>E =至少1个阻止程序漏洞 | 关键 | &lt; B |
| 可靠性评级 | A =无错误 <br/>B =至少1个次要错误 <br/>C =至少1个主要错误 <br/>D =至少1个严重错误<br>E =至少1个阻止程序错误 | 关键 | &lt; D |
| 可维护性评级 | 由代码气味的未解决修复成本定义，以已进入应用程序的时间的百分比表示<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = > 50%</li></ul> | 重要信息 | &lt; A |
| 范围 | 由单位测试线覆盖率和条件覆盖率的混合使用公式定义： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` =已评估为 `true` 运行单元测试时至少一次</li><li>`CF` =已评估为 `false` 运行单元测试时至少一次</li><li>`LC` =覆盖行= lines_to_cover - oncovered_lines</li><li>`B` =条件总数</li><li>`EL` =可执行行的总数(linestocover)</li></ul> | 重要信息 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数 | 信息 | > 1 |
| 未决问题 | 总体问题类型 — 漏洞、错误和代码气味 | 信息 | > 0 |
| 复制的行 | 定义为重复块中涉及的行数。 在以下条件下，代码块会被视为重复的代码块。<br>非Java项目：<ul><li>应至少有100个连续令牌和重复令牌。</li><li>这些令牌应至少分布在以下几个位置： </li><li>COBOL的30行代码 </li><li>ABAP的20行代码 </li><li>10行代码，用于其他语言</li></ul>Java项目：<ul></li><li> 无论令牌和行的数量如何，都应至少有10个连续的和重复的语句。</li></ul>在检测重复项时，将忽略缩进和字符串文本中的差异。 | 信息 | > 1% |
| Cloud Service兼容性 | 已识别的云服务兼容性问题的数量 | 信息 | > 0 |

>[!NOTE]
请参阅 [SonarQube的度量定义](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) ，以了解更详细的定义。

>[!NOTE]
了解有关执行的自定义代码质量规则的更多信息 [!UICONTROL Cloud Manager]，请参阅此文档 [自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完美，有时会错误地识别实际上没有问题的问题。 这称为 **误报**.

在这些情况下，可以使用标准Java对源代码进行注释 `@SuppressWarnings` 将规则ID指定为注释属性的注释。 For example, one common false positive is that the SonarQube rule to detect hardcoded passwords can be aggressive about how a hardcoded password is identified.

以下代码在AEM项目中相当常见，该项目中有用于连接到某些外部服务的代码。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube随后会引发拦截器漏洞。 但是，在查看代码后，您会发现这不是一个漏洞，并且可以使用相应的规则ID对代码进行注释。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，如果代码为：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那么，正确的解决方案就是删除硬编码密码。

>[!NOTE]
虽然最好的做法是 `@SuppressWarnings` 尽可能具体的注释（即仅对导致问题的特定语句或块添加注释）可以在类级别添加注释。

>[!NOTE]
虽然没有明确的安全测试步骤，但在代码质量步骤中会评估与安全相关的代码质量规则。 请参阅文档 [AEMas a Cloud Service安全概述](/help/security/cloud-service-security-overview.md) 了解有关Cloud Service安全性的更多信息。

## 内容包扫描优化 {#content-package-scanning-optimization}

在质量分析流程中，Cloud Manager将对Maven内部版本生成的内容包进行分析。 Cloud Manager提供了优化功能来加快此过程，当发现某些包装约束时，这些功能非常有效。 最重要的是对输出单个内容包（通常称为“全部”包）的项目执行了优化，该包中包含由内部版本生成的许多其他内容包，这些内容包被标记为跳过。 当Cloud Manager检测到此方案时，将直接扫描各个内容包并根据依赖关系对其进行排序，而不是解压缩“所有”包。 例如，请考虑以下内部版本输出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` （跳过的内容包）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

如果 `myco-all-1.0.0-SNAPSHOT.zip` 是两个跳过的内容包，则将扫描两个嵌入的包，而不是“所有”内容包。

For projects that produce dozens of embedded packages, this optimization has been shown to save upwards of 10 minutes per pipeline execution.

A special case can occur when the &quot;all&quot; content package contains a combination of skipped content packages and OSGi bundles. 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 包含先前提到的两个嵌入式包以及一个或多个OSGi包，然后仅使用OSGi包构建一个新的、最小的内容包。 此包始终名为 `cloudmanager-synthetic-jar-package` 包装的包装在 `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
* 此优化不会影响部署到AEM的包。
* 由于嵌入的内容包与跳过的内容包之间的匹配基于文件名，因此如果多个跳过的内容包具有相同的文件名，或者在嵌入时更改了文件名，则无法执行此优化。

