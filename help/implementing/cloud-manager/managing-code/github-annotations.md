---
title: GitHub检查注释
description: 了解GitHub如何检查专用存储库的PR注释功能，以向您提供有用的反馈。
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: f7348d388918a31d255babcfb64b3dc547153d62
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# GitHub检查注释 {#github-annotations}

了解GitHub如何检查专用存储库的PR注释功能，以向您提供有用的反馈。

## 概述 {#overview}

如果您使用 [专用存储库](private-repositories.md) 对于您的Cloud Manager程序，将自动为每个拉取请求运行签入GitHub 。 这些代码带有有用信息，有助于您尽快了解代码的任何问题。

![GitHub检查注释示例](assets/github-check-annotations.png)

[代码质量](/help/implementing/cloud-manager/code-quality-testing.md) 检测到的问题 [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) 都清楚列在清单上。

![代码问题注释示例](assets/github-check-annotations-example.png)

提供了与此问题相关的确切代码行，您可以单击它以显示相关代码。 这些注释适用于所有代码问题，而不仅仅是拉取请求中更改的代码问题。

![代码问题注释示例](assets/github-check-annotations-example-code.png)

所有带注释的行将聚合在 **文件已更改** 选项卡上的GitHub拉取请求。 对于在拉取请求中未更改的文件，注释将显示在其自己的部分中。

![“文件已更改”选项卡上的注释示例](assets/github-check-annotations-files-changed.png)

## 代码质量管道 {#code-quality-pipelines}

此 [代码质量](/help/implementing/cloud-manager/code-quality-testing.md) 结果还可在管道中看到，该管道由底部的Cloud Manager自动触发。 **支票** 选项卡。 也可从 **详细信息** ，以检查拉取请求。

![注释示例](assets/github-check-annotations-code-quality.png)

![注释示例](assets/github-check-annotations-code-quality-2.png)

您还可以以CSV格式可视化问题。 可以检索此内容的人员为 [在Cloud Manager中查看管道执行的详细信息。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)
