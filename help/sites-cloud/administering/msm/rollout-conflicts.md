---
title: 转出冲突
description: 了解如何管理和解决多站点管理器转出冲突。
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: ht
source-wordcount: '923'
ht-degree: 100%

---

# 转出冲突 {#msm-rollout-conflicts}

如果在 Blueprint 分支和从属 Live Copy 分支中都创建了具有相同页面名称的新页面，则可能会发生冲突。转出时需要处理和解决此类冲突。

## 冲突处理 {#conflict-handling}

当 Blueprint 和 Live Copy 分支中的页面存在冲突时，MSM 允许您定义应如何（甚至是否）处理冲突。

为了确保转出不被阻止，可能的定义可以包括：

* 转出期间哪个页面（Blueprint 或 Live Copy）优先
* 哪些页面将进行重命名（以及重命名的方式）
* 这将如何影响任何发布的内容

AEM 现成的默认行为是发布的内容将不会受到影响。因此，如果在 Live Copy 分支中手动创建的页面已发布，则仍将在冲突处理和转出后发布该内容。

除了标准功能外，还可以添加自定义的冲突处理程序来实施其他规则。它们还允许将操作发布为单独的过程。

### 示例场景 {#example-scenario}

在以下部分中，我们使用在 Blueprint 和 Live Copy 分支（手动创建）中创建的新页面 `b` 的示例来说明解决冲突的各种方法：

* Blueprint：`/b`

   带 1 个子页面的母版页，`bp-level-1`

* Live Copy：`/b`

   在 Live Copy 分支中手动创建的带 1 个子页面的页面，`lc-level-1`

   * 在发布为 `/b` 时与子页面一起激活

#### 转出前 {#before-rollout}

|  | 转出前的 Blueprint | 转出前的 Live Copy | 转出前的 Publish |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 | 在 Blueprint 分支中创建，可供转出 | 在 Live Copy 分支中手动创建 | 包含在 Live Copy 分支中手动创建的页面 `b` 的内容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 在 Live Copy 分支中手动创建 | 包含在 Live Copy 分支中手动创建的页面 `child-level-1` 的内容 |

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器允许您激活或停用冲突管理。

可使用 **Day CQ WCM 转出管理器**&#x200B;的 [OSGi 配置](/help/implementing/deploying/configuring-osgi.md)实现此目标。如果转出管理器应处理 Live Copy 中创建的页面的名称与 Blueprint 中已存在的名称发生的冲突，则将值&#x200B;**处理与手动创建的页面相关的冲突** ( `rolloutmgr.conflicthandling.enabled`) 设置为 true。

[当冲突管理被停用时，AEM 具有预定义的行为。](#behavior-when-conflict-handling-deactivated)

## 冲突处理程序 {#conflict-handlers}

AEM 使用冲突处理程序来解决在将内容从 Blueprint 转出到 Live Copy 时存在的任何页面冲突。重命名页面是解决此类冲突的常用（而非唯一）方法。可以运行多个冲突处理程序以允许选择不同的行为。

AEM 提供：

* [默认冲突处理程序](#default-conflict-handler)：
   * `ResourceNameRolloutConflictHandler`
* 实施[自定义处理程序](#customized-handlers)的可能性
* 服务排名机制，可让您设置每个单独处理程序的优先级
   * 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理程序为 `ResourceNameRolloutConflictHandler`

* 对于此处理程序，Blueprint 页面将获得优先权。
* 此处理程序的服务排名设置得很低，即低于 `service.ranking` 属性的默认值，因为假设自定义处理程序需要更高的排名。然而，排名并不是在必要时确保灵活性的绝对最低标准。

此处理程序为 Blueprint 页面提供优先权。例如，Live Copy 页面 `/b` 在 Live Copy 分支中移至 `/b_msm_moved`。

* Live Copy：`/b`

   在 Live Copy 中移至 `/b_msm_moved`。这将充当备份，并确保不丢失任何内容。

   * 不会移动 `lc-level-1`。

* Blueprint：`/b`

   转出到 Live Copy 页面 `/b`。

   * `bp-level-1` 转出到 Live Copy。

#### 转出后 {#after-rollout}

|  | 转出后的 Blueprint | 转出后的 Live Copy | 转出后的 Live Copy | 转出后的 Publish |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 注释 |  | 具有已转出的 Blueprint 页面 `b` 的内容 | 具有在 Live Copy 分支中手动创建的页面 `b` 的内容 | 无更改，包含已在 Live Copy 分支中手动创建的原始页面 `b` 的内容，现称作 `b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  |  | 无更改 | 无更改 |

### 自定义处理程序 {#customized-handlers}

自定义冲突处理程序允许您实施自己的规则。利用服务排名机制，您还可以定义它们如何与其他处理程序交互。

自定义冲突处理程序可以：

* 根据您的要求进行命名。
* 根据您的要求进行开发/配置。
   * 例如，您可以开发一个处理程序，以便为 Live Copy 页面获得优先权。
* 可设计为通过 [OSGi 配置](/help/implementing/deploying/configuring-osgi.md)进行配置。具体而言：
   * **服务排名**&#x200B;定义与其他冲突处理程序相关的顺序 (`service.ranking`)。
      * 默认值为 `0`。

### 冲突处理被停用时的行为 {#behavior-when-conflict-handling-deactivated}

如果您手动[停用冲突处理](#rollout-manager-and-conflict-handling)，AEM 不会对任何冲突页面执行操作。非冲突页面按预期转出。

>[!CAUTION]
>
>当冲突处理被停用时，AEM 不会指示将忽略冲突。由于在这种情况下必须显式配置此行为，因此假定它是所需的行为。

在此情况下，Live Copy 将获得优先权。不会复制 Blueprint 页面 `/b`，并且 Live Copy 页面 `/b` 保持不变。

* Blueprint：`/b`

   根本不复制，而是忽略。

* Live Copy：`/b`

   保持不变。

#### 转出后 {#after-rollout-no-conflict}

|  | 转出后的 Blueprint | 转出后的 Live Copy | 转出后的 Publish |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 |  | 无更改，具有在 Live Copy 分支中手动创建的页面 `b` 的内容 | 无更改，包含在 Live Copy 分支中手动创建的页面 `b` 的内容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 无更改 | 无更改 |

### 服务排名 {#service-rankings}

[OSGi](https://www.osgi.org/) 服务排名可用于定义各个冲突处理程序的优先级。
