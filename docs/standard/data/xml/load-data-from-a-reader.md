---
title: Načtení dat z čtečky
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 7e74918c-bc72-4977-a49b-e1520a6d8f60
ms.openlocfilehash: 90a66e04bda4fb2ee4216e8aabd631afb2f28dd0
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710710"
---
# <a name="load-data-from-a-reader"></a>Načtení dat z čtečky
Pokud je dokument XML načten pomocí metody <xref:System.Xml.XmlDocument.Load%2A> a parametru <xref:System.Xml.XmlReader>, existují rozdíly v chování, ke kterému dochází v porovnání s chováním při načítání dat z jiných formátů. Pokud je čtenář v jeho počátečním stavu, <xref:System.Xml.XmlDocument.Load%2A> spotřebovává celý obsah čtecího zařízení a sestaví XML model DOM (Document Object Model) (DOM) ze všech dat ve čtečce.  
  
 Pokud je čtenář již umístěn v uzlu někam v dokumentu a čtecí modul je pak předán metodě <xref:System.Xml.XmlDocument.Load%2A>, <xref:System.Xml.XmlDocument.Load%2A> se pokusí přečíst aktuální uzel a všechny položky na stejné úrovni až po koncovou značku, která zavírá aktuální hloubku do paměti. Úspěch <xref:System.Xml.XmlDocument.Load%2A> v závislosti na uzlu, ke kterému je čtenář zapnutý při pokusu o načtení, tak, jak <xref:System.Xml.XmlDocument.Load%2A> ověřuje, že XML ze čtecího zařízení je ve správném formátu. Pokud XML není ve správném formátu, <xref:System.Xml.XmlDocument.Load%2A> vyvolá výjimku. Například následující sada uzlů obsahuje dva elementy na kořenové úrovni, XML není ve správném formátu a <xref:System.Xml.XmlDocument.Load%2A> vyvolá výjimku.  
  
- Uzel komentáře následovaný uzlem elementu následovaným uzlem elementu následovaným uzlem EndElement.  
  
 Následující sada uzlů vytvoří nekompletní model DOM, protože neexistuje žádný element na úrovni root.  
  
- Uzel komentáře následovaný uzlem ProcessingInstruction následovaným uzlem komentáře následovaným uzlem EndElement.  
  
 Tím se nevyvolá výjimka a data se načtou. Kořenový element můžete přidat do horní části těchto uzlů a vytvořit kód XML ve správném formátu, který lze uložit bez chyb.  
  
 Pokud je čtecí modul umístěn na listovém uzlu, který je neplatný pro kořenovou úroveň dokumentu (například prázdný znak nebo uzel atributu), čtecí modul bude pokračovat v čtení, dokud nebude umístěn na uzlu, který lze použít pro kořen. Dokument začíná v tomto okamžiku načten.  
  
 Ve výchozím nastavení <xref:System.Xml.XmlDocument.Load%2A> neověřuje, zda je XML platný, pomocí definice typu dokumentu (DTD) nebo ověřování schématu. Ověřuje pouze to, zda je soubor XML správně vytvořen. Aby bylo ověřování provedeno, je třeba vytvořit <xref:System.Xml.XmlReader> pomocí <xref:System.Xml.XmlReaderSettings> třídy. Třída <xref:System.Xml.XmlReader> může vyhovět ověřování pomocí schématu DTD nebo schématu definice jazyka (XSD). Vlastnost <xref:System.Xml.ValidationType> třídy <xref:System.Xml.XmlReaderSettings> určuje, zda instance <xref:System.Xml.XmlReader> vynutila ověřování. Další informace o ověřování dat XML naleznete v části poznámky na referenční stránce <xref:System.Xml.XmlReader>.  
  
## <a name="see-also"></a>Viz také:

- [Model DOM (Document Object Model) dokumentu XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
