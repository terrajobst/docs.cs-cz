---
title: Událost Trasování událostí pro Windows výjimky Thrown_V1
ms.date: 03/30/2017
helpviewer_keywords:
- ExceptionThrown_V1 event [.NET Framework]
- ETW, ExceptionThrown_V1 event (CLR)
ms.assetid: 0d3da389-6b7b-40f6-a877-fac546d6019c
ms.openlocfilehash: 80faf6e607755ee79c7ec17f2d7d3d5bdce822b7
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716056"
---
# <a name="exception-thrown_v1-etw-event"></a>Událost Trasování událostí pro Windows výjimky Thrown_V1
Tato událost zachycuje informace o vyvolaných výjimkách.  
  
 Následující tabulka ukazuje klíčové slovo, pod kterým je událost vyvolána, a úroveň události. (Další informace najdete v tématu [klíčová slova a úrovně CLR ETW](clr-etw-keywords-and-levels.md).)  
  
|Klíčové slovo pro vyvolání události|Úroveň|  
|-----------------------------------|-----------|  
|`ExceptionKeyword` (0x8000)|Upozornění (2)|  
  
 V následující tabulce jsou uvedeny informace o události.  
  
|Událost|ID události|Vyvolá se, když|  
|-----------|--------------|-----------------|  
|`ExceptionThrown_V1`|80|Je vyvolána spravovaná výjimka.|  
  
 V následující tabulce jsou uvedena data události.  
  
|Název pole|Datový typ|Popis|  
|----------------|---------------|-----------------|  
|Typ výjimky|win:UnicodeString|Typ výjimky; například `System.NullReferenceException`.|  
|Zpráva o výjimce|win:UnicodeString|Skutečná zpráva výjimky|  
|EIPCodeThrow|win:Pointer|Ukazatel na instrukci, kde došlo k výjimce.|  
|ExceptionHR|Win: UInt32|Výjimka [HRESULT](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).|  
|ExceptionFlags|Win: UInt16|0x01: HasInnerException (viz [události CLR ETW](clr-etw-events.md) v dokumentaci k Visual Basic).<br /><br /> 0x02: IsNestedException.<br /><br /> 0x04: IsRethrownException.<br /><br /> 0x08: IsCorruptedStateException (označuje, že stav procesu je poškozen; viz [zpracování výjimek poškozených stavů](https://docs.microsoft.com/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).<br /><br /> 0x10: IsCLSCompliant (výjimka odvozená od <xref:System.Exception> je kompatibilní se specifikací CLS; v opačném případě není kompatibilní se specifikací CLS).|  
|ClrInstanceID|Win: UInt16|Jedinečné ID pro instanci CLR nebo CoreCLR.|  
  
## <a name="see-also"></a>Viz také:

- [Události Trasování událostí pro Windows v CLR](clr-etw-events.md)
