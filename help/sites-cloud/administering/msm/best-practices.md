---
title: MSM最佳实践
description: 了解由Adobe工程和咨询团队编译的最佳实践，帮助您快速入门和使用AEM多站点管理器。
translation-type: tm+mt
source-git-commit: 66b2fb19cbc4c8aa480f1ace31a7f973dc7fb0f7
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---


# MSM最佳实践{#msm-best-practices}

## 常规 {#general}

MSM是一个可配置的框架，用于自动进行内容部署。 实施通常涉及网站的主要部分，并且跨组织和地域。 因此，强烈建议在规划网站时如同谨慎地规划MSM实施：

* 在开始实施之前，请仔细&#x200B;**规划结构和内容流**。
* **自定义所需内容，但尽可能少。** 虽然MSM支持高度自定义（例如转出配置），但通常，网站的性能、可靠性和可升级性的最佳实践是最大限度地减少自定义。
* 尽早建立&#x200B;**治理**&#x200B;模型，并相应地培训用户，以确保成功。 从视图的治理角度来说，最佳做法是&#x200B;**最大限度地减少本地内容制作者**&#x200B;向其他本地用户及其各自的Live Copy分配/连接内容的权限。 这是因为，不受管制的链式继承可以显着增加MSM结构的复杂性并损害其性能和可靠性。
* 一旦存在针对您的结构、内容流、自动化和管理的计划，**将原型化并在开始实时实施之前对系统**&#x200B;进行彻底测试。
* 请记住，**Adobe咨询和领先的系统集成商**&#x200B;在MSM中拥有深入的内容规划和实施自动化的经验，因此他们可以帮助您开始使用MSM项目并贯穿整个实施过程。

## Live Copy源和Blueprint配置{#live-copy-sources-and-blueprint-configurations}

