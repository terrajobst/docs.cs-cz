---
title: Zabezpečení zpráv s anonymním klientem
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cad53e1a-b7c9-4064-bc87-508c3d1dce49
ms.openlocfilehash: fccdd021e392e6c37615a9091ce13f0e94167246
ms.sourcegitcommit: 09b4090b78f52fd09b0e430cd4b26576f1fdf96e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2020
ms.locfileid: "76212007"
---
# <a name="message-security-with-an-anonymous-client"></a>Zabezpečení zpráv s anonymním klientem

V následujícím scénáři vidíte klient a službu zabezpečený službou Windows Communication Foundation (WCF) zabezpečení zpráv. Cílem návrhu je použít zabezpečení zpráv místo zabezpečení přenosu, aby v budoucnu bylo možné podporovat bohatší model založený na deklaracích. Další informace o používání bohatých deklarací pro autorizaci najdete v tématu [Správa deklarací identity a autorizace pomocí modelu identity](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md).

Ukázkovou aplikaci najdete v tématu [zabezpečení zpráv anonymně](../../../../docs/framework/wcf/samples/message-security-anonymous.md).

![Zabezpečení zpráv pomocí anonymního klienta](../../../../docs/framework/wcf/feature-details/media/b361a565-831c-4c10-90d7-66d8eeece0a1.gif "b361a565-831c-4c10-90d7-66d8eeece0a1")

|Charakteristika|Popis|
|--------------------|-----------------|
|Režim zabezpečení|Zpráva|
|Interoperabilita|Pouze WCF|
|Ověřování (Server)|Počáteční vyjednávání vyžaduje ověření serveru, ale ne ověřování klientů.|
|Ověřování (klient)|Žádné|
|Integrita|Ano, použití sdíleného kontextu zabezpečení|
|Důvěrnost|Ano, použití sdíleného kontextu zabezpečení|
|Doprava|HTTP|

## <a name="service"></a>Service

Následující kód a konfigurace jsou určeny ke spuštění nezávisle. Proveďte jednu z těchto akcí:

- Vytvořte samostatnou službu pomocí kódu bez konfigurace.

- Vytvořte službu pomocí zadané konfigurace, ale nedefinujte žádné koncové body.

### <a name="code"></a>Kód

Následující kód ukazuje, jak vytvořit koncový bod služby, který používá zabezpečení zpráv.

[!code-csharp[C_SecurityScenarios#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#8)]
[!code-vb[C_SecurityScenarios#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#8)]

### <a name="configuration"></a>Konfigurace

Místo kódu lze použít následující konfiguraci. Element chování služby se používá k určení certifikátu, který se používá k ověření služby klientovi. Element Service musí specifikovat chování pomocí atributu `behaviorConfiguration`. Element Binding určuje, že `None`typ přihlašovacích údajů klienta, což umožňuje anonymním klientům používat službu.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior name="ServiceCredentialsBehavior">
          <serviceCredentials>
            <serviceCertificate findValue="contoso.com"
                                storeLocation="LocalMachine"
                                storeName="My" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <services>
      <service behaviorConfiguration="ServiceCredentialsBehavior"
               name="ServiceModel.Calculator">
        <endpoint address="http://localhost/Calculator"
                  binding="wsHttpBinding"
                  bindingConfiguration="WSHttpBinding_ICalculator"
                  name="CalculatorService"
                  contract="ServiceModel.ICalculator" />
      </service>
    </services>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" >
          <security mode="Message">
            <message clientCredentialType="None" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client />
  </system.serviceModel>
</configuration>
```

## <a name="client"></a>Klient

Následující kód a konfigurace jsou určeny ke spuštění nezávisle. Proveďte jednu z těchto akcí:

- Vytvořte samostatného klienta pomocí kódu (a kódu klienta).

- Vytvořte klienta, který nedefinuje žádné adresy koncových bodů. Místo toho použijte konstruktor klienta, který převezme název konfigurace jako argument. Příklad:

    [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
    [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]

### <a name="code"></a>Kód

Následující kód vytvoří instanci klienta. Vazba používá zabezpečení režimu zprávy a typ přihlašovacích údajů klienta je nastaven na hodnotu None.

[!code-csharp[C_SecurityScenarios#15](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#15)]
[!code-vb[C_SecurityScenarios#15](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#15)]

### <a name="configuration"></a>Konfigurace

Následující kód nakonfiguruje klienta.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" >
          <security mode="Message">
            <message clientCredentialType="None" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client>
      <endpoint address="http://machineName/Calculator"
        binding="wsHttpBinding"
        bindingConfiguration="WSHttpBinding_ICalculator"
        contract="ICalculator"
        name="WSHttpBinding_ICalculator">
        <identity>
          <dns value="contoso.com" />
        </identity>
      </endpoint>
    </client>
  </system.serviceModel>
</configuration>
```

## <a name="see-also"></a>Viz také:

- [Přehled zabezpečení](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Zabezpečení distribuované aplikace](../../../../docs/framework/wcf/feature-details/distributed-application-security.md)
- [Zabezpečení zpráv s anonymní metodou](../../../../docs/framework/wcf/samples/message-security-anonymous.md)
- [Identita a ověřování služby](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [Model zabezpečení pro Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
