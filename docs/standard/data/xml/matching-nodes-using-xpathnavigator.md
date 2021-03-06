---
title: Párování uzlů pomocí XPathNavigator
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: e6848c47-ee5d-401a-89a5-50b5eed40f30
ms.openlocfilehash: f0988c3a112fefc351175de02c790dc25fe6e94a
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710684"
---
# <a name="matching-nodes-using-xpathnavigator"></a>Párování uzlů pomocí XPathNavigator
Třída <xref:System.Xml.XPath.XPathNavigator> poskytuje metodu <xref:System.Xml.XPath.XPathNavigator.Matches%2A> k určení, zda uzel odpovídá výrazu XPath. Metoda <xref:System.Xml.XPath.XPathNavigator.Matches%2A> přebírá výraz XPath jako vstup a vrací <xref:System.Boolean>, která označuje, zda aktuální uzel odpovídá danému výrazu XPath nebo danému kompilovanému objektu <xref:System.Xml.XPath.XPathExpression>.  
  
## <a name="matching-nodes"></a>Vyhovující uzly  
 Metoda <xref:System.Xml.XPath.XPathNavigator.Matches%2A> vrátí `true`, pokud aktuální uzel odpovídá zadanému výrazu XPath. Například v následujícím příkladu kódu metoda <xref:System.Xml.XPath.XPathNavigator.Matches%2A> vrátí `true`, pokud je aktuální uzel `b`elementu a element `b` má atribut `c`.  
  
> [!NOTE]
> Metoda <xref:System.Xml.XPath.XPathNavigator.Matches%2A> nemění stav <xref:System.Xml.XPath.XPathNavigator>.  
  
```vb  
Dim document as XPathDocument = New XPathDocument("input.xml")  
Dim navigator as XPathNavigator = document.CreateNavigator()  
  
navigator.Matches("b[@c]")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.Matches("b[@c]");  
```  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [Zpracování dat XML pomocí modelu dat XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [Výběr dat XML pomocí XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [Vyhodnocení výrazů XPath pomocí XPathNavigator](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [Rozpoznané typy uzlů s dotazy XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [Dotazy XPath a obory názvů](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
- [Zkompilované výrazy XPath](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
