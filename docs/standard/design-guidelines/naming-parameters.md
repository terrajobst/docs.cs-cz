---
title: Parametry pojmenování
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: ebe2e2db4b109057bf576d4e18cfe511c657707e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2020
ms.locfileid: "76743827"
---
# <a name="naming-parameters"></a>Parametry pojmenování
Kromě zjevného důvodu čitelnosti je důležité postupovat podle pokynů pro názvy parametrů, protože parametry jsou zobrazeny v dokumentaci a v návrháři, když nástroje vizuálního návrhu poskytují funkce IntelliSense a procházení tříd.

 ✔️ použít camelCasing v názvech parametrů.

 ✔️ použít popisné názvy parametrů.

 ✔️ Zvažte použití názvů založených na významu parametru, nikoli typu parametru.

### <a name="naming-operator-overload-parameters"></a>Parametry přetížení operátoru názvů
 ✔️ použít `left` a `right` pro názvy parametrů přetížení binárního operátoru, pokud neexistuje význam pro parametry.

 ✔️ použít `value` pro názvy parametrů přetížení unárních operátorů, pokud neexistuje význam parametrů.

 Pokud to uděláte, ✔️ zvažte smysluplné názvy parametrů přetížení operátoru.

 ❌ Nepoužívejte zkratky ani číselné indexy pro názvy parametrů přetížení operátorů.

 *Části © 2005, 2009 Microsoft Corporation. Všechna práva vyhrazena.*

 *Přetištěno oprávněním Pearsonova vzdělávání, Inc. z [pokynů pro návrh rozhraní: konvence, idiomy a vzory pro opakovaně použitelné knihovny .NET, druhá edice](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) od Krzysztof Cwalina a Brad Abrams, publikovaly 22. října 2008 Addison-Wesley Professional jako součást sady Microsoft Windows Development Series.*

## <a name="see-also"></a>Viz také

- [Pokyny k návrhu architektury](../../../docs/standard/design-guidelines/index.md)
- [Pokyny pro pojmenování](../../../docs/standard/design-guidelines/naming-guidelines.md)
