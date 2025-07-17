---
title: HTML5 Forms的Picture子句支持
description: HTML5 forms支持XFA Picture子句用于显示日期、文本和数字符号的值以及格式化的值。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# HTML5 Forms的Picture子句支持 {#picture-clause-support-for-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5 forms支持XFA Picture子句用于显示日期、文本和数字符号的值以及格式化的值。 支持以下Picture子句表达式：

* 类别（区域设置）{picture-clause} | 类别（区域设置）{picture-clause} | 类别（区域设置）{picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支持Edit Picture子句。 此外，不支持DateTime和Time Picture子句符号。

## 支持的日期字段符号 {#supported-date-field-symbols}

Date Picture子句支持的表达式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* 日期{date Picture Clause symbols}

>[!NOTE]
>
>picture子句的默认模式为{MMM D， YYYY}模式。 如果未应用图案，则使用缺省图案。

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th>解释</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月的1或2位数(1-31)日</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月两位(01-31)的补零日期。<br /> </td>
  </tr>
  <tr>
   <td>周一</td>
   <td>一年中的1或2位数(1-12)月份。<br /> </td>
  </tr>
  <tr>
   <td>毫米</td>
   <td>月份中填充零的两位数(01-12)。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>当前区域设置<br />的缩写月份名称 </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>当前区域设置<br />的完整月份名称 </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>当前区域设置<br />的缩写工作日名称 </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>当前区域设置<br />的完整工作日名称 </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2位数年份，其中00 = 2000,29 = 2029,30 = 1930,99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位数年份<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> 根据设计，HTML5 Forms中的日期字段不支持编辑格式中的`MM-YYYY`模式。 但是，显示格式支持该模式。

## Numeric图片子句 {#numeric-picture-clause}

HTML5表单支持数字图片符号。 但是，PDF forms与HTML Forms之间的支持存在差异。

在&#x200B;**PDF forms**&#x200B;中，一个数字的格式与Picture子句中的符号数无关

在&#x200B;**HTML Forms**&#x200B;中，仅当数字的位数小于Picture子句中的符号数时，才会格式化该数字。

**示例**：考虑使用Picture子句： num{zzz，zzz，zz9}。

在HTML和PDF forms中，数字&#x200B;**10000**&#x200B;的格式均为&#x200B;**10,000**。

在PDF forms中，数字1000000的格式为1,000,000。 但是，在HTML Forms中，该数字的格式仍为1000000。

**HTML Forms**&#x200B;中的Numeric Picture子句支持的表达式包括：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* 数字{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th><strong>解释</strong></th>
   <th>输入解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>输出格式</strong>：一位数。 或者，如果输入数据为空或相应位置有空格，则为零位数。<br /> </td>
   <td>单数字</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>输出格式</strong>：一位数。 或者，如果输入数据为空、空格或对应位置中的零位数，则为空格。<br /> </td>
   <td>一位数或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>输出格式</strong>：一位数。 或者，如果输入数据为空、有空格或对应位置中的零位数，则无意义。<br /> </td>
   <td>一位数或无</td>
  </tr>
  <tr>
   <td>错误</td>
   <td><strong>输出格式</strong>：由指数符号(E)组成的浮点数的指数部分。 后跟一个可选的加号或减号。 后跟指数值。<br /> </td>
   <td>与输出格式设置相同</td>
  </tr>
  <tr>
   <td>CR或cr<br /> </td>
   <td>如果数字为负，则为贷方符号(CR)。 否则什么也没有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>输出格式：数字为负数时为负号。 其他空间。<br /> </td>
   <td>如果数字为负数，则使用负号。 如果数字为正，则使用加号</td>
  </tr>
  <tr>
   <td>V</td>
   <td>当前区域设置的十进制基数。 允许在输入解析时隐含十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>当前区域设置的十进制基数。 允许在输入解析和输出格式化时隐含十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>当前区域设置的十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>， (U+FF0C)</td>
   <td>主要区域设置的分组分隔符</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>主要区域设置的货币符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>主要区域设置的百分比符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>如果数字为负，则使用左括号。 其他空格。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>如果数字为负，则使用右括号。 其他空格。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>制表符</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文本图片子句 {#text-picture-clause}

HTML5 Forms支持以下Text Picture子句表达式：

* text{text Picture clause symbols}

| **符号** | **解释** |
|---|---|
| A | 单个字母字符。 |
| X | 单个字符。 |
| O | 单个字母数字字符。 |
| 0（零） | 单个字母数字字符。 |
| 9 | 一位数字。 |
