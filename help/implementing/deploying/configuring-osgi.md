---
title: 为Adobe Experience Manager配置OSGi作为Cloud Service
description: '具有密钥值和环境特定值的OSGi配置 '
feature: 部署
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: b28202a4e133f046b50477c07eb5a37271532c90
workflow-type: tm+mt
source-wordcount: '2927'
ht-degree: 0%

---

# 为Adobe Experience Manager配置OSGi作为Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[](https://www.osgi.org/) OSG是Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。它用于控制AEM及其配置的复合包。

OSGi提供了标准化的基元，这些基元允许从可重用的小型协作组件构建应用程序。 这些组件可以组合成一个应用程序并进行部署。 这样可以轻松管理OSGi包，因为可以单独停止、安装和启动这些包。 互依关系会自动处理。 每个OSGi组件都包含在各种包中的一个包中。 有关更多信息，请参阅[OSGi规范](https://www.osgi.org/Specifications/HomePage)。

您可以通过AEM代码项目中的配置文件来管理OSGi组件的配置设置。

## OSGi配置文件 {#osgi-configuration-files}

配置更改在AEM Project的代码包(`ui.apps`)中定义为运行模式特定配置文件夹下的配置文件(`.cfg.json`):

`/apps/example/config.<runmode>`

OSGi配置文件的格式基于JSON，使用Apache Sling项目定义的`.cfg.json`格式。

OSGi配置通过OSGi组件的永久标识(PID)来定位OSGi组件，该标识默认为OSGi组件的Java™类名称。 例如，为通过以下方式实施的OSGi服务提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi配置文件在以下位置定义：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循cfg.json OSGi配置格式。

>[!NOTE]
>
>以前版本的AEM支持使用不同文件格式（如.cfg.、.config和XML sling:OsgiConfig资源定义）的OSGi配置文件。 这些格式已由cfg.json OSGi配置格式取代。

## 运行模式分辨率 {#runmode-resolution}

使用运行模式，可以将特定OSGi配置定位到特定AEM实例。 要使用运行模式，请在`/apps/example`下创建配置文件夹（例如，您的项目名称），格式为：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果配置文件夹名称中定义的运行模式与AEM使用的运行模式匹配，则会使用此类文件夹中的任何OSGi配置。

例如，如果AEM使用运行模式创作和开发，则会应用`/apps/example/config.author/`和`/apps/example/config.author.dev/`中的配置节点，而不应用`/apps/example/config.publish/`和`/apps/example/config.author.stage/`中的配置节点。

如果同一PID的多个配置适用，则应用匹配运行模式数目最多的配置。

此规则的粒度处于PID级别。 这意味着您不能在`/apps/example/config.author/`中为同一PID定义某些属性，而在`/apps/example/config.author.dev/`中为同一PID定义更多特定属性。 具有最大匹配运行模式数的配置将对整个PID有效。

>[!NOTE]
>
>`config.preview` OSGI配置文件夹&#x200B;**不能以与声明`config.publish`文件夹相同的方式声明**。 预览层而是会从发布层的值继承其OSGI配置。

在本地开发时，可以传递运行模式启动参数，以指示使用哪种运行模式OSGI配置。

## OSGi配置值的类型 {#types-of-osgi-configuration-values}

有三种OSGi配置值，可将Adobe Experience Manager用作Cloud Service。

1. **内联值**，这些值是在OSGi配置中硬编码并存储在Git中的值。例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **密钥值**，出于安全原因，这些值不得存储在Git中。例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **特定于环境的值**，这些值在各个开发环境中有所不同，因此无法按运行模式准确定位(因为在Adobe Experience Manager `dev` 作为Cloud Service中只有一个运行模式)。例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   请注意，单个OSGi配置文件可以结合使用这些配置值类型的任意组合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何选择适当的OSGi配置值类型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常见用例使用内联OSGi配置值。 特定于环境的配置仅用于开发环境中值不同的特定用例。

![](assets/choose-configuration-value-type_res1.png)

特定于环境的配置扩展了包含内联值的传统静态定义OSGi配置，从而提供了通过Cloud Manager API在外部管理OSGi配置值的功能。 与将值抽象为特定于环境的配置相比，何时应使用通用的和传统的方法（定义内联值并将其存储在Git中），这一点非常重要。

以下指南介绍了何时使用非机密和机密环境特定配置：

### 何时使用内联配置值 {#when-to-use-inline-configuration-values}

内联配置值被视为标准方法，应尽可能使用。 内联配置具有以下优势：

* 它们由Git中的管理和版本历史记录进行维护
* 值会隐式绑定到代码部署
* 它们不需要任何额外的部署考虑事项或协调

每当定义OSGi配置值时，请以内联值开头，并在用例中必要时只选择机密或特定于环境的配置。

### 何时使用非机密环境特定的配置值 {#when-to-use-non-secret-environment-specific-configuration-values}

当预览层的值不同或开发环境不同时，仅将特定于环境的配置(`$[env:ENV_VAR_NAME]`)用于非机密配置值。 这包括本地开发实例和任何作为Cloud Service开发环境的Adobe Experience Manager。 除了为预览层设置唯一值之外，请避免将Adobe Experience Manager的非机密环境特定配置用作Cloud Service暂存或生产环境。

* 仅对发布层和预览层之间存在差异的配置值，或对于开发环境（包括本地开发实例）之间存在差异的值，使用非机密环境特定配置。
* 除了预览层需要与发布层不同的情况外，在OSGi配置中为暂存值和生产非机密值使用标准内联值。 关于此问题，不建议使用特定于环境的配置来便于在运行时对暂存和生产环境进行配置更改；应通过源代码管理引入这些更改。

### 何时使用特定于环境的机密配置值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as aCloud Service要求将特定于环境的配置(`$[secret:SECRET_VAR_NAME]`)用于任何秘密OSGi配置值，例如密码、专用API密钥，或出于安全原因无法存储在Git中的任何其他值。

使用特定于密钥环境的配置，将机密值存储在所有Adobe Experience Manager作为Cloud Service环境（包括暂存和生产环境）上。

## 创建OSGi配置 {#creating-sogi-configurations}

创建OSGi配置的方法有两种，如下所述。 前一种方法通常用于配置自定义OSGi组件，这些组件具有开发人员所知的OSGi属性和值，后一种方法则用于AEM提供的OSGi组件。

### 编写OSGi配置 {#writing-osgi-configurations}

JSON格式的OSGi配置文件可以直接手动写入AEM项目。 这通常是为知名OSGi组件创建OSGi配置的最快捷方式，尤其是由定义配置的相同开发人员设计和开发的自定义OSGi组件。 此方法还可用于在不同运行模式文件夹中复制/粘贴和更新同一OSGi组件的配置。

1. 在IDE中，打开`ui.apps`项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)，该文件夹定位新OSGi配置需要生效的运行模式
1. 在此配置文件夹中，创建一个新的`<PID>.cfg.json`文件。 PID是OSGi组件的永久标识，通常是OSGi组件实现的全类名称。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
请注意，OSGi配置工厂文件名使用命 `<PID>-<factory-name>.cfg.json` 名约定
1. 打开新的`.cfg.json`文件，并按照[JSON OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1)定义OSGi属性和值对的键/值组合。
1. 保存对新`.cfg.json`文件所做的更改
1. 将新的OSGi配置文件添加到Git并将其提交到Git

