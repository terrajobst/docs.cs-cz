---
ms.openlocfilehash: 734041f5921571cd11225a359e794526cbd8d0e1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62088479"
---
### <a name="systemuriiswellformeduristring-method-returns-false-for-relative-uris-with-a-colon-char-in-first-segment"></a>System.Uri.IsWellFormedUriString metoda vrátí hodnotu false pro relativní identifikátor URI se znak dvojtečky. v první segment

|   |   |
|---|---|
|Podrobnosti|Od verze rozhraní .NET Framework 4.5, <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)> relativní identifikátor URI se bude zacházet <code>:</code> v jejich první segment, protože není ve správném. Jedná se o změnu z <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name> chování v rozhraní .NET Framework 4.0, který byl vytvořen tak, aby odpovídal na RFC3986.|
|Doporučení|Tato změna (stejně jako mnoho dalších změn identifikátor URI) ovlivní pouze aplikace cílené na rozhraní .NET Framework 4.5 (nebo novější). Pokud chcete dál používat staré chování, cílové aplikace proti rozhraní .NET Framework 4.0. Můžete také zkontrolovat identifikátorů URI před voláním <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name> hledáte <code>:</code> znaky, které můžete chtít odebrat pro účely ověření, pokud je žádoucí staré chování.|
|Rozsah|Vedlejší|
|Version|4.5|
|Type|Změna cílení|
|Ovlivněná rozhraní API|<ul><li><xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=nameWithType></li></ul>|
