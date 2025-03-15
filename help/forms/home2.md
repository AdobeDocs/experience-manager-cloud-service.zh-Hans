---
title: ' [!DNL AEM Forms] as a Cloud Service 简介'
description: 探索如何通过 AEM Forms 生成业务就绪表单、创建业务流程工作流以及使用文档服务生成和保护文档。
landing-page-description: 了解如何在 AEM as a Cloud Service 中使用表单。
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 11%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>正在查找其他版本的文档？</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html">AEM 6.5 Forms文档</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong>（当前）</li>
  </ul>
</div>

<div class="aem-forms-hero">
  <h2>AEM Forms as a Cloud Service</h2>
  <p>Adobe的云原生解决方案，用于创建、管理和提供智能表单、自动化工作流和个性化的客户通信。</p>
</div>

<div class="solutions-grid">
  <div class="solution-card">
    <div class="solution-icon">??</div>
    <h3>自适应表单</h3>
    <p>为最终用户的数字注册流程提供无缝表单填写体验</p>
  </div>
  <div class="solution-card">
    <div class="solution-icon">??</div>
    <h3>工作流</h3>
    <p>使用可配置工作流（如路由数据）自动化特定于业务的流程</p>
  </div>
  <div class="solution-card">
    <div class="solution-icon">??</div>
    <h3>客户通信</h3>
    <p>通过持续的个性化出站通信提高客户忠诚度</p>
  </div>
  <div class="solution-card">
    <div class="solution-icon">??</div>
    <h3>Headless Forms</h3>
    <p>跨渠道无缝地进行注册和注册</p>
  </div>
  <div class="solution-card">
    <div class="solution-icon">✍️</div>
    <h3>Acrobat Sign集成</h3>
    <p>捕获跨设备具有法律约束力且全球安全的电子签名</p>
  </div>
  <div class="solution-card">
    <div class="solution-icon">??</div>
    <h3>自动化表单转换</h3>
    <p>将基于PDF的旧版表单转换为可轻松在线管理和分发的自适应Forms</p>
  </div>

</div>

## 特性和功能 {#features}