请记住，Live Copy可以使用[常规页面](creating-live-copies.md#creating-a-live-copy-of-a-page)或[蓝图配置](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)创建。 这两个都是有效的用例。

使用Blueprint配置的其他好处是：

* 允许作者在Blueprint上使用&#x200B;**Rollout**&#x200B;选项，以便将修改显式推送到继承自此Blueprint的Live Copy。
* 允许作者使用&#x200B;**创建站点**&#x200B;以便轻松选择语言并配置Live Copy的结构。
* 为与Blueprint有关的Live Copy定义默认转出配置。

如果未引用Blueprint配置，则只能从Live Copy本身启动推出，实质上是从源中提取内容。

使用Live Copy创建新站点时，创建Blueprint配置是非常有利的，可以确保完整MSM功能集的可用性。

## 组件和容器同步{#components-and-container-synchronization}

通常，MSM中关于组件同步的转出规则为：

* 将执行组件同步，同步蓝图中包含的任何资源。
* 容器仅同步当前资源。

这意味着组件被视为聚合，在推广中，组件本身及其所有子项将替换为Blueprint中的组件。 这意味着，如果资源在本地添加到此类组件，则在转出时将丢失到Blueprint的内容。

要支持组件嵌套，以便在本地添加的组件在转出中进行维护，必须将组件声明为容器。

>[!NOTE]
>
>将属性`cq:isContainer`添加到组件以将其指定为容器。

## 创建站点 {#create-site}

请注意，AEM有两种主要的创建Live Copy的方法：

* 当[创建Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page)时 — 这可以视为更通用的方法，允许您从任何页面创建Live Copy。 Live Copy的内容结构与源完全匹配。

* 当[创建站点](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)时 — 这是一种更专业的方法，主要用于创建具有多语言结构的网站。

以下是创建站点时要注意的几个注意事项：

* 要创建新站点，您需要[blueprint配置](creating-live-copies.md#managing-blueprint-configurations)。
* 要允许选择要在新站点中创建的语言路径，Blueprint（源）中必须存在相应的语言根。
* 将[新站点创建为Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)（使用&#x200B;**创建**，然后使用&#x200B;**站点**）后，此Live Copy的前两个级别为&#x200B;*浅*。 页面的子项不属于实时关系，但如果找到与触发器匹配的实时关系，则滚动仍将下降。

有助于避免：

* 在Blueprint中手动添加语言（在第一级以下）。
* 手动将内容直接添加到语言根目录下，因为这不会导致在转出时自动将新内容转移到Live Copy。

## MSM和多语言网站{#msm-and-multilingual-websites}

MSM可通过两种方式协助创建多语言网站：

创建语言主页时，请牢记以下几点：

* 虽然MSM本身&#x200B;**不提供内容转换**，但它可以与提供内容转换的第三方转换连接器集成。 请注意：
   * MSM允许您在页面和/或组件级别取消继承。 这有助于防止在下一次转出时覆盖已翻译的内容（来自Live Copy，包含来自Blueprint的尚未翻译的内容）。
      * 某些第三方翻译连接器可自动管理MSM继承。
      * 请咨询您的翻译服务提供商以了解更多信息。
      * 创建和翻译语言母版的另一种方法是将语言副本与AEM现成的翻译集成框架结合使用。

有关详细信息，请参阅[多语言站点的翻译内容](/help/sites-cloud/administering/translation/overview.md)和[翻译最佳实践。](/help/sites-cloud/administering/translation/best-practices.md)

## 结构更改和转出{#structure-changes-and-rollouts}

Live Copy中对Blueprint/源树中内容结构的修改会以不同方式反映。 这取决于修改类型：

* **在** Blueprint中创建新页面将导致在转出后使用标准转出配置在Live Copy中创建相应页面。
* **在** 转出后，删除Blueprint中的页面将导致从Live Copy中删除相应页面（转出后带有标准转出配置）。
* **在** Blueprint中移动页面不 **** 会导致相应页面在转出后在Live Copy中移动，转出时带有标准转出配置：
   * 此行为的原因是页面移动隐式地包含页面删除。 这可能会在发布时导致意外行为，因为在作者上删除页面会自动在发布时停用相应的内容。 这也会对相关项目（如链接、书签和其他）产生额外影响。
      * 相应Live Copy页面中的内容继承将更新，以反映其源在Blueprint中的新位置。
      * 要完全实现页面从Blueprint移动到Live Copy，请考虑[页面移动最佳实践。](#page-move)

### 页面移动最佳实践{#page-move}

在考虑在Live Copy中移动页面时，请考虑以下最佳实践。

>[!NOTE]
>
>以下内容仅适用于[On Rollout触发器](live-copy-sync-config.md#rollout-triggers)。

1. 创建自定义转出配置。
   * 此新配置必须包含操作`PageMoveAction`。
   * 请勿向此配置添加其他操作。
1. 定位新配置。
   * 要在删除Live Copy中旧位置的各个页面时完全展开页面移动，请执行以下操作：
      * 在标准转出配置之前定位新创建的配置。 标准转出配置将负责删除其旧位置中的页面。
      * 要在将各个页面保留在Live Copy中旧位置（实质上是复制内容）的同时，滚出页面移动：
         * 在标准转出配置之后定位新创建的配置。 这将确保未在Live Copy中删除或从发布中取消激活任何内容。

## 自定义推广{#customizing-rollouts}

MSM转出配置可高度自定义。 您应该知道，自动推广可能会产生深远影响。 作为最佳实践，在进行以下活动之前，您应非常谨慎地进行计划：

* 自动推出，如使用[onModify触发器](#onmodify)
* 自定义[节点类型/属性](#node-types-properties)
* 开始后续工作流
* 作为推广的一部分激活内容

### onModify {#onmodify}

使用[转出触发器](live-copy-sync-config.md#rollout-triggers) `onModify`时，您应考虑：

* 使用`onModify`触发器实现自动转出可能会对创作性能产生负面影响，因为它们在每次页面修改后都会触发转出。
* 转出结果可能与预期结果不同：
   * 您不能指定生成的修改事件的顺序。
   * 基于事件的体系结构无法保证传递到转出管理器的事件的序列。
* 如果发生同一资源的并发更新，使用此类转出配置可能会导致提交冲突。

因此，建议仅在自动转出启动的好处超过任何潜在性能问题时使用`onModify`触发器。

### 节点类型/属性{#node-types-properties}

除了自定义转出操作之外，MSM还允许您自定义正在转出的节点属性。 [MSM OSGi配置允许您排除从源复制到Live Copy的节点类型](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)。

## 更多信息 {#further-information}

有关MSM和Live Copy的更多详细信息，请参阅以下文章。

* [创建和同步Live Copy](creating-live-copies.md)
* [Live Copy概述控制台](live-copy-overview.md)
* [配置 Live Copy 同步](live-copy-sync-config.md)
* [MSM转出冲突](rollout-conflicts.md)
