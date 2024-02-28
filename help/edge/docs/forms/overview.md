---
title: AEM Forms Edge Delivery Service 概述
description: AEM Forms Edge Delivery Service 专为实现最佳性能而构建，让您能够畅想简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1dc4915f0b149ef67dfa22c8d4c6be7538170d38
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 65%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}


<div>
&lt;style="font-family: Arial, sans-serif; margin: 0; padding: 0;"&gt;
    <main class="content">
      <section class="content-section">
        <p style="line-height: 1.5;">AEM Forms Edge Delivery Service 是 Adobe 提供的一项可组合服务，允许您创建和交付具有高影响力、可快速执行的 Web 表单。您可以使用该服务执行以下操作：</p>
        </section> <section class="content-section">
        <h2 style="font-size: 20px; margin-bottom: 10px;">使用令人惊叹的表单Captivate用户</h2>
        <img src="/help/edge/assets/enrollment-form.png" alt="注册表单" style="float: left; margin: 0 20px 20px 0; width: 150px;">
        <p style="line-height: 1.5;">使用预建组件库轻松构建复杂且引人入胜的表单。 轻松集成reCAPTCHA，将表单直接提交到电子邮件，并允许无缝文件上传到Sharepoint、Azure Storage和Amazon S3等安全存储解决方案。 甚至可创建您自己的自定义表单组件，将您独特的愿景变为现实。</p>
        </section> <section class="content-section">
        <h2 style="font-size: 20px; margin-bottom: 10px;">使用完美的Lighthouse分数构建表单</h2>
        <img src="/help/edge/assets/lighthouse-forms.png" alt="表单的完美灯塔分数" style="float: right; margin: 20px 0 0 20px; width: 150px;">
        <p style="line-height: 1.5;"> 构建可快速加载和渲染的表单，即使在Internet连接速度较慢的情况下也是如此。 缩短加载时间并优化用户体验有助于提高表单完成率和转化率。</p>
        </section>
        <section class="content-section">
        <h2 style="font-size: 20px; margin-bottom: 10px;">使用您选择的工具创建数字注册体验</h2>
        <img src="/help/edge/assets/edge-delivery-forms-authoring-tools.png" alt="注册表单" style="float: left; margin: 0 20px 20px 0; width: 150px;">
        <p style="line-height: 1.5;">通过分离内容来源而提高创作效率。可直接使用 AEM 创作和基于文档的创作。因此，您可以在同一网站上使用多个内容源，并使用首选创作工具，例如Microsoft Excel、Google Sheets或AEM编辑器。</p>
        </section>
</div>


<!-- >
* **Captivate users with stunning forms**: 
Build complex and engaging forms with ease using a library of pre-built components. Easily integrate reCAPTCHA, submit forms directly to email, and allow seamless file uploads to secure storage solutions like Sharepoint, Azure Storage, and Amazon S3. Even create your own custom forms components to bring your unique vision to life. 

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 从基础知识开始

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="使用 EDS Forms 创建表单" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用Google Sheets或Microsoft Excel创建表单</b>
        </a>
        <p>创建可在移动设备上快速加载和渲染并自动回流的表单。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="提交表单" alt="在 EDS Form 中使用表单片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">将表单提交到电子表格</b>
        </a>
        <p>直接将表单提交到您的 Microsoft Excel 或 Google Sheets。</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="对 EDS Form 应用样式或主题" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">自定义主题</b>
        </a>
        <p>通过在不同表单中应用相同的主题来创建一致的品牌形象。</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="向表单字段添加验证" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">应用字段验证</b>
        </a>
        <p>通过检查表单输入的格式是否正确，减少错误和挫败感。</p>
    </div> 
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="翻译 EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">翻译表单</b>
        </a>
        <p>扩大表单的覆盖范围，同时控制成本。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="在 EDS Form 中使用表单片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">创建表单片段</b>
        </a>
        <p>跨多种表单重复使用预配置的片段。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="在 EDS Form 中添加可重复部分" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">添加可重复的部分</b>
        </a>
        <p>轻松创建可重复的部分并将其添加到表单中。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="使用标准 JavaScript 和 CSS 创建自定义表单组件"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">创建自定义组件</b>
        </a>
        <p>使用标准 JavaScript 和 CSS 创建组件和主题。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="以 EDS Form 的形式使用 reCAPTCHA" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用 reCAPTCHA</b>
        </a>
        <p>使用 OOTB reCAPTCHA 集成实现强大的垃圾邮件和机器人防护功能。</p>
    </div>

</div>


</br>









