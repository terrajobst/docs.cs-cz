---
title: <net.pipe>
ms.date: 03/30/2017
ms.assetid: 6a0f0318-f8f6-466c-9fae-199d7274a82e
ms.openlocfilehash: dd984b2ab89060451b1b2d02c324e803766908ce
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397716"
---
# <a name="netpipe"></a>\<> NET. pipe
Určuje nastavení konfigurace pro aktivační službu pojmenovaného kanálu, která spravuje životnost připojení pojmenovaného kanálu a zpracovává požadavky na aktivaci přicházející přes pojmenované kanály.  
  
[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel. Activation >** ](system-servicemodel-activation.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<> NET. pipe**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<configuration>
  <system.serviceModel.activation>
    <net.pipe maxPendingAccepts="Integer"
              maxPendingConnections="Integer"
              receiveTimeout="TimeSpan">
      <allowAccounts>
        <!-- LocalSystem account -->
        <add securityIdentifier="S-1-5-18" />
        <!-- LocalService account -->
        <add securityIdentifier="S-1-5-19" />
        <!-- Administrators account -->
        <add securityIdentifier="S-1-5-20" />
        <!-- Network Service account -->
        <add securityIdentifier="S-1-5-32-544" />
        <!-- IIS_IUSRS account (Vista only) -->
        <add securityIdentifier="S-1-5-32-568" />
      </allowAccounts>
    </net.pipe>
  </system.serviceModel.activation>
</configuration>
```  
  
## <a name="type"></a>type  
 `Type`  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|`maxPendingAccepts`|Celé číslo, které určuje maximální počet nedokončených souběžných přijímajících vláken na koncovém bodu naslouchání pro službu sdílení. Výchozí hodnota je 2.|  
|`maxPendingConnections`|Celé číslo, které určuje maximální počet připojení, které mohou čekat na odeslání. Výchozí hodnota je 100.|  
|`receiveTimeout`|A <xref:System.TimeSpan> určuje časový limit pro čtení dat rámců a provádění odesílání připojení z připojení s podtržením. Výchozí hodnota je "00:00:10".|  
  
### <a name="child-elements"></a>Podřízené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<allowAccounts>](allowaccounts.md)|Kolekce elementů konfigurace, které obsahují `securityIdentifier` atribut pro určení uživatelských účtů pro procesy, které hostují služby WCF, a kterým je udělen přístup k připojení ke službě sdílení.|  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<system.serviceModel.activation>](system-servicemodel-activation.md)|Obsahuje nastavení konfigurace procesu naslouchacího procesu SMSvcHost. exe.|  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Activation.Configuration.NetPipeSection>
