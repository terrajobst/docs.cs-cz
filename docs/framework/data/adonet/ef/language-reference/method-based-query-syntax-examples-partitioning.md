---
title: 'Příklady syntaxe dotazů založených na volání metody: Dělení'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b7b64874-c3c8-4bdb-862c-89a168d07827
ms.openlocfilehash: 168fea5ffe6b8fbb4c08b95578beebbdee171c9f
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398481"
---
# <a name="method-based-query-syntax-examples-partitioning"></a>Příklady syntaxe dotazů založených na volání metody: Dělení
Příklady v tomto tématu ukazují <xref:System.Linq.Enumerable.Skip%2A>, jak používat metody a <xref:System.Linq.Enumerable.Take%2A> k dotazování [modelu prodeje AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) pomocí syntaxe výrazu dotazu. Model prodeje společnosti AdventureWorks použitý v těchto příkladech je sestaven z tabulek Contact, adresa, produkt, SalesOrderHeader a SalesOrderDetail v ukázkové databázi AdventureWorks.  
  
 Příklady v tomto tématu používají následující `using` / `Imports` příkazy:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="skip"></a>Skip  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Skip%2A> metodu k získání všech, ale prvních pět kontaktů tabulky kontaktů.  
  
 [!code-csharp[DP L2E Examples#SkipSimple](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#skipsimple)]
 [!code-vb[DP L2E Examples#SkipSimple](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#skipsimple)]  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Skip%2A> metodu k získání všech kromě prvních dvou adres v Praze.  
  
 [!code-csharp[DP L2E Examples#SkipNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP L2E Examples#SkipNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#skipnested)]  
  
## <a name="take"></a>Take  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Take%2A> metodu k získání pouze prvních pěti kontaktů z tabulky kontaktů.  
  
 [!code-csharp[DP L2E Examples#TakeSimple](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#takesimple)]
 [!code-vb[DP L2E Examples#TakeSimple](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#takesimple)]  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Take%2A> metodu k získání prvních tří adres v Praze.  
  
 [!code-csharp[DP L2E Examples#TakeNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#takenested)]
 [!code-vb[DP L2E Examples#TakeNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#takenested)]  
  
## <a name="see-also"></a>Viz také:

- [Dotazy v technologii LINQ to Entities](queries-in-linq-to-entities.md)
