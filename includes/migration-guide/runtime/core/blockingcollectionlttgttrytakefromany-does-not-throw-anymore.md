---
ms.openlocfilehash: 9e8f9c616d5ae4ed17f35665cff21acbbacda457
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "59803706"
---
### <a name="blockingcollectionttrytakefromany-does-not-throw-anymore"></a>BlockingCollection\<T >. TryTakeFromAny už nevyvolá

|   |   |
|---|---|
|Podrobnosti|Pokud jedna vstupní kolekcí je označena jako dokončená, <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)> již nevrátí hodnotu −1 a <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)> již nevyvolá výjimku. Tato změna umožňuje pracovat s kolekcemi, pokud je jedna z kolekcí prázdná nebo dokončená, ale další kolekce stále obsahuje položky, které lze načíst.|
|Doporučení|Pokud vrátí hodnotu -1 nebo vyvolání TakeFromAny TryTakeFromAny byly použity pro účely tok řízení v případech blokující kolekce probíhá její dokončování, takového kódu by měla nyní změnit použití <code>.Any(b =&gt; b.IsCompleted)</code> ke zjištění této podmínky.|
|Rozsah|Vedlejší|
|Version|4.5|
|Type|Modul runtime|
|Ovlivněná rozhraní API|<ul><li><xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li></ul>|
