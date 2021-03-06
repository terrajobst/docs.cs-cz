---
title: <authentication><clientCertificate> elementu
ms.date: 03/30/2017
ms.assetid: 4a55eea2-1826-4026-b911-b7cc9e9c8bfe
ms.openlocfilehash: 99084f6b7afbdd8586ee706cd6ec44b349d81ff2
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398269"
---
# <a name="authentication-of-clientcertificate-element"></a>\<ověřování > \<elementu ClientCertificate >
Určuje chování ověřování pro klientské certifikáty používané službou.  
  
[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> chování**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> chování**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceCredentials >** ](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> clientCertificate**](clientcertificate-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> ověřování**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<authentication customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                includeWindowsGroups="Boolean"
                mapClientCertificateToWindowsAccount="Boolean"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|customCertificateValidatorType|Volitelný řetězec. Typ a sestavení, které slouží k ověření vlastního typu. Tento atribut musí být nastaven, `certificateValidationMode` je-li `Custom`nastavena na hodnotu.|  
|certificateValidationMode|Volitelný výčet. Určuje jeden z režimů používaných k ověření přihlašovacích údajů. Tento atribut je <xref:System.ServiceModel.Security.X509CertificateValidationMode> typu. Je-li <xref:System.ServiceModel.Security.X509CertificateValidationMode.Custom?displayProperty=nameWithType>nastaveno na hodnotu, musí být zadána také. `customCertificateValidator` Výchozí hodnota je <xref:System.ServiceModel.Security.X509CertificateValidationMode.ChainTrust?displayProperty=nameWithType>.|  
|includeWindowsGroups|Volitelná logická hodnota. Určuje, zda jsou skupiny systému Windows zahrnuty v kontextu zabezpečení. Nastavení tohoto atributu na `true` má vliv na výkon, protože má za následek rozšíření celé skupiny. Nastavte tento atribut na `false` , pokud nepotřebujete vytvořit seznam skupin, do kterých uživatel patří.|  
|mapClientCertificateToWindowsAccount|Datového. Určuje, jestli je možné klienta namapovat na identitu Windows pomocí certifikátu. K tomu musí být povolená služba Active Directory.|  
|revocationMode|Volitelný výčet. Jeden z režimů, který slouží ke kontrole seznamů odvolaných certifikátů (RCL). Výchozí hodnota je `Online`. Tato hodnota se při použití zabezpečení přenosu HTTP ignoruje.|  
|trustedStoreLocation|Volitelný výčet. Jedno ze dvou umístění úložiště systému: `LocalMachine` nebo. `CurrentUser` Tato hodnota se používá, když je certifikát služby vyjednán klientovi. Ověřování se provádí pro úložiště **důvěryhodných osob** v zadaném umístění úložiště. Výchozí hodnota je `CurrentUser`.|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType – atribut  
  
|Value|Popis|  
|-----------|-----------------|  
|String|Určuje název typu a sestavení a další data, která se používají k vyhledání typu.|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode – atribut  
  
|Value|Popis|  
|-----------|-----------------|  
|Výčet|Jedna z následujících hodnot: None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom.<br /><br /> Další informace najdete v tématu [práce s certifikáty](../../../wcf/feature-details/working-with-certificates.md).|  
  
## <a name="revocationmode-attribute"></a>revocationMode – atribut  
  
|Value|Popis|  
|-----------|-----------------|  
|Výčet|Jedna z následujících hodnot: Nekontrolujte, online, offline. Další informace najdete v tématu [práce s certifikáty](../../../wcf/feature-details/working-with-certificates.md).|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation – atribut  
  
|Value|Popis|  
|-----------|-----------------|  
|Výčet|Jedna z následujících hodnot: `LocalMachine` nebo. `CurrentUser` Výchozí hodnota je `CurrentUser`. Pokud klientská aplikace běží pod účtem systému, certifikát se obvykle nachází v části `LocalMachine`. Pokud klientská aplikace běží pod uživatelským účtem, bude certifikát typicky v `CurrentUser`.|  
  
### <a name="child-elements"></a>Podřízené elementy  
 Žádné  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<clientCertificate>](clientcertificate-of-servicecredentials.md)|Definuje certifikát X. 509, který se používá k ověření klienta ke službě.|  
  
## <a name="remarks"></a>Poznámky  
 `<authentication>` Prvek odpovídá<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> třídě. Umožňuje vám přizpůsobit způsob ověřování klientů. Můžete nastavit `certificateValidationMode` atribut na `None`, `ChainTrust` `PeerOrChainTrust` ,,`Custom`nebo. `PeerTrust` Ve výchozím nastavení je úroveň nastavena na `ChainTrust`hodnotu, která určuje, že každý certifikát musí být nalezen v hierarchii certifikátů končících *kořenovou autoritou* v horní části řetězce. Toto je nejbezpečnější režim. Můžete také nastavit hodnotu na `PeerOrChainTrust`, což znamená, že jsou přijímány certifikáty vystavené svým držitelem (vztah důvěryhodnosti peering) i certifikáty, které jsou v důvěryhodném řetězci. Tato hodnota se používá při vývoji a ladění klientů a služeb vzhledem k tomu, že certifikáty vystavené svým držitelem nemusejí být zakoupeny důvěryhodnou autoritou. Při nasazování klienta použijte `ChainTrust` místo něj hodnotu.  
  
 Můžete také nastavit hodnotu na `Custom`. Pokud je nastaveno na `Custom` hodnotu, je nutné také `customCertificateValidatorType` nastavit atribut na sestavení a typ použitý k ověření certifikátu. Chcete-li vytvořit vlastní validátor, je nutné dědit z abstraktní <xref:System.IdentityModel.Selectors.X509CertificateValidator> třídy. Další informace najdete v tématu [jak: Vytvořte službu, která využívá vlastní validátor](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)certifikátů.  
  
## <a name="example"></a>Příklad  
 Následující kód Určuje certifikát X. 509 a typ vlastního ověřování v `<authentication>` elementu.  
  
```xml  
<serviceBehaviors>
  <behavior name="myServiceBehavior">
    <clientCertificate>
      <certificate findValue="www.cohowinery.com"
                   storeLocation="CurrentUser"
                   storeName="TrustedPeople"
                   x509FindType="FindByIssuerName" />
      <authentication customCertificateValidatorType="MyTypes.Coho"
                      certificateValidationMode="Custom"
                      revocationMode="Offline"
                      includeWindowsGroups="false"
                      mapClientCertificateToWindowsAccount="true" />
    </clientCertificate>
  </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>
- <xref:System.ServiceModel.Security.X509CertificateValidationMode>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Authentication%2A>
- <xref:System.ServiceModel.Configuration.X509ClientCertificateAuthenticationElement>
- [Chování zabezpečení](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Postupy: Vytvoření služby, která používá vlastní validátor certifikátů](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [Práce s certifikáty](../../../wcf/feature-details/working-with-certificates.md)
