---
title: AEM Forms Edge Delivery Service 概述
description: AEM Forms Edge Delivery Service 专为实现最佳性能而构建，让您能够畅想简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d0c4f2f880ef7c11b11144502d30430336ac682e
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 30%

---


# AEM Forms Edge Delivery Service

利用Adobe的AEM Forms Edge Delivery Service，简化表单创建并提高完成率。 这项功能强大、可组合的服务使您能够构建具有卓越性能和视觉吸引力的企业级表单。 AEM会优先处理用户体验和业务目标，从而确保超快加载时间和增加表单完成次数。

您可以使用该服务执行以下操作：

* **使用令人惊叹的表单Captivate用户**：使用预建组件库轻松构建复杂且吸引人的表单。 轻松集成reCAPTCHA，将表单直接提交到电子邮件，并允许无缝文件上传到Sharepoint、Azure Storage和Amazon S3等安全存储解决方案。 甚至可创建您自己的自定义表单组件，将您独特的愿景变为现实。

* **使用您选择的工具创建数字注册体验**：通过分离内容源提高创作效率。 开箱即用地您可以使用基于文档的创作(Microsoft 365和Google Workspace)和AEM创作(AEM编辑器)。 因此，您可以在同一网站上使用多个内容源并使用首选创作工具，例如Microsoft Excel、Google Sheets或自适应Forms编辑器。

* **使用完美的Lighthouse分数构建表单**：构建可快速加载和渲染的表单，即使在Internet连接速度较慢的情况下也是如此。 缩短加载时间并优化用户体验有助于提高表单完成率和转化率。

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms主要功能">
    </div>


</div>

<!--

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

## 主要功能

* **基于HTML5的表单字段组件**：通过AEM Forms Edge Delivery Service，您可以使用基于有效HTML的表单字段创建用户友好的交互式表单5 [输入类型](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文本区域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">选择</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">字段集</a>  组件。 这些组件适用于不同类型的数据收集，并可轻松自定义以满足您的特定需求。

* **辅助功能**：可访问表单块中的字段。 每个标签都与其相应的输入元素链接，并且自动生成ID以进行链接。 与字段关联的描述通过aria-descripted by属性链接。 支持使用标准Tab/Shift + Tab键进行键盘导航。

* **表单规则**：创建逻辑以根据用户输入或预定义条件调整字段可见性、验证和行为。 规则提供了一种灵活且直观的方式为表单添加智能，确保它们根据用户输入进行无缝调整。

* **文件上传**：通过无缝文件附件功能增强表单。 无论您需要从用户那里收集文档、图像或其他文件，自适应表单块都能让您轻松集成文件上传功能。 利用自定义处理选项，您可以定制文件上传过程以满足特定要求。

* **表单验证**：在提交之前，表单经过验证，并且无效字段会适当地标示为向用户显示的错误消息。 可以使用各种模式来显示这些错误。

* **设置Forms样式**：每个表单字段都有一个固定的HTML结构，可以使用自定义CSS或JavaScript文件进一步修饰该结构。 在CSS/JS中，根据类型和名称提供了用于定位字段的选择器。

## 工作流

![基于文档的创作生态系统](/help/edge/assets/document-based-authoring-workflow.png)

## 开始创建表单

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
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="使用规则向表单添加动态行为" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用规则向表单添加动态行为</b>
        </a>
        <p>跨多种表单重复使用预配置的片段。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="翻译 EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">翻译表单</b>
        </a>
        <p>扩大表单的覆盖范围，同时控制成本。</p>
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









