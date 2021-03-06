---
title: <comContracts>
ms.date: 03/30/2017
ms.assetid: 42e74148-223d-4888-a8ed-1d928527eb09
ms.openlocfilehash: d061d48374a8745dc61e1ca156e4fcbbccee5ef7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919479"
---
# <a name="comcontracts"></a>\<comContracts>
`comContracts` Konfigurační oddíl obsahuje prvky, které umožňují zadat různé vlastnosti smlouvy služby COM+ Integration Service.  
  
## <a name="specifying-namespace-and-contract"></a>Zadání oboru názvů a kontraktu  
 Kontrakty integrační služby com+ jsou aktuálně omezeny `http://tempuri.org` na obor názvů a název kontraktu je odvozen z doprovodného rozhraní modelu COM. Můžete však zadat alternativy pomocí `comContracts` oddílu v konfiguračním souboru.  
  
 Pomocí následující konfigurace můžete například zadat obor názvů a název kontraktu služby a také možnost vyhodnotit využití u vazeb s relacemi.  
  
```xml  
<comContracts>
  <comContract contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"
               namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"
               name="_Broker"
               requireSession="true">
  </comContract>
</comContracts>
```  
  
 Po inicializaci služby se zadané obory názvů a názvy kontraktů aplikují na vygenerované popisy služby.  
  
 Pokud je tato část prázdná, použije se pro inicializaci služby výchozí obor názvů a název kontraktu z doprovodného IDENTIFIKÁTORu rozhraní COM.  
  
 Kromě toho můžete pomocí [ \<elementu prvků exposedMethod >](exposedmethod.md) určit metody com+, které jsou vystaveny v případě, že je rozhraní komponenty modelu COM vystaveno jako webová služba. [ \<> PersistableTypes](persistabletypes.md) můžete použít také k určení trvalých typů, které se používají v integraci. Nakonec můžete pomocí [ \<elementu typu UserDefinedType >](userdefinedtype.md) zahrnout uživatelsky definované typy (UDT), které mají být zahrnuty do kontraktu služby.  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Configuration.ComContractElementCollection>
- <xref:System.ServiceModel.Configuration.ComContractElement>
- [\<Prvků exposedMethod >](exposedmethod.md)
- [\<persistableTypes >](persistabletypes.md)
- [\<userDefinedType>](userdefinedtype.md)
- [\<comContract>](comcontract.md)
- [Integrace s aplikacemi modelu COM+](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [Postupy: Konfigurace nastavení služby modelu COM+](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
