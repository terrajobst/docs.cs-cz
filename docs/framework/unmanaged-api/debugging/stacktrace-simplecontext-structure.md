---
title: StackTrace_SimpleContext – struktura
ms.date: 03/30/2017
api_name:
- StackTrace_SimpleContext
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- SimpleContext
helpviewer_keywords:
- SimpleContext structure [.NET Framework debugging]
- StackTrace_SimpleContext structure [.NET Framework debugging]
ms.assetid: d4cef11f-a8ca-49bc-a1b8-6631f9e28f3e
topic_type:
- apiref
ms.openlocfilehash: c81a5787eb06971e3d52aff5d1c1154a72564daf
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/28/2020
ms.locfileid: "76790338"
---
# <a name="stacktrace_simplecontext-structure"></a>StackTrace_SimpleContext – struktura
Poskytuje jednoduchý kontext, který lze použít místo úplné `CONTEXT` struktury.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
struct StackTrace_SimpleContext  
{  
    ULONG64 StackOffset;       // ESP on x86  
    ULONG64 FrameOffset;       // EBP on x86  
    ULONG64 InstructionOffset; // EIP on x86  
};  
```  
  
## <a name="members"></a>Členové  
  
|Člen|Popis|  
|------------|-----------------|  
|`StackOffset`|Ukazatel zásobníku nebo ukazatel na vložení zásobníku (ESP) na platformách x86.|  
|`FrameOffset`|Posun snímku nebo EBP registr na platformách x86.|  
|`InstructionOffset`|Ukazatel na instrukci nebo ukazatel na instrukci ENTER (EIP) na platformách x86.|  
  
## <a name="remarks"></a>Poznámky  
 Vzhledem k tomu, že funkce trasování zásobníku obvykle potřebují vracet pouze adresu, posun snímku a adresu zásobníku, můžete místo velké `CONTEXT` struktury použít `SimpleContext` strukturu.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Hlavička:** SOS_Stacktrace. h  
  
 **Verze .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [Struktury pro ladění](debugging-structures.md)
- [Ladění](index.md)
