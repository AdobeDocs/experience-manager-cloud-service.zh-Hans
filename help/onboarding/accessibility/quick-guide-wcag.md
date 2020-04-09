---
title: WCAG 2.1快速指南
seo-title: WCAG 2.1快速指南
translation-type: tm+mt
source-git-commit: 11f0509334ebe4456612789fd415a3099687dc64

---


# WCAG 2.1快速指南{#quick-guide-to-wcag}

Adobe Experience Manager(AEM)作为云服务的开发旨在最大限度地遵守Web内容辅助功能准则。

Web内 [容辅助功能准则2.1版(WCAG)](https://www.w3.org/TR/WCAG/) ，是由 [World Wide Web Consortium(W3C)](https://www.w3.org/) (Web Accessibility Initiative(WAI))根据其 [Web辅助功能计划(WAI)制定的一组国际公认准则](https://www.w3.org/WAI/)。

WCAG 2.1 包含一系列非技术层面的准则及成功标准，旨在确保残障人士能够访问并使用 Web 内容。他们向Web内容作者、设计人员和开发人员提供建议，确保他们制作的资源尽可能多地可供尽可能多的人访问，而不管他们有任何残疾；例如，视觉障碍、听力损失、学习困难、年龄限制等。

例如，使用HTML中的属性描述图像（或任何其他非文本内容） `alt` 会使失明或部分视力受损的人受益匪浅。 属性中的文本描 `alt` 述可以转换为语音输出或传输到电子可刷新的盲文显示。

此外，WCAG 2.1还可为其他受益人带来好处，包括可能被认为处于残疾状态 *的人*。 由于浏览技术、网络连接速度或浏览环境等情况，可能会遇到与残疾人类似的障碍的人。

使用Adobe Experience Manager，内容作者和／或网站所有者可以创建满足相关WCAG 2.1 A级和AA级成功标准的Web内容。

因此，了解WCAG 2.1的目标以及指南的结构是理解Web辅助功能以及指南如何有助于创建可访问的Web内容的重要部分。

WCAG 2.1的目的是提供以下准则：

* 与技 **术无关：**&#x200B;换句话说，可以应用于各种Web内容格式的准则，而不仅仅是HTML。 因此，WCAG 2.1可以涵盖由PDF、Flash、JavaScript和其他当前和未来Web技术生成或提供的内容。 <!-- This aims to address a recognized weakness of WCAG 1.0, in that it was focused on HTML at the expense of other web content formats. -->

* 可测 **试：**&#x200B;每个准则的编写方式都是这样的，即可以客观地测试，以确保一组辅助功能专家一般都同意该准则已经得到满足。 辅助功能准则的一个挑战是，虽然一些准则在技术上可以测试，但另一些准则则需要人为判断来确定准则是否成功地得到了满足。 <!-- WCAG 2.1 has been written with the aim of reducing the subjectivity that was present in some of the WCAG 1.0 guidelines and checkpoints. -->

* 支持优 **先化和情境式实施：**
   <!-- As with WCAG 1.0, --> WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. This allows authors to make an informed decision on the most important guidelines for their particular situation. In addition, the concept of *accessibility supported* is introduced. This allows authors to make decisions on how best to use web technologies that may not have full accessibility support, or may require users to have specific assistive technologies and/or browsers in order to benefit from accessibility features.

这些目标对WCAG 2.1的结构有显着的影响。

>[!NOTE]
>
>不可能创建满足各种可能残疾或人类型的网站。 WCAG 2.1旨在帮助Web作者创建在特定条件和合理范围内尽可能可访问的站点。

<!--
>[!NOTE]
>
>If you are familiar with WCAG 1.0, you will notice some changes in WCAG 2.1. These relate to scope, organization and aim.
-->

## 结构 {#structure}

WCAG 2.1的结构形式是以渐进详细的方式引入可访问Web内容创建的概念。 这可能给人以一种印象，即WCAG 2.1是一组非常复杂的相互关联的文档，但其目标是（逐步）在作者需要时提供更详细的信息，而不是在一个非常大的文档中提供所有信息。

WCAG 2.1包含有四个用于辅助设计的关键原则，有时由首字母缩写 **POUR提及**。 这些是：

1. **可感知**:用户能否感知到问题的Web内容？
1. **可操作**:用户能否导航、输入数据或与Web内容进行交互？
1. **可以理解**:用户能否处理和理解呈现给他们的Web内容？
1. **强大**:Web内容是否以预期方式在各种浏览环境(包括旧版和新兴的浏览环境)中可用？

详细说明：
* 每个 **原则** ，都包括一个或多个 **准则**。

* 准则的措辞为说明，说明为正面的(Do this...)或负面的(Do not this...)。
* 准则编号为1.1至4.1，其中第一个编号与父准则相对应。
* 每个准则都包含一个或多个成 **功标准**。
* 成功标准将编写为语句，这些语句是任何给 `True` 定网 `False` 页的语句或语句。
* 成功标准可能包括／或选择，或可能包括例外；不满足成功标准的情况。
* 成功标准按照父准则和原则编号，从1.1.1到4.1.1。它们还有一个简短的名称，用于总结标准的意图，以便于参考。 例如，成功标准1.1.1是非文本替代内容。
* 成功标准包括相关技 **术列表** （详见下文）。

## 支持资源 {#supporting-resources}

除了原则、准则和成功标准的核心WCAG 2.1组件外，还有一系列支持文档。 其中一些人就如何满足指南的某些方面提供具体建议，而另一些人则是更一般的参考资料，帮助所有能力的Web作者、设计人员和开发人员尽可能有效地理解和使用WCAG 2.1。

虽然WCAG 2.1是一个稳定的文档，不会改变，但这些支持资源大多是动态文档;随着新技术的出现，它们会随着时间的推移而改变和增长，并会发现如何实现Web辅助功能的新示例。

### WCAG 2.1资源 {#wcag-resources}

本列表并非详尽无遗，它介绍了可用的资源：
* [WCAG所有相关文档的概要](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [不同文档的摘要](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Web内容辅助功能指南(WCAG)2.1](https://www.w3.org/TR/WCAG21/)
* [WCAG 2.1的新增功能](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [如何满足WCAG 2.1的快速参考指南](https://www.w3.org/WAI/WCAG21/quickref/)
* [WCAG 2常见问题解答](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### WCAG 2.1的新增功能 {#what-is-new}

[WCAG 2.1中的新增功能提供了有关WCAG和2.0以及WCAG 2.1之间的增量的有价值信息](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) 。

[WCAG 2.0和2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) 进一步阐明其关系状况。

### WCAG 2.1的技术 {#techniques-for-wcag}

WCAG 2.1的技术可在WCAG 2.1 [的技术页上找到](https://www.w3.org/WAI/WCAG21/Techniques/) 。

**在** WCAG 2.1层次结构中，技术构成成功标准以下的级别。 它们被WAI列为信息量，而非规范性的。 换句话说，资源符合WCAG 2.1不需要遵循特定技术。

由于技术比成功标准具体得多，它们通常指特定的技术或内容类型（例如HTML或视频）或情况（例如电子商务或电子教学应用程序）。 您可以将技巧视为如何满足特定准则和成功标准的经验证示例，因此这些技巧对于特定上下文的作者和开发人员有帮助。

可以访问以下技术：

* 按集合（技术可能是通用的，或与特定技术或格式相关——例如HTML、CSS或客户端脚本），或
* 根据相关成功标准。 技术可应用于多个成功标准。

每种技术都有一个与其集合相关的唯一编号。 例如，ARIA技术之一是 *Technique ARIA2:使用“required”属性标识必填字段*。

技术可能足够、建议或失败：

* 充分 *技术是* “充分技术”，如果遵循，就足以满足特定成功标准。
* 建议 *技术* （如果遵循该技术）对辅助功能具有积极影响，但可能仅仅仅不足以确保满足特定成功标准)。
* “ *失败* ”是一种技术，用于描述不满足成功标准的具体示例。

技术的详细信息包括说明、适用性、示例、资源，以获取更多信息以及作者如何测试该技术是否成功应用的详细信息。

技术列表不完善，WAI不断用新的示例更新列表，反映了Web技术、设计方法和研究成果的发展。 因此，定期检查新增功能的列表是值得的。

### 了解WCAG 2.1 {#understanding-wcag}

这是指一系列文档，它们为读者理解具体准则和成功标准的目的提供了建议。 您可以下 [载简介，以及指向更详细信息的链接](https://www.w3.org/WAI/WCAG21/Understanding/)。

每个单独的准则和成功标准都有自己的“了解”页面，提供以下信息：

* 准则的意图；
* 具体成功标准；
* 建议技术，有助于满足准则的要求，但不属于任何特定成功标准。

每个成功标准的单个“了解”页面都提供以下信息：

* 成功标准的意图；
* 成功标准如何达到的一般示例；
* 相关（非W3C）资源，介绍如何达到成功标准；
* 技巧与失败：如何达到成功标准的具体和详细示例（详细说明如下）
* 关键术语——对理解成功标准重要的术语表。

例如：了 [解成功标准1.1.1（“非文本内容”）](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content)。

### 如何达到WCAG 2.1 {#how-to-meet-wcag}

有关如何达到WCAG 2.1页面上 [提供了“如何达到”部分](https://www.w3.org/WAI/WCAG21/quickref/) 。 本节提供了WCAG的替代演示，允许根据与读者自身兴趣或情况最相关的准则内容进行优化。 读者可以通过指定特定Web内容技术（如层叠样式表或脚本）或指定特定优先级来筛选他们希望视图的成功标准技术。

如果不进行筛选，此资源将提供按指南分组的所有成功标准。 对于每个成功标准，提供以下内容：

* 成功标准的文本；
* 链接到相应的“理解”文档;
* 列表相关的充分技术，链接到每项技术的细节；
* 列表相关的建议技术，链接到每种技术的详细信息（如果存在）;
* 相关故障的列表，链接到每个故障的详细信息。