### 使用AEM SDK快速入门生成OSGi配置 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK快速入门Jar的AEM Web Console可用于配置OSGi组件，以及将OSGi配置导出为JSON。 这对于配置AEM提供的OSGi组件非常有用，因为开发人员在AEM项目中定义OSGi配置时可能无法很好地了解这些组件的OSGi属性及其值格式。

>[!NOTE]
>
>AEM Web控制台的配置UI会将`.cfg.json`文件写入存储库。 因此，当AEM项目定义的OSGi配置可能与生成的配置不同时，为避免在本地开发期间出现潜在的意外行为，请注意这一点。

1. 以管理员用户身份登录到AEM SDK快速入门Jar的AEM Web控制台
1. 导航到OSGi >配置
1. 要配置，请找到OSGi组件并点按其标题以进行编辑
   ![OSGi配置](./assets/configuring-osgi/configuration.png)
1. 根据需要通过Web UI编辑OSGi配置属性值
1. 将永久身份(PID)记录到安全位置。 以后将使用它生成OSGi配置JSON
1. 点按保存
1. 导航到OSGi > OSGi安装程序配置打印机
1. 在步骤5中复制的PID中粘贴，确保将序列化格式设置为“OSGi配置器JSON”
1. 点按打印
1. JSON格式的OSGi配置将显示在序列化配置属性部分中
   ![OSGi安装程序配置打印机](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，打开`ui.apps`项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)，该文件夹定位新OSGi配置需要生效的运行模式。
