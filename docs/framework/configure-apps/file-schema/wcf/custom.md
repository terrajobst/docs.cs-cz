---
title: <custom>
ms.date: 03/30/2017
ms.assetid: a6f65a00-bd1a-4d4a-955a-fe009ec02ab8
ms.openlocfilehash: 598b341e8b09acd11ba215e6add3adf9e44b2b81
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400456"
---
# <a name="custom"></a>\<vlastní >
Určuje nastavení pro službu Custom peer resolver Service.  
  
[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> vazeb**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<netPeerTcpBinding >** ](netpeertcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> vazby**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> překladače**](resolver.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<vlastní >**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<custom address="Uri"
        resolverType="String">
  <headers/>
  <identity/>
</custom>
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|`address`|Identifikátor URI, který určuje adresu koncového bodu partnerského uzlu, který hostuje službu Custom peer resolver Service.|  
|`resolverType`|Řetězec, který určuje typ služby Custom peer resolver Service.|  
  
### <a name="child-elements"></a>Podřízené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<identity>](identity.md)|Určuje identitu pro vlastní překladače rovnocenných uzlů nakonfigurované s tímto elementem. Tento prvek je typu <xref:System.ServiceModel.Configuration.IdentityElement>.|  
|[\<headers>](headers-element.md)|Kolekce záhlaví adresy používané pro zprávy SOAP, které jsou zpracovávány vlastním překladačem peer.|  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<resolver>](resolver.md)|Peer resolver, který se používá k překladu ID partnerské sítě na sadu adres rovnocenných uzlů, které představují několik uzlů, které se účastní sítě.|  
  
## <a name="remarks"></a>Poznámky  
 Tento prvek definuje základní nastavení pro službu Custom peer resolver Service, včetně adresy koncového bodu partnerského zařízení, který hostuje službu, a všech specifických nastavení vazby. Další informace o vytvoření vlastního překladače najdete v tématu [Přidání vlastního překladače do aplikace PeerChannel](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90)).  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService>
- <xref:System.ServiceModel.PeerResolvers.PeerCustomResolverSettings>
- <xref:System.ServiceModel.Configuration.PeerResolverElement.Custom%2A>
- <xref:System.ServiceModel.Configuration.PeerCustomResolverElement>
- [Překladače partnerských uzlů](../../../wcf/feature-details/peer-resolvers.md)
- [Přidání vlastního překladače do aplikace PeerChannel](https://docs.microsoft.com/previous-versions/ms730105(v=vs.90))
