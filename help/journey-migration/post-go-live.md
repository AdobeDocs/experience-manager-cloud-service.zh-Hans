---
title: 上線後
description: 瞭解如何監控問題並改善效能
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 39%

---

# 上線後 {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM 故障排除"
>abstract="查看有关持续开发和管理日志的最佳实践，以及使用 Developer Console 和 CRXDE Lite 等工具帮助排除 AEM 的问题"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="访问和管理日志"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service 开发工具"

這是歷程的最後一部分，因此您將瞭解如何監視問題，並在移轉完成後改善效能。 您應該確保清理暫存檔，審查持續開發的最佳實務並管理記錄。

## 迄今为止的故事 {#story-so-far}

在歷程的上一步中，您已瞭解如何執行移轉並 [上線](/help/journey-migration/go-live.md) 在程式碼和內容準備好移至AEMas a Cloud Service中後。

## 目标 {#objective}

本檔案說明可用於疑難排解AEMas a Cloud Service環境的工具：

* **开发人员控制台**
* **CRXDE Lite**
* **管理日志**

## 开发人员控制台 {#developer-console}

開發人員控制檯中提供AEMas a Cloud Service開發人員環境的偵錯功能，可用於開發、測試和生產環境。

请参阅[实施 AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，了解有关开发工具的更多信息。

## CRXDE Lite {#crxde-lite}

作为用户，您可以在开发环境中访问 CRXDE Lite，但不能在暂存或生产环境中访问。

>[!IMPORTANT]
>寫入不可變的存放庫，例如 `/libs` 和 `/apps` 在執行階段導致錯誤。 此外，您無權存取測試和生產環境的開發人員工具。

请参阅[使用 CRXDE Lite 进行开发](/help/implementing/developing/tools/crxde.md)，了解如何使用 CRXDE Lite 来开发 AEM 应用程序。

## 管理日志 {#managing-logs}

用户可以访问选定环境的可用日志文件列表。

请参阅[访问和管理日志](/help/implementing/cloud-manager/manage-logs.md)，了解如何通过 UI 或通过 Cloud Manager 从 API 访问和管理日志。

## 連絡支援 {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="帮助与支持"
>abstract="请联系我们的 AEM 支持团队，获取说明或解决任意问题。"
>additional-url="https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html" text="Experience Cloud 支持"

如果您對存取Cloud Service有任何疑問，請聯絡您的Adobe代表或 [支援Experience Cloud](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html) 以取得更多詳細資料。

## 檔案學習 {#document-learnings}

移轉一旦完成，您應該記錄在此過程中獲得的知識。 可能有助於說明檔案流程的一些問題包括：

* 哪些程式效果良好，哪些程式效果缺佳？
* 主要煩惱為何？
* Recommendations，以備日後移轉時使用。

然後，您應該與組織內的利害關係人和團隊分享這些移轉後學習。

## 历程结束 - 是吗？ {#journey-ends}

恭喜！您已完成AEMas a Cloud Service移轉歷程！ 您應該瞭解如何：

* 開始使用AEMas a Cloud Service
* 判斷您的部署是否已準備好移至AEMas a Cloud Service
* 讓您的程式碼和內容雲端準備就緒
* 執行移轉
* 監控問題並改善效能
