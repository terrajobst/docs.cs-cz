---
title: Přehled časových pásem
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], about time zones
- transition time [.NET Framework]
- TimeZoneInfo class, about TimeZoneInfo class
- time zones [.NET Framework], creating
- invalid time [.NET Framework]
- fixed rule [.NET Framework]
- ambiguous time [.NET Framework]
- floating rule [.NET Framework]
- daylight saving time [.NET Framework]
- adjustment rule [.NET Framework]
- time zones [.NET Framework], terminology
ms.assetid: c4b7ed01-5e38-4959-a3b6-ef9765d6ccf1
ms.openlocfilehash: 83fa7609c9500bc51581b7b20db3992b4265488b
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131606"
---
# <a name="time-zone-overview"></a>Přehled časových pásem

Třída <xref:System.TimeZoneInfo> zjednodušuje vytváření aplikací pracujících s časovými pásmy. Třída <xref:System.TimeZone> podporuje práci s místním časovým pásmem a koordinovaný světový čas (UTC). Třída <xref:System.TimeZoneInfo> podporuje obě tyto zóny i časové pásmo, o které jsou informace v registru předdefinovány. Pomocí <xref:System.TimeZoneInfo> můžete také definovat vlastní časová pásma, o kterých systém neobsahuje žádné informace.

## <a name="time-zone-essentials"></a>Základy časového pásma

Časové pásmo je geografická oblast, ve které se používá stejný čas. Obvykle ale ne vždy sousedící časová pásma jsou jedna hodina od. Čas v jakémkoli časovém pásmu světa může být vyjádřen jako posun od koordinovaného světového času (UTC).

Spousta časových pásem na světě podporuje letní čas. Letní čas se pokusí Maximalizovat letní čas tím, že posune dobu dopředu o jednu hodinu na jaře nebo v létě a vrátí se do normálního (nebo standardního) času v noci nebo na konci. Tyto změny do a ze standardního času se označují jako pravidla úprav.

Přechod do a z letního času v určitém časovém pásmu může být definován pomocí pevného nebo plovoucího pravidla úpravy. Pevné pravidlo úprav nastavuje konkrétní datum, kdy se v každém roce vyskytuje přechod do nebo z letního času. Například přechod z letního času na běžný čas, který probíhá každý rok dne 25. října, se provede pevně nastaveným pravidlem pro úpravu. Mnohem častěji jsou plovoucí pravidla úprav, která pro přechod do nebo z letního času nastaví určitý den konkrétního týdne konkrétního měsíce. Například přechod ze standardního času na letní čas, který se vyskytuje u třetí neděle v březnu, sleduje pravidlo plovoucí úpravy.

Pro časová pásma, která podporují pravidla úpravy, vytváří přechod do a z letního času dva druhy neobvyklé časů: neplatný čas a nejednoznačné časy. Neplatný čas je neexistujícím časem vytvořeným přechodem ze standardního času na letní čas. Například pokud k tomuto přechodu dojde v určitém dni v 2:00 ráno a způsobí, že se čas změní na 3:00 ráno, každý časový interval v rozmezí 2:00 dop. a 2:59:99 dop. je neplatný. Dvojznačný čas je čas, který může být v jednom časovém pásmu namapován na dvě různé časy. Vytvoří se přechodem z letního času na běžný čas. Například pokud k tomuto přechodu dojde v určitém dni v 2:00 ráno a způsobí, že se čas změní na 1:00 ráno, každý časový interval v rozmezí 1:00 dop. a 1:59:99 dop. může být interpretována buď standardním časem, nebo letním časem.

## <a name="time-zone-terminology"></a>Terminologie časových pásem

Následující tabulka definuje výrazy běžně používané při práci s časovými pásmy a vývoj aplikací pracujících s časovými pásmy.

| Termín            | Definice |
| --------------- | ---------- |
| Pravidlo úpravy | Pravidlo, které definuje, kdy dojde k přechodu ze standardního času na letní čas a zpět z letního času na běžný čas. Každé pravidlo úpravy má počáteční a koncové datum, které definuje, kdy je pravidlo na místě (například pravidlo úpravy je nastaveno od 1. ledna 1986 do 31. prosince 2006), rozdíl (množství času, kdy se v důsledku použití aplikace th mění standardní čas). pravidlo pro úpravu e a informace o konkrétním datu a čase, kdy se mají přechody provést během období úpravy. Přechody mohou následovat buď s pevným pravidlem, nebo s plovoucím pravidlem. |
| Dvojznačný čas  | Čas, který může být namapován na dvě různé časy v jednom časovém pásmu. K tomu dochází, když se změní čas v čase, například během přechodu z letního času v časovém pásmu do standardního času. Například pokud k tomuto přechodu dojde v určitém dni v 2:00 ráno a způsobí, že se čas změní na 1:00 ráno, každý časový interval v rozmezí 1:00 dop. a 1:59:99 dop. může být interpretována buď standardním časem, nebo letním časem. |
| Pevné pravidlo      | Pravidlo úpravy, které nastaví konkrétní datum pro přechod na nebo z letního času. Například přechod z letního času na běžný čas, který probíhá každý rok dne 25. října, se provede pevně nastaveným pravidlem pro úpravu. |
| Plovoucí pravidlo   | Pravidlo úpravy, které nastaví určitý den určitého týdne konkrétního měsíce pro přechod do nebo z letního času. Například přechod ze standardního času na letní čas, který se vyskytuje u třetí neděle v březnu, sleduje pravidlo plovoucí úpravy. |
| Neplatný čas    | Neexistující čas, který je artefaktem přechodu ze standardního času na letní čas. K tomu dochází, když se časem upraví čas v čase, například během přechodu ze standardního času časového pásma na jeho letní čas. Například pokud k tomuto přechodu dojde v určitém dni v 2:00 ráno a způsobí, že se čas změní na 3:00 ráno, každý časový interval v rozmezí 2:00 dop. a 2:59:99 dop. je neplatný. |
| Doba přechodu | Informace o konkrétní změně času, jako je například změna z letního času na běžný čas nebo naopak, v konkrétním časovém pásmu. |

