---
title: 'Postupy: Přímé spuštění příkazů SQL'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 04671bb0-40c0-4465-86e5-77986f454661
ms.openlocfilehash: 3f28351a29915bebd698e00113bb05647d8412b4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781993"
---
# <a name="how-to-directly-execute-sql-commands"></a>Postupy: Přímé spuštění příkazů SQL
Za předpokladu, že se <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> připojenídápoužítkprovedenípříkazůSQL,kterénevracejíobjekty.<xref:System.Data.Linq.DataContext>  
  
## <a name="example"></a>Příklad  
 Následující příklad způsobí, SQL Server zvýšit JednotkováCena o 1,00.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#3)]
 [!code-vb[DLinqCommunicatingWithDatabase#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>Viz také:

- [Postupy: Přímé spouštění dotazů SQL](how-to-directly-execute-sql-queries.md)
- [Komunikace s databází](communicating-with-the-database.md)
