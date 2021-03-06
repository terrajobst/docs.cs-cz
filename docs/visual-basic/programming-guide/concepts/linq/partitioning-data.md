---
title: Segmentace dat
ms.date: 07/20/2015
ms.assetid: 69c59379-b66e-422c-b324-5b5c07760ef7
ms.openlocfilehash: 2ab4e27ef6d825b9100fc3c15b7a9554ae49e516
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353156"
---
# <a name="partitioning-data-visual-basic"></a>Dělení dat (Visual Basic)
Dělení v jazyce LINQ odkazuje na operaci rozdělení vstupní sekvence do dvou oddílů bez přeuspořádání prvků a vrácení jedné z sekcí.  
  
 Následující ilustrace znázorňuje výsledky tří různých operací dělení na sekvenci znaků. První operace vrátí první tři prvky v sekvenci. Druhá operace přeskočí první tři prvky a vrátí zbývající prvky. Třetí operace přeskočí první dva prvky v sekvenci a vrátí další tři prvky.  
  
 ![Obrázek, který ukazuje tři operace dělení na oddíly LINQ.](./media/partitioning-data/linq-partitioning-operations.png)  
  
 Standardní metody operátoru dotazu, které sekvence oddílů jsou uvedeny v následující části.  
  
## <a name="operators"></a>Operátory  
  
|Název operátoru|Popis|Visual Basic syntaxe výrazu dotazu|Další informace|  
|-------------------|-----------------|------------------------------------------|----------------------|  
|Přeskočit|Přeskočí prvky až do zadané pozice v sekvenci.|`Skip`|<xref:System.Linq.Enumerable.Skip%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Skip%2A?displayProperty=nameWithType>|  
|SkipWhile –|Přeskočí prvky založené na funkci predikátu, dokud element nesplní podmínku.|`Skip While`|<xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=nameWithType>|  
|Take|Přebírá prvky až do zadané pozice v sekvenci.|`Take`|<xref:System.Linq.Enumerable.Take%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Take%2A?displayProperty=nameWithType>|  
|TakeWhile –|Převezme prvky založené na funkci predikátu, dokud element nesplní podmínku.|`Take While`|<xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>Příklady syntaxe výrazů dotazů  
  
### <a name="skip"></a>Přeskočit  
 Následující příklad kódu používá klauzuli `Skip` v Visual Basic k přeskočení prvních čtyř řetězců v poli řetězců před vrácením zbývajících řetězců v poli.  
  
 [!code-vb[CsLINQPartitioning#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#1)]  
  
### <a name="skipwhile"></a>SkipWhile –  
 Následující příklad kódu používá klauzuli `Skip While` v Visual Basic k přeskočení řetězce v poli, zatímco první písmeno řetězce je "a". Zbývající řetězce v poli jsou vráceny.  
  
 [!code-vb[CsLINQPartitioning#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#2)]  
  
### <a name="take"></a>Take  
 Následující příklad kódu používá klauzuli `Take` v Visual Basic k vrácení prvních dvou řetězců v poli řetězců.  
  
 [!code-vb[CsLINQPartitioning#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#3)]  
  
### <a name="takewhile"></a>TakeWhile –  
 Následující příklad kódu používá klauzuli `Take While` v Visual Basic k vrácení řetězců z pole, zatímco délka řetězce je pět nebo méně.  
  
 [!code-vb[CsLINQPartitioning#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#4)]  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Linq>
- [Přehled standardních operátorů dotazů (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Klauzule Skip](../../../../visual-basic/language-reference/queries/skip-clause.md)
- [Klauzule Skip While](../../../../visual-basic/language-reference/queries/skip-while-clause.md)
- [Klauzule Take](../../../../visual-basic/language-reference/queries/take-clause.md)
- [Klauzule Take While](../../../../visual-basic/language-reference/queries/take-while-clause.md)
