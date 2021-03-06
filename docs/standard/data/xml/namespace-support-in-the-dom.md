---
title: Podpora oboru názvů v modelu DOM
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f0548ead-0fed-41ee-b33e-117ba900d3bc
ms.openlocfilehash: 7efe03f25fde0681ebd9e3c7c8ea81f6686a8ec1
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710606"
---
# <a name="namespace-support-in-the-dom"></a>Podpora oboru názvů v modelu DOM
XML model DOM (Document Object Model) (DOM) je plně podporující obor názvů. Jsou podporovány pouze dokumenty XML zohledňující obor názvů. Konsorcium World Wide Web (W3C) určuje, že aplikace modelu DOM, které implementují úroveň 1, můžou být nezohledňované a funkce DOM úrovně 2 se s oborem názvů nepodporují. Všechny funkce v modelu XML DOM však podporují obor názvů bez ohledu na to, zda je metoda z doporučení úrovně 1 nebo 2 DOM.  
  
 Například v případě nastavení, které nepoužívá obor názvů, volání `setAttribute("A:b", "123")`, jak je uvedeno v doporučení DOM úrovně 1, nemá za následek atribut s předponou `A` a místním názvem `b`. Výsledkem by byl atribut s hodnotou `A:b`.  
  
 V prostředí s oborem názvů je volání DOM úrovně 2 `setAttribute("A:b", "123")` výsledkem atribut s předponou `A` a místním názvem `b`. Tímto způsobem funguje Microsoft .NET Framework DOM.  
  
 Proto pro všechny metody, které přijímají parametr Name, tyto metody také převezmou předponu, která bude kvalifikována název. Parametr Name, například `A:b` v metodě **SetAttributes** DOM úrovně 1, se analyzuje takto:  
  
- Pokud neexistují žádné dvojtečky (:) znaky, místní název je nastaven na parametr `name` a předpona a NamespaceURI jsou prázdné řetězce.  
  
- Je-li nalezen dvojtečka, název je rozdělen do dvou částí na základě pozice prvního znaku dvojtečky. Předpona je nastavena na řetězec, který byl nalezen před dvojtečkou a místní název je nastaven na řetězec, který byl nalezen za dvojtečkou. Pro metody, které nevezmou hodnotu NamespaceURI, NamespaceURI není vyřešen a zůstane nastaven na prázdný řetězec. V opačném případě je NamespaceURI nastaven na řetězec předaný metodě. Pokud není předpona definována, pak vlastnosti **Save** a **InnerXml** a **OuterXml** selžou.  
  
## <a name="see-also"></a>Viz také:

- [Model DOM (Document Object Model) dokumentu XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
