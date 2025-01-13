---
title: 适用于AEM as a Cloud Service的客户托管密钥
description: 了解如何管理AEM as a Cloud Service的加密密钥
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 为AEM as a Cloud Service设置客户管理的密钥 {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service当前将客户数据存储在Azure Blob Storage和MongoDB中，默认情况下利用提供商管理的加密密钥来保护数据。 虽然这种设置满足了许多组织的安全需求，但受管控行业或那些需要增强数据主权的企业可能会寻求对其加密实践实施更大的控制。 对于优先考虑数据安全性、法规遵从性和管理其加密密钥的组织，客户管理的密钥(CMK)解决方案提供了重要的增强功能。

## 正在解决的问题 {#the-problem-being-solved}

提供商管理的密钥可能会引起金融、医疗和政府等行业企业的担忧，在这些行业，严格的法规要求全面控制数据安全。 如果不能控制关键管理，公司在满足法规遵从性要求、实施定制安全策略以及确保完整的数据主权方面将面临挑战。

客户管理的密钥(CMK)的引入通过使AEM客户能够完全控制其加密密钥，解决了这些问题。 通过通过Microsoft Entra ID（以前称为Azure Active Directory）进行身份验证，AEM CS可安全地连接到客户的Azure Key Vault，从而允许他们管理其加密密钥的生命周期，涵盖密钥创建、轮换和撤销。

CMK具有以下几个优势：

* **增强的安全性：**&#x200B;客户可以确保其加密实践符合特定的安全要求，从而无需担心数据保护问题。
* **法规遵从性灵活性：**&#x200B;如果能够完全控制关键生命周期，企业可以轻松地适应不断演变的法规标准，如GDPR、HIPAA或CCPA ，以确保其法规遵从性状态保持强健。
* **无缝集成：** CMK解决方案直接与AEM CS中的Azure Blob Storage和MongoDB集成，确保不会中断存储操作或可用性，同时为客户提供强大的加密功能。

通过采用CMK ，客户可以增强对其数据安全和加密实践的控制，增强合规性并降低风险，同时继续享有AEM CS的可扩展性和灵活性。

AEM as a Cloud Service允许您自带加密密钥，对静态数据进行加密。 本指南提供了在适用于AEM as a Cloud Service的Azure Key Vault中设置客户管理的密钥(CMK)的步骤。

>[!WARNING]
>
>设置CMK后，无法还原为系统管理的密钥。 您有责任安全地管理您的密钥，并提供对Azure中您的密钥库、密钥和CMK应用程序的访问权限，以防止无法访问您的数据。

还将指导您完成以下步骤来创建和配置所需的基础架构：

1. 设置环境
1. 从Adobe获取应用程序ID
1. 创建新资源组
1. 创建键错误
1. 授予Adobe访问密钥的权限
1. 创建加密密钥

您需要与Adobe共享密钥保管库URL、加密密钥名称以及有关密钥保管库的信息。

## 设置环境 {#setup-your-environment}

Azure命令行界面(CLI)是本指南的唯一要求。 如果尚未安装Azure CLI，请按照[此处](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)的正式安装说明操作。

在继续本指南的其余部分之前，请使用`az login`登录CLI。

>[!NOTE]
>
>虽然本指南使用Azure CLI，但可以通过Azure控制台执行相同的操作。 如果您希望使用Azure控制台，请使用以下命令作为参考。

## 从Adobe获取应用程序ID {#obtain-an-application-id-from-adobe}

Adobe将为您提供本指南其余部分中所需要的Entra应用程序ID。 如果您还没有应用程序ID，请与Adobe联系以获取此ID。

## 创建新资源组 {#create-a-new-resource-group}

在您选择的位置中创建新资源组。

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

如果您已经拥有资源组，请随时改用它。 在本指南的其余部分中，资源组的位置及其名称分别由`$location`和`$resourceGroup`标识。

## 创建密钥存储库 {#create-a-key-vault}

您需要创建一个密钥库来包含您的加密密钥。 密钥保管库必须启用清除保护。 清除保护对于从其他Azure服务加密静态数据是必需的。 还必须启用公共网络访问，以确保Adobe租户可以访问密钥保管库。

>[!IMPORTANT]
>创建禁用了公共网络访问的密钥保管库后，必须从对KeyVault具有网络访问权限的环境中执行所有与密钥保管库相关的操作，如密钥创建或轮换，例如，可以访问该KeyVault的VM。

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## 授予Adobe访问密钥库的权限 {#grant-adone-access-to-the-key-vault}

在此步骤中，您将允许Adobe通过Entra应用程序访问您的密钥保管库。 Entra应用程序的ID应已由Adobe提供。

首先，您必须创建一个附加到Entra应用程序的服务主体，并为其分配&#x200B;**密钥保管库Reader**&#x200B;和&#x200B;**密钥保管库加密用户**&#x200B;角色。 这些角色仅限于本指南中创建的密钥存储库。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## 创建加密密钥 {#create-an-ecryption-key}

最后，您可以在密钥库中创建加密密钥。 请注意，您需要具有&#x200B;**密钥库加密管理人员**&#x200B;角色才能完成此步骤。 如果登录用户没有此角色，请联系您的系统管理员以将此角色授予您，或要求已具有该角色的用户为您完成此步骤。

创建加密密钥需要网络访问密钥保管库。 首先，验证您是否可以访问密钥保管库并继续创建密钥：

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## 共享密钥保管库信息 {#share-the-key-vault-information}

此时，您已准备就绪。 您只需要与Adobe共享一些必需的信息，他将为您配置环境。

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## 撤销关键访问权限的影响 {#implications-of-revoking-key-access}

撤销或禁用对Key Vault、Key或CMK应用程序的访问权限可能会导致严重中断，包括对您平台操作的重大更改。 禁用这些键后，Platform中的数据可能会变得不可访问，并且任何依赖此数据的下游操作都将停止运行。 在对关键配置进行任何更改之前，充分了解下游影响至关重要。

如果您决定撤销Platform对您的数据的访问权限，可以通过从Azure中的密钥保管库中删除与应用程序关联的用户角色来执行此操作。

## 后续步骤 {#next-steps}

联系Adobe并共享：

* 您的密钥库的URL。 您在此步骤中检索了它，并将其保存在`$keyVaultUri`变量中。
* 您的加密密钥的名称。 您已在上一步中创建该键并将其保存在`$keyName`变量中。
* 设置与密钥保管库的连接所需的`$resourceGroup`、`$subscriptionId`和`$tenantId`。

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Private Beta中的客户管理的密钥 {#customer-managed-keys-in-private-beta}

Adobe的工程团队目前正在致力于利用Azure的私有链接来增强CMK的实施。 新实施将允许通过Azure骨干网络共享您的密钥，这归功于Adobe租户和您的密钥库之间的直接私有链接连接。

此增强型实施当前位于Private Beta中，可为同意订阅Private Beta计划并与Adobe工程部密切合作的选定客户启用。 如果您对使用专用链接的Private Beta for CMK感兴趣，请联系Adobe以获取更多信息。
