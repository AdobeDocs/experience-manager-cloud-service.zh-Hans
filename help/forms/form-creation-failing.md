---
title: 如何对表单创建失败进行故障排除？
description: 对AEM Formsas a Cloud Service环境中表单创建失败进行故障诊断。
feature: Adaptive Forms
role: User
exl-id: 169ea727-0941-4a1d-bc33-d9fe208b27ab
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# 发布表单时出现问题{#form-creation-fails}

用户更新到AEM Formsas a Cloud Service版本`2024.5.16461`后：

**某些用户**&#x200B;在创建表单时可能会遇到问题，这个问题使得当用户创建表单时，创建对话框中会弹出以下错误消息：

`A server error occurred. Try again after sometime.`

## 原因 {#cause-form-creation-fails}

出现此问题是因为作者发布表单时没有&#x200B;**先发布其中使用的模板**。 这会导致向`<template-path>/initial/jcr:content`节点中添加`jcr:uuid`和其他受保护且系统生成的属性，从而导致后续表单创建失败。

## 解决方法 {#resolution-form-creation-fails}

要解决此问题，请执行以下步骤：

1. 确保您在表单中使用的模板在路径`<template-path>/initial/jcr:content node`处没有`jcr:uuid`和其他系统生成的受保护属性。
1. 使用“模板”控制台明确Publish模板。
1. 现在，在发布模板时，尝试使用该模板创建新表单。
1. 如果在未来版本中使用了模板，请再次Publish该模板（如步骤2中所述）以防止表单创建失败问题。


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->
