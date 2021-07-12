---
title: MSM问题故障诊断和常见问题解答
description: 了解如何对最常见的MSM相关问题进行故障诊断，并获取最常见的MSM相关问题的答案。
feature: 多站点管理器
role: Admin
exl-id: 50f02f4f-a347-4619-ac90-b3136a7b1782
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# MSM问题故障诊断和常见问题解答 {#troubleshooting-msm}

## 首要步骤故障诊断 {#first-steps}

如果您遇到MSM中的错误行为或错误，请在开始和详细疑难解答之前，确保：

* 检查[MSM FAQ](#faq)，因为您的问题或问题可能已在此处解决。
* 查看[MSM最佳实践文章](best-practices.md)，因为在文章中提供了一些提示，并澄清了一些误解。

## 查找有关Blueprint和Live Copy状态的高级信息 {#advanced-info}

MSM在资源URL中注册多个可通过选择器请求的Servlet。 这些状态供UI使用，但也可以直接请求它们查看页面的其他高级计算MSM状态：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在Blueprint页面上使用此选项可检索链接到该页面的所有Live Copy的列表，以及其他Live Copy状态信息。
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在Live Copy页面上使用此功能可检索有关其与Blueprint页面连接的高级信息。 如果页面不是Live Copy，则不会返回任何内容。

这些Servlet通过`com.day.cq.wcm.msm`日志记录器生成DEBUG Log消息，这些消息也会很有用。

## 检查存储库中的MSM特定信息 {#checking-repo}

以前的Servlet根据MSM特定的节点和mixin返回计算信息。 该信息通过以下方式存储在存储库中。

* `cq:LiveSync` 混合类型
   * 这在`jcr:content`节点上设置，并定义根Live Copy页面。
   * 这些页面将具有`cq:LiveSyncConfig`类型为`cq:LiveCopy`的子节点，该节点将通过以下属性包含Live Copy的基本和必需信息：
      * `cq:master` 指向Live Copy的Blueprint页面。
      * `cq:rolloutConfigs` 指示应用于Live Copy的活动转出配置。
      * `cq:isDeep` 如果此根Live Copy页面的子页面包含在Live Copy中，则为true。
* `cq:LiveRelationship` 混合类型
   * 任何Live Copy页面的`jcr:content`节点上都具有此类混合类型。
   * 如果不包含，则页面会在某个时间点通过Live Copy操作之外的创作界面（创建或转出）进行分离或手动创建。
* `cq:LiveSyncCancelled` 混合类型
   * 已添加到已暂停的Live Copy页面的`jcr:content`节点。
   * 如果暂停对子页面也有效，则在同一节点上将`cq:isCancelledForChildren`属性设置为true。

这些属性中显示的信息应反映在UI中，但是在进行故障诊断时，当MSM操作发生时，直接在存储库中观察MSM行为可能会很有帮助。

了解这些属性对于查询存储库并查找一组处于特定状态的页面也非常有用。 例如：

* `select * from cq:LiveSync` 返回所有Live Copy根页面。

## 常见问题解答 {#faq}

以下是一些与MSM和Live Copy相关的常见问题。

### 为什么在MSM转出过程中某些属性（例如标题、批注）未更新？ {#missing-properties}

MSM同步操作可进行高度配置。 在转出过程中修改的属性或组件直接取决于这些配置的属性。

有关此主题的更多信息，请参阅[本文](best-practices.md)。

### 如何删除一组作者的转出权限？ {#remove-rollout-permissions}

没有可以为AEM主体（用户或组）设置或删除的&#x200B;**rollout**&#x200B;权限。

作为替代方法，您可以：

* 自定义产品UI以隐藏给定主体的转出操作。
* 从Live Copy树中删除不允许转出的作者的写入权限。

### 为什么我会看到后缀为“_msm_moved”的Live Copy页面？ {#moved-pages}

如果转出了Blueprint页面，它将更新其Live Copy页面，或者在该页面尚不存在时创建新的Live Copy页面（例如，首次转出或手动删除Live Copy页面）。

但是，在后一种情况下，如果存在具有相同名称且不包含`cq:LiveRelationship`属性的页面，则在创建Live Copy页面之前，将相应地重命名此页面。

默认情况下，转出需要链接的Live Copy页面（Blueprint更新将转出到该页面），或者创建Live Copy页面时不需要页面()。

如果找到“独立”页面，MSM会选择重命名此页面，并创建单独的链接Live Copy页面。

Live Copy子树中的此类独立页面通常是&#x200B;**Detach**&#x200B;操作的结果，或者之前的Live Copy页面被作者手动删除，然后使用相同的名称重新创建。

要避免这种情况，请使用Live Copy **Suspend**&#x200B;功能，而不是&#x200B;**Detach**。 有关[本文中&#x200B;**Detach**&#x200B;操作的更多详细信息。](creating-live-copies.md)
