---
title: <comContract>
ms.date: 03/30/2017
ms.assetid: 3f8e1c0c-cfdf-4c79-ac65-c64e9323a51c
ms.openlocfilehash: b499294af71ba230dcf985d4af1d013b1ca260cf
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2019
ms.locfileid: "70850025"
---
# <a name="comcontract"></a>\<comContract>
Určuje kontrakt služby integrace modelu COM+.  
  
[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Konfigurační oddíl comContracts >** ](comcontracts.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<comContract >**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<comContracts>
  <comContract contract="String"
               namespace="String"
               name="String"
               requireSession="Boolean">
    <exposedMethods>
      <exposedMethod name="String" />
    </exposedMethods>
    <userDefinedTypes>
      <userDefinedType name="String"
                       typeLibID="String"
                       typeLibVersion="String"
                       typeDefID="String">
      </userDefinedType>
    </userDefinedTypes>
    <persistableTypes>
      <persistableType id="String"
                       name="String">
      </persistableType>
    </persistableTypes>
  </comContract>
</comContracts>
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|Dodavatele|Řetězec, který obsahuje typ kontraktu.|  
|name|Řetězec, který obsahuje název kontraktu.|  
|– obor názvů|Řetězec, který obsahuje obor názvů kontraktu.|  
|requiresSession|Logická hodnota určující, zda lze kontrakt použít pouze pro vazby s relacemi. Po inicializaci služby Integration runtime zajistí, že toto nastavení je konzistentní s typem vazby, která se má použít. Výjimka je vygenerována v případě, že jedna nebo více vazeb pro kontrakt jsou v konfliktu. Pokud je `false`Tato vlastnost a používá se jednosměrný kanál a existují parametry [out], vygeneruje se taky výjimka.|  
  
### <a name="child-elements"></a>Podřízené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|persistableTypes|Všechny typy, které jsou trvalé.|  
|userDefinedTypes|Kolekce uživatelsky definovaných typů (UDT), které mají být zahrnuty do kontraktu služby.|  
|exposedMethods|Kolekce metod modelu COM+, která je vystavena v případě, že je rozhraní součásti modelu COM vystaveno jako webová služba.|  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|comContracts|Obsahuje kolekci `comContract` prvků.|  
  
## <a name="remarks"></a>Poznámky  
 Kontrakty integrační služby com+ jsou aktuálně omezeny `http://tempuri.org` na obor názvů a název kontraktu je odvozen z doprovodného rozhraní modelu COM. Můžete však zadat alternativy pomocí `comContracts` oddílu a také `comContract` elementu v konfiguračním souboru. Pomocí následující konfigurace můžete například zadat obor názvů, název kontraktu a uživatelsky definované typy, které se mají zahrnout, a další nastavení pro kontrakt služby.  
  
```xml  
<comContracts>
  <comContract contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"
               namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"
               name="_Broker"
               requireSession="true">
    <exposedMethods>
      <exposedMethod name="BuyStock" />
      <exposedMethod name="SellStock" />
      <exposedMethod name="ExecuteTransaction" />
    </exposedMethods>
  </comContract>
</comContracts>
```  
  
 Po inicializaci služby se zadané obory názvů a názvy kontraktů aplikují na vygenerované popisy služby.  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Configuration.ComContractElementCollection>
- <xref:System.ServiceModel.Configuration.ComContractElement>
- [\<comContracts>](comcontracts.md)
- [Integrace s aplikacemi modelu COM+](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [Postupy: Konfigurace nastavení služby modelu COM+](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
