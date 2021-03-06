---
title: Příklad odloženého spuštění (C#)
ms.date: 07/20/2015
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
ms.openlocfilehash: 0816594ad016f19af4c97198160b4bafb9b4b8b4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/14/2020
ms.locfileid: "70204130"
---
# <a name="deferred-execution-example-c"></a>Příklad odloženého spuštění (C#)
Toto téma ukazuje, jak odložené spuštění a opožděné vyhodnocení ovlivňují provádění dotazů LINQ na dotazy XML.  
  
## <a name="example"></a>Příklad  
 Následující příklad ukazuje pořadí provádění při použití metody rozšíření, která používá odložené spuštění. Příklad deklaruje pole tří řetězců. Potom iterace prostřednictvím kolekce `ConvertCollectionToUpperCase`vrácené .  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 Tento příklad vytváří následující výstup:  
  
```output  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 Všimněte si, že při iterace prostřednictvím kolekce vrácené `ConvertCollectionToUpperCase`, každá položka je načtena ze zdrojového pole řetězce a převedena na velká písmena před další položkou je načten ze zdrojového pole řetězce.  
  
 Můžete vidět, že celé pole řetězců není převedenna velká písmena před každou položku `foreach` v `Main`vrácené kolekci je zpracována ve smyčce v .  
  
 Další téma v tomto kurzu ilustruje řetězení dotazů dohromady:  
  
- [Příklad zřetězení dotazů (C#)](./chaining-queries-example.md)  
  
## <a name="see-also"></a>Viz také

- [Kurz: Řetězení dotazů dohromady (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
