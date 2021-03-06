---
title: ICorProfilerFunctionControl – rozhraní
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl
helpviewer_keywords:
- ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 4e3d3141-4662-4166-8f05-bc857c1b4216
topic_type:
- apiref
ms.openlocfilehash: 1286ce953c96eb3e3164ba5b209031dd1ec5c453
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76864697"
---
# <a name="icorprofilerfunctioncontrol-interface"></a>ICorProfilerFunctionControl – rozhraní
Poskytuje metody, které umožňují, aby Profiler kódu komunikoval s modulem CLR (Common Language Runtime), který řídí, jak by kompilátor JIT měl generovat kód při rekompilaci konkrétní metody.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Popis|  
|------------|-----------------|  
|[SetCodegenFlags – metoda](icorprofilerfunctioncontrol-setcodegenflags-method.md)|Nastaví jeden nebo více příznaků z výčtu [COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md) pro řízení generování kódu pro rekompilován funkci just-in-time (JIT).|  
|[SetILFunctionBody – metoda](icorprofilerfunctioncontrol-setilfunctionbody-method.md)|Nahrazuje tělo Common Intermediate Language (CIL) metody.|  
|[SetILInstrumentedCodeMap – metoda](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)|Nastaví mapu kódu pro určenou funkci pomocí zadaných položek mapování Common Intermediate Language (CIL).|  
  
## <a name="remarks"></a>Poznámky  
 Rozhraní `ICorProfilerFunctionControl` poskytuje metody pro řízení generování kódu pro jednu rekompilovaný funkce. Profiler získá instanci tohoto rozhraní prostřednictvím zpětného volání [ICorProfilerCallback4:: GetReJITParameters –](icorprofilercallback4-getrejitparameters-method.md) . Každá instance `ICorProfilerFunctionControl` řídí všechny instance jedné funkce.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICorProfilerInfo4 – rozhraní](icorprofilerinfo4-interface.md)
- [Rozhraní pro profilaci](profiling-interfaces.md)
- [EnumJITedFunctions2 – metoda](icorprofilerinfo4-enumjitedfunctions2-method.md)
