---
title: ' [!DNL AEM Forms] as a Cloud Service 简介'
description: 探索如何通过 AEM Forms 生成业务就绪表单、创建业务流程工作流以及使用文档服务生成和保护文档。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表单。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 4b4bc6f754c6336136d409cf49617c7fafd4f4c3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 11%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>正在查找其他版本的文档？</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html?lang=zh-Hans">AEM 6.5 Forms文档</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong>（当前）</li>
  </ul>
</div>

## 什么是AEM Forms as a Cloud Service？

AEM Forms as a Cloud Service是Adobe的云原生解决方案，用于创建、管理和交付数字表单和通信。 它使组织能够在整个客户历程中将复杂的交易转换为简单的数字体验。 利用该服务，您可以：

* 数字化和简化注册与登录体验
* 提供个性化的通信
* 自动化后台工作流程
* 将表单和通信体验与数据源集成
* 跟踪和优化表单性能

这项服务始终最新、可用，且在不断学习。企业可以使用 [!DNL AEM Forms] as a Cloud Service，在云中获得所有这些功能，而无需任何本地基础架构。这项服务还将企业从复杂的升级周期中解放出来，因为它会持续更新最新功能。

Adobe [!DNL Experience Manager Forms as a Cloud Service] 是一个以客户为中心的解决方案，可帮助完成客户历程的每一步：

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>自适应表单</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>创建适应用户输入和设备类型的响应式动态表单：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">创建自适应Forms</a> — 生成可自动调整到不同屏幕大小和用户输入的表单</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type">富组件库</a> — 使用各种输入字段和UI组件</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components">样式自适应Forms</a> — 将一致的品牌和视觉设计应用于表单</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">使用预建主题和模板</a> — 使用现成的组件加快开发</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components">表单验证</a> — 实施客户端和服务器端验证规则</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components">提交操作</a> — 配置用户提交表单时发生的情况</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components">记录文档</a> — 创建已提交表单数据的永久记录</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">将Forms添加到AEM Sites页面</a> — 将表单无缝集成到您的网站</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page">将Forms添加到第三方网站页面</a> — 将表单无缝集成到您的网站</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>通信API</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>以编程方式生成、操作和保护文档：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation">生成个性化通信</a> — 基于模板和数据创建自定义文档</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">汇编和处理PDF</a> — 合并、拆分和修改PDF文档</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">创建PDF/A文档</a> — 生成存档质量文档</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis">应用签名</a> — 具有签名的安全文档</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">加密和解密PDF</a> — 保护敏感文档内容</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">将XDP转换为PostScript</a> — 将XDP文档转换为PostScript格式</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">将XDP转换为PCL</a> — 将XDP文档转换为打印机命令语言</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">将XDP转换为ZPL</a> — 将XDP文档转换为Zebra打印语言</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">将PDF转换为PDF/A标准</a> — 创建符合存档要求的PDF文档</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards">添加数字签名</a> — 对文档进行数字签名以进行身份验证</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>适用于Forms的Edge Delivery Services</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>使用Edge Delivery Services创建和提交表单：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Edge Delivery Forms概述</a> — 了解Edge Delivery Services的表单</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">适用于Forms的通用编辑器</a> — 使用WYSIWYG通用编辑器创建表单</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial">基于文档的创作</a> — 使用Microsoft Word或Google Docs创建表单</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">为Edge Delivery Forms设置样式</a> — 为表单应用自定义样式</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Headless Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>跨任何渠道或前端框架交付表单体验：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-headless-adaptive-forms/using/overview">Headless Forms简介</a> — 了解Headless表单方法</li>
        <li>使用React或其他前端框架构建表单</li>
        <li>将表单集成到移动应用程序、网站和聊天应用程序中</li>
        <li>将现有UI组件用于表单功能</li>
        <li>维护后端表单逻辑，同时具有前端灵活性</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>工作流自动化</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>自动化涉及表单和文档的业务流程：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step">创建业务流程</a> — 发送表单以供审批或反馈、提交后工作流或后端工作流来管理注册流程</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">在AEM工作流中使用Adobe Sign</a> — 发送文档以供签名 </li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">生成记录文档</a> — 按需生成或提交表单</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>电子签名</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>在表格和文档中添加具有法律约束力的电子签名：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Adobe Sign集成</a> — 在自适应Forms中启用电子签名</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">向工作流添加电子签名</a> — 在业务流程中包含签名步骤</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">带签名的记录文档</a> — 生成表单提交的签名记录</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Analytics和Insights</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>深入了解表单使用情况和性能：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">启用Adobe Analytics</a> — 跟踪表单使用情况和性能</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics">手动Analytics集成</a> — 设置分析以进行详细跟踪</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports">查看Analytics报表</a> — 分析表单性能和用户行为</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>数据集成</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>将表单连接到现有数据源和系统：</p>
      <h4>Adobe生态系统</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> — 通过Adobe Sign发送电子签名</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a> — 将表单与Adobe Marketo Engage集成</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">AEM工作流</a> — 通过提交表单触发AEM工作流</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> — 将自适应表单提交到Adobe Workfront Fusion</li>
      </ul>
      <h4>Microsoft集成</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> — 与Microsoft的CRM集成</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Azure Blob存储</a> — 将表单数据存储在Microsoft的云存储中</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">SharePoint文档库</a> — 连接到Microsoft SharePoint文档库</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">SharePoint列表</a> — 连接到Microsoft SharePoint列表</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a> — 连接到Microsoft OneDrive</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a> — 触发Microsoft Power Automate流程</li>
      </ul>
      <h4>其他数据源和服务</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> — 与Salesforce CRM集成</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">RESTful服务</a> — 连接到任何REST API终结点</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">RDBMS数据库</a> — 连接到关系数据库</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email">电子邮件</a> — 通过电子邮件发送表单数据</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Forms门户</a> — 提交到Forms门户以保存草稿</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email">通过电子邮件发送PDF</a> — 通过电子邮件发送已提交表单的PDF版本</li>
        <li><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model">使用表单数据模型提交</a> — 使用表单数据模型提交数据</li>
      </ul>
    </div>
  </div>
