---
title: ICorProfilerCallback::JITCachedFunctionSearchFinished – metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchFinished
helpviewer_keywords:
- JITCachedFunctionSearchFinished method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchFinished method [.NET Framework profiling]
ms.assetid: 3c325c82-cddd-4b00-b3da-e450c36abf62
topic_type:
- apiref
ms.openlocfilehash: ad155c4efb9f11565eeed8bc0a3540311aca4eb7
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76866270"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchfinished-method"></a>ICorProfilerCallback::JITCachedFunctionSearchFinished – metoda
Upozorní profileru, že vyhledávání skončilo pro funkci, která byla dříve kompilována pomocí generátoru nativních imagí (NGen. exe).  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT JITCachedFunctionSearchFinished(  
    [in] FunctionID        functionId,  
    [in] COR_PRF_JIT_CACHE result);  
```  
  
## <a name="parameters"></a>Parametry

- `functionId`

  \[in] ID funkce, pro kterou bylo hledání provedeno.

- `result`

  \[in] hodnota výčtu [COR_PRF_JIT_CACHE](cor-prf-jit-cache-enumeration.md) , která určuje výsledek hledání.

## <a name="remarks"></a>Poznámky  
 V .NET Framework verze 2,0 nebudou zpětná volání [ICorProfilerCallback:: jitcachedfunctionsearchstarted –](icorprofilercallback-jitcachedfunctionsearchstarted-method.md) a `JITCachedFunctionSearchFinished` pro všechny funkce v normálních bitových kopiích Ngen provedeny. Zpětná volání pro všechny funkce v imagi budou generovat pouze image NGen optimalizované pro Profiler. V důsledku dodatečné režie by měl Profiler vyžádat image NGen optimalizované profilerem jenom v případě, že má v úmyslu použít tato zpětná volání k vynucení funkce JIT just-in-time (JIT). V opačném případě by Profiler měl používat opožděnou strategii pro shromažďování informací o funkcích.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICorProfilerCallback – rozhraní](icorprofilercallback-interface.md)
