---
title: Learn about using references in Content Fragments
description: Learn about using references in Content Fragments, for content, other fragments and other assets (media). Introduce the necessity for, and the mechanics of, nested fragments for Headless CMS Authoring.
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# Learn about using references in Content Fragments {#author-headless-references}

## The Story so Far {#story-so-far}

[](overview.md)[](introduction.md)

You have learned the basics of Headless CMS Authoring, with an introduction to authoring with AEMaaCS and in particular, authoring Content Fragments.

This article builds on these so you understand how to use references to author your own content for your AEM headless project.

## 目标 {#objective}

* ****
* **** What sorts of references are available, and what are their purposes:

   * 内容引用
   * Asset/Media References
   * Fragment References
   * Ad hoc references from within a text block

## What are references {#what-are-references}

References are simply a mechanism for connecting your resources, be it other content, assets (as in images), or other fragments. Although very similar, there are some differences.

Some references have dedicated data-types (for example, Content References and Fragment References), whereas others are simply added as a reference within a text block (asset references and ad hoc references).

![](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 内容引用 {#content-references}

Content References do just that - they allow you to reference any other content. This will open a browser that allows you to select the content item.

## Asset/Media References {#assets-media-references}

**** This will open a browser that allows you to select the asset.

![](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Fragment References {#fragment-references}

Again Fragment References do just that - they allow you to reference another fragment. Why this is significant needs a bit more explanation.

For example, you might have the following Content Fragment Models defined:

* 城市
* 公司
* 人员
* Awards

Seems pretty straightforward, but of course a Company has both a CEO and Employees....and these are all people, each defined as a Person.

And a Person can have an Award (or maybe two).

* My Company - Company
   * CEO - Person
   * Employee(s) - Person
      * Personal Award(s) - Award

And that&#39;s just for starters. Depending on the complexity, an Award could be Company-specific, or a Company could have its main office in a specific City.

Representing these interrelationships can be achieved with Fragment References, as they are understood by both you (the author) and the headless applications.

As an author you&#39;re not responsible for defining these relationships (that&#39;s done by the Content Architect when creating the Content Fragment Model), but you need to know how to recognize and edit the references.

<!--
![Content Modeling with Content Fragments](/help/journey-headless/developer/assets/headless-modeling-01.png "Content Modeling with Content Fragments")
-->

### How to author nested fragments {#author-nested-fragment}

**** You can either type in the reference directly, or (more likely) select the folder icon to open a browser that allows you to navigate and select the fragment you need.

![](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

The definition of the Content Fragment Model controls:

* whether you can select to add multiple references
* the model types of Content Fragments that you can select; the Content Fragment Model defines the fragment models allowed for the reference, so AEM only presents fragments based on those models.

### How to navigate nested fragments {#navigate-nested-fragment}

**** Selecting a reference opens that fragment for editing.

>[!NOTE]
>
>Using the breadcrumbs in the main panel you can navigate back to your starting point.

![](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Ad Hoc References {#adhoc-references}

Ad hoc references can be added as a simple link within a block of text:

![](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## What&#39;s Next {#whats-next}

[](metadata-tagging.md)This will introduce and discuss how you can define metadata and tags for your Content Fragments.

## 其他资源 {#additional-resources}

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [Apply the Configuration to your Assets Folder](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creating a Content Fragment](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variations - Authoring Content Fragments](/help/assets/content-fragments/content-fragments-variations.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [Content Fragment Models - Data Types](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Content Fragment Models - Properties](/help/assets/content-fragments/content-fragments-models.md#properties)


* Getting Started Guides
   * [Creating an Assets Folder Headless Quick Start Guide](/help/implementing/developing/headless/getting-started/create-assets-folder.md)

* AEM Headless Content Architect Journey

* AEM Headless Translation Journey
