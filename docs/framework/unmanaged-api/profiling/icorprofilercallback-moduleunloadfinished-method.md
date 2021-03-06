---
title: ICorProfilerCallback::ModuleUnloadFinished – metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleUnloadFinished
helpviewer_keywords:
- ModuleUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleUnloadFinished method [.NET Framework profiling]
ms.assetid: 185e3327-9f9c-44bc-8a5c-febea9a6bb5b
topic_type:
- apiref
ms.openlocfilehash: b13573d19ab4d8bb655c1e153530dc70173abe82
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76866140"
---
# <a name="icorprofilercallbackmoduleunloadfinished-method"></a>ICorProfilerCallback::ModuleUnloadFinished – metoda
Upozorní profileru, že se dokončilo uvolňování modulu.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT ModuleUnloadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
## <a name="parameters"></a>Parametry  
 `moduleId`  
 pro ID modulu, který byl uvolněn.  
  
 `hrStatus`  
 pro Hodnota HRESULT, která označuje, zda byl modul úspěšně uvolněn.  
  
## <a name="remarks"></a>Poznámky  
 Hodnota `moduleId` není platná pro požadavek na informace po návratu metody [ICorProfilerCallback:: moduleunloadstarted –](icorprofilercallback-moduleunloadstarted-method.md) .  
  
 Některé části uvolňování třídy mohou pokračovat po `ModuleUnloadFinished` zpětného volání. Selhání HRESULT v `hrStatus` označuje selhání. Úspěšnost HRESULT v `hrStatus` však znamená, že první část uvolňování modulu byla úspěšná.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICorProfilerCallback – rozhraní](icorprofilercallback-interface.md)
