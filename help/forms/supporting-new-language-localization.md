---
title: 如何为基于基础组件的自适应表单添加新区域设置支持？
description: 对于自适应Forms，除了现成可用的语言之外，您还可以为更多语言添加区域设置。
feature: Adaptive Forms, Foundation Components
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 3%

---

# 支持自适应Forms本地化的新区域设置 {#supporting-new-locales-for-adaptive-forms-localization}

>[!NOTE]
>
> Adobe建议为[创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md)或[将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)使用现代的、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)。 这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html) |
| 核心组件 | [单击此处](supporting-new-language-localization-core-components.md) |
| Foundation 组件  | 本文 |

AEM Forms为英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾(zh-TW)和韩语(ko-KR)语言环境提供开箱即用支持。 您还可以添加对更多区域设置的支持，如印地语(hi_IN)。

## 了解区域设置词典 {#about-locale-dictionaries}

自适应表单的本地化依赖于两种类型的区域设置词典：

* **表单特定词典**&#x200B;包含自适应表单中使用的字符串。 例如，标签、字段名称、错误消息、帮助说明。 它作为每个区域设置的一组XLIFF文件进行管理，您可以在`[author-instance]/libs/cq/i18n/gui/translator.html`处访问它。

* **全局词典** AEM客户端库中有两个作为JSON对象管理的全局词典。 这些词典包含默认错误消息、月份名称、货币符号、日期和时间模式等。 您可以在`[author-instance]/libs/fd/xfaforms/clientlibs/I18N`找到这些词典。 这些位置包含每个区域设置的单独文件夹。 由于全局字典不经常更新，因此对于每种区域设置保留单独的JavaScript文件使浏览器能够在同一服务器上访问不同的自适应表单时缓存这些文件并降低网络带宽使用率。

## 添加对新区域设置的支持 {#add-support-for-new-locales}

执行以下步骤来添加对新区域设置的支持：

