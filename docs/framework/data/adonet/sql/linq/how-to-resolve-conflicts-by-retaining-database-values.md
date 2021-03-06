---
title: 'Postupy: Řešení konfliktů zachováním hodnot v databázi'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b475cf72-9e64-4f6e-99c1-af7737bc85ef
ms.openlocfilehash: e42f48a188741c3ddff44f6444fa351192c8175f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793347"
---
# <a name="how-to-resolve-conflicts-by-retaining-database-values"></a>Postupy: Řešení konfliktů zachováním hodnot v databázi
Pro sjednocení rozdílů mezi očekávanými a skutečnými hodnotami databáze předtím, než se pokusíte znovu odeslat změny <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues> , můžete použít k zachování hodnot nalezených v databázi. Aktuální hodnoty v objektovém modelu jsou poté přepsány. Další informace najdete v tématu [Optimistická souběžnost: Přehled](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> Ve všech případech se záznam v klientovi poprvé aktualizuje načtením aktualizovaných dat z databáze. Tato akce zajistí, že se další pokus o aktualizaci nebude při stejných kontrolách souběžnosti selhat.  
  
## <a name="example"></a>Příklad  
 V tomto scénáři <xref:System.Data.Linq.ChangeConflictException> je vyvolána výjimka, když se uživatel1 pokusí odeslat změny, protože uživatel2 má mezitím změněné sloupce asistent a oddělení. V následující tabulce je uvedena situace.  
  
||Správce|Pomocníka|Oddělení|  
|------|-------------|---------------|----------------|  
|Původní stav databáze při dotazování od uživatele User1 a uživatel2.|Alfreds|Maria|Prodej|  
|Uživatel1 připraví odeslání těchto změn.|Alfred||Marketing|  
|Uživatel2 již odeslal tyto změny.||Marie|Služba|  
  
 Uživatel1 se rozhodne tento konflikt vyřešit tak, že novější hodnoty databáze přepíší aktuální hodnoty v objektovém modelu.  
  
 Když uživatel1 vyřeší konflikt <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues>pomocí, výsledek v databázi je následující v tabulce:  
  
||Správce|Pomocníka|Oddělení|  
|------|-------------|---------------|----------------|  
|Nový stav po vyřešení konfliktu.|Alfreds<br /><br /> původně|Marie<br /><br /> (z uživatel2)|Služba<br /><br /> (z uživatel2)|  
  
 Následující příklad kódu ukazuje, jak přepsat aktuální hodnoty v objektovém modelu s hodnotami databáze. (K žádné kontrole nebo vlastní manipulaci s jednotlivými členy nedochází.)  
  
 [!code-csharp[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Viz také:

- [Postupy: Správa konfliktů změn](how-to-manage-change-conflicts.md)
