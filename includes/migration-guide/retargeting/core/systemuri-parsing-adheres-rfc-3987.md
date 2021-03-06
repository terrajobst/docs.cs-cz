---
ms.openlocfilehash: 6c2c6422ca4d426fcc2ff5827a2387abb5578e3d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62088480"
---
### <a name="systemuri-parsing-adheres-to-rfc-3987"></a>Analýza kódu System.Uri dodržuje RFC 3987

|   |   |
|---|---|
|Podrobnosti|Parsování identifikátorů URI změnil v několika ohledech v rozhraní .NET Framework 4.5. Upozorňujeme však, že tyto změny se projeví pouze kód cílí na rozhraní .NET Framework 4.5. Binární cíle rozhraní .NET Framework 4.0, staré chování budou zachována. Změny v analýze identifikátoru URI v rozhraní .NET Framework 4.5 patří:<ul><li>Normalizace a znak kontrolu souladu s pravidly nejnovější IRI v dokumentu RFC 3987 provede parsování identifikátorů URI.</li><li>Formulář normalizace Unicode C se provede pouze na část hostitele v identifikátoru URI.</li><li>Neplatný mailto: Identifikátory URI nyní způsobí výjimku.</li><li>Nyní jsou zachovány koncové tečky na konci segmentu cesty.</li><li><code>file://</code> Identifikátory URI nejsou řídicí <code>?</code> znak.</li><li>Řídící znaky Unicode <code>U+0080</code> prostřednictvím <code>U+009F</code> nejsou podporovány.</li><li>Znak čárky <code>,</code> nebo <code>%2c</code> nejsou automaticky znakem.</li></ul>|
|Doporučení|Pokud původní analýzy sémantiku rozhraní .NET Framework 4.0 URI jsou nutné (často nejsou), můžete použít pomocí cílení na rozhraní .NET Framework 4.0. Můžete to udělat pomocí <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name> sestavení nebo prostřednictvím sady Visual Studio projekt systému uživatelského rozhraní na stránce Vlastnosti projektu.|
|Rozsah|Hlavní|
|Version|4.5|
|Type|Změna cílení|
|Ovlivněná rozhraní API|<ul><li><xref:System.Uri.%23ctor(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.String,System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.String,System.UriKind)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.Uri,System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.String,System.UriKind,System.Uri@)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.Uri,System.String,System.Uri@)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.Uri,System.Uri,System.Uri@)?displayProperty=nameWithType></li></ul>|
