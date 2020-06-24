---
title: Adobe Experience Manager保护和数据隐私法规——作为Cloud Service站点就绪性
description: '了解Adobe Experience Manager作为Cloud Service站点对各种数据保护和数据隐私法规的支持； 包括欧盟一般数据保护规定(GDPR)、加利福尼亚消费者隐私法，以及在将新AEM作为Cloud Service项目实施时如何遵守这些规定。 '
translation-type: tm+mt
source-git-commit: bffc335fdafe6bf12a66bcd2f7aacf029fce567e
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# Adobe Experience Manager作为Cloud Service站点，为数据保护和数据隐私法规做好准备 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律咨询，不能代替法律咨询。
>
>请咨询您的公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私权问题的回应，以及这对您作为Adobe客户意味着什么的更多信息，请 [参阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

Adobe Experience Manager作为Cloud Service站点，可以帮助客户履行其数据隐私和保护合规义务。 本页将指导客户完成在AEM Sites中处理此类请求的过程。 它描述了存储的私有数据的位置，以及如何手动或使用代码删除这些数据。

有关详细信息，请参 [阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>有关 [更多详细信息，请参阅Adobe Experience Manager作为Cloud Service就绪性数据保护和数据隐私](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) 法规。

## AEM 创作层 {#aem-author-tier}

AEM Foundation文档中介绍了作者服务器上的用户帐 [户和UGC内容](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

## AEM 发布层 {#aem-publish-tier}

AEM Foundation文档中介绍用于验证站点上访客和发布服务器上UGC内 [容的用户帐户](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

默认情况下，AEM Sites组件不存储访客在发布服务器上输入的表单数据。 建议将数据转发给第三方系统或Adobe Campaign以进一步处理。

## 选择加入／选择退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager受用于管理用户选择加入／选择退出的cookie选择退出服务的约束。

要选择退出：

1. 导航至:
   [Adobe隐私中心——选择退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下滚动到 **服务** - **Experience Cloud服务使用数据**。

1. 选择引用的链接； 当前的 **标题**。

1. 您将获得以下详细信息，以及指向或选择退出在其中的选项：

   * 要选择不汇总和分析您访问此站点的相关数据，必须在您的浏览器上安装一个Cookie。 此Cookie识别您已选择退出。

      如果您删除退出Cookie，或者您更改了计算机或Web浏览器，您将需要再次退出。

      选择退出——将我排除在访客会话聚合和分析之外(安 `amcglobal.sc.omtrdc.net` 装选择退出Cookie)-单击此处。

      选择加入——将我包括在访客会话聚合和分析中(不安 `amcglobal.sc.omtrdc.net` 装选择退出cookie)-单击此处。
   请按照上述步骤访问实际链接。

   <!--
    NOTE TO WRITER: Change link to https://www.adobe.com/legal/terms.html and edit note.
    -->

   >[!NOTE]
   >
   > 使用条款的隐私政策 **部分中** ，还有 [进一步说明](https://marketing.adobe.com/resources/help/zh_CN/terms.html)。

## Analytics基金会 {#analytics-foundation}

AEM Sites包括与Analytics基金会的可选集成，后者使用AdobeAnalytics点播服务中的功能。

有关管理与AdobeAnalytics相关的数据主体请求的更多信息，请 [参阅AdobeAnalytics和数据隐私](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)。

## 按目标划分的个性化基础 {#personalization-foundation-by-target}

AEM Sites包括按目标与个性化基础的可选集成，该集成使用Adobe Target点播服务中的功能。

有关管理与Adobe Target相关的数据主体请求的更多信息，请 [参阅Adobe Target-隐私和一般数据保护规定](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM为ContextHub提供可选数据层。 这会在浏览器中保留特定于访客的数据，以便用于基于规则的个性化。

默认情况下，此访客数据不存储在AEM中； AEM将规则发送到数据层，以便在浏览器中做出个性化决策。

### 实施加入／退出 {#implementing-opt-in-opt-out}

站点所有者需要根据以下准则实施退出组件。

这些准则将选择加入作为默认实施。 因此，网站访客必须明确同意，然后才能将任何个人数据存储在浏览器的（客户端）持久性中。

* 每次包含ContextHub组件时都应包含退出组件。
* 与网站数据保护和隐私相关的条款和条件必须显示在网站访客中，允许他们：

   * 接受
   * 拒绝
   * 更改前一选择

* 如果站点访客接受站点的条款和条件，则应删除ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果站点访客不接受该站点的条款和条件，则应设置ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查ContextHub是否在退出模式下运行，应在浏览器的控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览ContextHub的持久性 {#previewing-persistence-of-contexthub}

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台； 例如：

   * 铬黄：

      * 打开“开发人员工具”>“应用程序”>“存储”:

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Firefox:

      * 打开“开发人员工具”>“存储”:

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Safari:

      * 打开菜单栏中的“首选项”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示JavaScript控制台”

         * “控制台”>“存储”>“本地存储”>（网站）> ContextHubPersistence
         * “控制台”>“存储”>“会话存储”>（网站）> ContextHubPersistence
         * 控制台>存储> Cookies >（网站）> ContextHubPersistence
   * Internet Explorer:

      * 打开“开发人员工具”>“控制台”

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 使用浏览器控制台中的ContextHub API:

   * ContextHub提供以下数据持久性层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存储定义将使用的持久性层，因此，应检查所有层的持久性的当前状态。


例如，要视图存储在localStorage中的数据：

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台：

   * Chrome —— 打开“开发人员工具”>“应用程序”>“存储”:

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence
   * Firefox —— 打开“开发人员工具”>“存储”:

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence


* 使用浏览器控制台中的ContextHub API:

   * ContextHub提供以下数据持久性层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存储定义将使用的持久性层，因此，应检查所有层的持久性的当前状态。


例如，要视图存储在localStorage中的数据：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持久性 {#clearing-persistence-of-contexthub}

要清除ContextHub持久性，请执行以下操作：

* 清除当前加载的存储的持久性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久性层； 例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久性层，必须为所有层调用相应的代码：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
