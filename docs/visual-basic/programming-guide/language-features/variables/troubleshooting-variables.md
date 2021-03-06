---
title: Řešení potíží s proměnnými
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting [Visual Basic], variables
- variables [Visual Basic], troubleshooting
ms.assetid: 928a2dc8-e565-4ae4-8ba3-80cc0cb50090
ms.openlocfilehash: 929540788e8134760446e02c3377e78d00ca17d9
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351777"
---
# <a name="troubleshooting-variables-in-visual-basic"></a>Řešení potíží s proměnnými v jazyce Visual Basic
Tato stránka obsahuje některé běžné problémy, které mohou nastat při práci s proměnnými v Visual Basic.  
  
## <a name="unable-to-access-members-of-an-object"></a>Nejde získat přístup ke členům objektu.  
 Pokud se váš kód pokusí o přístup k vlastnosti nebo metodě objektu, existují dva možné výsledky chyby:  
  
- Kompilátor může generovat chybovou zprávu, pokud deklarujete proměnnou objektu pro konkrétní typ a potom odkazuje na člen, který není definován tímto typem.  
  
- <xref:System.MemberAccessException> modulu runtime nastává, když objekt přiřazený proměnné objektu nevystavuje člen, ke kterému se váš kód pokouší získat přístup. V případě proměnné [datového typu objektu](../../../../visual-basic/language-reference/data-types/object-data-type.md)lze tuto výjimku získat také v případě, že člen není `Public`. Důvodem je to, že pozdní vazba povoluje přístup pouze pro `Public` členy.  
  
 Pokud [příkaz Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) nastaví kontrolu typu `On`, proměnná objektu může přistupovat pouze k metodám a vlastnostem třídy, se kterou deklarujete. Toto dokládá následující příklad.  

 [!code-vb[VbVbalrVariables#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrVariables/VB/Class1.vb#2)]  
  
 V tomto příkladu může `p` použít pouze členy <xref:System.Object> třídy, které neobsahují vlastnost `Left`. Na druhé straně `q` byla deklarována jako typu <xref:System.Windows.Forms.Label>, takže může použít všechny metody a vlastnosti třídy <xref:System.Windows.Forms.Label> v oboru názvů <xref:System.Windows.Forms>.  
  
### <a name="correct-approach"></a>Správný přístup  
 Aby bylo možné získat přístup ke všem členům objektu určité třídy, deklarujte proměnnou objektu, aby byla typu této třídy, pokud je to možné. Pokud to nemůžete udělat, například pokud neznáte typ objektu v době kompilace, je nutné nastavit `Option Strict` na `Off` a deklarovat proměnnou, která má být [datového typu objektu](../../../../visual-basic/language-reference/data-types/object-data-type.md). To umožňuje, aby byly objekty libovolného typu přiřazeny proměnné a měli byste provést kroky, abyste zajistili, že aktuálně přiřazený objekt je přijatelného typu. K provedení tohoto určení můžete použít [operátor typeof](../../../../visual-basic/language-reference/operators/typeof-operator.md) .  
  
## <a name="other-components-cannot-access-your-variable"></a>Jiné součásti nemají přístup k proměnné.  
 V názvech Visual Basic se *nerozlišují malá a velká písmena*. Pokud se dva názvy liší pouze v abecedním případě, kompilátor je interpretuje jako stejný název. Například se považuje za `ABC` a `abc`, aby odkazovaly na stejný deklarovaný element.  
  
 Modul CLR (Common Language Runtime) však používá vazby *s rozlišováním velkých a* malých písmen. Proto při vytváření sestavení nebo knihovny DLL a zpřístupnění pro jiná sestavení, vaše jména nebudou rozlišovat velká a malá písmena. Například pokud definujete třídu s prvkem s názvem `ABC`a další sestavení využívají třídu pomocí modulu CLR (Common Language Runtime), musí odkazovat na prvek jako `ABC`. Pokud následně znovu zkompilujete třídu a změníte název prvku na `abc`, ostatní sestavení, která používají vaši třídu, již nebudou mít přístup k tomuto prvku. Proto při vydání aktualizované verze sestavení byste neměli měnit abecední případ všech veřejných prvků.  
  
 Další informace najdete v tématu [modul CLR (Common Language Runtime)](../../../../standard/clr.md).  
  
### <a name="correct-approach"></a>Správný přístup  
 Chcete-li jiným komponentám dovolit přístup k proměnným, považovat jejich názvy, jako by se jednalo o velká a malá písmena. Při testování třídy nebo modulu se ujistěte, že jsou jiná sestavení svázána s proměnnými, na které jste očekávali. Po publikování komponenty neprovádějte žádné úpravy existujících názvů proměnných, včetně změny jejich případů.  
  
## <a name="wrong-variable-being-used"></a>Používá se nesprávná proměnná.  
 Pokud máte více než jednu proměnnou se stejným názvem, Visual Basic kompilátor se pokusí přeložit každý odkaz na tento název. Pokud proměnné mají jiný obor, kompilátor vyřeší odkaz na deklaraci s nejužším oborem. Pokud mají stejný obor, řešení se nezdařilo a kompilátor signalizuje chybu. Další informace naleznete v tématu [odkazy na deklarované elementy](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
### <a name="correct-approach"></a>Správný přístup  
 Vyhněte se použití proměnných se stejným názvem, ale s jiným oborem. Pokud používáte jiná sestavení nebo projekty, nepoužívejte co nejvíce názvů definovaných v těchto externích součástech. Pokud máte více než jednu proměnnou se stejným názvem, ujistěte se, že jste kvalifikováni všechny odkazy na ni. Další informace naleznete v tématu [odkazy na deklarované elementy](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## <a name="see-also"></a>Viz také:

- [Proměnné](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [Deklarace proměnné](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [Objektové proměnné](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [Deklarace objektové proměnné](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [Postupy: Přístup ke členům v objektu](../../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [Hodnoty objektové proměnné](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)
- [Postupy: Určení, na jaký typ objektová proměnná odkazuje](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)
- [Odkazy na deklarované elementy](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Deklarované názvy elementů](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
