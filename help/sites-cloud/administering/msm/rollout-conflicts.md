---
title: 转出冲突
description: 了解如何管理和解决多站点管理器转出冲突。
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---

# 转出冲突 {#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中创建具有相同页面名称的新页面，则可能会发生冲突。 此类冲突需要在转出时进行处理和解决。

## 冲突处理 {#conflict-handling}

当存在冲突的页面（在Blueprint和Live Copy分支中）时，MSM允许您定义应如何处理（甚至是如果）这些页面。

为确保转出不被阻止，可能的定义可以包括：

* 在转出过程中，哪个页面（Blueprint或Live Copy）将具有优先级
* 将重命名哪些页面（以及如何重命名）
* 这将如何影响任何已发布的内容

AEM的现成默认行为是发布的内容不会受到影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容在处理和转出冲突后仍会发布。

除了标准功能外，还可以添加自定义冲突处理程序以实施不同的规则。 这些操作还允许将操作作为单个流程发布。

### 示例方案 {#example-scenario}

在以下部分中，我们使用了新页面的示例 `b`，以说明各种冲突解决方法：

* blueprint: `/b`

   一个主控的页面，其中包含1个子页面， `bp-level-1`

* Live Copy: `/b`

   在Live Copy分支中手动创建的页面，其中包含1个子页面 `lc-level-1`

   * 发布时激活为 `/b`，以及子页面

#### 转出前 {#before-rollout}

|  | 转出前的Blueprint | 转出前Live Copy | 转出前发布 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 | 在Blueprint分支中创建，准备转出 | 在Live Copy分支中手动创建 | 包含页面内容 `b` 在Live Copy分支中手动创建的 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 在Live Copy分支中手动创建 | 包含页面内容 `child-level-1` 在Live Copy分支中手动创建的 |

## 转出管理器和冲突处理 {#rollout-manager-and-conflict-handling}

转出管理器允许您激活或停用冲突管理。

这是使用完成的 [OSGi配置](/help/implementing/deploying/configuring-osgi.md) of **Day CQ WCM转出管理器**. 设置值 **处理与手动创建的页面的冲突** ( `rolloutmgr.conflicthandling.enabled`)，以使用Blueprint中存在的名称处理在Live Copy中创建的页面中的冲突。

AEM [已停用冲突管理时的预定义行为。](#behavior-when-conflict-handling-deactivated)

## 冲突处理程序 {#conflict-handlers}

AEM使用冲突处理程序来解决在将内容从Blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的常用（不仅如此）方法。 可以操作多个冲突处理程序以允许选择不同的行为。

AEM提供：

* 的 [默认冲突处理程序](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* 实施 [自定义处理程序](#customized-handlers)
* 用于设置每个处理程序优先级的服务排名机制
   * 使用排名最高的服务。

### 默认冲突处理程序 {#default-conflict-handler}

默认冲突处理程序为 `ResourceNameRolloutConflictHandler`

* 使用此处理程序时，Blueprint页面优先。
* 此处理程序的服务排名设置得较低，即低于 `service.ranking` 属性，因为假定自定义处理程序将需要更高的排名。 但是，排名并不是确保在需要时具有灵活性的绝对最小值。

此冲突处理程序优先于Blueprint。 以前的Live Copy页面为例 `/b` 在Live Copy分支中移动到 `/b_msm_moved`.

* Live Copy: `/b`

   在Live Copy中移到 `/b_msm_moved`. 此操作用作备份，并确保不会丢失任何内容。

   * `lc-level-1` 未移动。

* Blueprint: `/b`

   已转出到Live Copy页面 `/b`.

   * `bp-level-1` 将转出到Live Copy。

#### 转出后 {#after-rollout}

|  | 转出后的Blueprint | 转出后Live Copy | 转出后Live Copy | 转出后发布 |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 注释 |  | 具有Blueprint页面的内容 `b` 那个被推出来 | 具有页面内容 `b` 在Live Copy分支中手动创建的 | 无更改，包含原始页面的内容 `b` 在Live Copy分支中手动创建的，现在称为 `b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  |  | 无更改 | 无更改 |

### 自定义处理程序 {#customized-handlers}

自定义冲突处理程序允许您实施自己的规则。 使用服务排名机制，您还可以定义它们与其他处理程序的交互方式。

自定义冲突处理程序可以：

* 根据您的要求命名。
* 根据您的要求进行开发/配置。
   * 例如，您可以开发一个处理程序，以便优先使用Live Copy页面。
* 可以设计为使用 [OSGi配置](/help/implementing/deploying/configuring-osgi.md). 特别是：
   * **服务排名** 定义与其他冲突处理程序相关的顺序( `service.ranking`)。
      * 默认值为 `0`。

### 停用冲突处理时的行为 {#behavior-when-conflict-handling-deactivated}

如果您手动 [停用冲突处理，](#rollout-manager-and-conflict-handling) AEM不对任何冲突的页面执行任何操作。 非冲突页面会按预期推出。

>[!CAUTION]
>
>停用冲突处理后，AEM不会显示冲突被忽略的任何指示。 由于在这种情况下，必须明确配置此行为，因此假定这是所需的行为。

在这种情况下，有效的Live Copy具有优先权。 Blueprint页面 `/b` 不会复制，而是会复制Live Copy页面 `/b` 保持不变。

* Blueprint: `/b`

   根本不会复制，但会被忽略。

* Live Copy: `/b`

   保持不变。

#### 转出后 {#after-rollout-no-conflict}

|  | 转出后的Blueprint | 转出后Live Copy | 转出后发布 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 |  | 无更改，具有页面内容 `b` 在Live Copy分支中手动创建的 | 无更改，包含页面内容 `b` 在Live Copy分支中手动创建的 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 无更改 | 无更改 |

### 服务排名 {#service-rankings}

的 [OSGi](https://www.osgi.org/) 服务排名可用于定义单个冲突处理程序的优先级。
