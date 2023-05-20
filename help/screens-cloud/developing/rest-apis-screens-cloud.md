---
title: REST API
description: Screensas a Cloud Service提供遵循Siren規格的簡單RESTful API。 請依照本頁面的說明操作，瞭解如何導覽內容結構並傳送命令至環境中的裝置。
exl-id: 2c52583f-0dd9-4fa3-880b-7671442989ae
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---

# REST API {#rest-apis}

AEM Screens提供簡單的RESTful API，其會遵循 [警笛](https://github.com/kevinswiber/siren) 規格。 它可讓您導覽內容結構並傳送命令至環境中的裝置。

此API的存取網址為 [*http://localhost:4502/api/screens.json*](http://localhost:4502/api/screens.json).

## 導覽內容結構 {#navigating-content-structure}

API呼叫傳回的JSON會列出與目前資源相關的實體。 在所列出的自我連結後，這些實體中的每一個都可作為REST資源再次存取。

例如，若要存取示範旗艦位置中的顯示區，您可以呼叫：

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

或使用curl：

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

結果如下：

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

然後，若要存取「單熒幕顯示」，您可以呼叫：

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## 對資源執行動作 {#executing-actions-on-the-resource}

API呼叫傳回的JSON可包含資源上可用的動作清單。

例如，畫面會列出 *broadcast命令* 允許將命令傳送至指派給該顯示的所有裝置的動作。

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

或使用curl：

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***结果:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "title": "",
      "name": "broadcast-command",
      "method": "POST",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "fields": [
        {
          "name": ":operation",
          "value": "broadcast-command",
          "type": "hidden"
        },
        {
          "name": "msg",
          "type": "text"
        }
      ]
    }
  ]
}
```

若要觸發此動作，系統會呼叫：

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&msg=reboot
```

或使用curl：

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&msg=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```
