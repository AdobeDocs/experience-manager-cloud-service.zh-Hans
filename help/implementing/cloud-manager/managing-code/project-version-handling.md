---
title: Maven 项目版本处理
description: 对于 AEM as a Cloud Service 的暂存和生产部署，Cloud Manager 会生成一个独特的递增版本。
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---


# Maven 项目版本处理 {#maven-project-version-handling}

对于 AEM as a Cloud Service 的暂存和生产部署，Cloud Manager 会生成一个独特的递增版本

此版本将显示在[管道执行详细信息页面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)以及活动页面上。 在运行构建时，将更新 Maven 项目以使用此版本，并在 Git 存储库中创建一个标记，此版本会充当标记的名称。

如果原始项目版本符合特定条件，则更新后的 Maven 项目版本将合并原始项目版本和 Cloud Manager 生成的版本。不过，标记始终使用生成的版本。 为了使合并发生，原始项目版本必须由三个版本段组成，例如 `1.0.0` 或 `1.2.3`，而不是 `1.0` 或 `1`，并且原始版本不得以 `-SNAPSHOT` 结束。

>[!IMPORTANT]
>
>必须在 Git 存储库分支中的顶层 `pom.xml` 文件的 `<version>` 元素中静态设置此原始项目版本值。

如果原始版本不符合这些条件，则生成的版本会作为新版本段追加到原始版本。 此外，将略微修改生成的版本以包括正确的排序和版本处理。 例如，假设生成的 `2019.926.121356.0000020490` 版本会得到以下结果。

| 版本 | `pom.xml` 中的版本 | 注释 |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 格式正确的原始版本 |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | 快照版本，已覆盖 |
| `1` | `2019.926.121356.0000020490` | 未完成版本，已覆盖 |

>[!NOTE]
>
>无论原始版本是否已并入 Cloud Manager 初始化的版本中，原始版本都可用作名为 `cloudManagerOriginalVersion` 的 Maven 属性。
