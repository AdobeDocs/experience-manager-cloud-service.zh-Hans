---
title: Forms Experience Builder - 提示词库
description: 收集经过验证的提示词模式和示例，用于在表单管理用户界面、自适应表单编辑器和通用编辑器中使用 AI 辅助构建表单。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: ht
source-wordcount: '2193'
ht-degree: 100%

---


# Forms Experience Builder - 提示词库

针对 Forms Experience Builder 优化的可重复使用的提示词模式和示例收藏集。这个精简的提示词库专注于两种核心创建方法：从头开始创建以及导入和转换，并增强了对 LLM 驱动的智能字段和品牌一致性的支持。

>[!NOTE]
>
> Forms Experience Builder 在早期采用者计划中提供。请从您的工作地址发送电子邮件至 `aem-forms-ea@adobe.com`，以申请访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着 Forms Experience Builder 在早期采用者计划期间不断改进，提示词、示例和最佳实践可能会发生变化。

## 使用这个提示词库

此库为常见的表单构建场景提供了可重复使用的提示词模式。如需了解全面的最佳实践，请参阅 [Forms Experience Builder 快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

### 关于此库的快速小建议

- **从示例开始** - 使用库中提供的提示词作为模板，根据您的需求进行调整
- **两种创建方法** - 选择“从头创建”或“导入并转换”方法
- **描述具体** - 在一般示例中添加您自己的详细信息
- **彻底测试** - 始终在您的特定环境中验证结果

### 品牌模板和样式

**提前准备好品牌资产，以创建一致的表单：**

- **品牌模板** - 使用您组织的颜色、字体和布局模式准备标准化表单模板
- **样式指南** - 定义一致的字段样式、按钮设计和间距标准，供 Forms Experience Builder 应用
- **组件库** - 与您的开发团队合作，准备符合您品牌形象的可重复使用的表单组件
- **视觉资产** - 准备用于表单集成的徽标、图标和背景元素

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## 逐步开发示例

这些示例展示了如何逐步构建表单，从简单开始，逐渐增加复杂性：

### 示例 1：逐步构建一个联系表单

**步骤 1 - 从简单开始：**

    创建一个包含姓名、电子邮件和消息字段的基本联系表

**步骤 2 - 添加验证：**

    将 @name 和 @email 设为必填字段并添加适当的验证

**步骤 3 - 增强用户体验**

    添加占位符文本：@name“您的全名”、@email“your.email@company.com”、@message“告诉我们您需要什么帮助”

**步骤 4 - 添加高级功能：**

    添加一个下拉查询类型，其中包含以下选项：“一般问题”、“支持请求”、“销售查询”、“合作伙伴关系”

**步骤 5 - 实施条件逻辑：**

    /创建规则 只有在 @inquiryType 等于“支持请求”的情况下显示 @urgencyLevel 下拉菜单（低、中、高）

### 示例 2：逐步构建一个注册表单

**步骤 1- 基本结构：**

    创建一个包含个人信息面板的用户注册表

**步骤 2 - 添加必需字段：**

    添加 @firstName、@lastName、@email、@phoneNumber 字段以及适当的验证

**步骤 3 - 添加业务逻辑：**

    创建规则：如果 @age 未满 18 岁，则显示父母/监护人信息分区

**步骤 4 - 使用偏好设置进行增强：**

    添加一个包含 @newsletterSubscription、@marketingConsent、@termsAccepted 的偏好设置面板

**步骤 5 - 添加文件上传：**

    添加一个 @profilePicture 的文件上传字段，大小限制为 5MB

## 表单创建和管理

**何时使用：**&#x200B;当您需要创建新表单或修改现有表单时。

**如何使用：**&#x200B;选择以下两种方法之一：“从头创建”或者“导入并转换”（参见[快速入门指南](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)）。

**提示词示例 - 创建简单表单：**

    创建一个客户反馈表，其中包含：
    - 产品评分（1-5 星）
    - 提供详细反馈的备注字段
    - 客户电子邮件地址（可选）
    - 提交至电子邮件通知

**提示词示例 - 创建复杂表单：**

    创建一个全面的员工入职表，其中包含：
    
    **个人信息分区：**
    - 全名（名、中间名、姓）
    - 出生日期及年龄验证
    - 联系方式（电子邮件、电话、地址）
    - 紧急联系方式
    
    **雇佣详细信息：**
    - 职位和部门选择
    - 开始日期和工作日验证
    - 薪资信息和保密声明
    - 报告结构
    
    **文件上传：**
    - 简历/履历上传（PDF、DOC、DOCX）
    - 身份验证文件
    - 税表和银行信息
    - 已签名的雇佣合同
    
    **偏好设置：**
    - 福利选择和费用计算器
    - 工作计划偏好
    - 培训要求
    - 设备需求
    
    **验证规则：**
    - 电子邮件格式验证
    - 电话号码格式验证
    - 年龄必须 18 岁或以上
    - 必须上传所有必需文件
    - 必须接受条款和条件
    
    **提交操作：**
    - 向新员工发送确认电子邮件
    - 通知人力资源部门
    - 在人力资源系统中创建员工记录
    - 计划迎新介绍会

**表单管理提示词：**

    导入这个 PDF 申请表并将其转换为一个具有增强验证功能的自适应表单
    
    更新这个现有的联系表，添加社交媒体账号和首选联系方式
    
    将这个注册表重新组织为一个 3 步式向导：个人信息、偏好设置、确认

## 字段管理和配置

**何时使用：**&#x200B;当您需要添加、修改或配置表单字段时。

**如何使用：**&#x200B;明确说明字段类型、验证规则以及用户体验要求。

**提示词示例 - 添加基本字段：**

    添加一个“公司名称”文本输入字段，并添加占位符“输入您的公司名称”

**提示词示例 - 配置高级字段：**

    添加一个全面的地址分区，其中包含以下内容：
    
    **街道地址：**
    - 地址第 1 行（必填，最多 100 个字符）
    - 地址第 2 行（可选，最多 100 个字符）
    - 城市（必填，下拉菜单中包含常见城市）
    - 州/省（必填，下拉菜单）
    - 邮政编码（必填，格式验证）
    - 国家/地区（必填，默认为“美国”）
    
    **验证规则：**
    - 邮政编码必须与所选州匹配
    - 地址第 1 行不能为空
    - 城市必须是所选州中的有效城市
    
    **用户体验：**
    - 地址字段自动完成
    - 清除标签和帮助文本
    - 输入字段适合移动设备
    - 符合无障碍指南

**字段配置提示词：**

    将 @email 字段设为必填项，并添加实时验证和自定义错误消息
    
    为 @country 添加下拉菜单，其中包含美国、加拿大、英国、德国、法国和“其他”选项
    
    将 @phoneNumber 字段配置为 (XXX) XXX-XXXX 格式并添加验证
    
    为 @resume 添加文件上传字段，并限制为最大不超过 5MB 的 PDF 和 DOC

## LLM 增强型智能字段

**何时使用：**&#x200B;当您需要为字段提供利用 AI 知识库进行预填充的选项时。

**如何使用：**&#x200B;要求创建需要全面数据集的字段 - AI 可以使用其内置知识自动填充选项。

### 地理和地点字段

**机场和交通：**

    添加一个包含所有主要国际机场的出发机场下拉菜单
    添加一个包含 IATA 代码和完整名称的到达机场字段
    创建一个距离用户位置最近的机场的字段
    添加一个欧洲城市火车站的选择字段

**行政区域：**

    添加一个包含美国各州及其缩写的完整列表
    创建一个包含 ISO 代码和完整名称的国家/地区下拉菜单
    添加一个包含世界主要城市和时区的字段
    添加一个包含加拿大各省和地区的下拉菜单
    添加一个包含英国各郡和邮政区的字段

### 企业和行业数据

**公司分类：**

    添加一个用 NAICS 代码对行业分类的字段
    创建一个企业实体类型（有限责任公司、公司、合伙企业等）的下拉菜单
    添加一个企业规模类别字段（初创企业、中小型企业、大型企业）
    添加一个大型组织的部门选择
    添加一个专业服务类型的字段

**职业分类：**

    添加一个包含常见行业角色的职位名称字段
    创建一个按领域分类的专业认证的下拉菜单
    添加教育水平和学位类型
    添加一个工作经验年限范围的字段
    创建一个编程语言和框架的选择字段

### 标准和监管

**财务和法律：**

    添加一个包含相应符号和汇率的货币代码字段
    创建一个按国家/地区分类的税号下拉菜单
    添加一个法律文件类型的字段
    添加具有安全功能的支付方法选项
    创建一个按国家/地区分类的银行机构选择字段

**技术标准：**

    添加一个包含文件格式类型和扩展名的下拉菜单
    添加若干个网络协议选项
    添加一个数据库类型和版本的字段
    创建一个 API 身份验证方法的选择字段

### 医疗保健

**医学分类：**

    添加一个医学专科的字段
    创建一个包含常用药物和通用名称的下拉菜单
    添加一个保险提供商类型的字段
    添加一个医疗紧急联系人关系的选择字段
    创建一个饮食限制和过敏的字段

### 时间和日程表智能

**日期和时间字段：**

    添加一个工作时间和时区的字段
    创建一个按国家/地区分类的公共假日的下拉菜单
    添加几个季节性选项和日期范围
    添加一个预订会议室的字段并显示可用情况
    创建一个定期开会模式的选择字段

### 产品和服务类别

**电子商务分类：**

    添加一个产品类别和子类别的字段
    创建一个包含运输方式和预计送达时间的下拉菜单
    添加一个退货策略选项的字段
    添加一个客户优先级的选择
    创建一个订阅计费周期的字段

**智能字段提示词示例：**

    “添加一个出发机场字段，其中包含全球所有主要机场、IATA 代码和城市名称。”
    
    “创建一个全面的行业字段，使用标准 NAICS 分类并包括技术子类别”。
    
    “添加一个能够根据所选职业领域自动调整的专业认证下拉菜单”。
    
    “添加一个根据所选国家/地区显示相应格式的国际电话号码字段”。
    
    “创建一个按国家/地区和排名排列主要院校的大学选择字段”。

## 规则创建和业务逻辑

**何时使用：**&#x200B;当您需要实施条件逻辑、验证规则或业务流程时。

**如何使用：**&#x200B;清晰地描述业务逻辑，指定条件和操作。

**提示词示例 - 简单的条件逻辑：**

    创建一条规则：只在 @maritalStatus 等于“已婚”的情况下显示 @spouseInformation 面板

**提示词示例 - 复杂的业务规则：**

    实施一种全面的贷款申请验证：
    
    **收入验证：**
    - 如果 @annualIncome 小于 30000：
    - 显示警告消息：“收入可能不足以满足所申请的贷款金额的要求”
    - 需要额外的收入证明
    - 显示消息：“可能需要其他文件”
    - 如果 @annualIncome 大于 100000：
    - 显示高级服务选项
    - 启用优先处理复选框
    
    **基于年龄的验证：**
    - 如果 @age 未满 18 岁：
    - 显示父母/监护人信息分区
    - 将上传父母签名设为强制
    - 将提交按钮的文字改为“提交审核”
    - 如果 @age 为 65 岁或以上：
    - 显示老年人折扣选项
    - 添加可访问性偏好设置分区

**规则特定的提示词：**

    创建一个**可见性规则**，只有在 @maritalStatus 等于“已婚”或“同居关系”的情况下才显示 @spouseInformation 面板
    
    添加**渐进展开**方式，根据之前的回答显示附加问题。从基本信息开始，然后显示相关的后续信息
    
    实施**智能默认**，在 @country 选择中自动设置相关字段。允许手动覆盖

## 数据集成与提交

**何时使用：**&#x200B;当您需要将表单连接到后端系统、数据库或外部服务时。

**如何使用：**&#x200B;从基本的提交设置开始，然后逐步添加其他集成。指定集成类型、数据格式要求和错误处理偏好。

**提示词示例 - 从基本提交开始：**

    为 @applicationForm 配置基本的表单提交：
    
    **主要提交：**
    - 将表单数据发送到 REST 端点：`/API/v1/applications`
    - 将数据格式设为 JSON
    - 显示成功消息：“已成功提交申请”
    - 如果提交失败，显示错误消息：“提交失败，请重试”

**然后逐步添加辅助操作：**

    在 @applicationForm 中添加电子邮件通知：向 @email 地址发送确认电子邮件，其中包含申请参考编号
    
    在 @applicationForm 中添加 CRM 集成：创建包含 @firstName、@lastName、@email 的新的潜在客户记录，并将状态设为“新申请”

**提示词示例 - 标准多渠道提交：**

    配置具有多个数据目标的表单提交：
    
    **主要提交：**
    - 将表单数据发送到 REST 端点：`/API/v1/applications`
    - 包含身份验证头部和 API 密钥
    - 将数据设为 JSON 格式，为地址和雇佣信息使用嵌套对象
    - 显示感谢消息，处理成功响应 (201)
    
    **辅助操作：**
    - 向 @email 地址的申请人发送通知电子邮件
    - 将申请数据复制到跟踪系统
    - 触发审批流程的工作流
    - 在 CRM 中创建一条潜在客户状态为“新申请”的记录
    
    **错误处理：**
    - 如果主要提交失败，则在本地保存数据并重试
    - 显示用户友好的错误消息：“提交暂时不可用”
    - 提供下载表单数据作为个人备份的选项
    - 向管理团队发送有关提交失败的警报电子邮件
    
    **成功流程：**
    - 重定向到显示申请参考编号的确认页面
    - 发送包含后续步骤的确认电子邮件
    - 显示预计的处理时间线

**集成特定的提示词：**

    将此表单与**CRM 系统**连接，以创建新的潜在客户。将 @firstName 映射到 FirstName，将 @email 映射到 Email，将 LeadSource 设置为“Web Form”，将 Status 设置为“New”
    
    在提交表单时设置**工作流触发**。传递所有表单数据，并通过经理通知触发审批工作流
    
    配置**数据库集成**，以将表单提交保存为记录。为每个提交创建一个包含上传文件的新文件夹

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## 命令引用

### 基本命令

| 命令 | 最佳用例 | 示例 |
|---------|---------------|---------|
| `/create-form` | 开始构建新表单 | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | 将表单添加到页面 | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | 改变表单结构 | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | 更改字段属性 | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | 添加动态行为 | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | 组织表单部分 | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | 转换设计 | `/add-panel from uploaded form image with field recognition` |
| `/help` | 获取帮助 | `/help how to implement multi-step validation?` |

### 字段引用

使用 `@fieldName` 语法在提示词中引用现有字段：

- `@email` - 引用电子邮件字段
- `@firstName` - 引用名字字段
- `@maritalStatus` - 引用婚姻状况字段

### 组件类型

**输入组件：**

- `text`，`email`，`number`，`tel`，`date`，`checkbox`，`radio`，`dropdown`，`file`，`textarea`

**容器组件：**

- `fieldset`，`panel`，`repeatable`，`wizard`

### 组件属性

**通用属性（所有组件）：**

- **类型**：组件类型
- **名称**：表单提交的字段标识符
- **标签**：显示字段的文本
- **描述**：字段的帮助文本
- **可视**：表示初始可见性的布尔值
- **必填**：表示必填字段的布尔值

**输入字段属性：**

- **值**：默认/初始值
- **占位符**：输入字段的提示文本
- **Min**：最小值（数字/日期）
- **Max**：最大值（数字/日期）

**文件上传属性：**

- **接受**：文件类型（.pdf、.doc、.docx、.jpg、.png 等）
- **Multiple**：用于选择多个文件的布尔值

**选择控制属性：**

- **选项**：下拉菜单的选项（逗号分隔的列表）
- **已选中**：复选框/单选框的默认选择

**容器属性：**

- **Fieldset**：对相关字段进行分组
- **可重复**：可重复部分的布尔值

**高级属性：**

- **可见表达式**：条件可见性的公式（=公式）
- **值表达式**：计算值的公式（=公式）

### 集成命令

**提交操作：**

- 电子邮件通知
- REST API 提交
- 云存储（Azure、SharePoint）
- 工作流自动化（Power Automate、Workfront Fusion）
- 营销平台（Marketo）
- CRM 集成 

### 提示词语法指南

- **字段引用**：使用 `@fieldName` 引用现有字段
- **命令**：使用 `/command` 执行特定操作
- **自然语言**：清晰、具体地描述要求

### 验证清单

如需了解全面的最佳实践和验证指南，请参阅 [Forms Experience Builder 快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

*此提示词库会根据用户反馈和新的 Forms Experience Builder 功能不断更新。如需了解最新功能和示例，请查看 [AEM Forms 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html)。*
