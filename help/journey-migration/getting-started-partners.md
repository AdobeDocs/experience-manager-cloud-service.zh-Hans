---
title: 面向合作伙伴的 Experience Manager as a Cloud Service 迁移指南
description: 面向合作伙伴的 Experience Manager as a Cloud Service 迁移指南
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 21%

---

# Adobe Experience Manager as a Cloud Service合作夥伴移轉指南 {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="迁移至 AEM as a Cloud Service"
>abstract="概述推荐的分阶段方法，将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户提供无中断的互联体验"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="新增功能和不同功能"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="AEM as a Cloud Service 简介."

Adobe Experience Manager (AEM) as a Cloud Service提供重新架構的Experience Manager基礎，以容器式基礎架構、API導向開發和引導式DevOps流程為基礎，讓行銷人員和開發人員永遠領先於客戶體驗管理創新的曲線。

Cloud Service結合了Adobe Experience Manager豐富的現成可用功能及擴充性，以及現代雲端原生架構的靈活性，讓品牌能夠滿足不斷變化的消費者需求。

这份单页宣传材料概述了推荐的分阶段方法，用于将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户在这个专门构建的现代化体验管理平台上提供无中断的互联体验。

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

請參閱下圖，瞭解移轉歷程的一般呈現。

![图像](/help/journey-migration/assets/migration-process.png)

## Adobe Experience Manager as a Cloud Service快速入門 {#getting-started}

