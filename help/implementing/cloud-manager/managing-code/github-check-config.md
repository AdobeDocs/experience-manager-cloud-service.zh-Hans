---
title: 针对专用存储库的GitHub检查配置
description: 了解如何控制自动创建的管道，以验证对专用存储库的每个拉取请求。
source-git-commit: 73bd693d47f37b453209208816dfed15d65e9e09
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# 针对专用存储库的GitHub检查配置 {#github-check-config}

了解如何控制自动创建的管道，以验证对专用存储库的每个拉取请求。

## GitHub检查配置 {#configuration}

使用时 [专用存储库，](private-repositories.md#using) a [全栈代码质量管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 将自动创建。 每次更新提取请求时，此管道将启动。

您可以通过创建 `.cloudmanager/pr_pipelines.yml` 文件，该文件位于专用存储库的默认分支中。

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

| 参数 | 可能值 | 默认 | 描述 |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` 或 `false` | `false` | 是只保留其github拉取请求中代码扫描结果的最后一个注释，还是保留所有 |
| `type` | `CI_CD` | 不适用 | 定义CI/CD管道的行为 |
| `template.programID` | 整数 | 没有可重复使用的管道变量 | 可用于重用 [管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 在由每个PR自动创建的某个现有管道上设置的重复实例。 |
| `template.pipelineID` | 整数 | 没有可重复使用的管道变量 | 可用于重用 [管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 在由每个PR自动创建的某个现有管道上设置的重复实例。 |
| `namePrefix` | 字符串 | `Full Stack Code Quality Pipeline for PR` | 用于设置自动创建的管道的名称 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或 `FAIL` 或 `PAUSE` | `CONTINUE` | 设置管道的重要量度行为<br>`CONTINUE` =如果重要量度失败，管道将自动前进<br>`FAIL` =如果重要量度失败，管道将以失败状态结束<br>`PAUSE` =当重要量度失败且必须手动恢复时，代码扫描步骤将收到等待状态 |
