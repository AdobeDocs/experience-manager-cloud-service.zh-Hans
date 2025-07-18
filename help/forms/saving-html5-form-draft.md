---
title: 将HTML5表单另存为草稿
description: 将HTML5表单另存为草稿，并在稍后阶段继续填写表单。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 81a6c2b942df0e72a0b7d359f29c615a44640396
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 4%

---


# 将HTML5表单另存为草稿 {#saving-an-html-form-as-a-draft}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

您可以将HTML5表单另存为草稿，并在稍后阶段继续填写表单。 Forms Portal允许任何用户保存和恢复HTML5表单。 要启用另存为草稿功能，请将以下配置添加到配置文件节点：

## 自定义配置文件以允许另存为草稿功能 {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms开箱即用地提供&#x200B;**另存为草稿**&#x200B;配置文件。 您可以使用另存为草稿配置文件呈现表单，以启用HTML5表单的草稿功能。 您可以在&#x200B;**HTML Manager**&#x200B;中为表单指定Forms渲染配置文件。

要为现有[自定义配置文件](/help/forms/custom-profile.md)启用“另存为草稿”功能，请将以下属性添加到自定义配置文件节点：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>启用另存为草稿功能</p> <p>用于此配置文件。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>字符串</td>
   <td>true</td>
   <td><p>允许上载附件</p> <p>使用此配置文件。</p> </td>
  </tr>
 </tbody>
</table>

## 草稿存储和列表 {#drafts-storage-and-listing}

为表单启用另存为草稿功能后；保存表单时，该表单会列在草稿和提交组件中。 您可以检索并开始填写从“草稿和提交”组件保存的表单。

要为草稿和提交组件启用表单列表，请将以下属性添加到配置文件节点：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>价值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>字符串</td>
   <td>true</td>
   <td>要在提交后使草稿和表单列在<br /> Forms Portal草稿和提交组件中，请执行以下操作</td>
  </tr>
 </tbody>
</table>

默认情况下，AEM Forms会将与表单草稿和提交关联的用户数据存储在Publish实例上的/content/forms/fp节点中。 您可以添加自定义存储提供商，有关详细信息，请参阅[草稿和提交组件的自定义存储](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-forms-portal/adding-custom-storage-provider-forms)。
