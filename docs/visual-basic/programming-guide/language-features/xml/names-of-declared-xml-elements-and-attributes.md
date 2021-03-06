---
title: Názvy deklarovaných XML elementů a atributů
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [XML in Visual Basic]
- element names [XML in Visual Basic]
- names in XML literals [Visual Basic]
- attribute names [XML in Visual Basic]
- XML literals [Visual Basic], element names
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
ms.openlocfilehash: 12fbd1f4332391b1acdcf12e101d82627ebbeaff
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/22/2019
ms.locfileid: "74335988"
---
# <a name="names-of-declared-xml-elements-and-attributes-visual-basic"></a>Názvy deklarovaných XML elementů a atributů (Visual Basic)
Toto téma poskytuje pokyny pro Visual Basic pro pojmenovávání elementů XML a atributů v literálech XML.  V literálu XML můžete zadat místní název nebo kvalifikovaný název. Úplný název se skládá z předpony oboru názvů XML, dvojtečky a místního názvu. Další informace o předponách oboru názvů XML naleznete v tématu [literál elementu XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## <a name="rules"></a>Pravidla  
 Místní název elementu nebo atributu v Visual Basic musí splňovat následující pravidla.  
  
- Může začít s oborem názvů. Musí začínat abecedním znakem nebo podtržítkem (`_`).  
  
- Musí obsahovat jenom abecední znaky, desítkové číslice, podtržítka, tečky (.) a spojovníky (-).  
  
- Nesmí být delší než 1 024 znaků.  
  
- Dvojtečky, které se zobrazují v názvech označují vymezení oboru názvů. Proto můžete použít dvojtečky pouze k určení oboru názvů XML pro konkrétní název.  
  
 Kromě toho byste měli dodržovat následující pravidla.  
  
- Specifikace XML 1,0 rezervuje všechny názvy začínající řetězcem "XML" a jakékoli variace v malých písmenech. Proto tyto názvy nepoužívejte pro názvy elementů a atributů.  
  
### <a name="name-length-guidelines"></a>Pokyny pro délku názvu  
 V důsledku praktického hlediska by měl být název co nejkratší, ale stále jasně identifikuje povahu prvku. To zlepšuje čitelnost kódu a zkracuje délku řádku a velikost zdrojového souboru.  
  
 Nicméně vaše jméno by nemělo být tak krátké, že není dostatečně popisovat element nebo jak ho váš kód používá. To je důležité pro čitelnost kódu. Pokud se někdo jiný snaží ho pochopit, nebo pokud si ho po jeho zapsání sami napíšete, můžete si ušetřit čas vhodnými názvy elementů.  
  
## <a name="case-sensitivity-in-names"></a>Rozlišování velkých a malých písmen v názvech  
 Názvy elementů XML rozlišují velká a malá písmena. To znamená, že když kompilátor Visual Basic Porovná dva názvy, které se liší pouze v abecedním případě, interpretuje je jako jiné názvy. Například interpretuje `ABC` a `abc` jako odkazování na samostatné prvky.  
  
## <a name="xml-namespaces"></a>XML – obory názvů  
 Při vytváření literálu elementu XML můžete zadat předponu oboru názvů XML pro název elementu. Další informace naleznete v tématu [literál elementu XML](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md).  
  
## <a name="see-also"></a>Viz také:

- [Vytváření XML v Visual Basic](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [Literál XML elementu](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