<div class="features-section">
  <h3>表单创建和创作 {#form-creation}</h3>
  <div class="feature-category">
    <div class="feature-item">
      <h4>自适应表单</h4>
      <p>创建和管理交互式、动态、响应式、便于移动使用且由数据驱动的表单：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html">创建自适应表单</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">设置自适应表单的样式</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=zh-Hans">将自适应表单添加到AEM Sites页面</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html">使用现成的主题和模板</a></li>
      </ul>
    </div>

<div class="feature-item">
      <h4>Headless自适应Forms</h4>
      <p>在任何网站、应用程序或非可视化交互中构建并以本机方式呈现表单：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html">Headless自适应Forms简介</a></li>
        <li>使用首选编程语言（例如React）构建表单</li>
        <li>将表单本机集成到桌面和移动设备应用程序、网站和聊天应用程序中</li>
        <li>对表单应用程序重用您的专有UI组件</li>
        <li>以前端灵活性利用Adobe Experience Manager Forms的强大功能</li>
      </ul>
    </div>
  </div>

<div class="feature-category">
    <div class="feature-item">
      <h4>适用于Forms的Edge Delivery Services</h4>
      <p>创建并提供具有卓越用户体验的高性能表单：</p>
      <ul>
        <li><a href="/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md">使用通用编辑器进行WYSIWYG创作</a> — 用于生成表单的强大可视化界面</li>
        <li><a href="/help/edge/docs/forms/create-forms.md">基于文档的创作</a> — 使用熟悉的工具(如Microsoft Excel和Google Sheets)创建表单</li>
        <li>用于创建复杂表单逻辑的高级规则编辑器</li>
        <li>通过优化的表单加载获得近乎完美的Google Lighthouse分数</li>
        <li>以最少的开发时间更快地部署表单</li>
      </ul>
    </div>

<div class="feature-item">
      <h4>自动化表单转换服务</h4>
      <p>将基于PDF的旧表单转换为自适应Forms：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">配置自动化表单转换服务</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=zh-hans">将PDF forms转换为自适应Forms</a></li>
      </ul>
    </div>
  </div>


<h3>文档处理和通信 {#document-processing}</h3>
  <div class="feature-category">
    <div class="feature-item">
      <h4>通信 API</h4>
      <p>自动创建、管理和交付个性化通信：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation">生成个性化通信</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation">组合或分解PDF文档</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">创建符合PDF/A标准的文档</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html">使用DocAssurance API保护文档</a></li>
      </ul>
    </div>

<div class="feature-item">
      <h4>记录文档</h4>
      <p>创建和管理已提交表单的记录以供存档和遵守：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html">创建表单记录以进行长期存档</a></li>
        <li>自定义功能的服务器端可扩展性</li>
        <li>用于防篡改归档的记录文档功能</li>
      </ul>
    </div>
  </div>

<h3>工作流和流程自动化 {#workflow}</h3>
  <div class="feature-category">
    <div class="feature-item">
      <h4>表单工作流程</h4>
      <p>自动化涉及表单和文档服务的业务流程：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">发送表单或文档以供审阅</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">创建审批拒绝工作流</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br">将数据提交到数据存储或工作流</a></li>
      </ul>
    </div>

<div class="feature-item">
      <h4>电子签名</h4>
      <p>与Adobe Sign集成以获取电子签名：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html?lang=zh-Hans">使用Adobe Sign对自适应表单进行电子签名</a></li>
        <li>将<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">记录文档</a>或<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step">电子签名</a>步骤添加到业务工作流</li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=zh-Hans#sign-document-step">使用Adobe Sign和AEM工作流对文档进行电子签名</a></li>
      </ul>
    </div>
  </div>

<h3>数据集成和分析 {#data-integration}</h3>
  <div class="feature-category">
    <div class="feature-item">
      <h4>表单分析</h4>
      <p>使用Adobe Analytics获得有关用户行为的宝贵见解：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html?lang=zh-Hans">为自适应表单启用Adobe Analytics</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics.html">将AEM Forms与Adobe Analytics集成（手动方法）</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports.html">查看并了解自适应Forms分析报表</a></li>
      </ul>
    </div>

<div class="feature-item">
      <h4>Adobe集成</h4>
      <p>将表单与其他Adobe解决方案连接起来：</p>
      <ul>
        <li><a href="/help/forms/submit-adaptive-form-to-workfront-fusion.md">连接到Adobe Workfront Fusion</a>并将数据提交到Workfront方案</li>
        <li><a href="/help/forms/integrate-form-to-marketo-engage.md">连接到Adobe Marketo Engage</a>并<a href="/help/forms/submit-adaptive-form-to-marketo-engage.md">将数据提交到Marketo</a></li>
      </ul>
    </div>
  </div>

<div class="feature-category">
    <div class="feature-item">
      <h4>Microsoft集成</h4>
      <p>将表单与Microsoft服务连接起来：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=zh-Hans">连接到Microsoft® Dynamics 365</a></li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=zh-Hans">连接到Microsoft®Azure Blob Storage</a>并<a href="/help/forms/configure-submit-action-azure-blob-storage.md">将数据提交到Azure Blob Storage</a></li>
        <li><a href="/help/forms/connect-forms-to-sharepoint-document-library.md">连接到Microsoft® SharePoint文档库</a>并<a href="/help/forms/configure-submit-action-sharepoint.md">将数据提交到SharePoint</a></li>
        <li><a href="/help/forms/configure-submit-action-onedrive.md">连接到Microsoft® OneDrive</a>并将数据提交到OneDrive</li>
        <li><a href="/help/forms/forms-microsoft-power-automate-integration.md">连接到Microsoft®Power Automate</a>并在表单提交时触发流程</li>
        <li><a href="/help/forms/ms-dynamics-odata-configuration.md">连接到Microsoft® Dynamics OData</a></li>
      </ul>
    </div>

<div class="feature-item">
      <h4>其他数据源</h4>
      <p>连接到其他数据源和端点：</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=zh-Hans">连接到RDBMS或Rest端点</a></li>
        <li><a href="/help/forms/aem-forms-salesforce-integration.md">连接到Salesforce</a>并将数据提交到Salesforce</li>
        <li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-rest-endpoint">提交到 REST 端点</a></li>
      </ul>
    </div>
  </div>
</div>


<!-- 
## Start Quickly with AEM Forms {#quick-start}

<div class="quick-start-grid">
  <div class="quick-start-card">
    <div class="quick-start-icon">
      <img src="assets/create-form-icon.svg" alt="Create Form Icon">
    </div>
    <h3>Create your first form</h3>
    <p>Build an adaptive form in minutes using our step-by-step guide</p>
    <a href="/help/forms/creating-adaptive-form-core-components.md" class="quick-start-link">Get Started</a>
  </div>
  
  <div class="quick-start-card">
    <div class="quick-start-icon">
      <img src="assets/templates-icon.svg" alt="Templates Icon">
    </div>
    <h3>Explore ready-to-use templates</h3>
    <p>Browse our library of pre-built templates and themes to accelerate development</p>
    <a href="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html" class="quick-start-link">View Templates</a>
  </div>
  
  <div class="quick-start-card">
    <div class="quick-start-icon">
      <img src="assets/setup-icon.svg" alt="Setup Icon">
    </div>
    <h3>Set up your environment</h3>
    <p>Configure your local or cloud environment for AEM Forms development</p>
    <a href="/help/forms/setup-local-development-environment.md" class="quick-start-link">Configure Now</a>
  </div>
  
  <div class="quick-start-card">
    <div class="quick-start-icon">
      <img src="assets/data-icon.svg" alt="Data Icon">
    </div>
    <h3>Connect to data sources</h3>
    <p>Learn how to integrate forms with your existing data systems</p>
    <a href="/help/forms/create-form-data-models.md" class="quick-start-link">Connect Data</a>
  </div>
  
  <div class="quick-start-card">
    <div class="quick-start-icon">
      <img src="assets/migrate-icon.svg" alt="Migrate Icon">
    </div>
    <h3>Migrate from AEM 6.5</h3>
    <p>Follow our comprehensive guide to move from AEM 6.5 Forms to Cloud Service</p>
    <a href="/help/forms/migrate-to-forms-as-a-cloud-service.md" class="quick-start-link">Migrate Now</a>
  </div>
</div> 

-->

## 早期采用者功能 {#early-adopter-features}

<div class="early-adopter-section">
  <p><a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms抢先体验计划</a>提供对尖端功能的独家访问，这些功能在正式推出之前即可使用，包括：</p>

<ul class="early-adopter-list">
    <li><strong>AEM Forms AI Assistant (Gen AI)</strong> — 使用AI支持的建议更快地创建表单</li>
    <li><strong>AEM Forms Workfront Fusion Connector</strong> — 自动执行由表单提交触发的工作流</li>
    <li><strong>对话式Forms</strong> — 在任何AEM Sites页面上创建聊天式表单体验</li>
    <li><strong>适用于Edge Delivery的WYSIWYG创作</strong> — 使用Edge Delivery Services的通用编辑器生成表单</li>
    <li><strong>AEM Forms到Marketo Connector</strong> — 将表单提交与Marketo Engage集成</li>
  </ul>

<p>有关早期访问创新的完整列表和详细文档，请访问<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">AEM Forms早期访问计划页面</a>。</p>
</div>

## 准备好转变您的数字体验了吗？ {#get-started}

<div class="get-started-section">
  <p>立即开始创建引人入胜、响应迅速且智能的表单！</p>
  <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" class="get-started-button">加入AEM Forms as a Cloud Service</a>
</div>

<style>
/* Overall styling */
body {
  font-family: 'Adobe Clean', Arial, sans-serif;
  line-height: 1.6;
  color: #2c2c2c;
}

h2, h3, h4 {
  font-weight: 600;
  margin-top: 1.5em;
  margin-bottom: 0.5em;
}

h2 {
  font-size: 1.8em;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 0.5em;
}

h3 {
  font-size: 1.4em;
  color: #2c2c2c;
}

h4 {
  font-size: 1.2em;
  color: #2c2c2c;
}

a {
  color: #1473E6;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

ul {
  padding-left: 1.5em;
}

li {
  margin-bottom: 0.5em;
}

/* Hero section */
.aem-forms-hero {
  background-color: #f5f5f5;
  padding: 2em;
  border-radius: 8px;
  margin-bottom: 2em;
  text-align: center;
}

.aem-forms-hero h2 {
  font-size: 2em;
  margin-top: 0;
  border-bottom: none;
  color: #2c2c2c;
}

.aem-forms-hero p {
  font-size: 1.2em;
  max-width: 800px;
  margin: 0 auto;
}

/* Solutions grid */
.solutions-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5em;
  margin-bottom: 2em;
}

.solution-card {
  background-color: #ffffff;
  border: 1px solid #e1e1e1;
  border-radius: 8px;
  padding: 1.5em;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.solution-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.solution-icon {
  font-size: 2em;
  margin-bottom: 0.5em;
}

.solution-card h3 {
  margin-top: 0;
  font-size: 1.2em;
}

.solution-card p {
  margin-bottom: 0;
  font-size: 0.95em;
}

/* Features section */
.features-section {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.feature-category {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5em;
  margin-bottom: 2em;
}

.feature-item {
  background-color: #ffffff;
  border: 1px solid #e1e1e1;
  border-radius: 8px;
  padding: 1.5em;
}

.feature-item h4 {
  margin-top: 0;
  color: #2c2c2c;
}

.feature-item ul {
  margin-bottom: 0;
}

/* Quick start grid */
.quick-start-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 1.5em;
  margin: 2em 0;
}

.quick-start-card {
  background-color: #ffffff;
  border: 1px solid #e1e1e1;
  border-radius: 8px;
  padding: 1.5em;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.quick-start-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.quick-start-icon {
  margin-bottom: 1em;
}

.quick-start-icon img {
  width: 50px;
  height: 50px;
}

.quick-start-card h3 {
  margin-top: 0;
  font-size: 1.2em;
}

.quick-start-link {
  display: inline-block;
  margin-top: 1em;
  font-weight: 600;
}

/* Early adopter section */
.early-adopter-section {
  background-color: #f5f5f5;
  padding: 1.5em;
  border-radius: 8px;
  margin: 2em 0;
}

.early-adopter-list {
  margin-bottom: 0;
}

/* Get started section */
.get-started-section {
  text-align: center;
  margin: 3em 0 1em;
}

.get-started-section p {
  font-size: 1.2em;
  margin-bottom: 1em;
}

.get-started-button {
  display: inline-block;
  background-color: #1473E6;
  color: white;
  padding: 0.8em 1.5em;
  border-radius: 4px;
  font-weight: 600;
  transition: background-color 0.3s ease;
}

.get-started-button:hover {
  background-color: #0d66d0;
  text-decoration: none;
}

/* Version selector */
.version-selector {
  background-color: #f5f5f5;
  padding: 1em;
  border-radius: 8px;
  margin-bottom: 2em;
}

.version-selector p {
  margin-top: 0;
  font-weight: 600;
}

.version-selector ul {
  margin-bottom: 0;
}

/* Responsive adjustments */
@media (max-width: 1200px) {
  .feature-category {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .quick-start-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  .feature-category {
    grid-template-columns: 1fr;
  }
  
  .solutions-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .quick-start-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .solutions-grid {
    grid-template-columns: 1fr;
  }
  
  .quick-start-grid {
    grid-template-columns: 1fr;
  }
}
</style>
</style>
