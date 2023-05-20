---
title: 快速开发环境
description: 瞭解如何善用快速開發環境在雲端環境中進行快速開發反複專案。
exl-id: 1e9824f2-d28a-46de-b7b3-9fe2789d9c68
source-git-commit: 5bfa5a1df940b8903acd08f4c3cb7443adb897d8
workflow-type: tm+mt
source-wordcount: '3325'
ht-degree: 5%

---

# 快速开发环境 {#rapid-development-environments}

為了部署變更，目前的雲端開發環境需要使用採用廣泛計畫碼安全性和品質規則的程式，稱為CI/CD管道。 對於需要快速和反複變更的情況，Adobe已引入快速開發環境（簡稱RDE）。

RDE可讓開發人員快速部署和檢閱變更，將測試經證實可在本機開發環境中運作的功能所需的時間減至最少。

在RDE中測試變更後，可以透過Cloud Manager管道將它們部署到常規雲端開發環境。

>[!VIDEO](https://video.tv.adobe.com/v/3415582/?quality=12&learn=on)


您可以參考其他示範影片 [如何設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html)， [使用方式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html)，以及 [開發生命週期](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/development-life-cycle.html) 使用RDE。

## 简介 {#introduction}

RDE可用於程式碼、內容，以及Apache或Dispatcher設定。 與一般雲端開發環境不同，開發人員可以使用本機命令列工具，將本機建置的程式碼同步到RDE。

每個方案都布建了RDE。 若是沙箱帳戶，則會在閒置數小時後休眠。

建立後，RDE會設定為最新可用的AEM版本。 RDE重設（可使用Cloud Manager執行）將循環RDE並將其設定為最新可用的AEM版本。

通常，單一開發人員在指定時間會使用RDE來測試和偵錯特定功能。 完成開發工作階段後，RDE可以重設為預設狀態以供下次使用。

其他RDE可授權給生產（非沙箱）計畫。

## 在程式中啟用RDE {#enabling-rde-in-a-program}

按照以下步驟使用Cloud Manager為您的計畫建立RDE。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 按一下要新增RDE的計畫以顯示其詳細資訊。

   * RDE可新增至兩者 [沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 和 [生產計畫。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)

1. 从&#x200B;**程序概述**&#x200B;页面，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**添加环境**&#x200B;以添加环境。

   ![环境信息卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * **添加环境**&#x200B;选项也可在&#x200B;**环境**&#x200B;选项卡上使用。

      ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * **添加环境**&#x200B;选项可能由于缺少权限或根据许可的资源而被禁用。

1. 在出现的&#x200B;**添加环境**&#x200B;对话框中：

   * 選取 **快速開發** 在 **選取環境型別** 標題。
      * 可用/已使用環境的數量會顯示在環境型別後面的括弧中。
   * 提供 **名稱** 適用於環境。
   * 提供選填 **說明** 適用於環境。
   * 选择&#x200B;**云区域**。

   ![添加环境对话框](/help/implementing/cloud-manager/assets/add-environment-wizard.png)

1. 单击&#x200B;**保存**&#x200B;来添加指定环境。

**概述**&#x200B;屏幕现在在&#x200B;**环境**&#x200B;信息卡中显示您的新环境。 

建立後，RDE會設定為最新可用的AEM版本。 RDE重設（也可以使用Cloud Manager執行）將循環RDE並將其設定為最新可用的AEM版本。

如需有關使用Cloud Manager建立環境、管理誰有權存取環境以及指派自訂網域的詳細資訊，請參閱 [Cloud Manager檔案。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 安裝RDE命令列工具 {#installing-the-rde-command-line-tools}

使用Cloud Manager為您的計畫新增RDE後，您可以透過設定命令列工具與其互動，如以下步驟所述：

>[!IMPORTANT]
>
>請確定您擁有最新版本的 [節點和NPM已安裝](https://nodejs.org/en/download/) Adobe I/OCLI和相關外掛程式才能正常運作。


1. 依照下列程式安裝Adobe I/OCLI工具 [此處](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).
1. 安裝Adobe I/OCLI工具Cloud Manager外掛程式，並依照說明進行設定 [此處](https://github.com/adobe/aio-cli-plugin-cloudmanager).
1. 執行下列命令，安裝Adobe I/OCLI工具AEM RDE外掛程式：

   ```
   aio plugins:install @adobe/aio-cli-plugin-aem-rde
   aio plugins:update
   ```

1. 為組織ID設定Cloud Manager外掛程式：

   `aio config:set cloudmanager_orgid 4E03EQC05D34GL1A0B49421C@AdobeOrg`

   和將英數字串取代為您自己的組織ID，您可透過策略查詢此組織ID [此處](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

1. 接下來，設定您的程式id：

   `aio config:set cloudmanager_programid 12345`

1. 然後，設定要將RDE附加到的環境ID：

   `aio config:set cloudmanager_environmentid 123456`

1. 完成外掛程式的設定後，請透過以下方式登入：

   `aio login`

   成功登入時的回應應該類似於下面的輸出，但您可以忽略顯示的值。

   ```
   ...
   You are currently in:
   1. Org: <no org selected>
   2. Project: <no project selected>
   3. Workspace: <no workspace selected>
   ```

   注意：此步驟需要您是Cloud Manager的成員 **開發人員 — Cloud Service** 產品設定檔。 另請參閱 [此頁面](/help/journey-onboarding/assign-profiles-cloud-manager.md#assign-developer) 以取得更多詳細資料。

   或者，如果您可以透過執行此命令登入開發人員主控台，則可以確認您擁有此開發人員角色：

   `aio cloudmanager:environment:open-developer-console`

   >[!TIP]
   >
   >如果您看到 `Warning: cloudmanager:list-programs is not a aio command.` 錯誤，您必須安裝 [aio-cli-plugin-cloudmanager](https://github.com/adobe/aio-cli-plugin-cloudmanager) 透過執行以下命令：
   >
   >
   ```
   >aio plugins:install @adobe/aio-cli-plugin-cloudmanager
   >```

1. 執行以驗證登入是否成功完成

   `aio cloudmanager:list-programs`

   這應該會列出您設定之組織下的所有程式。


如需詳細資訊和示範，請參閱 [如何設定RDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-setup.html) 教學影片。

## 開發新功能時使用RDE {#using-rde-while-developing-a-new-feature}

Adobe建議使用下列工作流程來開發新功能：

* 當達到中繼里程碑並透過AEMas a Cloud ServiceSDK在本機成功驗證時，程式碼應提交到尚未成為主行一部分的Git功能分支，儘管提交到是Git的選擇性。 構成「中繼里程碑」的要素因團隊習慣而異。 範例包括幾行程式碼、半天的工作或完成子功能。

* 如果RDE已由其他功能使用，且您想重設RDE [將其重設為預設狀態](#reset-rde). <!-- Alexandru: hiding for now, please don't delete This can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). -->重設將需要幾分鐘的時間，且所有現有內容和程式碼都會被刪除。 您可以使用RDE狀態指令來確認RDE已就緒。 RDE將隨最新的AEM發行版本一起更新。

   >[!IMPORTANT]
   >
   > 如果您的測試和生產環境未收到自動AEM版本更新，並且遠低於最新的AEM版本版本，請留意，在RDE上執行的程式碼可能與程式碼在測試和生產環境中的運作方式不符。 在這種情況下，將程式碼部署到生產環境之前，在測試環境中對程式碼執行徹底測試尤為重要。


* 使用RDE命令列介面，將本機程式碼同步到RDE。 選項包括安裝內容套件、特定套件、OSGI設定檔案、內容檔案和Apache/Dispatcher設定的zip檔案。 也可以參考遠端內容套件。 請參閱 [RDE命令列工具](#rde-cli-commands) 區段以取得詳細資訊。 您可以使用status命令來驗證部署是否成功。 或者，使用封裝管理員來安裝內容封裝。

* 在RDE中測試程式碼。 Cloud Manager中有提供作者和發佈URL。

* 如果程式碼的行為與預期不符，請使用標準偵錯技術來瞭解問題並做出適當的變更。 若未將程式碼修改提交至Git （因尚未驗證），請使用本機CLI將程式碼同步至RDE。 持續反複運算，直到問題解決為止。

* 程式碼如預期運作後，將程式碼提交到Git功能分支。

* 同步至RDE的程式碼不會使用Cloud Manager管道，因此現在您應該使用Cloud Manager非生產管道將Git功能分支部署至雲端開發環境。 這將驗證計畫碼是否通過Cloud Manager品質關卡，並讓您確信稍後將使用Cloud Manager生產管道成功部署計畫碼。

* 對每個中繼里程碑重複上述步驟，直到功能的所有程式碼都準備就緒為止，並在RDE和雲端開發環境中正常運作。

* 透過Cloud Manager生產管道將計畫碼部署到生產環境。

## 使用RDE偵錯現有功能 {#use-rde-to-debug-an-existing-feature}

工作流程類似於開發新功能。 差異在於，同步至RDE的程式碼會反映推送至發現問題之環境的任何專案的Git標籤。 此外，部署符合上游環境的內容可能會有幫助。 這可透過匯出和匯入內容套件來完成。

## 多位開發人員在相同RDE上共同作業 {#multiple-developers-collaborating-on-the-same-rde}

RDE一次支援一個專案。 由於程式碼會從本機開發環境同步至RDE環境，因此開發人員在指定時間自行使用程式碼是最自然的做法。

不過，在仔細協調後，多位開發人員可以驗證特定功能或偵錯特定問題。 關鍵是每個開發人員都會保持其本機專案的同步，以便特定開發人員所做的程式碼變更被其他開發人員吸收，否則一個開發人員可能會無意中覆寫另一個開發人員的程式碼。 建議的策略是讓每位開發人員在同步至RDE之前，將其變更提交至共用Git分支，讓其他開發人員在自行進行變更之前先提取變更。

## RDE指令行工具指令 {#rde-cli-commands}

### 說明/一般資訊 {#help}

* 如需命令清單，請鍵入：

   `aio aem:rde`

* 如需命令的詳細說明，請輸入：

   `aio aem rde <command> --help`

### 部署至RDE {#deploying-to-rde}

本節說明如何使用RDE CLI來部署、安裝或更新套件組合、OSGI設定、內容套件、個別內容檔案以及Apache或Dispatcher設定。

一般使用模式為 `aio aem:rde:install <artifact>`.

您可以在下方找到一些範例：

<u>部署內容封裝</u>

`aio aem:rde:install sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip`

成功部署的回應類似於以下內容：

```
...
#1: deploy completed for content-package sample.demo.ui.apps.all-1.0.0-SNAPSHOT.zip on author,publish - done by 9E072FC75D54FE1A2B49431C@AdobeID at 2022-09-13T11:32:06.229Z
```

或者，您可以參考遠端存放庫：

`aio aem:rde:install -t content-package "https://repo1.maven.org/maven2/com/adobe/aem/guides/aem-guides-wknd.all/2.1.0/aem-guides-wknd.all-2.1.0.zip"`

依預設，成品會同時部署至製作和發佈層級，但「 — s」標幟可用於鎖定特定層級。

可以部署任何AEM套件，例如包含程式碼、內容或 [容器封裝](/help/implementing/developing/introduction/aem-project-content-package-structure.md#container-packages) （也稱為「全部」套件）。

>[!IMPORTANT]
>
>不會透過上述內容套件安裝來部署WKND專案的Dispatcher設定。 您將需要在「部署Apache/Dispatcher設定」步驟之後單獨部署它。

<u>部署OSGI設定</u>

`aio aem:rde:install com.adobe.granite.demo.MyServlet.cfg.json`

其中成功部署的回應類似於以下內容：

```
...
#2: deploy completed for osgi-config com.adobe.granite.demo.MyServlet.cfg.json on author,publish - done by 9E0725C05D54FE1A0B49431C@AdobeID at 2022-09-13T11:54:36.390Z
```

<u>部署套件組合</u>

若要部署套件組合，請使用：

`aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar`

其中成功部署的回應類似於以下內容：

```
...
#3: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D53BE1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
```

<u>部署內容檔案</u>

若要部署內容檔案，請使用：

`aio aem:rde:install world.txt -p /apps/hello.txt`

其中成功部署的回應類似於以下內容：

```
..
#4: deploy completed for content-file world.txt on author,publish - done by 9E0729C05C54FE1A0B49431C@AdobeID at 2022-09-14T07:49:30.644Z
```

<u>部署Apache/Dispatcher設定</u>

對於此類設定，整個資料夾結構都必須採用zip檔案的形式。

從 `dispatcher` AEM專案的模組，您可以透過執行以下maven命令來壓縮Dispatcher設定：

`mvn clean package`

或使用以下的zip命令 `src` 目錄 `dispatcher` 模組：

`zip -y -r dispatcher.zip .`

然後使用此命令部署設定：

`aio aem:rde:install target/aem-guides-wknd.dispatcher.cloud-X.X.X-SNAPSHOT.zip`

>[!TIP]
>
>上述命令假設您部署的是 [WKND](https://github.com/adobe/aem-guides-wknd) 專案的Dispatcher設定。 請務必取代 `X.X.X` 以及對應的WKND專案版本號碼或專案特定版本號碼，部署專案的Dispatcher設定時。

>[!NOTE]
>
>RDE支援「彈性模式」 Dispatcher設定，但不支援「舊版模式」 Dispatcher設定。 另請參閱 [dispatcher檔案](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以取得這兩種模式的相關資訊。 您也可以參閱以下檔案： [移轉至彈性模式](/help/implementing/dispatcher/validation-debug.md#migrating)，如果尚未這麼做的話。

成功部署將產生類似於以下內容的回應：

```
..
#5 deploy completed for dispatcher-config dispatcher.zip on author,publish - done by 9E0735C05T54FE1A0B49431C@AdobeID at 2022-10-03T10:26:31.286Z
Logs:
  Cloud manager validator 2.0.49
  2022/10/03 10:26:37 No issues found
  Syntax OK
```

部署到RDE的程式碼不會經歷Cloud Manager管道及其相關品質閘道，但程式碼會經過一些分析，這些分析會報告錯誤，如下列程式碼範例所示：

```
$ aio aem:rde:install ~/.m2/repository/org/apache/felix/org.apache.felix.gogo.jline/1.1.8/org.apache.felix.gogo.jline-1.1.8.jar
...
#19: deploy staged for osgi-bundle org.apache.felix.gogo.jline-1.1.8.jar on author,publish - done by 9E0725C05D74FR1A0B49431C@AdobeID at 2022-09-14T07:54:28.882Z
Logs:
The analyser found the following errors for author :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
The analyser found the following errors for publish :
[requirements-capabilities] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Artifact com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8 requires [org.apache.felix.gogo.jline/1.1.8] org.apache.felix.gogo; filter:="(&(org.apache.felix.gogo=command.implementation)(version>=1.0.0)(!(version>=2.0.0)))"; effective:=active in start level 20 but no artifact is providing a matching capability in this start level.
[api-regions-exportsimports] com.adobe.aem.temp:org.apache.felix.gogo.jline:1.1.8: Bundle org.apache.felix.gogo.jline:1.1.8 is importing package(s) [org.jline.builtins, org.jline.utils, org.apache.felix.service.command, org.apache.felix.service.threadio, org.jline.terminal, org.jline.reader, org.apache.felix.gogo.runtime, org.jline.reader.impl] in start level 20 but no bundle is exporting these for that start level.
```

上述程式碼範例說明套件無法解析時的行為，在此情況下，套件為「暫存」，且只有在透過安裝其他程式碼滿足需求（在此情況下為缺少匯入）時才會安裝。

### 檢查RDE的狀態 {#checking-rde-status}

您可以使用RDE CLI來檢查環境是否已準備好部署到，以及已透過RDE外掛程式進行了哪些部署。

正在运行:

`aio aem:rde:status`

將會傳回：

```
Info for cm-p12345-e987654
Environment: Ready
- Bundles Author:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Bundles Publish:
 com.adobe.granite.sample.demo-1.0.0.SNAPSHOT
- Configurations Author:
 com.adobe.granite.demo.MyServlet
- Configurations Publish:
 com.adobe.granite.demo.MyServlet
```

如果命令傳回部署執行個體的相關備註，您仍可執行下一次更新，但您的最後一次更新可能尚未顯示在執行個體上。

### 顯示部署歷史記錄 {#show-deployment-history}

您可以透過執行以下專案來檢查對RDE進行的部署歷史記錄：

`aio aem:rde:history`

會以下列形式傳回回應：

`#1: deploy completed for content-package aem-guides-wknd.all-2.1.0.zip on author,publish - done by 029039A55D4DE16A0A494025@AdobeID at 2022-09-12T14:41:55.393Z`

### 從RDE刪除 {#deleting-from-rde}

您可以透過CLI工具刪除先前部署至RDE的組態和套件組合。 使用 `status` 可刪除專案清單的命令，包括 `bsn` 適用於套件組合和 `pid` 供設定在delete指令中參照。

例如，如果 `com.adobe.granite.demo.MyServlet.cfg.json` 已安裝， `bsn` 只是 `com.adobe.granite.demo.MyServlet`，不含 **cfg.json** 字尾。

不支援刪除內容套件或內容檔案。 為了移除它們，應重設RDE，這會使其恢復到預設狀態。

如需更多詳細資訊，請參閱以下範例：

```
aio aem:rde:delete com.adobe.granite.csrf.impl.CSRFFilter
#13: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on author - done by karl at 2022-09-12T22:01:01.955Z
#14: delete completed for osgi-config com.adobe.granite.csrf.impl.CSRFFilter on publish - done by karl at 2022-09-12T22:01:12.979Z
```

如需詳細資訊和示範，請參閱 [如何使用RDE指令](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/how-to-use.html) 教學影片。

## 重置 {#reset-rde}

重設RDE會移除製作和發佈執行個體中的所有自訂程式碼、設定和內容。 例如，如果已使用RDE來測試特定功能，而且您想要將其重設為預設狀態以測試不同功能，則此選項會很有用。

重設會將RDE設定為最新可用的AEM版本。

<!-- Alexandru: hiding for now, please don't delete

Resetting can be done via [Cloud Manager](#reset-the-rde-cloud-manager) or via the [command line](#reset-the-rde-command-line). Resetting takes a few minutes and all existing content and code will be deleted from the RDE.

>[NOTE!]
>
>You must be assigned the Cloud Manager Developer role in order to be able to use the reset feature. If not, a reset action will result in an error.

### Reset the RDE via Command Line {#reset-the-rde-command-line}

You can reset the RDE and return it to a default state by running:

`aio aem:rde:reset`

This usually takes a few minutes. Use the [status command](#checking-rde-status) to check when the environment is ready again.

### Reset the RDE in Cloud Manager {#reset-the-rde-cloud-manager} -->

您可以使用Cloud Manager透過以下步驟重設您的RDE：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 按一下要重設RDE的程式。

1. 在&#x200B;**概述**&#x200B;页面中，单击屏幕顶部的&#x200B;**环境**&#x200B;选项卡。

   ![“环境”信息卡](/help/implementing/cloud-manager/assets/environments-tab2.png)

   * 或者，单击&#x200B;**环境**&#x200B;信息卡上的&#x200B;**全部显示**&#x200B;按钮，直接跳转到&#x200B;**环境**&#x200B;选项卡。

      ![显示所有选项](/help/implementing/cloud-manager/assets/environment-showall.png)

1. 此 **環境** 視窗會開啟並列出該計畫的所有環境。

   ![“环境”选项卡](/help/implementing/cloud-manager/assets/environments-tab-populated.png)

1. 按一下要重設的RDE的省略符號按鈕，然後選取 **重設**.

   ![查看环境详细信息](/help/implementing/cloud-manager/assets/rde-reset.png)

1. 按一下以確認您要重設RDE **重設** 在對話方塊中。

   ![確認重設](/help/implementing/cloud-manager/assets/rde-reset-confirm.png)

1. Cloud Manager會透過橫幅通知確認重設程式已開始。

   ![重設橫幅通知](/help/implementing/cloud-manager/assets/rde-reset-banner.png)

RDE重設程式啟動後，通常需要幾分鐘才能完成，並讓環境恢復到其預設狀態。 您可以隨時在中檢視重設程式的狀態 **狀態** 的欄 **環境** 卡片或 **環境** 視窗。

![RDE重設狀態](/help/implementing/cloud-manager/assets/rde-reset-status-environments-card.png)

您也可以使用省略符號按鈕直接從重設RDE **環境** 卡在上 **概觀** 頁面。

![從環境卡重設RDE](/help/implementing/cloud-manager/assets/rde-reset-environments-card.png)

有關如何使用Cloud Manager管理環境的詳細資訊，請參閱 [Cloud Manager檔案。](/help/implementing/cloud-manager/manage-environments.md)

## 运行模式 {#runmodes}

您可以在資料夾名稱上使用尾碼來套用RDE特定的OSGI設定，如下面的範例所示：

* `config.rde`
* `config.author.rde`
* `config.publish.rde`

請參閱 [runmode檔案](/help/implementing/deploying/overview.md#runmodes) 以取得關於執行模式的一般資訊。

>[!NOTE]
>
>RDE OSGI設定是唯一的，因為它會繼承套件所宣告的任何OSGI屬性的值， `dev` 執行模式。

RDE與其他環境不同，因為其內容可以安裝在/apps下的install.rde資料夾（或install.author.rde或install.publish.rde）中。 這可讓您使用命令列工具將內容提交到Git並將其傳送到RDE。

## 填入內容 {#populating-content}

重設RDE時，會移除所有內容，因此如有需要，必須執行明確動作以新增內容。 作為最佳實務，請考慮組合一組內容以用作在RDE中驗證或偵錯功能的測試內容。 有幾種可能的策略可將該內容填入RDE：

1. 使用命令列工具將內容套件明確同步到RDE

1. 將範例內容放入/apps下的install.rde資料夾內並提交Git中，然後使用命令列工具將整體內容套件同步到RDE。

1. 使用 [內容複製工具](/help/implementing/developing/tools/content-copy.md) 從prod、stage或dev環境，或從其他RDE複製已定義的內容集。

1. 使用封裝管理員

請注意，同步內容套件時限製為1GB。

## 日志记录 {#logging}

記錄層級可藉由修改OSGi設定來設定。 檢查 [檔案](/help/implementing/developing/introduction/logging.md) 以取得詳細資訊。

## RDE與雲端開發環境有何不同？ {#how-are-rds-different-from-cloud-development-environments}

雖然RDE在許多方面類似於雲端開發環境，但為了允許快速同步程式碼，有一些細微的架構差異。 將程式碼傳入RDE的機制不同 — 對於RDE，一個會從本機開發環境同步程式碼，而對於雲端開發環境，一個會透過Cloud Manager部署程式碼。

基於這些原因，建議您在RDE環境中驗證程式碼後，使用非生產管道將程式碼部署到雲端開發環境。 最後，在使用生產管道部署之前測試計畫碼。

另請注意下列考量事項：

* RDE不包含預覽階層
* RDE目前不支援檢視和偵錯使用Cloud Manager前端管道部署的前端計畫碼。
* RDE目前不支援發行前通道。


## 我需要多少個RDE？ {#how-many-rds-do-i-need}

RDE適用於每個已授權的解決方案，而Adobe也提供其他RDE，這些可授權用於生產（非沙箱）計畫。

所需的RDE數目取決於組織的組成與處理。 最具彈性的模式是組織為每位AEM Cloud Service開發人員購買專屬的RDE。 在此模型中，每個開發人員都可以在RDE上測試他們的計畫碼，而無需與其他團隊成員就RDE環境是否可用進行協調。

在另一個極端，具有單一RDE的團隊可以使用內部流程來協調哪些開發人員可以在給定時間使用環境。 這有可能是當開發人員達到中繼功能里程碑，並準備好在雲端環境中進行驗證時，他們可以快速進行所需的變更。

中間模式是指組織購買多個RDE，因此使用未使用RDE的可能性較大。 一種策略可能是針對每個Scrum團隊或主要功能分配RDE。 內部程式可用於協調環境的使用。

## AEM FormsCloud Service快速開發環境(RDE)與其他環境有何不同？ {#how-are-forms-rds-different-from-cloud-development-environments}

Forms開發人員可以使用AEM FormsCloud Service快速開發環境來快速開發最適化Forms、工作流程和自訂專案，例如自訂核心元件、與協力廠商系統的整合等等。 AEM FormsCloud Service快速開發環境(RDE)不支援通訊API和需要記錄檔案的功能，例如產生提交調適型表單的記錄檔案。 下列列出的AEM Forms功能不適用於快速開發環境(RDE)：

* 設定最適化表單的記錄檔案
* 在提交最適化表單時或透過工作流程步驟產生記錄檔案
* 透過電子郵件提交動作或工作流程中的電子郵件步驟將記錄檔案作為附件傳送
* 在最適化表單或工作流程步驟中使用Adobe Sign
* 通訊API

>[!NOTE]
>
> 快速開發環境(RDE)的UI和Forms的其他Cloud Service環境之間沒有差異。 所有與記錄檔案相關的選項（例如為最適化表單選擇記錄檔案範本）會繼續出現在UI中。 這些環境沒有通訊API和記錄檔案功能來測試這些選項。 因此，當您選擇需要通訊API或記錄檔案功能的任何選項時，不會執行任何動作，且會顯示或傳回錯誤訊息。

## rde教學課程

若要瞭解AEMas a Cloud Service中的RDE，請參閱 [示範如何設定、使用及開發生命週期的影片教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/developing/rde/overview.html)
