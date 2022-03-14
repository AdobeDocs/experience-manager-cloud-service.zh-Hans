---
title: MSM 最佳实践
description: 了解由Adobe工程和咨询团队编译的最佳实践，以帮助启动和运行AEM多站点管理器。
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 1%

---

# MSM 最佳实践 {#msm-best-practices}

## 常规 {#general}

MSM是用于自动进行内容部署的可配置框架。 实施通常涉及网站的主要部分，并跨组织和地理区域。 因此，强烈建议在规划网站时谨慎规划MSM实施：

* 小心 **规划结构和内容流** 开始实施之前。
* **根据需要尽可能多地进行自定义，但尽可能少地进行自定义。** 虽然MSM支持高度自定义（例如转出配置），但是对于网站的性能、可靠性和可升级性，通常的最佳实践是最大限度地减少自定义。
* 建立 **治理** 及早建模，并相应培训用户，以确保成功。 从治理角度来看，最佳做法是 **最大限度地减少本地内容制作者的权限** 将内容分配/连接到其他本地用户及其各自的Live Copy。 这是因为不受管理、链式继承可以显着增加MSM结构的复杂性并降低其性能和可靠性。
* 一旦您的结构、内容流、自动化和管理存在计划， **原型和全面测试系统** 开始实时实施之前，请执行以下操作：
* 请记住 **Adobe咨询和领先的系统集成商** 拥有使用MSM进行内容自动化的深入规划和实施体验，因此他们可以帮助您开始使用MSM项目，并在其整个实施过程中帮助您。

## Live Copy源和Blueprint配置 {#live-copy-sources-and-blueprint-configurations}