1. [为不受支持的区域设置添加本地化支持](#add-localization-support-for-non-supported-locales)
1. [在自适应Forms中使用添加的区域设置](#use-added-locale-in-af)

### 为不受支持的区域设置添加本地化支持 {#add-localization-support-for-non-supported-locales}

AEM Forms当前支持英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾(zh-TW)和韩语(ko-KR)本地化自适应Forms内容。

要在自适应Forms运行时添加新区域设置支持，请执行以下操作：

1. [克隆存储库](#clone-the-repository)
1. [向GuideLocalizationService服务添加区域设置](#add-a-locale-to-the-guide-localization-service)
1. [添加区域设置名称特定的文件夹](#add-locale-name-specific-folder)
1. [为字典添加区域设置支持](#add-locale-support-for-the-dictionary)
1. [在存储库中提交更改并部署管道](#commit-changes-in-repo-deploy-pipeline)

#### 1.克隆存储库 {#clone-the-repository}

1. 在命令行中，导航到要克隆FormsCloud Service存储库的位置。
1. 执行[从Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)检索到的命令。 它类似于`git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`。
1. 使用Git用户名和密码克隆存储库。
1. 在首选编辑器中打开克隆的FormsCloud Service存储库文件夹。

#### 2.向指南本地化服务添加区域设置 {#add-a-locale-to-the-guide-localization-service}

1. 找到`Guide Localization Service.cfg.json`文件并将要添加的区域设置添加到支持的区域设置列表中。

   >[!NOTE]
   >
   > 创建名为`Guide Localization Service.cfg.json`文件的文件（如果尚未存在）。

#### 3.添加特定于区域设置名称的文件夹客户端库 {#add-locale-name-specific-folder}

1. 在UI.content文件夹中，创建`etc/clientlibs`文件夹。
1. 在`etc/clientlibs`下进一步创建一个名为`locale-name`的文件夹以用作xfa和af clientlibs的容器。

##### 3.1在区域设置名称文件夹中添加区域设置的XFA客户端库

使用类别`xfaforms.I18N.<locale>`在`etc/clientlibs/locale_name`下创建名为`[locale-name]_xfa`且类型为`cq:ClientLibraryFolder`的节点，并添加以下文件：

* **I18N.js**&#x200B;定义了`/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`中定义的`<locale>`的`xfalib.locale.Strings`。
* **js.txt**&#x200B;包含以下内容：
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2.为区域设置名称文件夹添加自适应表单客户端库

1. 在`etc/clientlibs/locale_name`下创建名为`[locale-name]_af`且类型为`cq:ClientLibraryFolder`的节点，类别为`guides.I18N.<locale>`，依赖项为`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。
1. 创建名为`javascript`的文件夹并添加以下文件：

   * **i18n.js**&#x200B;定义`guidelib.i18n`，根据[区域设置集规范](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)中描述的XFA规范，其模式为`<locale>`的“calendarSymbols”、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`和`typefaces`。
   * **LogMessages.js**&#x200B;定义了`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`中定义的`<locale>`的`guidelib.i18n.strings`和`guidelib.i18n.LogMessages`。

1. 添加包含以下内容的&#x200B;**js.txt**：

   ```
     i18n.js
     LogMessages.js
   ```

#### 4.为字典添加区域设置支持 {#add-locale-support-for-the-dictionary}

仅当要添加的`<locale>`不属于`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`时才执行此步骤。

1. 在`etc`下创建文件夹`languages`（如果尚未存在）。

1. 将多值字符串属性`languages`添加到节点（如果尚不存在）。
1. 添加`<locale-name>`默认区域设置值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`（如果尚未存在）。

1. 将`<locale>`添加到`/etc/languages`的`languages`属性的值。
1. 在`filter.xml`中etc/META-INF/[文件夹层次结构]下添加已创建的文件夹，如下所示：

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

在将更改提交到AEM Git存储库之前，您需要访问[Git存储库信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git)。

#### 5.在存储库中提交更改并部署管道 {#commit-changes-in-repo-deploy-pipeline}

添加区域设置支持后，将更改提交到GIT存储库。 使用全栈管道部署代码。 了解[如何设置管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)以添加新的区域设置支持。
管道完成后，新添加的区域设置将显示在AEM环境中。

### 在自适应Forms中使用添加的区域设置 {#use-added-locale-in-af}

执行以下步骤以使用新添加的区域设置来使用和渲染自适应表单：

1. 登录到您的AEM创作实例。
1. 转到&#x200B;**Forms** > **Forms和文档**。
1. 选择一个自适应表单，然后单击&#x200B;**添加词典**&#x200B;和&#x200B;**将词典添加到翻译项目**&#x200B;向导。
1. 指定&#x200B;**项目标题**&#x200B;并从&#x200B;**将字典添加到翻译项目**&#x200B;向导的下拉菜单中选择&#x200B;**目标语言**。
1. 单击&#x200B;**完成**&#x200B;并执行已创建的翻译项目。
1. 选择自适应表单并单击&#x200B;**作为HTML预览**。
1. 在自适应表单的URL中添加`&afAcceptLang=<locale-name>`。
1. 刷新页面，自适应表单在指定的区域设置中呈现。

可以使用两种方法识别自适应表单的区域设置。 呈现自适应表单时，它通过以下方式标识请求的区域设置：

* 正在检索自适应表单URL中的`[local]`选择器。 URL 的格式为 `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`。使用`[local]`选择器允许缓存自适应表单。

* 正在按列出的顺序检索以下参数：

   * 请求参数`afAcceptLang`
要覆盖用户的浏览器区域设置，您可以传递`afAcceptLang`请求参数以强制实施区域设置。 例如，以下URL强制以加拿大 — 法语区域设置呈现表单：
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 使用`Accept-Language`标头在请求中指定的用户的浏览器区域设置。

如果所请求区域设置的客户端库不存在，它将检查客户端库是否存在区域设置中存在的语言代码。 例如，如果所请求的区域设置为`en_ZA` （南非英语）并且`en_ZA`的客户端库不存在，则自适应表单将使用`en` （英语）语言的客户端库（如果存在）。 但是，如果这些字典都不存在，则自适应表单会使用`en`区域设置的字典。


标识区域设置后，自适应表单会选取特定于表单的词典。 如果未找到所请求区域设置的表单特定词典，则它会使用用于创作自适应表单的语言的词典。

如果未提供区域设置信息，则自适应表单将采用表单的原始语言交付。 原始语言是开发自适应表单时使用的语言。

获取[示例客户端库](/help/forms/assets/locale-support-sample.zip)以添加对新区域设置的支持。 您需要以所需的区域设置更改文件夹的内容。

## 支持新本地化的最佳实践 {#best-practices}

* Adobe建议在创建自适应表单之后创建翻译项目。

* 在现有自适应表单中添加新字段时：
   * **对于机器翻译**：重新创建词典并运行翻译项目。 创建翻译项目后添加到自适应表单的字段保持未翻译状态。
   * **对于人工翻译**：通过`[server:port]/libs/cq/i18n/gui/translator.html`导出词典。 更新新添加字段的字典并上传。


## 另请参阅 {#see-also}

{{see-also}}