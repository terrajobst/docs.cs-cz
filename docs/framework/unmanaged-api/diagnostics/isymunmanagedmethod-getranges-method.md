---
title: ISymUnmanagedMethod::GetRanges – metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRanges
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRanges
helpviewer_keywords:
- ISymUnmanagedMethod::GetRanges method [.NET Framework debugging]
- GetRanges method [.NET Framework debugging]
ms.assetid: a85283d8-379c-417a-9736-ddeeef9bcf50
topic_type:
- apiref
ms.openlocfilehash: 1f1bd9c33f24847eae4ff7d26c5b996cd34afb72
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448936"
---
# <a name="isymunmanagedmethodgetranges-method"></a>ISymUnmanagedMethod::GetRanges – metoda
Vzhledem k pozici v dokumentu vrátí pole párů počátečního a koncového posunu, které odpovídají rozsahům v rámci této metody, které odpovídají rozsahům jazyka MSIL (Microsoft Intermediate Language), které umístění pokrývá. Pole je pole celých čísel a má formát [Start, end, Start, end]. Počet párů rozsahů je délka pole děleného 2.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT GetRanges(  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32                line,  
    [in]  ULONG32                column,  
    [in]  ULONG32                cRanges,  
    [out] ULONG32                *pcRanges,  
    [out, size_is(cRanges),  
        length_is(*pcRanges)] ULONG32 ranges[]);  
```  
  
## <a name="parameters"></a>Parametry  
 `document`  
 pro Dokument, pro který je požadován posun.  
  
 `line`  
 pro Řádek dokumentu odpovídající rozsahům.  
  
 `column`  
 pro Sloupec dokumentu odpovídající rozsahům  
  
 `cRanges`  
 pro Velikost pole `ranges`.  
  
 `pcRanges`  
 mimo Ukazatel na `ULONG32`, který přijímá velikost vyrovnávací paměti vyžadované k omezení rozsahu.  
  
 `ranges`  
 mimo Ukazatel na vyrovnávací paměť, která přijímá rozsahy.  
  
## <a name="return-value"></a>Návratová hodnota  
 S_OK, pokud je metoda úspěšná; v opačném případě E_FAIL nebo nějaký jiný kód chyby.  
  
## <a name="requirements"></a>Požadavky  
 **Hlavička:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Viz také:

- [ISymUnmanagedMethod – rozhraní](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)
