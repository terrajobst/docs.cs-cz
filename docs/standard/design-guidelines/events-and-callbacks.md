---
title: Události a zpětná volání
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], extensibility
- methods [.NET Framework], callback
- callback methods
- callbacks
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
ms.openlocfilehash: 7dab759ba48104530fc41e46f6f2bba18d6c4456
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2020
ms.locfileid: "76741654"
---
# <a name="events-and-callbacks"></a>Události a zpětná volání
Zpětná volání jsou body rozšiřitelnosti, které umožňují rozhraní volat zpět do uživatelského kódu prostřednictvím delegáta. Tyto delegáty jsou obvykle předávány rozhraní prostřednictvím parametru metody.

 Události jsou zvláštním případem zpětných volání, která podporují praktické a konzistentní syntaxi pro poskytnutí delegáta (obslužná rutina události). Kromě toho dokončování příkazů sady Visual Studio a návrháři poskytují podporu pro používání rozhraní API založených na událostech. (Viz [návrh události](../../../docs/standard/design-guidelines/event.md).)

 ✔️ Zvažte použití zpětných volání k umožnění uživatelům poskytnout vlastní kód, který má být spuštěn rozhraním.

 ✔️ Zvažte použití událostí, aby uživatelé mohli přizpůsobit chování architektury bez nutnosti porozumění objektově orientovanému návrhu.

 ✔️ preferovat události proti prostým zpětným voláním, protože jsou více obeznámené s širší škálou vývojářů a jsou integrovány s dokončováním příkazů sady Visual Studio.

 ❌ Vyhněte se použití zpětných volání v rozhraních API citlivých na výkon.

 Při definování rozhraní API pomocí zpětných volání ne✔️ použít nové typy `Func<...>`, `Action<...>`nebo `Expression<...>` a nikoli vlastní delegáty.

 `Func<...>` a `Action<...>` reprezentují Obecné delegáty. `Expression<...>` představuje definice funkcí, které lze zkompilovat a následně vyvolávat za běhu, ale mohou být také serializovány a předány vzdáleným procesům.

 místo použití `Func<...>` a `Action<...>` delegátů ✔️ měřit a porozumět důsledkům použití `Expression<...>`.

 typy `Expression<...>` jsou ve většině případů logicky ekvivalentní `Func<...>` a `Action<...>` delegáty. Hlavním rozdílem mezi nimi je to, že Delegáti mají být použiti v rámci scénářů místních procesů; výrazy jsou určené pro případy, kdy je výhodné a možné vyhodnotit výraz ve vzdáleném procesu nebo počítači.

 ✔️ pochopit, že voláním delegáta spouštíte libovolný kód, který by mohl mít zabezpečení, správnost a vliv na kompatibilitu.

 *Části © 2005, 2009 Microsoft Corporation. Všechna práva vyhrazena.*

 *Přetištěno oprávněním Pearsonova vzdělávání, Inc. z [pokynů pro návrh rozhraní: konvence, idiomy a vzory pro opakovaně použitelné knihovny .NET, druhá edice](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) od Krzysztof Cwalina a Brad Abrams, publikovaly 22. října 2008 Addison-Wesley Professional jako součást sady Microsoft Windows Development Series.*

## <a name="see-also"></a>Viz také

- [Navrhování pro rozšiřitelnost](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [Pokyny k návrhu architektury](../../../docs/standard/design-guidelines/index.md)