## <a name="time-zones-and-the-timezoneinfo-class"></a>Časová pásma a Třída TimeZoneInfo

V rozhraní .NET představuje objekt <xref:System.TimeZoneInfo> časové pásmo. Třída <xref:System.TimeZoneInfo> obsahuje metodu <xref:System.TimeZoneInfo.GetAdjustmentRules%2A>, která vrací pole objektů <xref:System.TimeZoneInfo.AdjustmentRule>. Každý prvek tohoto pole poskytuje informace o přechodu do a z letního času na konkrétní časové období. (Pro časová pásma, která nepodporují letní čas, metoda vrátí prázdné pole.) Každý objekt <xref:System.TimeZoneInfo.AdjustmentRule> má <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionStart%2A> a vlastnost <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionEnd%2A> definující konkrétní datum a čas přechodu na a z letního času. Vlastnost <xref:System.TimeZoneInfo.TransitionTime.IsFixedDateRule%2A> označuje, zda je tento přechod pevný nebo plovoucí.

Rozhraní .NET spoléhá na informace o časovém pásmu poskytované operačním systémem Windows a uložené v registru. V důsledku počtu časových pásem země není všechna existující časová pásma v registru zastoupena. Kromě toho, vzhledem k tomu, že registr je dynamická struktura, předdefinovaná časová pásma mohou být přidána nebo z něj odebrána. Nakonec registr nutně neobsahuje historické údaje o časovém pásmu. Například v systému Windows XP registr obsahuje data pouze pro jednu sadu úprav časových pásem. Systém Windows Vista podporuje dynamická data časového pásma, což znamená, že jedno časové pásmo může mít více pravidel úprav, která se vztahují na konkrétní intervaly roků. Většina časových pásem definovaných v registru systému Windows Vista a podpora letního času však má pouze jedno nebo dvě předdefinovaná pravidla úprav.

Závislost <xref:System.TimeZoneInfo> třídy v registru znamená, že aplikace využívající časová pásma nemůže být konkrétní časová pásma definovaná v registru. V důsledku toho by se měl při pokusu o vytvoření instance konkrétního časového pásma (jiné než místní časové pásmo nebo časového pásma, které představuje UTC) použít zpracování výjimek. Měla by také poskytnout určitou metodu, která umožní, aby aplikace pokračovala, pokud požadovaný objekt <xref:System.TimeZoneInfo> nemůžete z registru vytvářet instance.

Chcete-li zpracovat absenci požadovaného časového pásma, třída <xref:System.TimeZoneInfo> zahrnuje metodu <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>, kterou můžete použít k vytvoření vlastních časových pásem, které nejsou v registru nalezeny. Podrobnosti o vytvoření vlastního časového pásma najdete v tématu [Postupy: vytváření časových pásem bez pravidel úprav](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) a [Postupy: vytváření časových pásem s pravidly úpravy](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md). Kromě toho můžete použít metodu <xref:System.TimeZoneInfo.ToSerializedString%2A> k převedení nově vytvořeného časového pásma na řetězec a jeho uložení v úložišti dat (například databáze, textový soubor, registr nebo prostředek aplikace). Pak můžete použít metodu <xref:System.TimeZoneInfo.FromSerializedString%2A> k převedení tohoto řetězce zpět na objekt <xref:System.TimeZoneInfo>. Podrobnosti najdete v tématu [Postupy: ukládání časových pásem do vloženého prostředku](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) a [Postup: Obnovení časových pásem z vloženého prostředku](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).

Vzhledem k tomu, že každé časové pásmo je charakterizován základním posunem od času UTC a posunem od času UTC, který odráží všechna existující pravidla úprav, je možné čas v jednom časovém pásmu snadno převést na čas v jiném časovém pásmu. Pro účely tohoto účelu objekt <xref:System.TimeZoneInfo> zahrnuje několik metod převodu, včetně:

- <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>, který převede čas UTC na čas v určeném časovém pásmu.

- <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A>, která převede čas v určeném časovém pásmu na čas UTC.

- <xref:System.TimeZoneInfo.ConvertTime%2A>, která převede čas v jednom určeném časovém pásmu na čas v jiném určeném časovém pásmu.

- <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>, která používá identifikátory časového pásma (místo <xref:System.TimeZoneInfo> objektů) jako parametry pro převod času v jednom určeném časovém pásmu na čas v jiném určeném časovém pásmu.

Podrobnosti o převodu časů mezi časovými pásmy najdete v tématu [Převod časů mezi časovými pásmy](../../../docs/standard/datetime/converting-between-time-zones.md).

## <a name="see-also"></a>Viz také:

- [Data, časy a časová pásma](../../../docs/standard/datetime/index.md)
