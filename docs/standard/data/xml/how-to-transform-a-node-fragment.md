---
title: 'Postupy: transformace fragmentu uzlu'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
ms.openlocfilehash: 56e9ef6031a5736acfa066ed6c068f954bd5af8d
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710814"
---
# <a name="how-to-transform-a-node-fragment"></a>Postupy: transformace fragmentu uzlu
Při transformaci dat obsažených v <xref:System.Xml.XmlDocument> nebo objektu <xref:System.Xml.XPath.XPathDocument> se transformace XSLT vztahují na dokument jako celek. Jinými slovy, Pokud předáte v jiném než kořenovém uzlu dokumentu, nezabrání to procesu transformace v přístupu ke všem uzlům v načteném dokumentu. Chcete-li transformovat fragment uzlu, je nutné vytvořit samostatný objekt obsahující pouze fragment uzlu a předat tento objekt metodě <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## <a name="procedures"></a>Procedury  
  
#### <a name="to-transform-a-node-fragment"></a>Transformace fragmentu uzlu  
  
1. Vytvořte objekt obsahující zdrojový dokument.  
  
2. Najděte fragment uzlu, který chcete transformovat.  
  
3. Vytvořte samostatný objekt se pouze fragmentem uzlu.  
  
4. Předejte fragment uzlu do metody <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## <a name="example"></a>Příklad  
 Následující příklad transformuje fragment uzlu a výstupy výsledků do konzoly.  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### <a name="input"></a>Vstup  
  
##### <a name="booksxml"></a>Books. XML  
 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### <a name="singlexsl"></a>Single. xsl  
 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### <a name="output"></a>Výstup  
 Titul knihy je důvěryhodný člověk.  
  
## <a name="see-also"></a>Viz také:

- [Používání třídy XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)
