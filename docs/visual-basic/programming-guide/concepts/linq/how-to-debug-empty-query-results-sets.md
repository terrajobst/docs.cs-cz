---
title: 'Postupy: ladění prázdných sad výsledků dotazu'
ms.date: 07/20/2015
ms.assetid: b242c90a-d2b8-4309-8a1e-e4e70736c727
ms.openlocfilehash: 21c161a702338c0c6943fa09212deaea7fdd72f9
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353077"
---
# <a name="how-to-debug-empty-query-results-sets-visual-basic"></a>Postupy: ladění prázdných sad výsledků dotazu (Visual Basic)

Jedním z nejběžnějších problémů při dotazování na stromy XML je, že pokud má strom XML výchozí obor názvů, vývojář někdy zapíše dotaz, jako by kód XML nebyl v oboru názvů.

První sada příkladů v tomto tématu ukazuje typický způsob, jakým je načten XML ve výchozím oboru názvů a je dotaz na něj nesprávně.

Druhá sada příkladů ukazuje nezbytné opravy, aby bylo možné dotazovat XML v oboru názvů.

Další informace najdete v tématu [obory názvů Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).

## <a name="example"></a>Příklad

Tento příklad ukazuje vytvoření XML v oboru názvů a dotaz, který vrací prázdnou sadu výsledků dotazu.

```vb
Dim root As XElement = _
    <Root xmlns='http://www.adventure-works.com'>
        <Child>1</Child>
        <Child>2</Child>
        <Child>3</Child>
        <AnotherChild>4</AnotherChild>
        <AnotherChild>5</AnotherChild>
        <AnotherChild>6</AnotherChild>
    </Root>
Dim c1 As IEnumerable(Of XElement) = _
        From el In root.<Child> _
        Select el
Console.WriteLine("Result set follows:")
For Each el As XElement In c1
    Console.WriteLine(el.Value)
Next
Console.WriteLine("End of result set")
```

Tento příklad vytvoří následující výsledek:

```console
Result set follows:
End of result set
```

## <a name="example"></a>Příklad

Tento příklad ukazuje vytvoření XML v oboru názvů a dotaz, který je správně kódován.

Řešením je deklarovat a inicializovat globální výchozí obor názvů. Tím se umístí všechny vlastnosti XML ve výchozím oboru názvů. V příkladu nejsou k dispozici žádné další úpravy, aby mohla správně fungovat.

```vb
Imports <xmlns="http://www.adventure-works.com">

Module Module1
    Sub Main()
        Dim root As XElement = _
            <Root xmlns='http://www.adventure-works.com'>
                <Child>1</Child>
                <Child>2</Child>
                <Child>3</Child>
                <AnotherChild>4</AnotherChild>
                <AnotherChild>5</AnotherChild>
                <AnotherChild>6</AnotherChild>
            </Root>
        Dim c1 As IEnumerable(Of XElement) = _
                From el In root.<Child> _
                Select el
        Console.WriteLine("Result set follows:")
        For Each el As XElement In c1
            Console.WriteLine(CInt(el))
        Next
        Console.WriteLine("End of result set")
    End Sub
End Module
```

Tento příklad vytvoří následující výsledek:

```console
Result set follows:
1
2
3
End of result set
```

## <a name="see-also"></a>Viz také:

- [Základní dotazy (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
