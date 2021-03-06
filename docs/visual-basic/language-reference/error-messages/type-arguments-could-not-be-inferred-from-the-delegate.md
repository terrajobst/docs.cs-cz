---
title: Argumenty typu nelze odvodit z delegáta.
ms.date: 07/20/2015
f1_keywords:
- bc36564
- vbc36564
helpviewer_keywords:
- BC36564
ms.assetid: 21312807-e1cd-4ac1-ae1c-c28a9c25164d
ms.openlocfilehash: 3e2902da7fe9d8fa2194db681df098f0148cbbaf
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2019
ms.locfileid: "64584248"
---
# <a name="type-arguments-could-not-be-inferred-from-the-delegate"></a>Argumenty typu nelze odvodit z delegáta.
Přiřazovací příkaz používá `AddressOf` přiřazení adresy obecný postup delegáta, ale neposkytuje žádné argumenty typu pro obecný postup.  
  
 Za normálních okolností při vyvolání obecného typu, zadáte argument typu pro každý z parametrů typu, který definuje obecného typu. Pokud nezadáte žádné argumenty typu, kompilátor se pokusí odvodit typy, které se mají předat parametry typu. Pokud kontextu neposkytuje dostatek informací pro kompilátor k odvození typů, je vygenerována chyba.  
  
 **ID chyby:** BC36564  
  
## <a name="to-correct-this-error"></a>Oprava této chyby  
  
- Zadejte argumenty typu pro obecný postup v `AddressOf` výrazu.  
  
## <a name="see-also"></a>Viz také:

- [Obecné typy v jazyce Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [Operátor AddressOf](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Obecné procedury v jazyce Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)
- [Seznam typů](../../../visual-basic/language-reference/statements/type-list.md)
- [Rozšiřující metody](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
