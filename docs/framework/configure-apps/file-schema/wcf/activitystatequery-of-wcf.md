---
title: <activityStateQuery>služby WCF
ms.date: 03/30/2017
ms.assetid: d6cdc04b-6f3a-4097-a623-ee4a1be3b5c4
ms.openlocfilehash: 49c507424e813067e1dad9b08167d9661acef36f
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991219"
---
# <a name="activitystatequery-of-wcf"></a>\<activityStateQuery > WCF

Představuje dotaz, který se používá ke sledování změn životního cyklu aktivit, které tvoří instance pracovního postupu. Například můžete chtít sledovat pokaždé, když se aktivita odeslat E-Mail dokončí v instanci pracovního postupu. Tento dotaz je nezbytné pro sledování účastníka přihlásit k odběru objekty záznam stavu aktivity. Dostupné stavy přihlásit k odběru jsou uvedeny v ActivityStates.  
  
Další informace o sledování dotazů profilů najdete v tématu [sledování profilů](../../../windows-workflow-foundation/tracking-profiles.md).

[ **\<> Konfigurace**](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<sledování >** ](tracking-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> profilů**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Profil TrackingProfile >** ](trackingprofile-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> pracovního postupu**](workflow-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<activityStateQueries >** ](activitystatequeries-of-wcf.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<activityStateQuery >**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<tracking>
  <profiles>
    <trackingProfile name="Name">
      <workflow>
        <activityStateQueries>
          <activityStateQuery activityName="String">
            <arguments>
              <argument name="String" />
            </arguments>
            <states>
              <state name="String" />
            </states>
            <variables>
              <variable name="String" />
            </variables>
          </activityStateQuery>
        </activityStateQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  

Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|Název aktivity activityName|Řetězec, který určuje název aktivity k filtrování <xref:System.Activities.Tracking.ActivityStateRecord> instancí na.|  
  
### <a name="child-elements"></a>Podřízené prvky  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<arguments>](../windows-workflow-foundation/arguments.md)|Kolekce argumenty přidružené k tomuto dotazu aktivity.|  
|[\<states>](../windows-workflow-foundation/states.md)|Kolekce elementů konfigurace, které obsahují stavy předplacenému aktivity, pro který by měl vyzařovaného záznamem sledování.|  
|[\<states>](../windows-workflow-foundation/states.md)|Kolekce proměnných spojených s Tento dotaz aktivity.|  
  
### <a name="parent-elements"></a>Nadřazené prvky  
  
|Prvek|Popis|  
|-------------|-----------------|  
|[\<faultPropagationQuery>](../windows-workflow-foundation/faultpropagationquery.md)|Představuje seznam konfigurační prvky, které se používají ke sledování požadavků pro zrušení podřízené aktivity Nadřazená aktivita. Dotaz, je nezbytné pro sledování účastníka přihlásit k odběru zrušit požadavek záznam objekty.|  
  
## <a name="remarks"></a>Poznámky

Jeden jedinečné funkce ActivityStateQuery je schopnost extrahování dat při sledování provádění pracovního postupu. Tímto způsobem další kontext při přístupu k sledování záznamů příspěvek provádění. Můžete použít [ \<argumenty >](../windows-workflow-foundation/arguments.md), [ \<stavy >](../windows-workflow-foundation/states.md) a [ \<>](../windows-workflow-foundation/states.md) prvky pro extrakci jakékoli proměnné nebo argumentu z jakékoli aktivity v pracovním postupu. Následující příklad ukazuje dotaz na stav aktivity, který extrahuje proměnné a argumenty při vygenerování `Closed` záznamu sledování aktivity. Proměnné a argumenty lze extrahovat pouze pomocí ActivityStateRecord, a proto jsou přihlášeni v rámci sledovacího profilu pomocí [ \<> ActivityStateQuery](../windows-workflow-foundation/activitystatequery.md).  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">
  <states>
    <state name="Closed" />
  </states>
  <variables>
    <variable name="FromAddress" />
  </variables>
  <arguments>
    <argument name="Result" />
  </arguments>
</activityStateQuery>
```  
  
## <a name="see-also"></a>Viz také:

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement>
- <xref:System.Activities.Tracking.ActivityStateQuery>
- [Sledování a trasování pracovních postupů](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [Sledování profilů](../../../windows-workflow-foundation/tracking-profiles.md)
