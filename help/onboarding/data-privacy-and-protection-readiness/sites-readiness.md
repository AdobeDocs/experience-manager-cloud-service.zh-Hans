---
title: 数据保护和数据隐私规定- Adobe Experience Manager即云服务站点就绪
description: '了解Adobe Experience manager作为各种数据保护和数据隐私法规的云服务站点支持；包括欧盟一般数据保护规定(GDPR)、加利福尼亚州消费者隐私法以及在将新AEM作为云服务项目实施时如何遵守这些规定。 '
translation-type: tm+mt
source-git-commit: 1130e8a07bc3826380483a7560ebda7e8a17e238

---


# Adobe Experience manager作为云服务站点，为数据保护和数据隐私法规做好准备 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的内容不构成法律咨询，不代替法律咨询。
>
>有关数据保护和数据隐私法规的建议，请咨询贵公司的法务部门。

>[!NOTE]
>
>有关Adobe对隐私权问题的回应以及作为Adobe客户对您意味着什么的更多信息，请参 [阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

Adobe Experience manager作为云服务站点，可以帮助客户履行数据隐私和保护合规义务。 本页将指导客户完成在AEM Sites中处理此类请求的过程。 它描述了存储的专用数据的位置，以及如何手动或使用代码删除这些数据。

有关详细信息，请参 [阅Adobe隐私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>有关更 [多详细信息，请参阅Adobe Experience Manager作为数据保护和数据隐私法规的云服务就绪](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) 。

## AEM作者层 {#aem-author-tier}

AEM Foundation文档中介绍了作者服务器上的用户帐户和 [UGC内容](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

## AEM发布层 {#aem-publish-tier}

AEM Foundation文档中介绍了用于验证站点访客身份以及发布服务器上的UGC内容的 [用户帐户](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)。

默认情况下，AEM站点组件不存储访客在发布服务器上输入的表单数据。 建议将数据转发给第三方系统或Adobe Campaign以进一步处理。

## 选择加入／选择退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience manager受Cookie选择退出服务约束，该服务用于管理用户的选择加入／选择退出。

要选择退出：

1. 导航至:
   [Adobe隐私中心——选择退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下滚动到服 **务** - **Experience cloud服务使用数据**。

1. 选择引用的链接；当前已 **在此标题**。

1. 您将看到以下详细信息以及选择退出或加入的选项：

   * 要选择不汇总和分析有关您访问此站点的数据，必须在您的浏览器上安装Cookie。 此Cookie可识别您已选择退出。

      如果您删除退出Cookie，或者您更改了计算机或Web浏览器，您将需要再次退出。

      选择退出——将我排除在访客会话汇总和分析之外(安装 `amcglobal.sc.omtrdc.net` 选择退出Cookie)-单击此处。

      选择加入——将我纳入访客会话汇总和分析中(请勿安装 `amcglobal.sc.omtrdc.net` 选择退出cookie)-单击此处。
   请按照上述步骤访问实际链接。

   >[!NOTE]
   >
   > 使用条款的“隐私 **政策** ”部分中有 [进一步说明](https://marketing.adobe.com/resources/help/en_US/terms.html)。

## 分析基础 {#analytics-foundation}

AEM Sites包括与Analytics Foundation的可选集成，后者使用Adobe Analytics点播服务中的功能。

有关管理与Adobe Analytics相关的数据主体请求的更多信息，请参 [阅Adobe Analytics和数据隐私](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)。

## 按Target划分的个性化基础 {#personalization-foundation-by-target}

AEM Sites包括与Personalization Foundation by Target的可选集成，后者使用Adobe Target点播服务中的功能。

有关管理与Adobe Target相关的数据主体请求的更多信息，请参阅 [Adobe Target —— 隐私和一般数据保护规定](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM为ContextHub提供了一个可选数据层。 这会将特定访客的数据保留在浏览器中，以便用于基于规则的个性化。

默认情况下，此访客数据不存储在AEM中；AEM将规则发送到数据层，以在浏览器中做出个性化决策。

### 实施选择加入／选择退出 {#implementing-opt-in-opt-out}

站点所有者需要根据以下准则实施退出组件。

这些准则将选择加入作为默认值。 因此，网站访问者必须明确同意，然后才能将任何个人数据存储在浏览器的（客户端）持久性中。

* 每次包含ContextHub组件时，都应包含退出组件。
* 与网站数据保护和隐私相关的条款和条件必须显示给网站访客，以便他们：

   * 接受
   * 拒绝
   * 更改前一个选择

* 如果站点访问者接受站点的条款和条件，则应删除ContextHub退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果网站访客不接受网站的条款和条件，则应设置ContextHub退出Cookie:

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

* 使用浏览器的控制台；例如：

   * Chrome:

      * 打开“开发人员工具”>“应用程序”>“存储”:

         * “本地存储”>（网站）> ContextHubPersistence
         * “会话存储”>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Firefox:

      * 打开“开发人员工具”>“存储”:

         * “本地存储”>（网站）> ContextHubPersistence
         * “会话存储”>（网站）> ContextHubPersistence
         * Cookies >（网站）> SessionPersistence
   * Safari:

      * 打开菜单栏中的“首选项”>“高级”>“显示修改照片菜单”
      * 打开“开发”>“显示JavaScript控制台”

         * “控制台”>“存储”>“本地存储”>（网站）>“ContextHubPersistence”
         * “控制台”>“存储”>“会话存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“Cookie”>“（网站）”>“ContextHubPersistence”
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
      ContextHub存储定义将使用的持久层，因此，查看应检查所有层的持久性的当前状态。


例如，要查看存储在localStorage中的数据，请执行以下操作：

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台：

   * Chrome —— 打开“开发人员工具”>“应用程序”>“存储”:

      * “本地存储”>（网站）> ContextHubPersistence
      * “会话存储”>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence
   * Firefox —— 打开“开发人员工具”>“存储”:

      * “本地存储”>（网站）> ContextHubPersistence
      * “会话存储”>（网站）> ContextHubPersistence
      * Cookies >（网站）> SessionPersistence


* 使用浏览器控制台中的ContextHub API:

   * ContextHub提供以下数据持久性层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`
      ContextHub存储定义将使用的持久层，因此，查看应检查所有层的持久性的当前状态。


例如，要查看存储在localStorage中的数据，请执行以下操作：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub的持久性 {#clearing-persistence-of-contexthub}

清除ContextHub持久性：

* 清除当前加载的存储的持久性：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定的持久层；例如，sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有ContextHub持久层，必须为所有层调用相应的代码：

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
