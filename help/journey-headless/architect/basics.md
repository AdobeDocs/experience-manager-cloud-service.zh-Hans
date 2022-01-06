---
title: Learn Content Modeling Basics
description: Learn the basic of modeling content for your Headless CMS using Content Fragments.
exl-id: dc460490-dfc8-4a46-a468-3d03e593447d
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 4%

---

# Learn the Content Modeling Basics for Headless with AEM {#content-modeling-headless-basics}

## The Story so Far {#story-so-far}

[](overview.md)[](introduction.md)

This article builds on these so you understand how to model your content for your AEM headless project.

## 目标 {#objective}

* ****
* ****

## Content Modeling with Content Fragment Models {#architect-content-fragment-models}

Content (Data) Modeling is a set of established techniques, often used when developed relationship databases, so what does Content Modeling mean for AEM Headless?

### Why? {#why}

To ensure that your application can consistently and efficiently request and receive the required content from AEM, this content must be structured.

This means that your application knows in advance the form of response and therefore, how to process it. This is much easier than receiving free-form content, which has to be parsed to determine what it contains and therefore, how it can be used.

### Introduction to How? {#how}

AEM uses Content Fragments to provide the structures needed for Headless delivery of your content to your applications.

The structure of your content model is:

* realized by the definition of your Content Fragment Model,
* used as a basis of the Content Fragments used for your content generation.

>[!NOTE]
>
>The Content Fragment Models are also used as the basis of the AEM GraphQL Schemas, used for retrieving your content - more about that in the Developer Journey.

Requests for your content are made using the AEM GraphQL API, a customized implementation of the standard GraphQL API. The AEM GraphQL API allows applications to perform (complex) queries on your Content Fragments, with each query being according to a specific model type.

The content returned can then be used by your applications.

## Creating the Structure with Content Fragment Models {#create-structure-content-fragment-models}

Content Fragment Models provide various mechanisms that allow you to define the structure of your content.

A Content Fragment Model describes an entity.

>[!NOTE]
>Content Fragment functionality must be enabled in the Configuration Browser so that you can create new models.

>[!TIP]
>
>The model should be named so that the content author knows which model to select when creating a Content Fragment.

Within a model:

1. ************
1. ********
1. **** This is vital for your content modeling.

例如：

![](assets/headless-modeling-01.png "")

## 数据类型 {#data-types}

AEM provides the following data types for you to model your content:

* 单行文本
* 多行文本
* 数字
* 布尔型
* 日期和时间
* 枚举
* 标记
* 内容引用
* 片段引用
* JSON 对象

>[!NOTE]
>
>Further details are available under Content Fragment Models - Data Types.

## References and Nested Content {#references-nested-content}

Two data types provide references to content outside a specific fragment:

* **** For example, you can reference an image at a specified location.

* ****This type of reference is used to create nested content, introducing the relationships needed to model your content.
The data type can be configured to allow fragment authors to:
   * Edit the referenced fragment directly.
   * Create a new content fragment, based on the appropriate model

>[!NOTE]
>
>You can also create ad hoc references by using links within Text blocks.

## Levels of Structure (Nested Fragments) {#levels-of-structure-nested-fragments}

****

** This allows the headless application to follow the connections and access the content as necessary.

>[!NOTE]
>
>**

Fragment References do just that - they allow you to reference another fragment.

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

Representing these interrelationships can be achieved with Fragment References, as they are understood by you (the architect), your content author and the headless applications.

## What&#39;s Next {#whats-next}

[](model-structure.md)This will introduce and discuss the various references available, and how to create levels of structure with the Fragment References - a key part of modeling for headless.

## 其他资源 {#additional-resources}

* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

   * [Content Fragment Models - Data Types](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [](/help/sites-cloud/authoring/getting-started/basic-handling.md)************

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)
