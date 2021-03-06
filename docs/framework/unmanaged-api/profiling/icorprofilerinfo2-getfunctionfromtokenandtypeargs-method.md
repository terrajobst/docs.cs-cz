---
title: ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs – metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs
helpviewer_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
- GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: ce8f6aa6-4ebf-4a86-b429-4bbc8af41a8f
topic_type:
- apiref
ms.openlocfilehash: 945cf84e6f6201879514e29a21f7f5462aa33fdb
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76868652"
---
# <a name="icorprofilerinfo2getfunctionfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs – metoda
Získá `FunctionID` funkce pomocí zadaného tokenu metadat, obsahující třídy a hodnot `ClassID` jakýchkoli argumentů typu.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetFunctionFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdMethodDef funcDef,  
    [in] ClassID classId,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] FunctionID* pFunctionID);  
```  
  
## <a name="parameters"></a>Parametry  
 `moduleID`  
 pro ID modulu, ve kterém je funkce umístěna.  
  
 `funcDef`  
 pro Token metadat `mdMethodDef`, který odkazuje na funkci.  
  
 `classId`  
 pro ID obsahující třídy funkce  
  
 `cTypeArgs`  
 pro Počet parametrů typu pro danou funkci. Pro neobecné funkce musí být tato hodnota nula.  
  
 `typeArgs`  
 pro Pole hodnot `ClassID`, z nichž každý je argumentem funkce. Hodnota `typeArgs` může mít hodnotu NULL, pokud je `cTypeArgs` nastavena na hodnotu nula.  
  
 `pFunctionID`  
 mimo Ukazatel na `FunctionID` zadané funkce.  
  
## <a name="remarks"></a>Poznámky  
 Volání metody `GetFunctionFromTokenAndTypeArgs` s metadaty `mdMethodRef` namísto tokenu metadat `mdMethodDef` může mít nepředvídatelné výsledky. Volající by při předávání měli `mdMethodDef` `mdMethodRef` vyřešit.  
  
 Není-li funkce již načtena, volání `GetFunctionFromTokenAndTypeArgs` způsobí nasazování, což je nebezpečná operace v mnoha kontextech. Například volání této metody během načítání modulů nebo typů může vést k nekonečné smyčce, protože modul runtime se pokusí cyklicky načíst věci.  
  
 Obecně platí, že použití `GetFunctionFromTokenAndTypeArgs` se nedoporučuje. Pokud jsou profilery zajímat události pro konkrétní funkci, měly by uložit `ModuleID` a `mdMethodDef` této funkce a pomocí [ICorProfilerInfo2:: GetFunctionInfo2 –](icorprofilerinfo2-getfunctioninfo2-method.md) ověřit, zda daný `FunctionID` má požadovanou funkci.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICorProfilerInfo – rozhraní](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 – rozhraní](icorprofilerinfo2-interface.md)
