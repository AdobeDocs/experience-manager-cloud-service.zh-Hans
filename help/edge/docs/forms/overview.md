---
title: AEM Forms Edge Delivery Service 概述
description: AEM Forms Edge Delivery Service 专为实现最佳性能而构建，让您能够畅想简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d63d0f1152d0a23623c197924a44bc6b1e69fb42
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 25%

---


# AEM Forms Edge Delivery Service

利用Adobe的AEM Forms Edge Delivery Service，简化表单创建并提高完成率。 这项功能强大、可组合的服务使您能够构建具有卓越性能和视觉吸引力的企业级表单。 AEM会优先处理用户体验和业务目标，从而确保超快加载时间和增加表单完成次数。

利用该服务，您可以：

* **使用令人惊叹的表单Captivate用户**：使用预建组件库轻松构建复杂且吸引人的表单。 轻松集成 reCAPTCHA、直接将表单提交到电子邮件，并允许将文件无缝上传到安全存储解决方案，例如 Sharepoint、Azure 存储和 Amazon S3。甚至创建您自己的自定义表单组件来实现您的独特愿景。

* **使用选定工具创建数字注册体验**：通过分离内容来源而提高创作效率。开箱即用地您可以使用基于文档的创作(Microsoft 365和Google Workspace)和AEM创作(AEM编辑器)。 因此，您可以在同一网站上使用多个内容源并使用首选创作工具，例如Microsoft Excel、Google Sheets或自适应Forms编辑器。

* **使用完美的Lighthouse分数构建表单**：构建可快速加载和渲染的表单，即使在Internet连接速度较慢的情况下也是如此。 缩短加载时间并优化用户体验有助于提高表单完成率和转化率。

  <div>
    <style>
    .image-container {
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container 
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="EDS Forms主要功能">
    </div>


</div>

<!--

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
    >[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## 主要功能

* **基于HTML5的表单字段组件**：通过AEM Forms Edge Delivery Service，可使用基于HTML5的表单组件创建用户友好的交互式表单 [输入类型](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types)， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">文本区域</a>， <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">选择</a>、和 <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">字段集</a>  元素。 这些组件适用于不同类型的数据收集，并可轻松自定义以满足您的特定需求。

* **辅助功能**：可访问表单块中的字段。 每个标签都与其相应的输入元素链接，并且自动生成ID以进行链接。 与字段关联的描述通过aria-descripted by属性链接。 支持使用标准Tab/Shift + Tab键进行键盘导航。

* **样式**：每个表单字段都有一个固定的HTML结构，使用自定义CSS或JavaScript文件可轻松进行修饰。 CSS和JS中用于定位字段的选择器根据类型和名称提供。 由于该标准化的结构，您可以轻松创建新的选择器。

* **规则**：轻松创建逻辑以根据用户输入或预定义条件调整字段可见性、验证和行为。 规则提供了一种灵活且直观的方式为表单添加智能，确保它们根据用户输入进行无缝调整。

* **验证**：在提交之前，表单经过验证，并且无效字段会适当地标示为向用户显示的错误消息。 可以使用各种模式来显示这些错误。

我们应请求提供了以下一些高级功能：

* **文件上传**：您可以将文件附件功能添加到表单。 无论您需要从用户那里收集文档、图像或其他文件，文件上传功能都能为您轻松提供。 利用自定义处理选项，您可以定制文件上传过程以满足特定要求。

* **reCAPTCHA**：通过我们的开箱即用(OOTB)支持将Google reCAPTCHA无缝集成到您的表单中，从而从中受益。 保护您的表单免受欺诈性活动、垃圾邮件和滥用，同时保持流畅且无中断的用户体验。

* **在提交表单时发送电子邮件通知**：消除手动跟进的麻烦，并确保与我们内置的表单提交电子邮件自动化功能及时通信。 此集成解决方案让您在有人填写您网站上的表单时，可以轻松通知相关方，包括发送表单数据。 无需复杂的配置或额外的工具 — 开箱即用。


## 可用的Forms块

AEM Forms Edge Delivery Service提供两种类型的表单块以满足不同需求：

* **基本Forms块**：这是一个通用选项，适用于创建具有基本功能的简单表单。 它允许您集成各种输入类型，如文本字段、下拉菜单和单选按钮，使您能够有效地收集用户数据。

* **自适应Forms块**：此高级块可解锁基本Forms块以外的其他功能，使您能够构建更复杂且更具交互性的表单。 以下是其主要功能的划分说明：

   * 规则：在表单中定义基于逻辑的操作。 您可以使用规则有条件地显示或隐藏表单节、根据用户输入预填充字段以及执行各种验证以确保数据完整性。

   * 服务器端可扩展性：通过将表单与服务器端逻辑集成来扩展表单的功能。 这样，您就可以执行复杂的计算，与外部系统交互，并根据表单中的用户操作自动执行特定任务。

   * Cross Walk：简化工作流和数据管理：利用AEM的强大功能可以：

      * 使用AEM编辑器设计用户友好的表单。

      * 生成“记录文档”，用于提交数据的安全和防篡改存档。

      * 加快使用Adobe Sign进行电子签名以实现流畅安全的签名体验。

      * 通过AEM工作流自动化业务流程，根据表单提交触发操作。

      * 轻松与各种数据源集成，实现无缝的数据流和交换。

  使用Adaptive Forms Block需要额外的许可证。

### 选择正确的Forms块

Basic和Adaptive Forms块之间的选择取决于您的特定要求。 如果您需要一个直接的解决方案来收集基本用户信息，那么Basic Forms Block将是您的最佳选择。 但是，如果您的表单需要复杂的逻辑、数据操作、与外部系统集成，或使用AEM功能简化工作流，以及 **您拥有必要的许可证**，自适应Forms块提供实现目标所需的功能和灵活性。


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
            <br><b style="margin-top: 5px;">使用 Google Sheets 或 Microsoft Excel 创建表单</b>
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









