---
title: AEM Forms Edge交付服务概述
description: AEM Forms Edge交付服务专为实现卓越性能而打造，使您能够预见简化数据收集和用户参与的未来。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# AEM Forms Edge Delivery Service {#aem-forms-edge-delivery-service-overview}

AEM Forms边缘交付服务是由Adobe提供的一项可组合服务，允许您创建和交付影响大、性能快的Web窗体。 您可以使用该服务执行以下操作：

* **制作令人惊叹的视觉表单**：抛弃平淡无奇的饼干切割器设计，用反映您品牌身份的动态现代形式吸引用户。 利用预建组件或创建您自己的自定义组件，快速轻松地实现您的愿景。

* **使用完美的Lighthouse分数构建表单**：构建可快速加载和渲染的表单，即使在Internet连接速度较慢的情况下也是如此。 更快的加载时间和优化的用户体验有助于提高表单完成率和转化率。

* **简化创作和提交**：使用熟悉的工具(如Microsoft Excel或Google Sheets)创建表单，而不是使用传统的创作环境。 将表单直接提交到Microsoft Excel或Google工作表，并使用其生态系统轻松处理提交的数据。


此可组合服务与内容源分离，通过允许用户使用其首选的创作工具，提供了内容创建的灵活性。

![Edge Delivery表单创作工具](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

内容创建者可以利用他们熟悉的工具(如Microsoft Excel或Google Sheets（基于文档的创作）、JSON编辑器或AEM Forms自适应Forms编辑器以进行WYSIWYG编辑(AEM Forms项目))来设计和创建表单。

>[!NOTE]
>
>
> 所见即所得编辑功能和Cross Walk区在早期采用者计划下提供。 您可以从官方电子邮件ID写信到aem-forms-early-adopter-program@adobe.com ，加入率先采用者计划并请求获取该功能的访问权限。

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="使用eds forms创建表单" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用Google Sheets或Microsoft Excel创建表单</b>
        </a>
        <p>创建可在移动设备上快速加载和渲染并自动重排的表单。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="向表单字段添加验证" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">应用字段验证</b>
        </a>
        <p>通过检查表单输入内容中的格式是否正确，减少错误和挫折。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="在EDS表单中使用表单片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">创建表单片段</b>
        </a>
        <p>在多个表单中重用预配置的片段。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="翻译EDS表单" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">翻译表单</b>
        </a>
        <p>在控制成本的同时，扩大表单的覆盖范围。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="将样式或主题应用于eds表单" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">自定义主题</b>
        </a>
        <p>通过在表单中应用相同主题来创建一致的品牌图像。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="向EDS表单添加可重复的部分" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">添加可重复部分</b>
        </a>
        <p>轻松创建可重复的部分并将其添加到表单中。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="使用标准JavaScript和CSS创建自定义表单组件"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">创建自定义组件</b>
        </a>
        <p>使用标准JavaScript和CSS创建组件和主题。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="在EDS表单中使用reCAPTCHA" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">使用reCAPTCHA</b>
        </a>
        <p>使用OOTB reCAPTCHA集成提供强大的垃圾邮件和机器人保护。</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="提交表单" alt="在EDS表单中使用表单片段" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">将表单提交到电子表格</b>
        </a>
        <p>将表单直接提交到Microsoft Excel或Google工作表。</p>
    </div>
</div>


</br>