| 有哪些不同之處？ | 架构概述 |
|--------------------------|--------------------------|
| <ul><li>[現代架構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[自動更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[资源微服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[直接存取二進位檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[程式碼和內容的分離](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[復寫即服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=zh-Hans)</li><li>[Admin Console、群組/使用者成員資格和ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[AEM架構簡介](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[環境棧疊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[创作层](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[發佈階層](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=zh-Hans) 透過 [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[asset compute服務](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service - 运行时架构](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - 运行时架构")

<br>

## Adobe Experience Manager as a Cloud Service中的開發人員歷程 {#developer-journey}

### 开发

Adobe Experience Manager as a Cloud Service中的程式碼開發基礎與Adobe Experience Manager內部部署和Managed Services解決方案類似。

開發人員會撰寫程式碼並在本機測試，然後推送至遠端Adobe Experience Manager as a Cloud Service環境。

請參閱Experience Manageras a Cloud Service實作的相關自助資源，瞭解如何自訂Experience Manageras a Cloud Service部署。

| 本機開發設定 | 開始前須知 |
|-----------|------------|
| <ol><li>檢閱 [ADOBE EXPERIENCE MANAGER SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) 檔案，以瞭解更多。</li><li>觀看 [安裝Dispatcher SDK](https://video.tv.adobe.com/v/30601) 瞭解如何安裝Dispatcher SDK</li><li>觀看 [設定Dispatcher SDK](https://video.tv.adobe.com/v/30602) 瞭解如何設定Dispatcher SDK</li><li>檢閱 [本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) 更多相關檔案</li><li>設定Experience Manager的存取權 [逐步說明](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Development Essentials](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[瞭解Experience Manager專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)</li><li>[數位基礎藍圖](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[样式系统](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[叠加](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manageras a Cloud ServiceAPI參考](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> 請參閱教學課程，瞭解如何 [在本機Experience ManagerSDK上開發和部署WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)

### 部署

开发人员编写代码并在本地进行测试，然后将代码推送到远程 AEM as a Cloud Service 环境。

需要使用 Cloud Manager，它是 Managed Services 的一个可选内容交付工具。现在，这是用于将代码部署到 AEM as a Cloud Service 环境的唯一机制。

請參閱自助資源，瞭解如何設定並部署至AEMas a Cloud Service環境。

1. [設定CM管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * 生產管道
   * 仅非生产和代码质量管道
2. [部署程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [瞭解測試結果](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **存取記錄檔**
   * [透過CM UI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [透過Adobei/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [作業與維護](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [設定OSGI設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [备份和恢复](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> 請參閱教學課程，瞭解如何 [將WKND部署至Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)

### 帮助及资源

1. [偵錯提示與秘訣](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (僅適用於本機SDK和Experience Manager雲端開發環境)
4. [記錄檔和記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [CM記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) （建置單元測試、程式碼掃描、建置影像、部署）
   * [Experience Manager Cloud Service記錄](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror、aemaccess、aemrequest、aemdispatcher、httpderror、httpcaccess)
   * 本機SDK記錄（位於host：port/crx-quickstart/logs下）

>[!NOTE]
> 如需其他說明，您可能需要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群與論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## 迁移至 Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="迁移至 Adobe Experience Manager as a Cloud Service"
>abstract="这份单页宣传材料概述了推荐的分阶段方法，用于将客户从各种 Experience Manager 部署过渡到 Experience Manager as a Cloud Service，并帮助现有客户在这个专门构建的现代化体验管理平台上提供无中断的互联体验。"

**Experience Manageras a Cloud Service為Experience Manager Sites和Assets提供可擴充、安全且敏捷的技術基礎，讓行銷人員和IT人員專注於大規模提供具影響力的體驗。**

透過Experience Manageras a Cloud Service，您的團隊可以專注於創新而不是規劃產品升級。 新產品功能會經過徹底測試，並持續傳送給您的團隊，確保團隊可隨時存取最先進的應用程式。

过渡到云服务的历程包括三个阶段 - 规划、执行和上线后。要成功、顺利的过渡，您应确保进行适当的规划并遵守本指南中概述的最佳实践。

下圖顯示建議的Cloud Service轉換歷程的高層級表示。

![图像](/help/journey-migration/assets/home-img1.png)

<br>

### 规划

在開始轉換至Cloud Service的歷程之前，您應該熟悉Experience Manageras a Cloud Service並檢閱已對它所做的重大變更，並檢閱已取代或已棄用的功能。

<table>
<tr>
<td>專案探索與評估</td>
<td><ul><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=zh-Hans">Experience Manageras a Cloud Service重大變更</a> 來瞭解Adobe Experience Manager as a Cloud Service和Experience Manager6.x之間的重要差異。</li><li>請參閱 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">已棄用的功能</a> 以進一步瞭解已標示為過時的功能。</li><li>[僅適用於Cloud Service移轉]評估Cloud Service整備：執行 <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer (BPA)</a> 在來源環境中 </li><li>針對Experience ManagerCS中的重大變更和已棄用功能完成評估</li></ul></td>
</tr>
<tr>
<td>审核</td>
<td><ul><li>根據探索，執行工作量估計和資源配置練習</li></ul></td>
</tr>
<tr>
<td>測量</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">建立專案KPI</a>，成功標準和專案時間表</li></ul></td>
</tr>
</table>

>[!NOTE]
>最佳實務分析報告會提供原本必須手動收集和評估的資訊，以加速評估轉換為AEMas a Cloud Service所需的時間和成本。


<br>

### 执行

在開始專案的執行階段之前，您應該先加入Cloud Service。 您也需要熟悉Cloud Manager。 這是將專案程式碼部署至Experience Manager Cloud Service執行個體的機制。

Cloud Manager可讓組織在雲端中自行管理Experience Manager。 其中包括持續整合和持續傳遞([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en))架構，可讓IT團隊與實作合作夥伴加速提供自訂或更新，而不會影響效能或安全性。

#### 内容迁移

1. [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) ：用於將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud Service例項。
2. [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) ：用於匯入和匯出存放庫的可變內容。


#### 重構/最佳化

| 快速入门 | 檢閱並重構程式碼 | Dispatcher評論 |
|---|---|---|
| <ul><li>[本機開發設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[本機Dispatcher設定](https://video.tv.adobe.com/v/30602/)</li><li>[使用SDK API jar編譯程式碼](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[檢閱AEM Dev指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>背景任務和長時間執行的工作</li><li>Sling排程器</li><li>輸入資料流使用量和更多內容</li></ul></li></ul> | <ul><li>執行 [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) 在來源環境中。[**僅限移轉**]<ul><li>專案建構考量事項(根據 [雲端原型](https://github.com/adobe/aem-project-archetype))<ul><li>程式碼和內容的分離（可變與不可變）</li><li>[自訂索引定義](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[自訂執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>檢閱並執行必要的變更</li><li>[部署](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) 在本機SDK上執行</li><li>透過AEM SDK執行煙霧測試</li></ul> | <ul><li>檢閱 [Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) 用於重構</li><li>使用 [Dispatcher轉換工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) 適當時使用該工具。 [**僅限移轉**]</li><li>可使用進行測試 [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> 資產客戶：使用檢閱和重構資產工作流程 [資產雲端移轉](https://github.com/adobe/aem-cloud-migration) 工具


#### 部署/上線

1. [部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. 透過 [Cloud Manager品質管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [部署至開發環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**僅限移轉**] 使用套件或進行內容轉移 [內容轉移工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. 執行建議的測試週期（煙霧、QA等）
6. 提升至Cloud Manager生產管道
7. 煙霧測試驗證
8. 上线

<br>

### 上線後

在上线后阶段，您应确保清理临时文件，审查持续开发的最佳实践并管理日志。

>[!TIP]
> 提供用於疑難排解AEMas a Cloud Service環境的工具
>1. [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [管理日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)


<br>

### 工具和资源

| 評估 | 重構 | Experience Manager現代化 | 内容迁移 |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Unified Experience Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[静态模板到可编辑模板](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[设计配置到策略](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[基础组件到核心组件](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[经典 UI 到触控式 UI](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans)</li><li>[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> 如需其他說明，您可能需要：
>1. [聯絡Experience Manager支援團隊](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. 探索 [Experience Manager社群與論壇](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

