---
title: Informační sada po kompilaci schématu
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 7f1bc7f4-401b-459f-9078-f099cc711fde
ms.openlocfilehash: 016032b2b37ced5592edc18934ed183c475f5598
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710476"
---
# <a name="post-schema-compilation-infoset"></a>Informační sada po kompilaci schématu
[Doporučení schématu XML pro konsorcium World Wide Web (W3C)](https://www.w3.org/XML/Schema) se zabývá sadou informací (informační sada), která musí být vystavena pro ověření před schématem a pro kompilaci po sestavení schématu. Model objektu XML schématu (SOM) zobrazuje tuto expozici před a po volání metody <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> <xref:System.Xml.Schema.XmlSchemaSet>.  
  
 Informační sada pro ověření před schématem je sestavena během úprav schématu. Informační sada po kompilaci po schématu je vygenerována po volání metody <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> <xref:System.Xml.Schema.XmlSchemaSet> je volána během kompilace schématu a je vystavena jako vlastnosti.  
  
 SOM je objektový model, který představuje ověření předběžného schématu a Infosets kompilace po sestavení. skládá se z tříd v oboru názvů <xref:System.Xml.Schema?displayProperty=nameWithType>. Všechny vlastnosti čtení a zápisu tříd v oboru názvů <xref:System.Xml.Schema> patří do informační sady předběžného schématu, zatímco všechny vlastnosti tříd, které jsou jen pro čtení třídy v oboru názvů <xref:System.Xml.Schema>, patří do informační sady pro kompilaci po schématu. Výjimkou z tohoto pravidla jsou následující vlastnosti, které jsou zároveň vlastnostmi sady inverze pro ověřování schématu a vlastností informačního doplňku pro kompilaci po schématu.  
  
|Třída|Vlastnost|  
|-----------|--------------|  
|<xref:System.Xml.Schema.XmlSchemaObject>|<xref:System.Xml.Schema.XmlSchemaObject.Parent%2A>|  
|<xref:System.Xml.Schema.XmlSchema>|<xref:System.Xml.Schema.XmlSchema.AttributeFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.BlockDefault%2A>, <xref:System.Xml.Schema.XmlSchema.ElementFormDefault%2A>, <xref:System.Xml.Schema.XmlSchema.FinalDefault%2A>, <xref:System.Xml.Schema.XmlSchema.TargetNamespace%2A>|  
|<xref:System.Xml.Schema.XmlSchemaExternal>|<xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A>|  
|<xref:System.Xml.Schema.XmlSchemaAttributeGroup>|<xref:System.Xml.Schema.XmlSchemaAttributeGroup.AnyAttribute%2A>|  
|<xref:System.Xml.Schema.XmlSchemaParticle>|<xref:System.Xml.Schema.XmlSchemaParticle.MaxOccurs%2A>, <xref:System.Xml.Schema.XmlSchemaParticle.MinOccurs%2A>|  
|<xref:System.Xml.Schema.XmlSchemaComplexType>|<xref:System.Xml.Schema.XmlSchemaComplexType.AnyAttribute%2A>|  
  
 Například třídy <xref:System.Xml.Schema.XmlSchemaElement> a <xref:System.Xml.Schema.XmlSchemaComplexType> mají vlastnosti `BlockResolved` a `FinalResolved`. Tyto vlastnosti jsou použity pro uchování hodnot `Block` a `Final` vlastností poté, co bylo schéma kompilováno a ověřeno. `BlockResolved` a `FinalResolved` jsou vlastnosti jen pro čtení, které jsou součástí informační sady po sestavení schématu.  
  
 Následující příklad ukazuje vlastnost <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A> <xref:System.Xml.Schema.XmlSchemaElement> sadě třídy po ověření schématu. Před ověřením vlastnost obsahuje `null` odkaz a <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> je nastaven na název daného typu. Po ověření se <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> přeloží na platný typ a objekt typu je k dispozici prostřednictvím vlastnosti <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A>.  
  
 [!code-cpp[PsciSample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/PsciSample/CPP/PsciSample.cpp#1)]
 [!code-csharp[PsciSample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/PsciSample/CS/PsciSample.cs#1)]
 [!code-vb[PsciSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/PsciSample/VB/PsciSample.vb#1)]  
  
## <a name="see-also"></a>Viz také:

- [Model objektu schématu (SOM) XML](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)
