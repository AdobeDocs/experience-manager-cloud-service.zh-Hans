---
title: 如何基于核心组件为自适应表单添加新区域设置支持？
description: 了解如何为自适应表单添加新区域设置。
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
source-git-commit: 7d49be6d4f58078270fb15b10ef34e81dfa790cb
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 3%

---

# 为基于核心组件的自适应表单添加区域设置 {#supporting-new-locales-for-adaptive-forms-localization}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| Foundation 组件  | [单击此处](supporting-new-language-localization.md) |
| 核心组件 | 本文 |

<span class="preview"> 从右至左语言支持功能在早期采用者计划下提供。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

AEM Forms为英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾(zh-TW)和韩语(ko-KR)语言环境提供开箱即用支持。 您还可以添加对更多区域设置的支持，如印地语(hi_IN)。 您还可以通过添加这些区域设置，以从右至左(RTL)语言（如阿拉伯语、波斯语和乌尔都语）展示自适应Forms。

## AEM Forms如何确定自适应表单的区域设置？

了解AEM Forms如何选择用于渲染自适应表单的区域设置对于正确的本地化至关重要。 以下是选择流程的细分：

### 基于优先级的区域设置选择

AEM Forms优先考虑以下方法来确定自适应表单的区域设置：

1. **URL区域设置选择器([区域设置])**：

   系统将使用 [区域设置] 选择器。 此格式允许缓存以获得更好的性能。

   格式： URL遵循以下格式： http:/[AEM Forms服务器URL]/content/forms/af/[afName].[区域设置].html？wcmmode=disabled.

   示例： https://[服务器]/content/forms/af/contact-us.hi.html以印地语呈现表单。


1. **afAcceptLang请求参数**：

   要覆盖用户的浏览器区域设置，您可以使用 `afAcceptLang` 参数。

   示例： https://[服务器]/forms/af/survey.ca-fr.html？afAcceptLang=ca-fr强制表单以加拿大法文呈现。

1. **用户的浏览器区域设置（Accept-Language标题）**：

   如果未指定其他区域设置，则AEM Forms会考虑使用发送的用户浏览器区域设置 `Accept-Language` 标题。


### 回退机制：


* 如果所请求区域设置的客户端库（添加新区域设置的进程，稍后将在本文档中介绍）不可用，则AEM Forms会根据区域设置中的语言代码检查库。

  示例：如果请求了en_ZA（南非英语）并且没有en_ZA库，则它会使用en（英语）（如果可用）。

  如果找不到合适的客户端库，则使用默认词典(通常 `en`)作为表单的创作语言。

  在没有任何区域设置信息的情况下，自适应表单会以开发期间使用的原始语言显示。


## 添加区域设置的先决条件

在开始为自适应Forms添加新区域设置之前，请确保满足以下条件：

**软件：**

