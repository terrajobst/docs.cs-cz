---
title: Názvy oborů názvů
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], conflicts
- names [.NET Framework], namespaces
- type names, conflicts
- namespaces [.NET Framework], names
- names [.NET Framework], type names
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
ms.openlocfilehash: 52fee0dfaff284c2c1a6afcb8aa7530c28a60d65
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2020
ms.locfileid: "76744136"
---
# <a name="names-of-namespaces"></a>Názvy oborů názvů
Stejně jako u jiných pokynů pro pojmenování je cílem při pojmenovávání oborů názvů vytváření dostatečné srozumitelnosti pro programátora pomocí rozhraní, aby okamžitě věděli, co může být obsah oboru názvů. Následující šablona určuje obecné pravidlo pro názvové obory názvů:

 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`

 Zde jsou příklady:

 `Fabrikam.Math` `Litware.Security`

 ✔️ DĚLAT předpony názvů oborů názvů s názvem společnosti, aby názvy oborů názvů z různých společností nemusely mít stejný název.

 ✔️ použít stabilní název produktu nezávislý na verzi na druhé úrovni názvu oboru názvů.

 ❌ nepoužívejte hierarchie organizace jako základ názvů v hierarchiích oboru názvů, protože názvy skupin v podnicích mají být krátkodobé. Uspořádejte hierarchii oborů názvů kolem skupin souvisejících technologií.

 ✔️ použít PascalCasing a samostatné komponenty oboru názvů s tečkami (například `Microsoft.Office.PowerPoint`). Pokud vaše značka používá netradiční velikost písmen, měli byste postupovat podle velkých a malých písmen definovaných vaší značkou, a to i v případě, že se liší od normálního velikosti oboru názvů.

 v případě potřeby ✔️ ZVÁŽIT použití názvů v množném čísle.

 Použijte například `System.Collections` místo `System.Collection`. Názvy značek a akronymy jsou však výjimkou tohoto pravidla. Použijte například `System.IO` místo `System.IOs`.

 ❌ nepoužívají stejný název pro obor názvů a typ v tomto oboru názvů.

 Nepoužívejte například `Debug` jako název oboru názvů a potom zadejte třídu s názvem `Debug` ve stejném oboru názvů. Několik kompilátorů vyžaduje, aby tyto typy byly plně kvalifikované.

### <a name="namespaces-and-type-name-conflicts"></a>Konflikty oborů názvů a typů
 ❌ nezavádí názvy obecných typů, například `Element`, `Node`, `Log`a `Message`.

 Existuje velmi vysoká pravděpodobnost, že by to mělo způsobit konflikty názvů typů v běžných scénářích. Měli byste kvalifikovat názvy obecných typů (`FormElement`, `XmlNode`, `EventLog`, `SoapMessage`).

 Existují konkrétní pokyny pro předcházení konfliktům názvů typů pro různé kategorie oborů názvů.

- **Obory názvů aplikačního modelu**

     Obory názvů patřící k jednomu aplikačnímu modelu se velmi často používají společně, ale nejsou skoro nikdy použity s obory názvů jiných modelů aplikací. Například obor názvů <xref:System.Windows.Forms?displayProperty=nameWithType> je velmi zřídka používán společně s oborem názvů <xref:System.Web.UI?displayProperty=nameWithType>. Následuje seznam známých skupin oborů názvů aplikačního modelu:

     `System.Windows*` `System.Web.UI*`

     ❌ neposkytují stejný název typům v oborech názvů v rámci jednoho aplikačního modelu.

     Nepřidejte například typ s názvem `Page` do <xref:System.Web.UI.Adapters?displayProperty=nameWithType> oboru názvů, protože <xref:System.Web.UI?displayProperty=nameWithType> obor názvů již obsahuje typ s názvem `Page`.

- **Obory názvů infrastruktury**

     Tato skupina obsahuje obory názvů, které se při vývoji běžných aplikací importují zřídka. Například `.Design` obory názvů se používají hlavně při vývoji programovacích nástrojů. Předcházení konfliktům s typy v těchto oborech názvů není důležité.

- **Základní obory názvů**

     Klíčové obory názvů zahrnují všechny obory názvů `System` s výjimkou oborů názvů modelů aplikací a oborů názvů infrastruktury. Mezi základní obory názvů patří mimo jiné `System`, `System.IO`, `System.Xml`a `System.Net`.

     ❌ Neposkytněte názvy typů, které by mohly být v konfliktu s jakýmkoli typem v základních oborech názvů.

     Například nikdy nepoužívejte `Stream` jako název typu. Je v konfliktu s <xref:System.IO.Stream?displayProperty=nameWithType>, často používaným typem.

- **Skupiny oboru názvů technologií**

     Tato kategorie zahrnuje všechny obory názvů se stejnými prvními dvěma uzly oboru názvů `(<Company>.<Technology>*`), například `Microsoft.Build.Utilities` a `Microsoft.Build.Tasks`. Je důležité, aby typy patřící do jedné technologie nebyly vzájemně v konfliktu.

     ❌ nepřiřazovat názvy typů, které by byly v konfliktu s jinými typy v rámci jedné technologie.

     ❌ nezavádí konflikty typů názvů mezi typy v oborech názvů technologie a oborem názvů aplikačního modelu (Pokud technologie není určena pro použití s modelem aplikace).

 *Části © 2005, 2009 Microsoft Corporation. Všechna práva vyhrazena.*

 *Přetištěno oprávněním Pearsonova vzdělávání, Inc. z [pokynů pro návrh rozhraní: konvence, idiomy a vzory pro opakovaně použitelné knihovny .NET, druhá edice](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) od Krzysztof Cwalina a Brad Abrams, publikovaly 22. října 2008 Addison-Wesley Professional jako součást sady Microsoft Windows Development Series.*

## <a name="see-also"></a>Viz také

- [Pokyny k návrhu architektury](../../../docs/standard/design-guidelines/index.md)
- [Pokyny pro pojmenování](../../../docs/standard/design-guidelines/naming-guidelines.md)
