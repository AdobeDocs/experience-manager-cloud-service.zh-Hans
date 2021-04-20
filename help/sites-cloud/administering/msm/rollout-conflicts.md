---
title: 转出冲突
description: 了解如何管理和解决多站点管理器转出冲突。
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 3%

---


# 转出冲突{#msm-rollout-conflicts}

如果在Blueprint分支和从属Live Copy分支中创建了具有相同页面名称的新页面，则可能会发生冲突。 此类冲突需要在转出时进行处理和解决。

## 冲突处理{#conflict-handling}

当存在冲突的页面（在Blueprint和Live Copy分支中）时，MSM允许您定义应如何（甚至是如何）处理这些页面。

要确保转出未被阻止，可能的定义可以包括：

* 转出期间，哪个页面（Blueprint或Live Copy）将具有优先级
* 将重命名哪些页面（以及如何）
* 这将如何影响任何已发布内容

AEM现成的默认行为是发布的内容不会受到影响。 因此，如果在Live Copy分支中手动创建的页面已发布，则该内容仍将在冲突处理和转出后发布。

除了标准功能，还可以添加自定义冲突处理程序以实施不同的规则。 这些组件还允许将发布操作作为单个进程执行。

### 方案{#example-scenario}示例

在以下各节中，我们将使用在Blueprint和Live Copy分支（手动创建）中创建的新页面`b`的示例来说明各种冲突解决方法：

* blueprint:`/b`

   主控页面，带有1个子页面，`bp-level-1`

* Live Copy: `/b`

   在Live Copy分支中手动创建的页面，其子页面为`lc-level-1`

   * 发布时已激活`/b`以及子页面

#### 转出前{#before-rollout}

|  | 转出前Blueprint | 转出前的Live Copy | 转出前发布 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 | 在blueprint分支中创建，准备转出 | 在Live Copy分支中手动创建 | 包含在Live Copy分支中手动创建的页面`b`的内容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 在Live Copy分支中手动创建 | 包含在Live Copy分支中手动创建的页面`child-level-1`的内容 |

## 转出管理器和冲突处理{#rollout-manager-and-conflict-handling}

转出管理器允许您激活或取消激活冲突管理。

使用&#x200B;**Day CQ WCM转出管理器**&#x200B;的[OSGi configuration](/help/implementing/deploying/configuring-osgi.md)完成。 如果转出管理器应使用Blueprint中存在的名称处理Live Copy中创建的页面中的冲突，则将值&#x200B;**处理与手动创建的页面冲突**(`rolloutmgr.conflicthandling.enabled`)设置为true。

当冲突管理已停用时，AEM具有[预定义行为。](#behavior-when-conflict-handling-deactivated)

## 冲突处理程序{#conflict-handlers}

AEM使用冲突处理程序解决将内容从Blueprint转出到Live Copy时存在的任何页面冲突。 重命名页面是解决此类冲突的常用（而不仅仅是）方法。 可以操作多个冲突处理程序以允许选择不同的行为。

AEM提供：

* [默认冲突处理函数](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* 实现[自定义处理程序](#customized-handlers)的可能性
* 允许您设置每个处理程序的优先级的服务排名机制
   * 使用排名最高的服务。

### 默认冲突处理程序{#default-conflict-handler}

默认冲突处理程序为`ResourceNameRolloutConflictHandler`

* 使用此处理程序，将优先处理Blueprint页面。
* 此处理函数的服务排名设置得较低，即低于`service.ranking`属性的默认值，因为假定自定义处理函数需要更高的排名。 但是，排名并不是确保必要时灵活性的绝对最低值。

此冲突处理程序优先于Blueprint。 前面的示例是，Live Copy页面`/b`将在Live Copy分支中移动到`/b_msm_moved`。

* Live Copy:`/b`

   在Live Copy中移动到`/b_msm_moved`。 这用作备份，并确保不会丢失任何内容。

   * `lc-level-1` 。

* Blueprint:`/b`

   将转出到Live Copy页面`/b`。

   * `bp-level-1` 将转出到Live Copy。

#### 转出{#after-rollout}后

|  | 转出后Blueprint | 转出后的Live Copy | 转出后的Live Copy | 转出后发布 |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 注释 |  | 是否包含已转出的Blueprint页面`b`的内容 | 具有在Live Copy分支中手动创建的页面`b`的内容 | 无更改，包含在Live Copy分支中手动创建的原始页面`b`的内容，现在称为`b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  |  | 无更改 | 无更改 |

### 自定义处理程序{#customized-handlers}

自定义的冲突处理程序允许您实施您自己的规则。 使用服务排名机制，您还可以定义它们与其他处理函数的交互方式。

自定义冲突处理程序可以：

* 根据您的要求命名。
* 根据您的要求进行开发/配置。
   * 例如，您可以开发一个处理程序，以便Live Copy页面优先。
* 可以设计为使用[OSGi配置](/help/implementing/deploying/configuring-osgi.md)进行配置。 特别是：
   * **服务** 授权定义与其他冲突处理程序()相关 `service.ranking`的顺序。
      * 默认值为 `0`.

### 停用冲突处理时的行为{#behavior-when-conflict-handling-deactivated}

如果手动[取消激活冲突处理，](#rollout-manager-and-conflict-handling) AEM不会对任何冲突页面执行任何操作。 非冲突页面会按预期方式转出。

>[!CAUTION]
>
>停用冲突处理时，AEM不会给出任何冲突被忽略的指示。 因为在这种情况下，必须显式配置此行为，因此假定这是所需的行为。

在这种情况下，Live Copy将有效地优先。 未复制Blueprint页面`/b`,Live Copy页面`/b`保持不变。

* Blueprint:`/b`

   完全没有复制，但被忽略。

* Live Copy:`/b`

   保持不变。

#### 转出{#after-rollout-no-conflict}后

|  | 转出后Blueprint | 转出后的Live Copy | 转出后发布 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 注释 |  | 没有更改，具有在Live Copy分支中手动创建的页面`b`的内容 | 无更改，包含在Live Copy分支中手动创建的页面`b`的内容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 注释 |  | 无更改 | 无更改 |

### 服务排名{#service-rankings}

[OSGi](https://www.osgi.org/)服务等级可用于定义单个冲突处理程序的优先级。
