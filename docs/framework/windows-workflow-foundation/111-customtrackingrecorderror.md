---
title: 111 – CustomTrackingRecordError
ms.date: 03/30/2017
ms.assetid: d469fb12-e094-4d6c-9b4d-abd7ce0d17da
ms.openlocfilehash: 737d48714020e20fc7b864de4e650ae234a8580e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009757"
---
# <a name="111---customtrackingrecorderror"></a>111 – CustomTrackingRecordError
## <a name="properties"></a>Vlastnosti  
  
|||  
|-|-|  
|ID|111|  
|klíčová slova|UserEvents, EndToEndMonitoring, Troubleshooting, HealthMonitoring, WFTracking|  
|úroveň|Chyba|  
|Kanál|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>Popis  
 Tato událost je vyzařovaného účastník sledování ETW, když aktivita v rámci instance pracovního postupu vysílá CustomTrackingRecord s chyba na úrovni.  
  
## <a name="message"></a>Zpráva  
 Záznam sledování = CustomTrackingRecord, ID instance = %1, číslo záznamu = %2, čas události = %3, název = %4, ActivityName = %5, ID aktivity = %6, ActivityInstanceId = %7, ActivityTypeName = %8, Data = %9, poznámky = % 10, název profilu = % 11  
  
## <a name="details"></a>Podrobnosti  
  
|Název položky dat|Datový typ položky|Popis|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|Id instance pracovního postupu|  
|Číslo záznamu|xs:long|Pořadové číslo emitovaný záznamu|  
|čas události|xs:dateTime|Čas ve standardu UTC, kdy události, protože ho|  
|Název|xs:string|Název CustomTrackingRecord|  
|ActivityName|xs:string|Název aktivity, která CustomTrackingRecord, protože ho|  
|ID aktivity|xs:string|Id aktivity, která CustomTrackingRecord, protože ho|  
|ActivityInstanceId|xs:string|Id instance aktivity, která CustomTrackingRecord, protože ho|  
|ActivityTypeName|xs:string|Název aktivity, která CustomTrackingRecord, protože ho|  
|Data|xs:string|Data, která je sledována s touto událostí.  Hodnoty jsou uloženy v elementu xml ve formátu \<položky >\< název položky = "dataName" type="System.String" > dataValue\</položky > \< /položky >.  Pokud se žádná data sledovat, řetězec obsahuje \<položky / >. Velikost události ETW je omezená velikost vyrovnávací paměti trasování událostí pro Windows nebo max datovou část události trasování událostí pro Windows. Pokud velikost události větší než omezení trasování událostí pro Windows, pak události je rozdělená do odstranit poznámky a že nahradíte hodnotu data s \<položky >...  \< /položky >.  Tyto typy jsou uloženy jako jejich hodnoty vrácené ToString(); String,Char,BOOL,int,short,Long,uint,ushort,ulong,System.Single,float,Double,System.GUID,System.DateTimeOffset,System.DateTime.  Všechny ostatní typy se serializují pomocí System.Runtime.Serialization.NetDataContractSerializer.|  
|Poznámky|xs:string|Poznámky, které byly přidány k této události.  Hodnoty jsou uloženy v elementu xml ve formátu \<položky >\< název položky = "annotationName" type="System.String" > annotationValue\</položky > \< /položky >.  Pokud nejsou zadány žádné poznámky, pak řetězec obsahuje \<položky / >. Velikost události ETW je omezená velikost vyrovnávací paměti trasování událostí pro Windows nebo max datovou část události trasování událostí pro Windows. Pokud velikost události větší než omezení trasování událostí pro Windows, pak události je rozdělená do odstranit poznámky a nahraďte hodnoty anotace s \<položky >...  \< /položky >.|  
|ProfileName|xs:string|Název nebo sledování profil, který je v tomto případě probíhá emitovány|  
|HostReference|xs:string|Hostované webové služby Toto pole jednoznačně identifikuje v hierarchii webové služby.  Jeho formát je definován jako "virtuální cesta aplikace název webu&#124;virtuální cesta služby&#124;ServiceName' Příklad: "Výchozí webový server/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService.|  
|AppDomain|xs:string|Řetězec vrácený funkcí AppDomain.CurrentDomain.FriendlyName.|
