---
title: Implicitní převod z '<typename1>' na '<typename2>' při kopírování hodnoty 'ByRef' parametru '<parametername> zpět na odpovídající argument
ms.date: 07/20/2015
f1_keywords:
- vbc41999
- bc41999
helpviewer_keywords:
- BC41999
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
ms.openlocfilehash: 7ac0e7961e1a039e505c85a35c7c31353ed6578e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661992"
---
# <a name="implicit-conversion-from-typename1-to-typename2-in-copying-the-value-of-byref-parameter-parametername-back-to-the-matching-argument"></a>Implicitní převod z '\<NázevTypu1 > "k"\<NázevTypu2 >' při kopírování hodnoty 'ByRef' parametru '\<parametername > "zpět do odpovídajícího argumentu.
Postup se nazývá se [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) argument jiného typu než jeho odpovídající parametr.  
  
 Pokud předáte argument `ByRef`, Visual Basic někdy kopíruje hodnotu argumentu do místní proměnné v postupu namísto předávání odkazem. V takovém případě se po návratu podle postupu Visual Basic musí potom zkopírujte hodnotu lokální proměnné zpět do argumentu ve volajícím kódu.  
  
 Pokud `ByRef` hodnota argumentu je zkopírován do procedury a argumentu a parametru jsou stejného typu, je nezbytné žádný převod. Ale pokud se typy liší, musíte převést jazyka Visual Basic v obou směrech. Protože nemůžete použít `CType` nebo některý z další klíčová slova převodu na argumentu procedury nebo parametr, takový převod je vždy implicitní.  
  
 Ve výchozím nastavení tato zpráva je upozornění. Informace o zobrazení nebo skrytí upozornění zpracování upozornění jako chyby, najdete v části [Konfigurace upozornění v jazyce Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID chyby:** BC41999  
  
## <a name="to-correct-this-error"></a>Oprava této chyby  
  
- Pokud je to možné použijte volání argument stejného typu jako parametr procedury, proto není nutné provádět jakýkoli převod jazyka Visual Basic.  
  
- Pokud je potřeba volání procedury s argumentem typu liší od typu parametru, ale není nutné vrátit hodnotu do volání argument, definujte parametr bude [ByVal](../../../visual-basic/language-reference/modifiers/byval.md) místo `ByRef`.  
  
## <a name="see-also"></a>Viz také:

- [Procedury](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [Parametry a argumenty procedury](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)
- [Předávání argumentů podle hodnoty a reference](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
- [Implicitní a explicitní převody](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
