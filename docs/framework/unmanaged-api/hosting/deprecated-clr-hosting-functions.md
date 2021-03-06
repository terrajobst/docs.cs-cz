---
title: Zastaralé funkce hostování CLR
ms.date: 03/30/2017
helpviewer_keywords:
- .NET Framework 1.1, hosting global static functions
- global static functions [.NET Framework hosting], version 2.0
- .NET Framework 2.0, hosting global static functions
- hosting global static functions [.NET Framework], version 2.0
ms.assetid: 91fbbb35-e543-4814-b806-371cebae8c5a
ms.openlocfilehash: 62773ce526b1f21c57ab85a106708589fcf92f6f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73138274"
---
# <a name="deprecated-clr-hosting-functions"></a>Zastaralé funkce hostování CLR
Tato část popisuje nespravované globální statické funkce, které používají starší verze rozhraní API pro hostování.  
  
 S výjimkou funkcí infrastruktury (`_Cor*` funkce), které jsou používány pouze .NET Framework, jsou tyto funkce v .NET Framework 4 zastaraly.  
  
## <a name="activation-functions"></a>Aktivační funkce  
 [ClrCreateManagedInstance – funkce](../../../../docs/framework/unmanaged-api/hosting/clrcreatemanagedinstance-function.md)  
 Zastaralé Vytvoří instanci zadaného spravovaného typu.  
  
 [CoInitializeCor – funkce](../../../../docs/framework/unmanaged-api/hosting/coinitializecor-function.md)  
 Zastaralé. Chcete-li inicializovat modul CLR (Common Language Runtime), použijte buď [CorBindToRuntimeEx –](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) nebo [CorBindToCurrentRuntime –](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md).  
  
 [CoInitializeEE – funkce](../../../../docs/framework/unmanaged-api/hosting/coinitializeee-function.md)  
 Zastaralé Zajišťuje, aby byl spouštěcí modul modulu CLR načten do procesu. Místo toho použijte metodu [ICLRRuntimeHost:: Start](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-start-method.md) .  
  
 [CorBindToCurrentRuntime – funkce](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)  
 Zastaralé Načte modul CLR (Common Language Runtime) do procesu pomocí informací o verzi uložených v souboru XML.  
  
 [CorBindToRuntime – funkce](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)  
 Zastaralé Umožňuje nespravovaným hostitelům načíst modul CLR do procesu.  
  
 [CorBindToRuntimeByCfg – funkce](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)  
 Zastaralé Načte CLR do procesu pomocí informací o verzi načtených ze souboru XML.  
  
 [CorBindToRuntimeEx – funkce](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)  
 Zastaralé Umožňuje nespravovaným hostitelům načíst modul CLR do procesu a umožňuje nastavit příznaky pro určení chování modulu CLR.  
  
 [CorBindToRuntimeHost – funkce](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)  
 Zastaralé Umožňuje hostitelům načíst zadanou verzi modulu CLR do procesu.  
  
 [GetCORRequiredVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/getcorrequiredversion-function.md)  
 Zastaralé Získá požadované číslo verze CLR.  
  
 [GetCORSystemDirectory – funkce](../../../../docs/framework/unmanaged-api/hosting/getcorsystemdirectory-function.md)  
 Zastaralé Vrátí instalační adresář modulu CLR, který je načten do procesu.  
  
 [GetRealProcAddress – funkce](../../../../docs/framework/unmanaged-api/hosting/getrealprocaddress-function.md)  
 Zastaralé Získá adresu zadané funkce, která je exportována z nejnovější nainstalované verze modulu CLR.  
  
 [GetRequestedRuntimeInfo – funkce](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)  
 Zastaralé Získá informace o verzi a adresáři modulu CLR, který požaduje aplikace.  
  
