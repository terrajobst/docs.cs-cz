---
title: ICorDebugManagedCallback – rozhraní
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback
helpviewer_keywords:
- ICorDebugManagedCallback interface [.NET Framework debugging]
ms.assetid: b47f1d61-c7dc-4196-b926-0b08c94f7041
topic_type:
- apiref
ms.openlocfilehash: 9a33b90bf39103756ab4fd07157739633997fb61
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76788402"
---
# <a name="icordebugmanagedcallback-interface"></a>ICorDebugManagedCallback – rozhraní
Poskytuje metody pro zpětná volání procesu ladicího programu.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Popis|  
|------------|-----------------|  
|[Break – metoda](icordebugmanagedcallback-break-method.md)|Upozorní ladicí program, když se spustí instrukce <xref:System.Reflection.Emit.OpCodes.Break> v datovém proudu kódu.|  
|[Breakpoint – metoda](icordebugmanagedcallback-breakpoint-method.md)|Upozorní ladicí program, když dojde k zarážce.|  
|[BreakpointSetError – metoda](icordebugmanagedcallback-breakpointseterror-method.md)|Oznamuje ladicímu programu, že modul CLR (Common Language Runtime) nedokázal přesně navazovat zarážku, která byla nastavena předtím, než byla funkce kompilována za běhu (just-in-time).|  
|[ControlCTrap – metoda](icordebugmanagedcallback-controlctrap-method.md)|Oznamuje ladicímu programu, že kombinace kláves CTRL + C je zachycena v laděném procesu.|  
|[CreateAppDomain – metoda](icordebugmanagedcallback-createappdomain-method.md)|Oznamuje ladicímu programu, že byla vytvořena doména aplikace.|  
|[CreateProcess – metoda](icordebugmanagedcallback-createprocess-method.md)|Upozorní ladicí program, když byl proces poprvé připojen nebo spuštěn.|  
|[CreateThread – metoda](icordebugmanagedcallback-createthread-method.md)|Oznamuje ladicímu programu, že vlákno zahájilo provádění spravovaného kódu.|  
|[DebuggerError – metoda](icordebugmanagedcallback-debuggererror-method.md)|Oznamuje ladicímu programu, že došlo k chybě při pokusu o zpracování události z CLR.|  
|[EditAndContinueRemap – metoda](icordebugmanagedcallback-editandcontinueremap-method.md)|Zastaralé Oznamuje ladicímu programu, že byla do integrovaného vývojového prostředí odeslána událost přemapování.|  
|[EvalComplete – metoda](icordebugmanagedcallback-evalcomplete-method.md)|Oznamuje ladicímu programu, že bylo dokončeno vyhodnocení.|  
|[EvalException – metoda](icordebugmanagedcallback-evalexception-method.md)|Oznamuje ladicímu programu, že vyhodnocení skončilo neošetřenou výjimkou.|  
|[Exception – metoda](icordebugmanagedcallback-exception-method.md)|Oznamuje ladicímu programu, že byla vyvolána výjimka ze spravovaného kódu.|  
|[ExitAppDomain – metoda](icordebugmanagedcallback-exitappdomain-method.md)|Oznamuje ladicímu programu, že doména aplikace byla ukončena.|  
|[ExitProcess – metoda](icordebugmanagedcallback-exitprocess-method.md)|Oznamuje ladicímu programu, že došlo k ukončení procesu.|  
|[ExitThread – metoda](icordebugmanagedcallback-exitthread-method.md)|Oznamuje ladicímu programu, že bylo ukončeno vlákno, které spustilo spravovaný kód.|  
|[LoadAssembly – metoda](icordebugmanagedcallback-loadassembly-method.md)|Oznamuje ladicímu programu, že bylo úspěšně načteno sestavení CLR.|  
|[LoadClass – metoda](icordebugmanagedcallback-loadclass-method.md)|Oznamuje ladicímu programu, že byla načtena třída.|  
|[LoadModule – metoda](icordebugmanagedcallback-loadmodule-method.md)|Oznamuje ladicímu programu, že modul CLR byl úspěšně načten.|  
|[LogMessage – metoda](icordebugmanagedcallback-logmessage-method.md)|Oznamuje ladicímu programu, že spravované vlákno CLR volalo metodu ve třídě <xref:System.Diagnostics.EventLog> k zaznamenání události.|  
|[LogSwitch – metoda](icordebugmanagedcallback-logswitch-method.md)|Oznamuje ladicímu programu, že spravované vlákno CLR volalo metodu ve třídě <xref:System.Diagnostics.Switch> k vytvoření, úpravě nebo odstranění přepínače ladění/trasování.|  
|[NameChange – metoda](icordebugmanagedcallback-namechange-method.md)|Oznamuje ladicímu programu, že došlo ke změně názvu domény aplikace nebo vlákna.|  
|[StepComplete – metoda](icordebugmanagedcallback-stepcomplete-method.md)|Oznamuje ladicímu programu, že byl krok dokončen.|  
|[UnloadAssembly – metoda](icordebugmanagedcallback-unloadassembly-method.md)|Oznamuje ladicímu programu, že bylo uvolněno sestavení CLR.|  
|[UnloadClass – metoda](icordebugmanagedcallback-unloadclass-method.md)|Oznamuje ladicímu programu, že je třída uvolňována.|  
|[UnloadModule – metoda](icordebugmanagedcallback-unloadmodule-method.md)|Oznamuje ladicímu programu, že byl uvolněn modul CLR (DLL).|  
|[UpdateModuleSymbols – metoda](icordebugmanagedcallback-updatemodulesymbols-method.md)|Oznamuje ladicímu programu, že se změnily symboly modulu CLR.|  
  
## <a name="remarks"></a>Poznámky  
 Všechna zpětná volání jsou serializována, volána ve stejném vlákně a volána s procesem v synchronizovaném stavu.  
  
 Každé implementaci zpětného volání musí volat metodu [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) , aby bylo možné pokračovat v provádění. Pokud `ICorDebugController::Continue` není volána před vrácením zpětného volání, proces zůstane zastaven a žádné další zpětné volání události nebude provedeno, dokud `ICorDebugController::Continue` není volána.  
  
 Ladicí program musí implementovat [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) , pokud ladí aplikace .NET Framework aplikací verze 2,0. Instance `ICorDebugManagedCallback` nebo `ICorDebugManagedCallback2` je předána jako objekt zpětného volání do [ICorDebug:: SetManagedHandler –](icordebug-setmanagedhandler-method.md).  
  
> [!NOTE]
> Toto rozhraní nepodporuje vzdálené volání, a to buď mezi počítačem, nebo mezi procesy.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorDebug. idl, CorDebug. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICorDebug – rozhraní](icordebug-interface.md)
- [ICorDebugManagedCallback2 – rozhraní](icordebugmanagedcallback2-interface.md)
- [Rozhraní pro ladění](debugging-interfaces.md)
