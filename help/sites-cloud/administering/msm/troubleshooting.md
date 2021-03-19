---
title: MSM问题和常见问题解答疑难解答
description: 了解如何解决最常见的MSM相关问题，并获得最常见的MSM相关问题的答案。
feature: 多站点管理器
role: 管理员
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# MSM问题疑难解答和常见问题解答{#troubleshooting-msm}

## 第一步{#first-steps}疑难解答

如果您在MSM中遇到错误行为或错误，请在开始和详细的疑难解答之前确保：

* 请检查[MSM常见问题解答](#faq)，因为您的问题或问题可能已在此处解决。
* 请查看[MSM最佳实践文章](best-practices.md)，因为该文章提供了许多提示，并澄清了许多误解。

## 查找有关您的Blueprint和Live Copy状态的高级信息{#advanced-info}

MSM注册多个Servlet，这些Servlet可以通过资源URL上的选择器进行请求。 这些状态由UI使用，但也可以直接请求查看页面的其他高级计算MSM状态：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在蓝图页上使用它可检索链接到它的所有Live Copy的列表，并提供其他Live Copy状态信息。
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在Live Copy页面上使用它可检索有关其与Blueprint页面连接的高级信息。 如果页面不是Live Copy，则不返回任何内容。

这些servlet通过`com.day.cq.wcm.msm`记录器生成DEBUG日志消息，这也很有帮助。

## 正在检查存储库{#checking-repo}中的MSM特定信息

先前的Servlet返回基于MSM特定节点和混合的计算信息。 信息以以下列方式存储在存储库中。

* `cq:LiveSync` 混音类型
   * 这在`jcr:content`节点上设置，并定义根Live Copy页面。
   * 这些页面将具有`cq:LiveSyncConfig`类型`cq:LiveCopy`的子节点，该子节点将通过以下属性包含有关Live Copy的基本和必需信息：
      * `cq:master` 指向Live Copy的blueprint页面。
      * `cq:rolloutConfigs` 指示应用于Live Copy的活动转出配置。
      * `cq:isDeep` 如果此Live Copy根页面的子页面包含在Live Copy中，则为true。
* `cq:LiveRelationship` 混音类型
   * 任何Live Copy页面的`jcr:content`节点上都有这样的混合类型。
   * 如果没有，则页面在某个时刻已通过Live Copy操作（创建或转出）外的创作界面分离或手动创建。
* `cq:LiveSyncCancelled` 混音类型
   * 已添加到已挂起的Live Copy页面的`jcr:content`节点。
   * 如果挂起对子页面也有效，则在同一节点上将`cq:isCancelledForChildren`属性设置为true。

这些属性中的信息应反映在UI中，但是，在进行疑难解答时，在发生MSM操作时，直接在存储库中观察MSM行为可能会有所帮助。

了解这些属性对于查询存储库和查找特定状态的页面集也很有用。 例如：

* `select * from cq:LiveSync` 返回所有Live Copy根页面。

## 常见问题解答{#faq}

以下是一些与MSM和Live Copy相关的常见问题。

### 为什么在MSM转出过程中某些属性（例如标题、注释）未更新？{#missing-properties}

MSM同步操作可进行高度配置。 在转出过程中修改哪些属性或组件直接取决于这些配置的属性。

请参阅[本文](best-practices.md)以了解有关此主题的详细信息。

### 如何删除作者组的转出权限？{#remove-rollout-permissions}

没有可以为AEM主体（用户或组）设置或删除的&#x200B;**rollout**&#x200B;权限。

作为替代方法，您可以：

* 自定义产品UI以隐藏给定主体的转出操作。
* 从Live Copy树中为不允许转出的作者删除写入权限。

### 为什么我会看到后缀为“_msm_moved”的Live Copy页面？{#moved-pages}

如果Blueprint页面已转出，则它将更新其Live Copy页面，或在尚不存在时创建新的Live Copy页面（例如，首次转出或手动删除Live Copy页面时）。

但在后一种情况下，如果存在名称相同但没有`cq:LiveRelationship`属性的页面，则在创建Live Copy页面之前，将相应地重命名该页面。

默认情况下，转出需要链接的Live Copy页面（Blueprint的更新将转出到该页面），或创建Live Copy页面时没有页面()。

如果找到“独立”页面，MSM会选择重命名此页面，然后创建单独的链接Live Copy页面。

Live Copy子树中的此类独立页面通常是&#x200B;**分离**&#x200B;操作的结果，或者之前的Live Copy页面被作者手动删除，然后使用相同的名称重新创建。

要避免这种情况，请使用Live Copy **暂停**&#x200B;功能，而不是&#x200B;**分离**。 有关本文[中&#x200B;**Detach**&#x200B;操作的详细信息。](creating-live-copies.md)
