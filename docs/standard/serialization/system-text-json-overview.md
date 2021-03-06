---
title: Serializace a deserializace C# JSON pomocí-.NET
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 660a2831aa6a807486fc47eae880bcd11347c547
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2020
ms.locfileid: "78159543"
---
# <a name="json-serialization-and-deserialization-marshalling-and-unmarshalling-in-net---overview"></a>Serializace a deserializace JSON (zařazení a zrušení zařazení) v .NET – přehled

Obor názvů `System.Text.Json` poskytuje funkce pro serializaci a deserializaci z JavaScript Object Notation (JSON).

Návrh knihovny zvýrazňuje vysoký výkon a nedostatečné přidělení paměti nad rozsáhlou sadu funkcí. Integrovaná podpora UTF-8 optimalizuje proces čtení a zápisu textu JSON kódovaného jako UTF-8, což je nejbezpečnější kódování dat na webu a soubory na disku.

Knihovna také poskytuje třídy pro práci s modelem objektů dokumentů v paměti (DOM). Tato funkce umožňuje náhodný přístup jen pro čtení prvků v souboru JSON nebo v řetězci.

## <a name="how-to-get-the-library"></a>Jak získat knihovnu

* Knihovna je integrovaná jako součást sdíleného rozhraní [.NET Core 3,0](https://aka.ms/netcore3download) .
* Pro jiná cílová rozhraní nainstalujte balíček NuGet [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) . Balíček podporuje:
  * .NET Standard 2,0 a novější verze
  * .NET Framework 4.7.2 a novější verze
  * .NET Core 2,0, 2,1 a 2,2

## <a name="additional-resources"></a>Další zdroje

* [Jak používat knihovnu](system-text-json-how-to.md)
* [Postup migrace z Newtonsoft.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Zápis převaděčů](system-text-json-converters-how-to.md)
* [zdrojový kód System.Text.Json](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json)
* [Reference k rozhraní API System.Text.Json](xref:System.Text.Json)
* [System.Text.Json. Reference k rozhraní API serializace](xref:System.Text.Json.Serialization)
<!-- * [Roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
