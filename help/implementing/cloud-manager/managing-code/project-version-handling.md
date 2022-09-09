---
title: Maven 项目版本处理
description: 对于AEM as a Cloud Service的暂存和生产部署，Cloud Manager会生成一个唯一的递增版本。
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Maven 项目版本处理 {#maven-project-version-handling}

对于AEM as a Cloud Service的暂存和生产部署，Cloud Manager会生成一个唯一的递增版本

此版本可在 [管道执行详细信息页面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 以及活动页面。 运行内部版本后，将更新Maven项目以使用此版本，并在git存储库中创建一个标记，并将该版本作为其名称。

如果原始项目版本符合某些标准，则更新的Maven项目版本将合并原始项目版本和Cloud Manager生成的版本。 但是，标记始终使用生成的版本。 要进行此合并，原始项目版本必须仅由三个版本区段组成，例如， `1.0.0` 或 `1.2.3`，但不是 `1.0` 或 `1`，且原始版本不得以 `-SNAPSHOT`.

>[!IMPORTANT]
>
>必须在 `<version>` 顶级元素 `pom.xml` 文件。

如果原始版本确实符合这些条件，则生成的版本将作为新版本区段附加到原始版本中。 生成的版本也将稍作修改，以包含正确的排序和版本处理。 例如，假定生成的 `2019.926.121356.0000020490` 会得到以下结果。

| 版本 | 版本 `pom.xml` | 注释 |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | 格式正确的原始版本 |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | 快照版本，覆盖 |
| `1` | `2019.926.121356.0000020490` | 版本不完整，被覆盖 |

>[!NOTE]
>
>无论原始版本是否纳入到Cloud Manager初始化的版本中，原始版本都可用作名为的Maven属性 `cloudManagerOriginalVersion`.