请记住，可以使用 [常规页面](creating-live-copies.md#creating-a-live-copy-of-a-page) 或 [Blueprint配置](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 这两种方法都是有效的用例。

使用Blueprint配置的其他好处是：

* 允许作者使用 **转出** 选项，以明确将修改推送到从此Blueprint继承的Live Copy。
* 允许作者使用 **创建网站** 以便轻松选择语言并配置Live Copy的结构。
* 为与Blueprint有关的Live Copy定义默认转出配置。

如果未引用Blueprint配置，则只能从Live Copy本身启动转出，实质上是从源中提取内容。

使用Live Copy创建新站点时，最好创建Blueprint配置，以确保完整MSM功能集的可用性。

>[!NOTE]
>
> 请注意，“权限”选项卡中的CUG无法从Blueprint中转出到Live Copy。 请在配置Live Copy时针对此进行规划。

## 组件和容器同步 {#components-and-container-synchronization}

通常，MSM中有关组件同步的转出规则为：

* 组件可以同步Blueprint中包含的所有资源。
* 容器仅同步当前资源。

这意味着组件被视为聚合，在推出过程中，组件本身及其所有子代将被蓝图中的组件替换。 这意味着如果资源在本地添加到此类组件，则在转出时将会丢失到Blueprint的内容。

要支持嵌套组件以便在转出中维护本地添加的组件，必须将组件声明为容器。

>[!NOTE]
>
>添加属性 `cq:isContainer` 将其指定为容器的组件。

## 创建站点 {#create-site}

请注意， AEM有两种主要方法可用于创建Live Copy:

* When [创建Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page)  — 这可以视为更宽泛的方法，允许您从任何页面创建Live Copy。 Live Copy的内容结构与源完全匹配。

* When [创建网站](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)  — 这是一种更为专业化的方法，主要用于创建具有多语言结构的网站。

在创建网站时，请注意以下事项：

* 要创建新站点，您需要 [Blueprint配置](creating-live-copies.md#managing-blueprint-configurations).
* 要允许选择要在新站点中创建的语言路径，相应的语言根必须存在于Blueprint（源）中。
* 一次 [新站点已创建为Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **创建**，则 **网站**)，此Live Copy的前两个级别是 *浅浅*. 页面的子项不属于实时关系，但如果找到与触发器匹配的实时关系，则转出仍将下降。

有助于避免：

* 在Blueprint中手动添加语言（在第一级以下）。
* 手动在语言根目录的正下方添加内容，因为这不会导致在转出时自动将新内容传递到Live Copy。

## MSM和多语言网站 {#msm-and-multilingual-websites}

MSM可通过两种方式协助创建多语言网站：

在创建语言母版时，请牢记以下几点：

* 而MSM本身 **不提供内容翻译**，则可以将其与需要的第三方翻译连接器集成。 请注意：
   * MSM允许您在页面和/或组件级别取消继承。 这有助于防止在下一个转出中覆盖已翻译的内容（来自Live Copy，包含来自Blueprint的尚未翻译的内容）。
      * 某些第三方翻译连接器会自动管理MSM继承。
      * 有关更多信息，请咨询您的翻译服务提供商。
      * 创建和翻译语言母版的另一种方法是结合AEM现成翻译集成框架使用语言副本。

有关详细信息，请参阅 [翻译多语言站点的内容](/help/sites-cloud/administering/translation/overview.md) 和 [翻译最佳实践。](/help/sites-cloud/administering/translation/best-practices.md)

## 结构更改和转出 {#structure-changes-and-rollouts}

对Blueprint/源树中内容结构的修改在Live Copy中的反映方式不同。 这取决于修改类型：

* **创建** 使用标准转出配置转出后，blueprint中的新页面将导致在Live Copy中创建相应的页面。
* **删除** 使用标准转出配置转出后，blueprint中的页面将导致从Live Copy中删除相应的页面。
* **移动** Blueprint中的页面将 **not** 导致在使用标准转出配置转出后，相应页面在Live Copy中移动：
   * 此行为的原因是页面移动会隐式包含页面删除。 这可能会在发布时导致意外行为，因为删除作者的页面会在发布时自动停用相应的内容。 这也会对相关项目（如链接、书签和其他项目）产生额外影响。
      * 相应Live Copy页面中的内容继承会进行更新，以反映其源在Blueprint中的新位置。
      * 要完全实现页面从Blueprint移动到Live Copy，请考虑 [页面移动最佳实践。](#page-move)

### 页面移动最佳实践 {#page-move}

考虑在Live Copy中移动页面时，请考虑以下最佳实践。

>[!NOTE]
>
>以下内容仅适用于 [转出触发器时](live-copy-sync-config.md#rollout-triggers).

1. 创建自定义转出配置。
   * 此新配置必须包含操作 `PageMoveAction`.
   * 请勿向此配置添加其他操作。
1. 定位新配置。
   * 要在Live Copy中的旧位置删除相应页面时完全转出页面移动，请执行以下操作：
      * 将新创建的配置放在标准转出配置之前。 标准转出配置将负责删除其旧位置中的页面。
      * 要在Live Copy中将相应页面保留在其旧位置（实质上是复制内容）的同时转出页面移动，请执行以下操作：
         * 在标准转出配置后放置新创建的配置。 这将确保Live Copy中未删除或从发布中停用任何内容。

## 自定义转出 {#customizing-rollouts}

MSM转出配置是高度可自定义的。 您应该知道，自动推广可能会产生深远的后果。 作为最佳实践，您应在参与以下活动之前非常仔细地进行规划：

* 自动执行转出，例如使用 [onModify触发器](#onmodify)
* 自定义 [节点类型/属性](#node-types-properties)
* 启动后续工作流
* 在转出中激活内容

### onModify {#onmodify}

使用 [转出触发器](live-copy-sync-config.md#rollout-triggers) `onModify` 您应考虑：

* 通过 `onModify` 触发器在每次页面修改后都会触发转出，因此可能会对创作性能产生负面影响。
* 转出结果可能与预期结果不同，如下所示：
   * 您无法指定结果修改事件的顺序。
   * 基于事件的架构无法保证传递到转出管理器的事件的顺序。
* 如果同一资源发生并发更新，使用此类转出配置可能会导致提交冲突。

因此，建议您仅使用 `onModify` 自动推出启动的好处超过任何潜在的性能问题时触发。

### 节点类型/属性 {#node-types-properties}

除了自定义转出操作之外，MSM还允许您自定义正在转出的节点属性。 的 [MSM OSGi配置允许您排除节点类型](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) 从源复制到Live Copy。

## 更多信息 {#further-information}

有关MSM和Live Copy的更多详细信息，请参阅以下文章。

* [创建并同步 Live Copy](creating-live-copies.md)
* [Live Copy 概述控制台](live-copy-overview.md)
* [配置 Live Copy 同步](live-copy-sync-config.md)
* [MSM转出冲突](rollout-conflicts.md)
