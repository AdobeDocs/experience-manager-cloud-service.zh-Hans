---
title: 记录自定义实施的交易
description: 使用TransactionRecorder API自动记录未作为事务入帐的操作
feature: Adaptive Forms, Foundation Components
exl-id: cb584f78-30af-4a58-be99-843352e8249c
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 16%

---

# 记录自定义实施的交易 {#record-a-transaction-for-custom-implementations}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-osgi/record-transaction-custom-implementation) |
| AEM as a Cloud Service | 本文 |

使用TransactionRecorder API自动记录未作为事务入帐的操作。

您可以使用自定义代码提交PDF表单。 或者，您也可以使用自定义方法提交表单，而不是使用AEM Forms提供的提交方法。 前面提到的AEM Forms API的所有操作和自定义实现都不会计为交易。 AEM Forms提供了一个API [TransactionRecorder](https://javadoc.io/doc/com.adobe.aem/aem-forms-sdk-api/latest/com/adobe/aem/transaction/core/ITransactionRecorder.html)，以将此类操作记录为事务。

要记录事务，请编写[标准sling servlet](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=zh-Hans)并从客户端调用servlet以记录事务。 您可以使用AJAX或任何其他标准方法调用servlet。

## 服务器端代码示例 {#sample-server-sided-code}

您可以使用以下示例代码通过自定义OSGi捆绑包从Java™类运行TransactionRecorder API。

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## 示例客户端代码 {#sample-client-side-code}

您可以使用以下示例代码调用具有`TransactionRecorder`API的servlet。

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 相关文章 {#related-articles}

* [交易报告计费 API](/help/forms/transaction-reports-billable-apis.md)
