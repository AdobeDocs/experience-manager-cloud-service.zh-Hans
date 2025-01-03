---
title: GitHub 检查专用存储库的配置
description: 了解如何控制自动创建的管道以验证对专用存储库的每个拉取请求。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0a08d5fc033f4f4f57b824492766e5b42a801b6e
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 33%

---

# GitHub 检查专用存储库的配置 {#github-check-config}

了解如何控制自动创建的管道以验证对专用存储库的每个提取请求。

## GitHub 检查的配置 {#configuration}

使用[专用存储库](private-repositories.md#using)时，系统会自动创建一个[全栈代码质量管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。每次更新提取请求时，此管道便会启动。

可以通过在专用存储库的默认分支中创建`.cloudmanager/pr_pipelines.yml`配置文件来控制这些检查。

```yaml
github:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| 参数 | 可能的值 | 默认 | 描述 |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` 或 `false` | `false` | 是只保留此GitHub拉取请求上代码扫描结果的最后一个注释，还是保留所有注释。 将其设置为`false`（默认）意味着不会删除以前的评论。 |
| `shouldSkipCheckAnnotations` | `true` 或 `false` | `false` | GitHub拉取请求检查中是否存在其他注释。 将其设置为`false`（默认）意味着不跳过检查批注，并将其包含在反馈中。 |
| `type` | `CI_CD` | 不适用 | 定义CI/CD（连续集成/连续部署）管道配置的行为。 |
| `template.programId` | 整数 | 没有重复使用管道变量 | 您可以使用它来重复使用在每个拉取请求自动创建的现有管道上设置的[管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `template.pipelineId` | 整数 | 没有重复使用管道变量 | 您可以使用它来重复使用在每个拉取请求自动创建的现有管道上设置的[管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `namePrefix` | 字符串 | `Full Stack Code Quality Pipeline for PR` | 用于为自动创建的管道的名称设置前缀。 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或者 `FAIL` 或者 `PAUSE` | `CONTINUE` | 设置管道的重要量度行为<br>`CONTINUE` =如果重要量度失败，则管道自动前进<br>`FAIL` =如果重要量度失败，则管道将以失败状态结束<br>`PAUSE` =当重要量度失败且必须手动恢复时，代码扫描步骤将收到“等待”状态 |




