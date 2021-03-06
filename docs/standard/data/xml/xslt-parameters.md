---
title: Parametry XSLT
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: fe60aaa0-ae43-4b1c-9be1-426af66ba757
ms.openlocfilehash: cc412042e69a43bbecec9dbe68618e2d307ca793
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75709696"
---
# <a name="xslt-parameters"></a>Parametry XSLT
Parametry XSLT jsou přidány do <xref:System.Xml.Xsl.XsltArgumentList> pomocí metody <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>. Úplný název a identifikátor URI oboru názvů jsou v daném čase přidruženy k objektu Parameter.  
  
### <a name="to-use-an-xslt-parameter"></a>Použití parametru XSLT  
  
1. Vytvořte objekt <xref:System.Xml.Xsl.XsltArgumentList> a přidejte parametr pomocí metody <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A>.  
  
2. Zavolejte parametr ze seznamu stylů.  
  
3. Předejte objekt <xref:System.Xml.Xsl.XsltArgumentList> do metody <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## <a name="parameter-types"></a>Typy parametrů  
 Objekt Parameter by měl odpovídat typu W3C. V následující tabulce jsou uvedeny odpovídající typy W3C, ekvivalentní třídy Microsoft .NET (typ) a zda typ W3C je typ XPath nebo typ XSLT.  
  
|Typ W3C|Ekvivalentní třída .NET (typ)|Typ XPath nebo XSLT|  
|--------------|------------------------------------|------------------------|  
|`String`|<xref:System.String?displayProperty=nameWithType>|XPath|  
|`Boolean`|<xref:System.Boolean?displayProperty=nameWithType>|XPath|  
|`Number`|<xref:System.Double?displayProperty=nameWithType>|XPath|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType>|XSLT|  
|`Node*`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=nameWithType>|XPath|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator><br /><br /> **XPathNavigator[]**|XPath|  
  
 \* To je ekvivalent sady uzlů, která obsahuje jeden uzel.  
  
 Pokud objekt Parameter není jedna z výše uvedených tříd, je převedena podle následujících pravidel. Číselné typy modulu CLR (Common Language Runtime) jsou převedeny na <xref:System.Double>. Typ <xref:System.DateTime> je převeden na <xref:System.String>. <xref:System.Xml.XPath.IXPathNavigable> typy jsou převedeny na <xref:System.Xml.XPath.XPathNavigator>. **Prvek XPathNavigator []** je převeden na <xref:System.Xml.XPath.XPathNodeIterator>.  
  
 Všechny ostatní typy vyvolávají chybu.  
  
## <a name="example"></a>Příklad  
 Následující příklad používá metodu <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> k vytvoření parametru pro uchování počítaného data slevy. Datum slevy se počítá jako 20 dní od data objednávky.  
  
 [!code-csharp[XSLT_Param#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Param/CS/xsltparam.cs#1)]
 [!code-vb[XSLT_Param#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Param/VB/xsltparam.vb#1)]  
  
### <a name="input"></a>Vstup  
  
##### <a name="orderxml"></a>Order. XML  
 [!code-xml[XSLT_Param#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/order.xml#2)]  
  
##### <a name="discountxsl"></a>sleva. xsl  
 [!code-xml[XSLT_Param#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/discount.xsl#3)]  
  
### <a name="output"></a>Výstup  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<order>  
  <total>36.9</total>  
     15% discount if paid by: 2/4/2004 12:00:00 AM  
</order>  
```  
  
## <a name="see-also"></a>Viz také:

- [Transformace XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)