</div>

## AEM Forms as a Cloud Service快速入门

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>适用于企业用户</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>了解基础知识</strong>：了解<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">自适应Forms</a>以及它们如何帮助您将业务流程数字化。</li>
        <li style="margin-bottom: 8px;"><strong>浏览模板</strong>：浏览<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">预建模板和主题</a>以抢滩您的表单项目。</li>
        <li style="margin-bottom: 8px;"><strong>了解表单创作</strong>：按照<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring">表单创作指南</a>创建您的第一个表单。</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>面向开发人员</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>设置环境</strong>：为AEM Forms配置<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">本地开发环境</a>。</li>
        <li style="margin-bottom: 8px;"><strong>学习架构</strong>：了解AEM Forms as a Cloud Service的<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">架构</a>。</li>
        <li style="margin-bottom: 8px;"><strong>浏览API</strong>：熟悉<a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/">可用于扩展和集成Forms的API </a>和SDK。</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>适用于管理员</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>加入Cloud Service</strong>：按照<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">加入指南</a>来设置AEM Forms as a Cloud Service。</li>
        <li style="margin-bottom: 8px;"><strong>配置服务</strong>：设置<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">与其他Adobe服务</a>(如Adobe Analytics)的集成。</li>
        <li style="margin-bottom: 8px;"><strong>从AEM 6.5迁移</strong>：如果您来自AEM 6.5，请按照<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=zh-Hans">迁移指南</a>迁移到Cloud Service。</li>
      </ol>
    </div>
  </div>
</div>

## 早期采用者功能

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; margin-bottom: 30px;">
  <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
    <h3>AEM Forms抢先体验计划</h3>
  </div>
  <div class="card-body" style="padding: 20px; background-color: #ffffff;">
    <p><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms抢先体验计划</a>提供对尖端功能的独家访问，这些功能在正式推出之前即可使用，包括：</p>
    <ul style="margin-top: 10px; padding-left: 25px;">
      <li style="margin-bottom: 8px;"><strong>AEM Forms AI Assistant (Gen AI)</strong> — 使用AI支持的建议更快地创建表单</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms Workfront Fusion Connector</strong> — 自动执行由表单提交触发的工作流</li>
      <li style="margin-bottom: 8px;"><strong>对话式Forms</strong> — 在任何AEM Sites页面上创建聊天式表单体验</li>
      <li style="margin-bottom: 8px;"><strong>适用于Edge Delivery的WYSIWYG创作</strong> — 使用Edge Delivery Services的通用编辑器生成表单</li>
      <li style="margin-bottom: 8px;"><strong>AEM Forms到Marketo Connector</strong> — 将表单提交与Marketo Engage集成</li>
    </ul>
    <p>有关早期访问创新的完整列表和详细文档，请访问<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms早期访问计划页面</a>。</p>
  </div>
</div>

<div style="background-color: #f0f7ff; border-left: 4px solid #1473e6; padding: 20px; margin: 30px 0; border-radius: 4px;">
  <h3 style="margin-top: 0; color: #1473e6;">准备好开始了吗？</h3>
  <p><a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" style="font-weight: bold; color: #1473e6;">立即加入AEM Forms as a Cloud Service</a>，并转变贵组织的数字表单体验。</p>
</div>
