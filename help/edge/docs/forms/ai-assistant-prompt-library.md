---
title: Forms Experience Builder — 提示库
description: 收集经过验证的提示词模式和示例，用于在表单管理用户界面、自适应表单编辑器和通用编辑器中使用 AI 辅助构建表单。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---


# Forms Experience Builder — 提示库

可重用提示模式的收藏集和针对Forms Experience Builder优化的示例。 这个简化的库重点关注两种核心创建方法：从头开始创建以及导入和转换，并增强对LLM支持的智能字段和品牌一致性的支持。

>[!NOTE]
>
> Forms Experience Builder在率先采用者计划下提供。 将工作地址中的电子邮件发送至`aem-forms-ea@adobe.com`以请求访问权限。

>[!IMPORTANT]
>
> **文档可能会发生变化**：此提示词库目前正在针对产品进行测试，因此可能会进行更新和修订。随着Forms Experience Builder在率先采用者计划中的不断演变，提示、示例和最佳实践可能会发生变化。

## 使用此提示库

此库为常见的表单构建方案提供了可重用的提示模式。 有关全面的最佳实践，请参阅[Forms Experience Builder快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

### 此库的快速提示

- **以示例开始** — 将提供的提示用作模板并适应您的需求
- **两种创建方法** — 选择“从头开始创建”或“导入并转换”方法
- **具体说明** — 将您自己的详细信息添加到常规示例
- **彻底测试** — 始终验证您特定环境中的结果

### 品牌模板和样式

**提前准备品牌资产以创建一致的表单：**

- **品牌模板** — 使用您组织的颜色、字体和布局模式创建标准化表单模板
- **样式准则** — 定义一致的字段样式、按钮设计和间距标准
- **组件库** — 生成与您的品牌标识匹配的可重用表单组件
- **可视化Assets** — 为表单集成准备徽标、图标和背景元素

**示例品牌模板提示：**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**自定义组件**：在实施自定义品牌元素之前，请与您的开发团队联系，了解如何使用特定于组织的组件及其与Forms Experience Builder的兼容性。

>[!NOTE]
>
> 此提示库已更新，以反映简化的Forms Experience Builder功能。 示例中显示的某些高级集成和测试功能可能需要额外的配置。



## 逐步开发示例

这些示例展示了如何逐步构建表单，从简单开始，逐渐增加复杂性：

### 示例 1：逐步构建一个联系表单

**步骤 1 - 从简单开始：**

```
Create a basic contact form with name, email, and message fields
```

**步骤 2 - 添加验证：**

```
Make @name and @email mandatory fields with appropriate validation
```

**步骤 3 - 增强用户体验**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**步骤 4 - 添加高级功能：**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**步骤 5 - 实施条件逻辑：**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### 示例 2：逐步构建一个注册表单

**步骤 1- 基本结构：**

```
Create a user registration form with personal information panel
```

**第2步 — 添加必填字段：**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**步骤3 — 添加业务逻辑：**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**步骤4 — 使用首选项进行增强：**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**步骤5 — 添加文件上传：**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## 表单创建和管理

**何时使用：**&#x200B;需要创建新表单或修改现有表单时。

**使用方法：**&#x200B;从头开始创建或导入并转换（请参阅[入门指南](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)）。

**示例提示 — 简单表单创建：**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**示例提示 — 复杂表单创建：**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**表单管理提示：**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## 字段管理和配置

**何时使用：**&#x200B;需要添加、修改或配置表单字段时。

**使用方法：**&#x200B;具体说明字段类型、验证规则和用户体验要求。

**示例提示 — 基本字段添加：**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**示例提示 — 高级字段配置：**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**字段配置提示：**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## LLM增强型智能字段

**何时使用：**&#x200B;您需要具有预填充选项的字段时，这些选项将利用AI知识库。

**如何使用：**&#x200B;请求需要全面数据集的字段 — AI可以使用其内置知识自动填充选项。

### 地理和位置字段

**机场和运输：**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**管理区域：**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### 商业和行业数据

**公司分类：**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**专业分类：**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### 标准和法规

**财务和法律信息：**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**技术标准：**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### 医疗保健业

**医疗分类：**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### 时间和日历智能

**日期和时间字段：**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### 产品和服务类别

**电子商务分类：**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**智能字段提示示例：**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## 规则创建和业务逻辑

**何时使用：**&#x200B;需要实施条件逻辑、验证规则或业务流程时。

**使用方式：**&#x200B;明确描述业务逻辑，指定条件和操作。

**示例提示 — 简单条件逻辑：**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**示例提示 — 复杂业务规则：**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**规则特定的提示词：**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
```

## 数据集成与提交

**何时使用：**&#x200B;当您需要将表单连接到后端系统、数据库或外部服务时。

**如何使用：**&#x200B;从基本的提交设置开始，然后逐步添加其他集成。指定集成类型、数据格式要求和错误处理偏好。

**提示词示例 - 从基本提交开始：**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**然后逐步添加次要操作：**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**示例提示 — 标准多渠道提交：**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**集成特定的提示词：**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## 导入和转换现有Forms

**何时使用：**&#x200B;当已有表单、文档或设计可转换为现代AEM表单时。

**如何使用：**&#x200B;上载您的源文件并描述转换要求（请参阅[导入指南](forms-ai-assistant-getting-started.md#2-import-and-convert)）。

**提示词示例 - PDF 表单转化：**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**设计导入提示词：**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
```

## 移动端优化与响应能力

**何时使用：**&#x200B;当表单需要在所有设备类型和屏幕尺寸上无缝工作时。

**如何使用：**&#x200B;从基本的移动端优化开始，然后通过高级功能将其增强。强调移动端优先的方法，逐步指定断点行为。

**提示词示例 - 从基本的移动端优化开始：**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**然后添加高级移动端功能：**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**提示词示例 - 全面的移动端优先优化：**

```
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
```

**特定于移动设备的提示：**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## 无障碍访问和合规性

**何时使用：**&#x200B;当表单需要满足辅助功能标准(WCAG)或合规性要求时。

**使用方式：**&#x200B;指定所需的合规性级别以及所需的任何特定辅助功能。

**示例提示 — 基本辅助功能：**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**示例提示 — 高级辅助功能：**

```
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
```

**特定于辅助功能的提示：**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## 性能优化

**何时使用：**&#x200B;当表单需要快速加载并在各种条件下运行良好时。

**如何使用：**&#x200B;指定性能要求和优化策略。

**示例提示 — 基本性能：**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**示例提示 — 高级性能：**

```
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
```

**特定于性能的提示：**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## 测试和质量保证

**何时使用：**&#x200B;当表单需要全面测试以确保可靠性和用户满意度时。

**如何使用：**&#x200B;指定测试方案、验证要求和质量量度。

**示例提示 — 基本测试：**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**示例提示 — 高级测试：**

```
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
```

**测试特定的提示词：**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## 疑难解答

Forms Experience Builder常见问题的快速解决方案：

| 问题 | 快速修复 |
|-------|-----------|
| 表单未提交 | 检查提交操作配置和验证规则 |
| 未显示验证错误 | 验证字段验证设置和错误消息放置 |
| 移动布局问题 | 查看响应式设计设置和字段大小 |
| 未显示字段 | 检查条件逻辑和可见性规则 |
| 导入失败 | 验证文件格式兼容性和大小限制 |
| 集成错误 | 验证API端点和身份验证凭据 |
| 性能问题 | 优化字段计数并删除不必要的验证 |
| 辅助功能问题 | 审查字段标签、ARIA属性和选项卡顺序 |

**调试模式提示：**

```
Enable debug mode to identify issues with form submission and field validation
```

**错误分析提示：**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## 高级分析和见解

**使用时间：**&#x200B;需要了解表单性能和用户行为时。

**如何使用：**&#x200B;指定所需的分析要求和见解。

**示例提示 — 基本分析：**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**示例提示 — 高级分析：**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**特定于Analytics的提示：**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## 安全性与数据保护

**何时使用：**&#x200B;当表单处理敏感数据并需要安全措施时。

**如何使用：**&#x200B;指定安全要求和数据保护措施。

**示例提示 — 基本安全性：**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**示例提示 — 高级安全性：**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**特定于安全性的提示：**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

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
| `/configure-submit` | 设置数据处理 | `/configure-submit to CRM and send confirmation email` |
| `/help` | 获取帮助 | `/help how to implement multi-step validation?` |

### 字段引用

使用`@fieldName`语法引用提示中的现有字段：

- `@email` — 引用电子邮件字段
- `@firstName` — 引用名字字段
- `@maritalStatus` — 参考婚姻状况字段

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

**文件上载属性：**

- **接受**：文件类型（.pdf、.doc、.docx、.jpg、.png 等）
- **Multiple**：用于选择多个文件的布尔值

**选择控件属性：**

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
- REST API提交
- 云存储(Azure、SharePoint)
- 工作流自动化(Power Automate、Workfront Fusion)
- 营销平台(Marketo)
- CRM集成

### 提示语法准则

- **字段引用**：将`@fieldName`用于现有字段
- **命令**：将`/command`用于特定操作
- **自然语言**：清晰明确地描述要求

### 验证核对清单

有关全面的最佳实践和验证准则，请参阅[Forms Experience Builder快速入门指南](forms-ai-assistant-getting-started.md#best-practices)。

*此提示库会根据用户反馈和新的Forms Experience Builder功能不断更新。 如需了解最新功能和示例，请查看 [AEM Forms 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html)。*
