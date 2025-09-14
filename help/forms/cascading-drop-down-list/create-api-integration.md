---
title: 创建 API 集成
description: 使用自适应Forms表达式可添加自动验证、计算以及打开或关闭部分的可见性。
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 3%

---


# 创建 API 集成

在本教程中，创建了2个API集成

- GetAllCountries返回国家/地区列表
- GetChildren — 返回geonameId所代表的国家或州的直接子项

## GetAllCountries - API集成配置

- API集成配置

   - 显示名称： GetAllCountries→系统中此API的标签。

   - API URL： `https://secure.geonames.org/countryInfoJSON` — 您正在调用的终结点。

   - HTTP方法： GET — 您正在发出一个简单的GET请求。

   - 内容类型：JSON — 响应应为JSON格式。

- 选项:

   - 无需加密（未选中） — 没有超过HTTPS的加密层。

   - 选中在客户端执行 — 调用从客户端/浏览器执行，而不是从服务器端执行。
- 身份验证类型
   - 无 — 因为GeoNames API不需要在标头中使用OAuth或API密钥
- 输入：
   - 输入部分定义发送到API中的内容
   - **用户名** →类型：字符串，在查询中发送，默认值： gbedekar。
   - 每个请求都会在URL中附加？username=gbedekar
- 输出
   - 输出定义要提取和使用JSON响应中的哪些字段。
地理名称响应如下所示：

  ![json-response](assets/geonames-data.png)
   - 从geonames数组内部映射了两个字段：

     geonames[*].geonameId →作为数字

     geonames[*].countryName →作为字符串

     [*]表示它会针对数组中的每个国家/地区重复执行。



![获取所有国家/地区](assets/api-integration.png)


## GetChildren

它会请求GeoNames来获取其geonamesId作为查询参数传递的地点的直接子项

- API集成配置

   - 显示名称： GetAllCountries→系统中此API的标签。

   - API URL： `https://secure.geonames.org/children`→您调用的终结点。

   - HTTP方法： GET→您正在发出一个简单的GET请求。

   - 内容类型：JSON→应使用JSON格式进行响应。

- 选项:

   - “需要加密”未选中→没有超过HTTPS的加密层。

   - 在客户端执行，→检查是否从客户端/浏览器而不是服务器端执行调用。
- 身份验证类型
   - 无 — 因为GeoNames API不需要在标头中使用OAuth或API密钥
- 输入：
   - 定义发送到API中的内容
   - **用户名** →类型：字符串，在查询中发送，默认值： gbedekar。
   - 每个请求都会在URL中附加？username=gbedekar
   - **geonameId** ->类型：字符串。 返回由geonameId表示的国家/州的子项
   - **类型** =>字符串。 将设置为JSON会以JSON格式返回响应。
- 输出
   - 定义将要提取和使用JSON响应中的哪些字段。
地理名称响应如下所示：

  ![json-response](assets/child-elements-data.png)
   - 从geonames数组内部映射了两个字段：

     geonames[*].geonameId →作为数字

     geonames[*].name→为字符串

     [*]表示它会针对数组中的每个国家/地区重复执行。


![get-children](assets/get-children-api-integration.png)
