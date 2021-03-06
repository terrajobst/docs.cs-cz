---
title: 'Postup: Načtení hodnoty prvku (LINQ do XML)'
ms.date: 07/20/2015
ms.assetid: 76b9b2a5-b3ba-49da-ba74-82100e1bd21c
ms.openlocfilehash: b1a61091dc59b403c5d967609e8870492c24347f
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2020
ms.locfileid: "80248931"
---
# <a name="how-to-retrieve-the-value-of-an-element-linq-to-xml-visual-basic"></a>Postup: Načtení hodnoty prvku (LINQ do XML) (Visual Basic)
Toto téma ukazuje, jak získat hodnotu prvků. Existují dva hlavní způsoby, jak to udělat. Jedním ze způsobů <xref:System.Xml.Linq.XElement> je <xref:System.Xml.Linq.XAttribute> obsazení nebo na požadovaný typ. Explicitní operátor převodu pak převede obsah prvku nebo atributu na zadaný typ a přiřadí jej proměnné. Případně můžete využít <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> ubytování nebo <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType> ubytovací zařízení.  
  
 S Visual Basic, nejlepší přístup <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> je použití vlastnosti.  
  
## <a name="example"></a>Příklad  
 Chcete-li načíst hodnotu prvku, <xref:System.Xml.Linq.XElement> stačí přetypovat objekt na požadovaný typ. Vždy můžete přetypovat prvek do řetězce takto:  
  
```vb  
Dim e As XElement = <StringElement>abcde</StringElement>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & e.Value)  
```  
  
 Tento příklad vytváří následující výstup:  
  
```xml  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>Příklad  
 Prvky můžete také přetypovat na jiné typy než řetězec. Například pokud máte prvek, který obsahuje celé číslo, můžete `int`přetypovat do , jak je znázorněno v následujícím kódu:  
  
```vb  
Dim e As XElement = <Age>44</Age>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & CInt(e))  
```  
  
 Tento příklad vytváří následující výstup:  
  
```xml  
<Age>44</Age>  
Value of e:44  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]poskytuje explicitní operátory přetypádky pro `int?` `uint`následující `uint?` `long`datové `long?` `ulong` `ulong?`typy: `float` `float?` `double` `double?` `decimal` `decimal?` `DateTime` `DateTime?` `string` `bool`, , `bool?` `int`, , , , , , , , , , , , , `TimeSpan`, `TimeSpan?`, `GUID`, , , a `GUID?`.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]poskytuje stejné operátory <xref:System.Xml.Linq.XAttribute> přetypádku pro objekty.  
  
## <a name="example"></a>Příklad  
 <xref:System.Xml.Linq.XElement.Value%2A> Vlastnost můžete použít k načtení obsahu prvku:  
  
```vb  
Dim e As XElement = <StringElement>abcde</StringElement>  
Console.WriteLine(e)  
Console.WriteLine("Value of e:" & e.Value)  
```  
  
 Tento příklad vytváří následující výstup:  
  
```xml  
<StringElement>abcde</StringElement>  
Value of e:abcde  
```  
  
## <a name="example"></a>Příklad  
 Někdy se pokusíte načíst hodnotu prvku, i když si nejste jisti, že existuje. V tomto případě při přiřazení přetypovaného prvku typu `string` s možnou hodnotou null (jeden nebo jeden z typů hodnot s možnou hodnotou null v rozhraní .NET Framework), pokud prvek neexistuje, je přiřazená proměnná pouze nastavena na `Nothing`. Následující kód ukazuje, že když prvek může nebo nemusí existovat, je <xref:System.Xml.Linq.XElement.Value%2A> jednodušší použít přetypování než použít vlastnost.  
  
```vb  
Dim root As XElement = <Root>  
                           <Child1>child 1 content</Child1>  
                           <Child2>2</Child2>  
                       </Root>  
  
' The following assignments show why it is easier to use  
' casting when the element might or might not exist.  
  
Dim c1 As String = CStr(root.Element("Child1"))  
Console.WriteLine("c1:{0}", IIf(c1 Is Nothing, "element does not exist", c1))  
  
Dim c2 As Nullable(Of Integer) = CType(root.Element("Child2"), Nullable(Of Integer))  
Console.WriteLine("c2:{0}", IIf(Not (c2.HasValue), "element does not exist", c2.ToString()))  
  
Dim c3 As String = CStr(root.Element("Child3"))  
Console.WriteLine("c3:{0}", IIf(c3 Is Nothing, "element does not exist", c3))  
  
Dim c4 As Nullable(Of Integer) = CType(root.Element("Child4"), Nullable(Of Integer))  
Console.WriteLine("c4:{0}", IIf(Not (c4.HasValue), "element does not exist", c4.ToString()))  
  
Console.WriteLine()  
  
' The following assignments show the required code when using  
' the Value property when the attribute might or might not exist.  
' Notice that this is more difficult than the casting approach.  
  
Dim e1 As XElement = root.Element("Child1")  
Dim v1 As String  
If (e1 Is Nothing) Then  
    v1 = Nothing  
Else  
    v1 = e1.Value  
End If  
Console.WriteLine("v1:{0}", IIf(v1 Is Nothing, "element does not exist", v1))  
  
Dim e2 As XElement = root.Element("Child2")  
Dim v2 As Nullable(Of Integer)  
If (e2 Is Nothing) Then  
    v2 = Nothing  
Else  
    v2 = e2.Value  
End If  
Console.WriteLine("v2:{0}", IIf(Not (v2.HasValue), "element does not exist", v2))  
  
Dim e3 As XElement = root.Element("Child3")  
Dim v3 As String  
If (e3 Is Nothing) Then  
    v3 = Nothing  
Else  
    v3 = e3.Value  
End If  
Console.WriteLine("v3:{0}", IIf(v3 Is Nothing, "element does not exist", v3))  
  
Dim e4 As XElement = root.Element("Child4")  
Dim v4 As Nullable(Of Integer)  
If (e4 Is Nothing) Then  
    v4 = Nothing  
Else  
    v4 = e4.Value  
End If  
Console.WriteLine("v4:{0}", IIf(Not (v4.HasValue), "element does not exist", v4))  
```  
  
 Výsledkem tohoto kódu je následující výstup:  
  
```console  
c1:child 1 content  
c2:2  
c3:element does not exist  
c4:element does not exist  
  
v1:child 1 content  
v2:2  
v3:element does not exist  
v4:element does not exist  
```  
  
 Obecně můžete napsat jednodušší kód při použití přetypování k načtení obsahu prvků a atributů.  
  
## <a name="see-also"></a>Viz také

- [LINQ na osy XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
