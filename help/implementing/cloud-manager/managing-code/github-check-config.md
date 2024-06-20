---
title: GitHub 检查专用存储库的配置
description: 了解如何控制自动创建的管道，以验证对专用存储库的每个拉取请求。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 77%

---

# GitHub 检查专用存储库的配置 {#github-check-config}

了解如何控制自动创建的管道，以验证对专用存储库的每个拉取请求。

## GitHub 检查的配置 {#configuration}

使用[专用存储库时，](private-repositories.md#using) 一个 [全栈代码质量管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)将自动创建。每次更新提取请求时，此管道将启动。

您可以通过在专用存储库的默认分支中创建一份 `.cloudmanager/pr_pipelines.yml` 文件来控制这些检查。

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| 参数 | 可能的值 | 默认 | 描述 |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` 或 `false` | `false` | 是只保留其github拉取请求中代码扫描结果的最后一个注释，还是保留所有 |
| `type` | `CI_CD` | 不适用 | 定义 CI/CD 管道的行为 |
| `template.programID` | 整数 | 没有重复使用管道变量 | 可用于重用在每个 PR 自动创建的现有管道之一上设置的[管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `template.pipelineID` | 整数 | 没有重复使用管道变量 | 可用于重用在每个 PR 自动创建的现有管道之一上设置的[管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `namePrefix` | 字符串 | `Full Stack Code Quality Pipeline for PR` | 用于设置自动创建的管道的名称 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或者 `FAIL` 或者 `PAUSE` | `CONTINUE` | 设置管道的重要量度行为<br>`CONTINUE` = 如果重要量度失败，管道将自动向前推进<br>`FAIL` = 如果重要量度失败，管道将以失败状态结束<br>`PAUSE` = 当重要量度失败且必须手动恢复时，代码扫描步骤将收到等待状态 |
