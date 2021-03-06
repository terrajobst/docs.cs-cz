---
title: <backupLists>
ms.date: 03/30/2017
ms.assetid: 593b3390-f65b-4684-ad40-0596b62f0954
ms.openlocfilehash: 5f2bb030d13389e15cb44f1ddff3b8168b4f2140
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2019
ms.locfileid: "70850268"
---
# <a name="backuplists"></a>\<backupLists >
Představuje konfigurační oddíl pro definování sady záložních služeb použitých při zpracování chyb. Každý podřízený element je seznam zálohování, který vytvoří výčet sady koncových bodů, které chcete, aby služba Směrování použila v případě, že není dostupný primární koncový bod. Pokud je první koncový bod v seznamu mimo provoz, směrovací služba se v seznamu automaticky převezme na další.  Díky tomu můžete rychle přidat do své aplikace spolehlivost, aniž byste museli poučit klientské aplikace o tom, jak zpracovávat složité vzory nebo kde jsou nasazené všechny služby.  
  
[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> směrování**](routing.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<backupLists >**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<routing>
  <backupLists>
    <backupList name="String">
      <add endpointName="String" />
    </backupList>
  </backupLists>
</routing>
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
 Žádné  
  
### <a name="child-elements"></a>Podřízené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<Filtrovat >](filter.md)|Obsahuje seznam koncových bodů, které by služba Směrování měla použít pro případ, že primární koncový bod není dostupný. .|  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<> směrování](routing.md)|Představuje konfigurační oddíl pro definování sady směrovacích filtrů, které určují typ Windows Communication Foundation (WCF)<xref:System.ServiceModel.Dispatcher.MessageFilter> , který se má použít při vyhodnocování příchozích zpráv, jakož i směrovací tabulky, které definují cílové koncové body. Odeslat zprávy, když odpovídá filtr.|  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection?displayProperty=nameWithType>
