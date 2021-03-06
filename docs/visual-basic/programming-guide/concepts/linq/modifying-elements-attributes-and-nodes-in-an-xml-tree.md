---
title: Změna elementů, atributů a uzlů v Tree1 XML
ms.date: 07/20/2015
ms.assetid: 865cf54e-f8ac-4871-863b-a3e6fc61a4b9
ms.openlocfilehash: d548e6f5912437e5c5df27f55fcdb28990e92c8d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61666141"
---
# <a name="modifying-elements-attributes-and-nodes-in-an-xml-tree"></a>Změna elementů, atributů a uzlů ve stromu XML
Následující tabulka shrnuje metody a vlastnosti, které můžete použít k úpravě prvek a jeho podřízené prvky nebo jeho atributy.  
  
 Upravte následující metody <xref:System.Xml.Linq.XElement>.  
  
|Metoda|Popis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>|Nahradí element analyzovaný kód XML.|  
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|Odebere všechny obsah elementu (podřízených uzlů a atributy).|  
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|Odebere atributy elementu.|  
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A?displayProperty=nameWithType>|Nahradí všechny obsah elementu (podřízených uzlů a atributy).|  
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A?displayProperty=nameWithType>|Nahradí atributy elementu.|  
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|Nastaví hodnotu atributu. Pokud neexistuje, vytvoří atribut. Pokud je hodnota nastavena na `null`, odebere atribut.|  
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|Nastaví hodnotu podřízený element. Vytvoří element, pokud neexistuje. Pokud je hodnota nastavena na `null`, odstraní prvek.|  
|<xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType>|Nahradí obsah elementu (podřízené uzly) zadaný text.|  
|<xref:System.Xml.Linq.XElement.SetValue%2A?displayProperty=nameWithType>|Nastaví hodnotu elementu.|  
  
 Upravte následující metody <xref:System.Xml.Linq.XAttribute>.  
  
|Metoda|Popis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType>|Nastaví hodnotu atributu.|  
|<xref:System.Xml.Linq.XAttribute.SetValue%2A?displayProperty=nameWithType>|Nastaví hodnotu atributu.|  
  
 Upravte následující metody <xref:System.Xml.Linq.XNode> (včetně <xref:System.Xml.Linq.XElement> nebo <xref:System.Xml.Linq.XDocument>).  
  
|Metoda|Popis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A?displayProperty=nameWithType>|Nahradí uzlu nový obsah.|  
  
 Upravte následující metody <xref:System.Xml.Linq.XContainer> ( <xref:System.Xml.Linq.XElement> nebo <xref:System.Xml.Linq.XDocument>).  
  
|Metoda|Popis|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A?displayProperty=nameWithType>|Nahradí nový obsah podřízených uzlů.|  
  
## <a name="see-also"></a>Viz také:

- [Změna stromů XML (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
