---
title: 代码质量测试
description: 了解管道代码质量测试的工作方式以及其提高部署质量的方式。
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 100%

---

# 代码质量测试 {#code-quality-testing}

了解管道代码质量测试的工作方式以及其提高部署质量的方式。

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="代码质量测试"
>abstract="代码质量测试根据一组质量规则评估应用程序代码。 它是代码质量专用管道的主要目的，并在所有生产和非生产管道的构建步骤之后立即执行。"

## 简介 {#introduction}

代码质量测试根据一组质量规则评估应用程序代码。 它是代码质量专用管道的主要目的，并在所有生产和非生产管道的构建步骤之后立即执行。

请参阅[配置您的 CI-CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)，了解更多有关不同类型管道的信息。

## 代码质量规则 {#understanding-code-quality-rules}

代码质量测试将扫描源代码以确保它符合特定的质量标准。 结合 SonarQube 和使用 OakPAL 的内容包级别检查来实现这一点。 有 100 多条规则结合了通用 Java 规则和特定于 AEM 的规则。 一些特定于 AEM 的规则基于来自 AEM Engineering 的最佳实践而创建，这些规则称作[自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)。

>[!NOTE]
>
>可以[使用此链接](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)下载规则的完整列表。

### 三层评级 {#three-tiered-gate}

代码质量测试确定的问题被分配到三个类别中的一个。

* **严重** – 这些是导致管道立即失效的问题。

* **重要** – 这些是导致管道进入暂停状态的问题。 部署经理、项目经理或业务负责人既可以覆盖问题，也可以接受问题，在前一种情况下，管道将继续运行，在后一种情况下，管道将停止并显示故障。

* **信息** – 这些是仅供参考并且对管道执行没有影响的问题

>[!NOTE]
>
>在仅代码质量管道中，无法覆盖代码质量审核中的重要故障，因为代码质量测试步骤是管道中的最后一个步骤。

### 评级 {#ratings}

此步骤的结果以&#x200B;**评级**&#x200B;的形式提供。

下表总结了每个关键、重要和信息类别的额定值和故障阈值。

| 名称 | 定义 | 类别 | 故障阈值 |
|--- |--- |--- |--- |
| 安全性评级 | A = 无漏洞<br/>B = 至少 1 个次要漏洞<br/>C = 至少 1 个主要漏洞<br/>D = 至少 1 个严重漏洞<br/>E = 至少 1 个阻断漏洞 | 严重 | &lt; B |
| 可靠性评级 | A = 无错误<br/>B = 至少 1 个次要错误<br/>C = 至少 1 个主要错误<br/>D = 至少 1 个严重错误<br>E = 至少 1 个阻断错误 | 严重 | &lt; D |
| 可维护性评级 | 定义为代码异味的未完成修复成本占应用程序已用时间的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 范围 | 在以下公式中结合使用单元测试行覆盖率和条件覆盖率来定义：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = 在运行单元测试时已评估为 `true` 至少一次的条件</li><li>`CF` = 在运行单元测试时已评估为 `false` 至少一次的条件</li><li>`LC` = 覆盖的行 = lines_to_cover - uncovered_lines</li><li>`B` = 条件总数</li><li>`EL` = 可执行的行总数 (lines_to_cover)</li></ul> | 重要 | &lt; 50% |
| 跳过的单元测试 | 跳过的单元测试数 | 信息 | > 1 |
| 未结问题 | 整体问题类型 – 漏洞、错误和代码异味 | 信息 | > 0 |
| 重复行 | 定义为重复块中涉及的行数。 在以下条件下，代码块被视为重复。<br>非 Java 项目：<ul><li>应有至少 100 个连续和重复的令牌。</li><li>这些令牌应至少分布在： </li><li>30 个代码行（对于 COBOL） </li><li>20 个代码行（对于 ABAP） </li><li>10 个代码行（对于其他语言）</li></ul>Java 项目：<ul></li><li> 无论令牌和行的数量如何，都应至少有 10 个连续和重复的语句。</li></ul>检测重复项时将忽略缩进和字符串文本的差异。 | 信息 | > 1% |
| Cloud Service 兼容性 | 确定的 Cloud Service 兼容性问题数 | 信息 | > 0 |

>[!NOTE]
>
>有关更多详细信息，请参阅 [SonarQube 的量度定义。](https://docs.sonarqube.org/latest/user-guide/metric-definitions/)

>[!NOTE]
>
>要了解有关 [!UICONTROL Cloud Manager] 运行的自定义代码质量规则的更多信息，请参阅[自定义代码质量规则。](/help/implementing/cloud-manager/custom-code-quality-rules.md)

## 处理误报 {#dealing-with-false-positives}

质量扫描过程并不完善，有时会错误地识别出实际上并不是问题的问题。 此情况称作&#x200B;**误报**。

在这些情况下，可以使用标准 Java `@SuppressWarnings` 注释为源代码添加注释，并将规则 ID 指定为注释属性。例如，一种常见误报是用于检测硬编码密码的 SonarQube 规则可能会妨碍识别硬编码密码的方式。

以下代码在 AEM 项目中相当常见，其中包含用于连接到某些外部服务的代码。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

之后，SonarQube 将引发阻断漏洞。 不过，在查看代码后，您会发现这并不是漏洞，并且可以使用适当的规则 ID 注释代码。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然而，如果代码的实际情况如此：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那么，正确的解决方案是删除硬编码的密码。

>[!NOTE]
>
>虽然最佳实践是尽可能创建具体的 `@SuppressWarnings` 注释（仅注释导致问题的特定语句或块），但可以添加类级别注释。

>[!NOTE]
>虽然没有明确的安全测试步骤，但在代码质量步骤中会评估与安全相关的代码质量规则。 请参阅 [AEM as a Cloud Service 安全性概述](/help/security/cloud-service-security-overview.md)，了解更多有关 Cloud Service 的安全性。

## 内容包扫描优化 {#content-package-scanning-optimization}

在质量分析过程中，Cloud Manager 会对 Maven 构建生成的内容包进行分析。 Cloud Manager 提供优化功能以加速此过程，当遵守某些打包限制时，这些优化功能将生效。 最重要的是对输出单个内容包（通常称为“所有”包）的项目执行的优化，其中包含构建生成的大量其他内容包（这些内容包标记为已跳过）。 当 Cloud Manager 检测到此情况时，它不会解压缩“所有”包，而是直接扫描各个内容包并根据依赖关系对它们进行排序。 例如，考虑以下构建输出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

如果 `myco-all-1.0.0-SNAPSHOT.zip` 中的唯一项目是两个跳过的内容包，则会扫描两个嵌入包而不是“所有”内容包。

对于产生数十个嵌入包的项目，此优化已被证明可将每次管道执行时间节省 10 分钟以上。

当“所有”内容包包含跳过的内容包和 OSGi 捆绑包的组合时，可能会出现特殊情况。 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 包含前面提到的两个嵌入式包以及一个或多个 OSGi 捆绑包，则仅使用 OSGi 捆绑包构建一个新的最小内容包。 此包始终名为 `cloudmanager-synthetic-jar-package`，并且包含的捆绑包将放置在 `/apps/cloudmanager-synthetic-installer/install` 中。

>[!NOTE]
>
>* 此优化不会影响部署到 AEM 的包。
>* 由于将根据文件名匹配嵌入的内容包和跳过的内容包，因此，如果多个跳过的内容包具有完全相同的文件名或文件名在嵌入时发生变化，则无法进行此优化。
