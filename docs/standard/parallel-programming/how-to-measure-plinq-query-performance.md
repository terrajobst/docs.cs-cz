---
title: 'Postupy: Měření výkonu dotazu PLINQ'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to measure performance
ms.assetid: 491ba43b-2c10-473d-9aab-e2cb96446711
ms.openlocfilehash: 91b6165be2f4f464626fb25f7152de68de9d86e8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2020
ms.locfileid: "73124997"
---
# <a name="how-to-measure-plinq-query-performance"></a>Postupy: Měření výkonu dotazu PLINQ
Tento příklad ukazuje, <xref:System.Diagnostics.Stopwatch> jak použít třídu k měření času, který trvá pro dotaz PLINQ spustit.  
  
## <a name="example"></a>Příklad  
 Tento příklad používá `foreach` prázdnou smyčku (`For Each` v jazyce Visual Basic) k měření doby, která trvá spuštění dotazu. V kódu reálného světa smyčky obvykle obsahuje další kroky zpracování, které přidávají k celkové době spuštění dotazu. Všimněte si, že stopky není spuštěna až těsně před smyčky, protože to je při spuštění dotazu začíná. Pokud požadujete více jemně odstupňovaného `ElapsedTicks` měření, `ElapsedMilliseconds`můžete použít vlastnost namísto .  
  
 [!code-csharp[PLINQ#19](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/measure2.cs#19)]
 [!code-vb[PLINQ#19](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/measure2.vb#19)]  
  
 Celková doba provádění je užitečná metrika při experimentování s implementacemi dotazu, ale ne vždy vypovídá celý příběh. Chcete-li získat hlubší a bohatší zobrazení interakce vláken dotazu mezi sebou a s jinými spuštěnými procesy, použijte vizualizér souběžnosti. Další informace naleznete v tématu [Vizualizér souběžnosti](/visualstudio/profiling/concurrency-visualizer).  
  
## <a name="see-also"></a>Viz také

- [Paralelní LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
