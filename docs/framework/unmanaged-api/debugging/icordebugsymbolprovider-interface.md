---
title: ICorDebugSymbolProvider – rozhraní
ms.date: 03/30/2017
ms.assetid: 85b24196-b6c6-4bda-9de3-47180bd6ff96
ms.openlocfilehash: 6f7a8a2b12c047b956a3b6e85fe8365e0360b3f2
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76791533"
---
# <a name="icordebugsymbolprovider-interface"></a>ICorDebugSymbolProvider – rozhraní
Poskytuje metody, které lze použít k načtení informací o symbolech ladění.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Popis|  
|------------|-----------------|  
|[GetAssemblyImageBytes – metoda](icordebugsymbolprovider-getassemblyimagebytes-method.md)|Načte data ze sloučeného sestavení s ohledem na relativní virtuální adresu (RVA) ve sloučeném sestavení.|  
|[GetAssemblyImageMetadata – metoda](icordebugsymbolprovider-getassemblyimagemetadata-method.md)|Vrátí metadata ze sloučeného sestavení.|  
|[GetCodeRange – metoda](icordebugsymbolprovider-getcoderange-method.md)|Získá počáteční adresu a velikost metody dané relativní virtuální adresy (RVA) v metodě.|  
|[GetInstanceFieldSymbols – metoda](icordebugsymbolprovider-getinstancefieldsymbols-method.md)|Načte symboly pole instance, které odpovídají token TypeSpec podpisu.|  
|[GetMergedAssemblyRecords – metoda](icordebugsymbolprovider-getmergedassemblyrecords-method.md)|Získá záznamy symbolů pro všechna Sloučená sestavení.|  
|[GetMethodLocalSymbols – metoda](icordebugsymbolprovider-getmethodlocalsymbols-method.md)|Načte místní symboly metody s relativní virtuální adresou (RVA) dané metody.|  
|[GetMethodParameterSymbols – metoda](icordebugsymbolprovider-getmethodparametersymbols-method.md)|Načte symboly parametrů metody vzhledem k relativní virtuální adrese (RVA) dané metody.|  
|[GetMethodProps – metoda](icordebugsymbolprovider-getmethodprops-method.md)|Vrátí informace o vlastnostech metody, jako je token metadat metody a informace o jeho obecných parametrech, s ohledem na relativní virtuální adresu (RVA) v této metodě.|  
|[GetObjectSize – metoda](icordebugsymbolprovider-getobjectsize-method.md)|Vrátí velikost objektu objektu na základě jeho signatury token TypeSpec.|  
|[GetStaticFieldSymbols – metoda](icordebugsymbolprovider-getstaticfieldsymbols-method.md)|Získá symboly statického pole, které odpovídají token TypeSpec podpisu.|  
|[GetTypeProps – metoda](icordebugsymbolprovider-gettypeprops-method.md)|Vrátí informace o vlastnostech typu, jako je například počet podpisů svých obecných parametrů, s ohledem na relativní virtuální adresu (RVA) v tabulce vtable.|  
  
## <a name="remarks"></a>Poznámky  
  
> [!NOTE]
> Toto rozhraní je dostupné jenom pro .NET Native. Pokud implementujete Toto rozhraní pro ICorDebug scénáře mimo .NET Native, modul CLR (Common Language Runtime) bude toto rozhraní ignorovat.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorDebug. idl, CorDebug. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [Rozhraní pro ladění](debugging-interfaces.md)
- [Ladění](index.md)