## <a name="clr-version-functions"></a>Funkce verze CLR  
 Funkce v této části vrátí verzi CLR; neaktivují modul CLR.  
  
 [GetCORVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/getcorversion-function.md)  
 Zastaralé Vrátí číslo verze modulu CLR, který je spuštěn v aktuálním procesu.  
  
 [GetFileVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/getfileversion-function.md)  
 Zastaralé Získá informace o verzi CLR zadaného souboru pomocí zadané vyrovnávací paměti.  
  
 [GetRequestedRuntimeVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)  
 Zastaralé Získá číslo verze modulu CLR požadované zadanou aplikací. Pokud tato verze není nainstalovaná, získá nejnovější verzi, která je nainstalovaná před požadovanou verzí.  
  
 [GetRequestedRuntimeVersionForCLSID – funkce](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversionforclsid-function.md)  
 Zastaralé Získá příslušné informace o verzi CLR pro třídu se zadaným identifikátorem CLSID.  
  
 [GetVersionFromProcess – funkce](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)  
 Zastaralé Získá číslo verze modulu CLR, který je spojen se zadaným popisovačem procesu.  
  
 [LockClrVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md)  
 Zastaralé Umožňuje hostiteli určit, která verze modulu CLR bude použita v rámci procesu před explicitním inicializací modulu CLR.  
  
## <a name="hosting-functions"></a>Hostování funkcí  
 [CallFunctionShim – funkce](../../../../docs/framework/unmanaged-api/hosting/callfunctionshim-function.md)  
 Zastaralé Provede volání funkce, která má zadaný název a parametry v zadané knihovně.  
  
 [CoEEShutDownCOM – funkce](../../../../docs/framework/unmanaged-api/hosting/coeeshutdowncom-function.md)  
 Zastaralé Uvolní sestavení modelu COM z procesu.  
  
 [CorExitProcess – funkce](../../../../docs/framework/unmanaged-api/hosting/corexitprocess-function.md)  
 Zastaralé Ukončí aktuální nespravovaný proces.  
  
 [CorLaunchApplication – funkce](../../../../docs/framework/unmanaged-api/hosting/corlaunchapplication-function.md)  
 Zastaralé Spustí aplikaci v zadané síťové cestě s použitím zadaných manifestů a dalších aplikačních dat.  
  
 [CorMarkThreadInThreadPool – funkce](../../../../docs/framework/unmanaged-api/hosting/cormarkthreadinthreadpool-function.md)  
 Zastaralé Označuje aktuálně spuštěné vlákno fondu vláken pro spuštění spravovaného kódu. Od verze .NET Framework 2,0 Tato funkce nemá žádný vliv. Není požadován a lze jej odebrat z vašeho kódu.  
  
 [CoUninitializeCor – funkce](../../../../docs/framework/unmanaged-api/hosting/couninitializecor-function.md)  
 Zastaralé. Modul CLR nelze z procesu uvolnit.  
  
 [CoUninitializeEE – funkce](../../../../docs/framework/unmanaged-api/hosting/couninitializeee-function.md)  
 Zastaralé.  
  
 [CreateDebuggingInterfaceFromVersion – funkce](../../../../docs/framework/unmanaged-api/hosting/createdebugginginterfacefromversion-function.md)  
 Zastaralé Vytvoří objekt [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) na základě zadaných informací o verzi.  
  
 [CreateICeeFileGen – funkce](../../../../docs/framework/unmanaged-api/hosting/createiceefilegen-function.md)  
 Zastaralé Vytvoří objekt [ICeeFileGen –](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md) .  
  
 [DestroyICeeFileGen – funkce](../../../../docs/framework/unmanaged-api/hosting/destroyiceefilegen-function.md)  
 Zastaralé Odstraní objekt [ICeeFileGen –](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md) .  
  
 [FExecuteInAppDomainCallback – ukazatel na funkci](../../../../docs/framework/unmanaged-api/hosting/fexecuteinappdomaincallback-function-pointer.md)  
 Zastaralé Odkazuje na funkci, kterou modul CLR volá ke spuštění spravovaného kódu.  
  
 [FLockClrVersionCallback – ukazatel na funkci](../../../../docs/framework/unmanaged-api/hosting/flockclrversioncallback-function-pointer.md)  
 Zastaralé Odkazuje na funkci, kterou modul CLR volá, aby upozornil hostitele, že se inicializace spustila nebo je dokončená.  
  
 [GetCLRIdentityManager – funkce](../../../../docs/framework/unmanaged-api/hosting/getclridentitymanager-function.md)  
 Zastaralé Získá ukazatel na rozhraní, které umožňuje CLR spravovat identity.  
  
 [LoadLibraryShim – funkce](../../../../docs/framework/unmanaged-api/hosting/loadlibraryshim-function.md)  
 Zastaralé Načte zadanou verzi knihovny DLL .NET Framework.  
  
 [LoadStringRC – funkce](../../../../docs/framework/unmanaged-api/hosting/loadstringrc-function.md)  
 Zastaralé Přeloží hodnotu HRESULT na chybovou zprávu pomocí výchozí jazykové verze aktuálního vlákna.  
  
 [LoadStringRCEx – funkce](../../../../docs/framework/unmanaged-api/hosting/loadstringrcex-function.md)  
 Zastaralé Přeloží hodnotu HRESULT na příslušnou chybovou zprávu pro zadanou jazykovou verzi.  
  
 [LPOVERLAPPED_COMPLETION_ROUTINE – ukazatel na funkci](../../../../docs/framework/unmanaged-api/hosting/lpoverlapped-completion-routine-function-pointer.md)  
 Zastaralé Odkazuje na funkci, která upozorňuje hostitele, když je dokončeno překrytí (tj. asynchronní) vstupně-výstupní operace se zařízením.  
  
 [LPTHREAD_START_ROUTINE – ukazatel na funkci](../../../../docs/framework/unmanaged-api/hosting/lpthread-start-routine-function-pointer.md)  
 Zastaralé Odkazuje na funkci, která upozorňuje hostitele na spuštění vlákna.  
  
 [RunDll32ShimW – funkce](../../../../docs/framework/unmanaged-api/hosting/rundll32shimw-function.md)  
 Zastaralé Provede zadaný příkaz.  
  
 [WAITORTIMERCALLBACK – ukazatel na funkci](../../../../docs/framework/unmanaged-api/hosting/waitortimercallback-function-pointer.md)  
 Zastaralé Odkazuje na funkci, která upozorňuje hostitele na to, že došlo k signalizaci nebo vypršel časový limit čekání.  
  
