---
title: 数据保护和数据隐私法规 — Adobe Experience Manager作为Cloud Service站点就绪性
description: 了解Adobe Experience Manager作为Cloud Service站点对各种数据保护和数据隐私法规的支持；包括欧盟《通用数据保护条例》(GDPR)、《加州消费者隐私法案》，以及在实施新的AEM as a Cloud Service项目时如何遵守这些规定。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# Adobe Experience Manager as a Data Protection和数据隐私法规的Cloud Service站点已准备就绪{#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询贵公司的法律部门，以获取有关数据保护和数据隐私法规的建议。

>[!NOTE]
>
>有关Adobe对隐私问题的响应以及这对Adobe客户有何影响的更多信息，请参阅[Adobe的隐私中心](https://www.adobe.com/privacy.html)。

Adobe Experience Manager as a Cloud Service站点随时准备帮助客户履行其数据隐私和保护合规义务。 本页将指导客户完成在AEM Sites中处理此类请求的过程。 它描述了存储的专用数据的位置，以及如何手动或使用代码删除这些数据。

有关详细信息，请参阅[Adobe隐私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>有关更多详细信息，请参阅[Adobe Experience Manager as a Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)Cloud Service就绪。

## AEM 创作层 {#aem-author-tier}

[AEM Foundation文档](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)中介绍了作者服务器上的用户帐户和UGC内容。

## AEM 发布层 {#aem-publish-tier}

[AEM Foundation文档](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)中介绍用于验证网站访客和发布服务器上UGC内容的用户帐户。

默认情况下，AEM Sites组件不存储访客在发布服务器上输入的表单数据。 建议将数据转发到第三方系统或Adobe Campaign以进行进一步处理。

## 选择启用/选择禁用{#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager受用于管理用户选择启用/选择禁用的cookie选择禁用服务的限制。

要选择禁用，请执行以下操作：

1. 导航至:
   [Adobe隐私中心 — 选择退出](https://www.adobe.com/privacy/opt-out.html)

1. 向下滚动到&#x200B;**Services** - **Experience Cloud服务使用数据**。

1. 选择引用的链接；当前的标题为&#x200B;**此处**。

1. 您将看到以下详细信息，以及选择禁用或启用的选项：

   * 要选择退出对您访问此网站的相关数据的汇总和分析，必须在浏览器上安装Cookie。 此Cookie标识您已选择退出。

      如果删除选择退出Cookie，或者更改计算机或Web浏览器，则需要再次选择退出。

      选择退出 — 将我从访客会话聚合和分析中排除（安装`amcglobal.sc.omtrdc.net`选择退出Cookie） — 单击此处。

      选择加入 — 将我包含在访客会话聚合和分析中（请不要安装`amcglobal.sc.omtrdc.net`选择退出Cookie） — 单击此处。
   请按照上述步骤访问实际链接。

   >[!NOTE]
   >
   > **2中有进一步的说明。 隐私.** Adobe一 [般使用条款](https://www.adobe.com/cn/legal/terms.html)中的部分。

## Analytics Foundation {#analytics-foundation}

AEM Sites包含与Analytics Foundation的可选集成，该集成使用Adobe Analytics On-demand Service中的功能。

有关管理与Adobe Analytics相关的数据主体请求的更多信息，请参阅[Adobe Analytics和数据隐私](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)。

## Target的个性化基础{#personalization-foundation-by-target}

AEM Sites包含一个可选的与Personalization Foundation by Target的集成，该集成使用Adobe Target On-demand Service中的功能。

有关管理与Adobe Target相关的数据主体请求的更多信息，请参阅[Adobe Target — 隐私和《通用数据保护条例》](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM通过ContextHub提供可选数据层。 这会保留浏览器中特定于访客的数据，以便用于基于规则的个性化。

默认情况下，此访客数据不存储在AEM中；AEM会向数据层发送规则，以便在浏览器中做出个性化决策。

### 实施选择启用/选择禁用{#implementing-opt-in-opt-out}

站点所有者需要根据以下准则实施选择退出组件。

这些准则将选择加入作为默认实施。 因此，在将任何个人数据存储到浏览器的（客户端）持久性中之前，网站访客必须明确同意。

* 每次包含ContextHub组件时，都应包含选择退出组件。
* 必须向网站访客显示与网站数据保护和隐私相关的条款和条件，以便他们能够：

   * 接受
   * 拒绝
   * 更改其先前的选择

* 如果网站访客接受网站的条款和条件，则应删除ContextHub选择退出Cookie:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果网站访客不接受网站的条款和条件，则应设置ContextHub选择退出Cookie:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查ContextHub是否在选择退出模式下运行，应在浏览器控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览ContextHub {#previewing-persistence-of-contexthub}的持久性

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台；例如：

   * 铬黄：

      * 打开开发人员工具>应用程序>存储：

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookie >（网站）> SessionPersistence
   * Firefox:

      * 打开开发人员工具>存储：

         * 本地存储>（网站）> ContextHubPersistence
         * 会话存储>（网站）> ContextHubPersistence
         * Cookie >（网站）> SessionPersistence
   * Safari:

      * 在菜单栏中打开“首选项”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示JavaScript控制台”

         * 控制台>存储>本地存储>（网站）> ContextHubPersistence
         * 控制台>存储>会话存储>（网站）> ContextHubPersistence
         * 控制台>存储> Cookie >（网站）> ContextHubPersistence
   * Internet Explorer:

      * 打开开发人员工具>控制台

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 在浏览器控制台中使用ContextHub API:

   * ContextHub提供以下数据持久层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存储定义将使用哪个持久层，以便查看持久层的当前状态，所有层都应被检查。


例如，要查看存储在localStorage中的数据，请执行以下操作：

要预览使用的ContextHub的永久性，用户可以：

* 使用浏览器的控制台：

   * Chrome — 打开开发人员工具>应用程序>存储：

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookie >（网站）> SessionPersistence
   * Firefox — 打开开发人员工具>存储：

      * 本地存储>（网站）> ContextHubPersistence
      * 会话存储>（网站）> ContextHubPersistence
      * Cookie >（网站）> SessionPersistence


* 在浏览器控制台中使用ContextHub API:

   * ContextHub提供以下数据持久层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (默认)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub存储定义将使用哪个持久层，以便查看持久层的当前状态，所有层都应被检查。


例如，要查看存储在localStorage中的数据，请执行以下操作：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除ContextHub {#clearing-persistence-of-contexthub}的持久性

要清除ContextHub持久性，请执行以下操作：

* 要清除当前已加载存储的持久性，请执行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 清除特定持久层；例如，sessionStorage:

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
