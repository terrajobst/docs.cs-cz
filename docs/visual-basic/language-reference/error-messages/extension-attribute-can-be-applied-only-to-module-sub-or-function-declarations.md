---
title: Atribut 'Extension' lze použít pouze v deklaracích 'Module', 'Sub' nebo 'Function'.
ms.date: 07/20/2015
f1_keywords:
- bc36550
- vbc36550
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
ms.openlocfilehash: 2ed3a10cdf941bb8d1d7c00379736e04e8cad4d7
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583186"
---
# <a name="extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations"></a>Atribut 'Extension' lze použít pouze v deklaracích 'Module', 'Sub' nebo 'Function'.

Jediným způsobem, jak rozšířit datový typ v Visual Basic, je definovat metodu rozšíření uvnitř standardního modulu. Metoda rozšíření může být `Sub` procedura nebo procedura `Function`. Všechny metody rozšíření musí být označené atributem rozšíření, `<Extension()>`, z oboru názvů <xref:System.Runtime.CompilerServices?displayProperty=nameWithType>. Volitelně může být modul, který obsahuje metodu rozšíření, označen stejným způsobem. Žádné jiné použití atributu Extension není platné.

**ID chyby:** BC36550

## <a name="to-correct-this-error"></a>Oprava této chyby

- Odeberte atribut Extension.

- Přenavrhněte své rozšíření jako metodu definovanou v ohraničujícím modulu.

## <a name="example"></a>Příklad

Následující příklad definuje metodu `Print` pro datový typ `String`.

```vb
Imports StringUtility
Imports System.Runtime.CompilerServices
Namespace StringUtility
    <Extension()>
    Module StringExtensions
        <Extension()>
        Public Sub Print (ByVal str As String)
            Console.WriteLine(str)
        End Sub
    End Module
End Namespace
```

## <a name="see-also"></a>Viz také:

- [Přehled atributů](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [Rozšiřující metody](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
- [Příkaz Module](../../../visual-basic/language-reference/statements/module-statement.md)
