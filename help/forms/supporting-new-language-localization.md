---
title: 支持自适应表单本地化的新区域设置
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms允许您为本地化自适应表单添加新区域设置。 英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾语(zh-TW)和韩语(ko-KR)区域设置。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: f8bbc6605e77cf2858c69dae96e9ab32698d1f16
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---

# 支持自适应Forms本地化的新区域设置{#supporting-new-locales-for-adaptive-forms-localization}

## 关于区域设置字典 {#about-locale-dictionaries}

自适应表单的本地化依赖于两种类型的区域设置字典：

* **表单特定词典** 包含自适应表单中使用的字符串。 例如，标签、字段名称、错误消息、帮助描述等。 它将作为每个区域设置的一组XLIFF文件进行管理，您可以在 `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **全局字典** AEM客户端库中有两个全局字典，管理为JSON对象。 这些字典包含默认错误消息、月名、货币符号、日期和时间模式等。 这些字典在 `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. 这些位置包含每个区域设置的单独文件夹。 由于全局字典不经常更新，因此为每个区域设置保留单独的JavaScript文件可使浏览器在访问同一服务器上的不同自适应表单时缓存它们并减少网络带宽使用。

支持AEM Forms新本地化的步骤：

1. [为不支持的区域设置添加本地化支持](#add-localization-support-for-non-supported-locales-add-localization-support-for-non-supported-locales)
1. [在自适应Forms中使用添加的区域设置](#use-added-locale-in-adaptive-forms-use-added-locale-in-af)

## 为不支持的区域设置添加本地化支持 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支持以英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中国 — 台湾语(zh-TW)和韩语(ko-KR)区域设置本地化自适应Forms内容。

要在自适应Forms运行时添加对新区域设置的支持，请执行以下操作：

1. [克隆存储库](#1-clone-the-repository-clone-the-repository)
1. [向GuideLocalizationService服务添加区域设置](#1-add-a-locale-to-the-guide-localization-service-add-a-locale-to-the-guide-localization-service-br)
1. [添加区域设置名称特定的文件夹](#3-add-locale-name-specific-folder-add-locale-name-specific-folder)
1. [为区域设置添加XFA客户端库](#3-add-xfa-client-library-for-a-locale)
1. [为区域设置添加自适应表单客户端库](#4-add-adaptive-form-client-library-for-a-locale-add-adaptive-form-client-library-for-a-locale-br)
1. [为词典添加区域设置支持](#5-add-locale-support-for-the-dictionary-add-locale-support-for-the-dictionary-br)
1. [提交存储库中的更改并部署管道](#7-commit-the-changes-in-the-repository-and-deploy-the-pipeline-commit-changes-in-repo-deploy-pipeline)

### 1.克隆存储库 {#clone-the-repository}

1. 在命令行中，导航到要克隆FormsCloud Service存储库的位置。
1. 执行您的 [从Cloud Manager中检索。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) 它类似于 `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. 使用git用户名和密码克隆存储库。
1. 在首选编辑器中打开克隆的FormsCloud Service存储库文件夹。

### 2.向指南本地化服务添加区域设置 {#add-a-locale-to-the-guide-localization-service-br}

1. 找到 `Guide Localization Service.cfg.json` 文件，并将要添加的区域设置添加到支持的区域设置列表中。

   >[!NOTE]
   >
   >* 创建名为的文件 `Guide Localization Service.cfg.json` 文件（如果尚不存在）。


### 3.添加区域名称特定的文件夹客户端库 {#add-locale-name-specific-folder}

1. 在UI.content文件夹中，创建 `etc/clientlibs` 文件夹。
1. 进一步创建名为的文件夹 `locale-name` 在 `etc/clientlibs` 用作xfa和af clientlibs的容器。

#### 3.1为locale-name文件夹中的区域设置添加XFA客户端库

1. 创建名为的节点 `[locale-name]_xfa` 并键入作为 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，类别 `xfaforms.I18N.<locale>`，并添加以下文件：
* **I18N.js** 定义 `xfalib.locale.Strings` 对于 `<locale>` 定义 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt** 包含以下内容：
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

#### 3.2.为区域设置名称文件夹添加自适应表单客户端库 {#add-adaptive-form-client-library-for-a-locale-br}

1. 创建名为的节点 `[locale-name]_af` 并键入作为 `cq:ClientLibraryFolder` 在 `etc/clientlibs/locale_name`，类别为 `guides.I18N.<locale>` 和依赖关系 `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` 和 `guide.common`.
1. 创建名为的文件夹 `javascript` 并添加以下文件：

   * **i18n.js** 定义 `guidelib.i18n`，具有“calendarSymbols”模式， `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` 对于 `<locale>` 根据 [区域设置规范](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js** 定义 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` 对于 `<locale>` 定义 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. 添加 **js.txt** 包含以下内容：

   ```text
     i18n.js
       LogMessages.js
   ```

### 4.为词典添加区域设置支持 {#add-locale-support-for-the-dictionary-br}

仅当 `<locale>` 您添加的不在 `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. 创建文件夹 `languages` 在 `etc`，如果尚不存在。

1. 添加多值字符串属性 `languages` 到节点（如果尚不存在）。
1. 添加 `<locale-name>` 默认区域设置值 `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`，如果尚不存在。

1. 添加 `<locale>` 的值 `languages` 财产 `/etc/languages`.


```text
Add the newly created folders in the `filter.xml` under etc/META-INF/[folder hierarchy] as:
<filter root="/etc/clientlibs/[locale-name]"/>
<filter root="/etc/languages"/>
```

在将更改提交到AEM Git存储库之前，您需要访问 [Git存储库信息](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

### 5.提交存储库中的更改并部署管道 {#commit-chnages-in-repo-deploy-pipeline}

添加新的区域设置支持后，将更改提交到GIT存储库。 使用完整堆栈管道部署代码。 学习 [如何设置管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) 添加新的区域设置支持。

管道完成后，新添加的区域设置将显示在AEM环境中。

### 在自适应Forms中使用添加的区域设置 {#use-added-locale-in-af}

使用新添加的区域设置来使用和渲染自适应表单的步骤：

1. 登录到您的AEM创作实例。
1. 转到 **Forms** >  **Forms和文档**.
1. 选择自适应表单并单击 **添加字典** 和 **将字典添加到翻译项目** 向导。
1. 指定 **项目标题** ，然后选择 **目标语言** 下拉菜单(位于 **将字典添加到翻译项目** 向导。
1. 单击 **完成** 并执行创建的翻译项目。
1. 选择自适应表单并单击 **预览为HTML**.
1. 添加 `&afAcceptLang=<locale-name>` 在自适应表单的URL中。
1. 刷新页面，并以指定的区域设置呈现自适应表单。

有两种方法可识别自适应表单的区域设置。 呈现自适应表单后，它会通过标识所请求的区域设置：

* 看 `[local]` 自适应表单URL中的选择器。 URL的格式为 `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. 使用 `[local]` 选择器允许缓存自适应表单。

* 按指定顺序查看以下参数：

   * 请求参数 `afAcceptLang`
要覆盖用户的浏览器区域设置，您可以通过 
`afAcceptLang` 请求参数强制设置区域。 例如，以下URL会强制在加拿大 — 法语区域设置中渲染表单：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * 为用户设置的浏览器区域设置，该区域设置在请求中使用 `Accept-Language` 标题。

如果所请求区域设置的客户端库不存在，则它会检查客户端库是否存在区域设置中存在的语言代码。 例如，如果请求的区域设置为 `en_ZA` （南非英语）和 `en_ZA` 不存在，自适应表单会使用 `en` （英语）语言（如果存在）。 但是，如果这些表单都不存在，则自适应表单会将字典用于 `en` 区域设置。


识别区域设置后，自适应表单会选取特定于表单的词典。 如果找不到所请求区域设置的特定于表单的词典，则该词典会使用该词典来编写自适应表单的语言。

如果没有区域设置信息，则以表单的原始语言提交自适应表单。 原始语言是开发自适应表单时使用的语言。

获取 [示例客户端库](/help/forms/assets/locale-support-sample.zip) 添加对新区域设置的支持。 您需要在所需的区域设置中更改文件夹的内容。

### 支持新本地化的最佳实践 {#best-practices}

* Adobe建议在创建自适应表单后创建翻译项目。

* 在现有自适应表单中添加新字段时：
   * **用于机器翻译**:重新创建字典并运行翻译项目。 创建翻译项目后添加到自适应表单的字段仍保持未翻译状态。
   * **用于人类翻译**:通过导出字典 `[server:port]/libs/cq/i18n/gui/translator.html`. 更新新添加字段的字典并上传它。