## <a name="infrastructure-functions"></a>Funkce infrastruktury  
 Funkce v této části jsou používány pouze .NET Framework.  
  
 [_CorDllMain – funkce](../../../../docs/framework/unmanaged-api/hosting/cordllmain-function.md)  
 Inicializuje modul CLR, vyhledá spravovaný vstupní bod v záhlaví modulu CLR sestavení knihovny DLL a zahájí provádění.  
  
 [_CorExeMain – funkce](../../../../docs/framework/unmanaged-api/hosting/corexemain-function.md)  
 Inicializuje modul CLR, vyhledá spravovaný vstupní bod v záhlaví modulu CLR spustitelného sestavení a zahájí provádění.  
  
 [_CorExeMain2 – funkce](../../../../docs/framework/unmanaged-api/hosting/corexemain2-function.md)  
 Provede vstupní bod v zadaném kódu mapované paměti. Tato funkce je volána zavaděčem operačního systému.  
  
 [_CorImageUnloading – funkce](../../../../docs/framework/unmanaged-api/hosting/corimageunloading-function.md)  
 Upozorní zavaděče na Nenačtené bitové kopie spravovaného modulu.  
  
 [_CorValidateImage – funkce](../../../../docs/framework/unmanaged-api/hosting/corvalidateimage-function.md)  
 Ověří bitové kopie spravovaného modulu a upozorní zavaděče operačního systému poté, co byly načteny.  
  
## <a name="see-also"></a>Viz také:

- [Globální statické funkce .NET Framework 4 pro hostování](../../../../docs/framework/unmanaged-api/hosting/net-framework-4-hosting-global-static-functions.md)
