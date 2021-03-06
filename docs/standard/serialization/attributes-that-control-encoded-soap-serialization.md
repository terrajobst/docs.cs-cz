---
title: Atributy, které řídí serializaci zakódovanou v protokolu SOAP
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 2961d9abc6c32e78b5a61e8f2bbea5cfcf6677bd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61794937"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>Atributy, které řídí serializaci zakódovanou v protokolu SOAP

World Wide Web Consortium (W3C) dokumentu s názvem [jednoduchý objekt přístup protokolu (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) obsahuje volitelný oddíl (oddíl 5), který popisuje, jak může být zakódován parametry protokolu SOAP. Tak, aby odpovídal pro oddíl 5 specifikace, musí používat speciální sadu atributů v nalezen <xref:System.Xml.Serialization> oboru názvů. Tyto atributy v závislosti na třídy a členy třídy aplikovat a pak <xref:System.Xml.Serialization.XmlSerializer> k serializaci instancí třídy nebo tříd.

V následující tabulce jsou uvedeny atributy, kde je lze použít, a jejich význam. Další informace o použití těchto atributů ovládacímu prvku serializace XML, naleznete v tématu [jak: Serializace objektu jako XML kódováním protokolu SOAP Stream](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) a [jak: Přepsat kódovaný protokol SOAP XML serializace](how-to-override-encoded-soap-xml-serialization.md).

Další informace o atributech najdete v tématu [atributy](../../../docs/standard/attributes/index.md).

|Atribut|Platí pro|Určuje|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|Veřejné pole, vlastnost, parametr nebo návratovou hodnotu.|Člen třídy bude serializována jako atribut XML.|
|<xref:System.Xml.Serialization.SoapElementAttribute>|Veřejné pole, vlastnost, parametr nebo návratovou hodnotu.|Třída bude serializována jako XML element.|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|Veřejné pole, které je identifikátor výčtu.|Název elementu člen výčtového typu.|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|Veřejné vlastnosti a pole.|Vlastnosti nebo pole mají být ignorovány, pokud je serializována třídu obsahující.|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|Veřejná odvozené třídy prohlášení a veřejné metody pro dokumenty služby popis jazyka WSDL (Web).|Typ by měly být zahrnuty při generování schémat (Chcete-li rozpoznán po serializován).|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|Deklarace veřejných tříd.|Třída by měla být serializován jako typ objektu XML.|

## <a name="see-also"></a>Viz také:

- [Serializace XML a SOAP](xml-and-soap-serialization.md)
- [Postupy: Serializace objektu jako XML kódováním protokolu SOAP Stream](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [Postupy: Přepsat kódovaný protokol SOAP serializace XML](how-to-override-encoded-soap-xml-serialization.md)
- [Atributy](../../../docs/standard/attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Postupy: Serializace objektu](how-to-serialize-an-object.md)
- [Postupy: Deserializace objektu](how-to-deserialize-an-object.md)