1. 在此配置文件夹中，创建一个新的`<PID>.cfg.json`文件。 PID与步骤5中的值相同。
1. 将步骤10中的序列化配置属性粘贴到`.cfg.json`文件中。
1. 将更改保存到新的`.cfg.json`文件。
1. 将新的OSGi配置文件添加到Git并将其提交到Git。


## OSGi配置属性格式 {#osgi-configuration-property-formats}

### 内联值 {#inline-values}

内联值采用标准JSON语法，以标准名称 — 值对格式设置。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 特定于环境的配置值 {#environment-specific-configuration-values}

OSGi配置应为要根据环境定义的变量分配一个占位符：

```
use $[env:ENV_VAR_NAME]
```

客户应仅将此技术用于与其自定义代码相关的OSGI配置属性；不得使用它覆盖Adobe定义的OSGI配置。

>[!NOTE]
>
>占位符不能用在[repoint语句](/help/implementing/deploying/overview.md#repoinit)中。

### 密钥配置值 {#secret-configuration-values}

OSGi配置应为要根据环境定义的密钥分配一个占位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 变量命名 {#variable-naming}

以下内容适用于特定于环境的配置值和密钥配置值。

变量名称必须遵循以下规则：

* 最小长度：2
* 最大长度：100
* 必须匹配正则表达式：`[a-zA-Z_][a-zA-Z_0-9]*`

变量的值不得超过2,048个字符。

>[!NOTE]
>
>前缀为`INTERNAL_`的变量名称由Adobe保留。 任何以此前缀开头的客户集变量都将被忽略。

### 默认值 {#default-values}

以下内容适用于特定于环境的配置值和密钥配置值。

如果未设置每个环境的值，则在运行时不会替换占位符，并且由于未发生插值而保留原位。 要避免这种情况，可以使用以下语法在占位符中提供默认值：

```
$[env:ENV_VAR_NAME;default=<value>]
```

如果提供了默认值，则占位符将替换为每个环境的值（如果提供）或提供的默认值。

### 地方发展 {#local-development}

以下内容适用于特定于环境的配置值和密钥配置值。

变量可以在本地环境中定义，以便本地AEM在运行时提取它们。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建议编写一个简单的bash脚本，该脚本可设置配置中使用的环境变量，并在启动AEM之前执行该变量。 诸如[https://direnv.net/](https://direnv.net/)之类的工具有助于简化此方法。 根据值的类型，如果可以在每个人之间共享，则可能会将它们签入到源代码管理中。

机密值从文件中读取。 因此，对于使用密钥的每个占位符，必须创建包含密钥值的文本文件。

例如，如果使用`$[secret:server_password]`，则必须创建名为&#x200B;**server_password**&#x200B;的文本文件。 所有这些密钥文件必须存储在同一目录中，并且框架属性`org.apache.felix.configadmin.plugin.interpolation.secretsdir`必须使用该本地目录进行配置。

### 创作配置与发布配置 {#author-vs-publish-configuration}

如果OSGi属性要求创作值与发布值不同，则：

* 必须使用单独的`config.author`和`config.publish` OSGi文件夹，如[运行模式分辨率部分](#runmode-resolution)中所述。
* 创建独立变量名称时，应使用以下两个选项：
   * 第一个选项，建议使用：在声明为定义不同值的所有OSGi文件夹（如`config.author`和`config.publish`）中，使用相同的变量名称。 例如
      `$[env:ENV_VAR_NAME;default=<value>]`，其中默认值对应于该层（创作或发布）的默认值。通过[Cloud Manager API](#cloud-manager-api-format-for-setting-properties)或通过客户端设置环境变量时，请根据[ API参考文档](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchEnvironmentVariables)中所述，使用“service”参数区分不同层。 “service”参数将变量的值绑定到相应的OSGi层。 它可以是“作者”、“发布”或“预览”。
   * 第二个选项，用于使用前缀（如`author_<samevariablename>`和`publish_<samevariablename>`）声明不同的变量

### 配置示例 {#configuration-examples}

在以下示例中，除了暂存和生产环境之外，还假设有三个开发环境。

**示例1**

OSGI属性`my_var1`的值对于暂存和生产而言是相同的，但对于三个开发环境中的每个环境，其意图是不同的。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
配置
</td>
<td>
<pre>
{ 
 "my_var1":"val",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

**示例2**

OSGI属性`my_var1`的值对于舞台、生产和三个开发环境中的每个环境都会有所不同。 因此，必须调用Cloud Manager API来为每个开发环境设置`my_var1`的值。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ 
 "my_var1":"val1",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1":"val2",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

**示例3**

其意图是使OSGi属性`my_var1`的值在暂存、生产和其中一个开发环境中相同，但在其他两个开发环境中不同。 在这种情况下，必须调用Cloud Manager API ，以便为每个开发环境设置值`my_var1`，包括为与暂存环境和生产环境具有相同值的开发环境设置值。 它将不会继承文件夹&#x200B;**config**&#x200B;中设置的值。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
配置
</td>
<td>
<pre>
{ 
 "my_var1":"val1",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" :"$[env:my_var1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

实现此目的的另一种方法是在config.dev文件夹中设置替换令牌的默认值，使其与&#x200B;**config**&#x200B;文件夹中的值相同。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
配置
</td>
<td>
<pre>
{ 
 "my_var1":"val1",
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1":"$[env:my_var1;default=val1]"
 "my_var2":"abc",
 "my_var3":500
}
</pre>
</td>
</tr>
</table>

## 用于设置属性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

请参阅[此页面](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) ，了解如何配置API。
>[!NOTE]
>
>确保使用的Cloud Manager API已分配角色“部署管理器 — Cloud Service”。 其他角色无法执行下面所有命令。

### 通过API设置值 {#setting-values-via-api}

调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟时间。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>默认变量不是通过API设置的，而是通过OSGi属性本身来设置。
>
>有关详细信息，请参阅[此页面](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)。

### 通过API获取值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

有关详细信息，请参阅[此页面](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables)。

### 通过API删除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

要删除变量，请将其包含为空值。

有关详细信息，请参阅[此页面](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables)。

### 通过命令行获取值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 通过命令行设置值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 通过命令行删除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>有关如何使用Cloud Manager插件配置Adobe I/OCLI值的详细信息，请参阅[此页面](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

### 变量数 {#number-of-variables}

每个环境最多可声明200个变量。

## 有关密钥和特定于环境的配置值的部署注意事项 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由于特定于密钥和环境的配置值位于Git之外，因此不是正式的Adobe Experience Manager(作为Cloud Service部署机制)的一部分，因此客户应该将管理、管理和集成到Adobe Experience Manager(作为Cloud Service部署过程)中。

如上所述，调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟时间。 请注意，在常规代码部署期间，Cloud Manager执行的质量门和测试在此过程中不会执行。

通常，客户会先调用API以设置环境变量，然后再在Cloud Manager中部署依赖于这些变量的代码。 在某些情况下，在部署代码后，您可能需要修改现有变量。

>[!NOTE]
>
>根据当时正在执行端到端管道的哪一部分，使用管道(AEM更新或客户部署)时，API可能会失败。 错误响应将指示请求未成功，但不会指示具体原因。

在某些情况下，计划客户代码部署会依赖现有变量来包含新值，而这与当前代码不符。 如果出于这一考虑，建议采用加法方式对变量进行修改。 要实现此目的，请创建新变量名称，而不只是更改旧变量的值，以便旧代码永远不会引用新值。 然后，当新客户版本看起来稳定时，您可以选择删除旧值。

同样，由于变量的值未进行版本控制，因此回滚代码可能会导致引用导致问题的较新值。 前面提到的加性变量策略在这方面也会有所帮助。

此附加变量策略对于灾难恢复情形也非常有用，在这些情况下，如果需要重新部署前几天的代码，则其引用的变量名称和值仍将保持不变。 这取决于一种策略，即客户在删除这些旧变量之前需要等待几天，否则旧代码将没有适当的变量可引用。
