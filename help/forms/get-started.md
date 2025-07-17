---
title: HTML5表单快速入门
description: 要开始配置，请部署AEM Forms附加组件包，并将现有HTML5表单导入到AEM。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# HTML5表单快速入门 {#getting-started-with-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5 forms提供了多项适用于移动设备的功能。 它可以帮助您通过HTML5浏览器将当前的解决方案和工作流程扩展到平板电脑或智能手机设备。 部分功能包括：

* **基于HTML5的XFA表单模板渲染：**&#x200B;除了常规PDF forms之外，您现在还可以以HTML5格式渲染现有的基于XFA的表单。 它可帮助您将客户端平台扩展到支持HTML5且不支持带有XFA Forms的Adobe Reader的移动设备(Apple iPad、Android平板电脑、智能手机等)。 有关基于HTML5的渲染功能的详细信息，请参阅[HTML5表单简介](/help/forms/introductionhtml5.md)。

* **管理Forms：**&#x200B;此外，AEM还包括一些新功能，可简化表单的组织和管理流程。 您可以激活、停用、发布和预览表单。<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## 为HTML5表单配置环境 {#installing-html-forms}

要启用表单提交和正确渲染HTML5 Forms，请执行以下步骤：

* **添加Dispatcher筛选器：**&#x200B;更新您的`src/conf.dispatcher.d/filters/filters.any`文件以允许HTML5 Forms的必要请求。 添加以下筛选规则：

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **添加包以供提交：**&#x200B;在您的项目中，在`src/main/content/jcr_root/content`文件夹中添加包以支持表单提交功能。

* **导入HTML5 Forms：**&#x200B;将表单从本地文件系统导入AEM Forms。
