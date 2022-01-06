---
title: Learn about Creating Content Fragment Models in AEM
description: Learn about the concepts and mechanics of modeling content for your Headless CMS using Content Fragments Models.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
source-git-commit: 3f6c96da3fd563b4c8db91ab1bc08ea17914a8c1
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 2%

---

# Learn about Creating Content Fragment Models in AEM {#architect-headless-content-fragment-models}

## The Story so Far {#story-so-far}

[](overview.md)[](basics.md)

This article builds on these so you understand how to create your own Content Fragment Models for your AEM headless project.

## 目标 {#objective}

* ****
* ****

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## Creating Content Fragment Models {#creating-content-fragment-models}

Then the Content Fragments Models can be created and the structure defined. This can be done under Tools -> Assets -> Content Fragment Models.

![](assets/cfm-tools.png)

**** Here you can enter various key details.

**** This means that your model will be available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![](/help/assets/content-fragments/assets/cfm-models-02.png)

********

## Defining Content Fragment Models {#defining-content-fragment-models}

****

![](/help/assets/content-fragments/assets/cfm-models-03.png)

So - what&#39;s to be done?

****

![](/help/assets/content-fragments/assets/cfm-models-04.png)

**** These depend on the type being used. 例如：

![](/help/assets/content-fragments/assets/cfm-models-05.png)

You can add as many fields as you need. 例如：

![内容片段模型](/help/assets/content-fragments/assets/cfm-models-07.png)

### Your Content Authors {#your-content-authors}

Your content authors do not see the actual Data Types and Properties that you&#39;ve used to create your models. This means that you might have to provide help and information on how they complete specific fields. For basic information you can use the Field Label and Default Value, but more complex cases project specific documentation might need to be considered.

>[!NOTE]
>
>See Additional Resources - Content Fragment Models.

## Managing Content Fragment Models {#managing-content-fragment-models}

<!-- needs more details -->

Managing your Content Fragment Models involves:

* Enabling (or disabling) them - this makes them available for authors when creating Content Fragments.
* Deleting - deletion is always needed, but you need to be aware of deleting a model that is already used for Content Fragments, in particular fragments that are already published.

## 发布 {#publishing}

<!-- needs more details -->

Content fragment models need to be published when/before any dependent content fragments are published.

>[!NOTE]
>
>If an author tries to publish a content fragment for which the model has not yet been published, a selection list will indicate this and the model will be published with the fragment.

** This aims to prevent changes that would result in errors to existing GraphQL schemas and queries, especially on the publish environment. ****

********

## What&#39;s Next {#whats-next}

Now that you have learned the basics, the next step is to start creating your own Content Fragment Models.

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [](/help/sites-cloud/authoring/getting-started/basic-handling.md)************

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [Defining your Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [Enabling or Disabling a Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [Allowing Content Fragment Models on your Assets Folder](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [Deleting a Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [Publishing a Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [Unpublishing a Content Fragment Model](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [Locked (Published) Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* Getting Started Guides

   * [Creating Content Fragment Models Headless Quick Start Guide](/help/implementing/developing/headless/getting-started/create-content-model.md)