* 纯文本编辑器(IDE)：虽然任何纯文本编辑器都可以工作，但集成开发环境(IDE)类似于 [Microsoft Visual Studio代码](https://code.visualstudio.com/download) 提供了高级功能以便于编辑。

* Git：此版本控制系统是管理代码更改所必需的。 如果未安装，请从以下位置下载 [https://git-scm.com](https://git-scm.com).


**代码存储库：**

克隆自适应Forms核心组件存储库：您需要来自此存储库的客户端库来添加区域设置。 要克隆存储库：

1. 打开命令行或终端窗口。

1. 导航到要在计算机上存储存储库的所需位置（例如，/adaptive-forms-core-components）。

1. 运行以下命令以克隆存储库：

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   此命令下载存储库并创建一个名为的文件夹 `aem-core-forms-components` 在你的电脑上。 在本指南中，我们将此文件夹称为 `[Adaptive Forms Core Components repository]`


## 添加区域设置 {#add-localization-support-for-non-supported-locales}

要根据核心组件向自适应表单中添加对新区域设置的支持，请执行以下步骤：

### 克隆AEMas a Cloud Service的Git存储库

1. 打开命令行并选择一个目录来存储AEMas a Cloud Service的存储库，例如 `/cloud-service-repository/`.

1. 运行以下命令以克隆存储库：

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   要克隆Git存储库，您需要以下信息：

   * **组织名称**：用于在Adobe Experience Manager as a Cloud Service (AEMas a Cloud Service)中标识您的团队或项目。

   * **项目ID**：指定与存储库关联的项目。

   * **凭据**：您需要用户名和密码（或个人访问令牌）才能安全访问存储库。

   **在哪里可以找到此信息？**

   有关查找这些详细信息的分步说明，请参阅Adobe Experience League文章»[访问Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)“。

   **您的项目已准备就绪！**

   当命令成功完成时，您会看到在本地目录中创建了一个新文件夹。 此文件夹以您的程序（例如，program-id）命名。 此文件夹包含从AEMas a Cloud ServiceGit存储库下载的所有文件和代码。

   在本指南中，我们将此文件夹称为 `[AEMaaCS project directory]`.


### 将新区域设置添加到指南本地化服务

1. 在编辑器中打开存储库文件夹。

   ![编辑器中的存储库文件夹](/help/forms/assets/repository-folder-in-an-editor.png)

1. 找到 `Guide Localization Service.cfg.json` 文件。 此文件可控制AEM Forms应用程序支持的区域设置。 您可以编辑此文件以添加新区域设置。

   * **现有文件**：如果文件已存在，请在AEM Forms项目目录中找到它。 典型位置为：

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     替换 `<appid>` 特定项目应用程序ID对应的字段。 您可以找到 `<appid>` 中的AEM项目 `archetype.properties` 文件。

     ![原型属性](/help/forms/assets/archetype-properties.png)

   * **新建文件**：如果文件不存在，则需要在上面提到的相同位置创建该文件。 请勿从此文档复制粘贴文件的名称，而是手动键入名称。 文件名 `Guide Localization Service.cfg.json` 包含空格。 这是有意为之，而不是文档中的打字错误。

     包含OOTB支持的区域设置列表的示例文件为：

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. 将所需语言的区域设置代码添加到文件中。
   1. 使用 [ISO 639-1代码列表](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) 以查找表示所需语言的双字母代码。

   1. 将区域设置代码包含到 `Guide Localization Service.cfg.json` 文件。 以下是一些示例：

      * 从左至右语言：
         * 英语（美国）：en-US
         * 西班牙语（西班牙）：es-ES
         * 法语（法国）：fr-FR
      * 从右至左语言：
         * 阿拉伯语（阿拉伯联合酋长国）： ar-ae
         * 希伯来语：he（或iw，供历史参考）
         * 波斯语： fa

1. 进行更改后，确保 `Guide Localization Service.cfg.json` 文件格式正确，为有效的JSON文件。 JSON格式中的错误会妨碍其正常运行。 保存文件。



### 利用示例客户端库轻松添加区域设置

AEM Forms提供了一个有用的示例客户端库， `clientlib-it-custom-locale`，以简化添加新区域设置。 此库是 [自适应Forms核心组件存储库](https://github.com/adobe/aem-core-forms-components)，可在GitHub上找到。


在开始之前，请确保您拥有 [自适应Forms核心组件存储库]. 如果不能，则可以使用以下命令通过Git轻松克隆它：

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

此命令可将整个存储库（包括clientlib-it-custom-locale库）下载到计算机上名为aem-core-forms-components的目录。

![本地计算机上的Adaptive Forms核心组件存储库目录](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### 集成示例客户端库

现在，让我们整合 `clientlib-it-custom-locale` 将库保存到您的AEMas a Cloud Service中， [AEMaaCS项目目录]：

1. 找到示例客户端库：

   在您的本地副本中 [自适应Forms核心组件存储库]，导航到以下路径：

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. 复制并粘贴库：

   1. 复制 `clientlib-it-custom-locale` 文件夹。

      ![复制clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. 导航到 [AEMaaCS项目目录]：

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **重要**：替换 `<app-id>` 以及应用程序的实际ID。

   1. 粘贴复制的 `clientlib-it-custom-locale` 文件夹放入此目录中。

      ![粘贴clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)


### 为您的新区域设置创建一个文件：

1. 导航到区域设置目录：

   在您的 `[AEMaaCS project directory]`，导航到以下路径：

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **重要**：替换 `<program-id>` 以及实际的应用程序ID。

1. 找到示例英语文件：

   AEM Forms提供 [GitHub上的示例英语区域设置文件(.json)](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   英语文件包含默认字符串集以供参考。 区域设置特定的文件应模拟英语文件的结构。

   对于阿拉伯语、希伯来语和波斯语等语言，文本从右至左(RTL)而不是从左至右(LTR)像英语一样阅读。 为确保您的表单在这些语言中正确显示，我们建议使用示例区域设置文件作为指南。 这些文件就如何设置RTL语言的文本、日期和其他元素的格式提供了参考。 您可以找到以下示例区域设置文件：

   * [阿拉伯语](/help/forms/assets/ar-ae.json)
   * [希伯来语](/help/forms/assets/he.json)
   * [波斯语](/help/forms/assets/fa.json)

   利用这些样例文件，您可以确保表单为使用RTL语言的用户提供无缝体验。


1. 创建区域设置文件：

   1. 在中创建新的.json文件 `i18n` 目录。
   1. 使用适用于所需语言的相应区域设置代码命名文件（例如，法语为fr-FR.json，阿拉伯语为ar-ae.json）。 此文件的结构应镜像英文区域设置文件。


1. 结构和翻译：

   1. 在文本编辑器中打开新创建的文件。

   1. 将英语值替换为目标语言的相应翻译。

   1. 翻译完字符串后，保存文件。




### 向字典添加区域设置支持

此步骤仅适用于除以下常用支持的区域设置之外的其他区域设置：英语(en)、德语(de)、西班牙语(es)、法语(fr)、意大利语(it)、巴西葡萄牙语(pt-br)、中文（简体 — zh_cn）、中文（繁体 — zh_tw）、日语(ja)和韩语(ko_kr)。

1. 找到配置文件夹：

   导航到 [AEMaaCS项目目录]：

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. 创建必要的文件夹（如果缺少）：

   如果 `etc` 文件夹不存在于 `jcr_root` 创建文件夹。 内部 `etc`，创建另一个名为 `languages` 如果它不见了。

1. 创建区域设置配置文件：

   在 `languages` 文件夹，新建一个名为的文件 `.content.xml`. 请勿从此文档复制粘贴文件的名称，而是手动键入名称。

   ![创建新文件，名为 `.content.xml`](etc-content-xml.png)

   打开此文件并粘贴以下内容，替换 [LOCALE_CODE] 实际区域设置代码（例如，阿拉伯语的ar-ae）。


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   警告：不要替换现有列表。 请改为将新的区域设置代码附加到方括号中，并用逗号分隔，如下所示（以ar-ae为例）：

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. 在filter.xml中包含新文件夹：

   导航至 `/ui.content/src/main/content/meta-inf/vault/filter.xml` 文件中的文件 [AEMaaCS项目目录].

   打开文件，并在末尾添加以下行：

   ```
   <filter root="/etc/languages"/>
   ```

   ![将创建的文件夹添加到 `filter.xml` 下 `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. 保存文件。

### 将新创建的区域设置部署到您的AEM环境

现在，您均设置为在自适应Forms中使用新的区域设置。 您可以

* 部署AEMas a Cloud Service， [AEMaaCS项目目录]，以在本地计算机上尝试新的区域设置配置。 要部署到本地开发环境，请执行以下操作：

   1. 确保您的本地开发环境已启动并正在运行。 如果您尚未设置本地开发环境，请参阅上的指南 [为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md).

   1. 打开终端窗口或命令提示符。

   1. 导航至 [AEMaaCS项目目录]

   1. 运行以下命令：

      ```
      mvn -PautoInstallPackage clean install
      ```

* 部署AEMas a Cloud Service， [AEMaaCS项目目录]，添加到您的Cloud Service环境。 要部署到Cloud Service环境，请执行以下操作：

   1. 提交更改：

      添加新的区域设置配置后，提交更改，并显示描述区域设置添加的清晰Git消息(例如，“添加支持 [区域设置名称]“)。

   1. 部署更新的代码：

      通过以下方式触发代码部署 [现有全栈管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline). 这会使用新的区域设置支持自动构建和部署更新的代码。

      如果尚未设置管道，请参阅上的指南 [如何设置AEM Formsas a Cloud Service的管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).


## 预览具有新添加区域设置的自适应表单

以下步骤将指导您预览具有新添加区域设置的自适应表单：

1. 登录到您的AEM Formsas a Cloud Service实例。
1. 转到 **Forms** >  **Forms和文档**.
1. 选择自适应表单并单击 **添加字典** 和 **将字典添加到翻译项目** 出现向导。
1. 指定 **项目标题** 并选择 **目标语言** 从 **将字典添加到翻译项目** 向导。
1. 单击 **完成** 并执行创建的翻译项目。
1. 转到 **Forms** >  **Forms和文档**.
1. 选择自适应表单，然后选择 **HTML预览** 选项。
1. 附加 `&afAcceptLang=<locale-name>` 到预览URL并按return键。 替换 `<locale-name>` 实际区域设置代码。 自适应表单会以指定的区域设置显示。

## 支持新本地化的最佳实践 {#best-practices}

* Adobe建议在创建自适应表单之后创建翻译项目。 这简化了本地化过程。
* 将数值框和日期选取器组件转换为特定区域设置时，可能会出现格式问题。 要缓解此问题，请 **语言** 选项已纳入的“配置”对话框中 [日期选取器组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab) 和 [数值框组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab).


* 处理新字段：

   * **机器翻译**：如果使用机器翻译，则需要重新创建词典并重新[运行翻译项目](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) 将新字段添加到现有自适应表单后。 在初始翻译项目后添加的新字段保持未翻译状态。

   * **人工翻译**：对于人工翻译工作流，请使用位于的UI导出字典 `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. 更新新字段的词典并上传修订版本。


## 另请参阅 {#see-also}

{{see-also}}

* [为自适应Forms生成记录文档](/help/forms/generate-document-of-record-core-components.md)
* [将自适应表单添加到 AEM Sites 页面或体验片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

