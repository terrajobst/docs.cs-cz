---
title: Delegáty a výrazy lambda
description: Zjistěte, jak delegáti definují typ, který určuje podpis konkrétní metody, který lze volat přímo nebo předán jiné metodě a volán.
author: richlander
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: fe2e4b4c-6483-4106-a4b4-a33e2e306591
ms.openlocfilehash: 34bfa4c6007ec771f784e927675f4e24d52e194f
ms.sourcegitcommit: a9b8945630426a575ab0a332e568edc807666d1b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391231"
---
# <a name="delegates-and-lambdas"></a>Delegáty a výrazy lambda

Delegáti definují typ, který určuje podpis konkrétní metody. Metoda (statická nebo instance), která splňuje tento podpis, může být přiřazena proměnné tohoto typu, poté volána přímo (s příslušnými argumenty) nebo předána jako samotný argument jiné metodě a poté volána. Následující příklad ukazuje použití delegáta.

```csharp
using System;
using System.Linq;

public class Program
{
    public delegate string Reverse(string s);

    static string ReverseString(string s)
    {
        return new string(s.Reverse().ToArray());
    }

    static void Main(string[] args)
    {
        Reverse rev = ReverseString;

        Console.WriteLine(rev("a string"));
    }
}
```

* Řádek `public delegate string Reverse(string s);` vytvoří typ delegáta určitého podpisu, v tomto případě metoda, která přebírá parametr řetězce a pak vrátí parametr řetězce.
* Metoda, `static string ReverseString(string s)` která má přesně stejný podpis jako definovaný typ delegáta, implementuje delegáta.
* Řádek `Reverse rev = ReverseString;` ukazuje, že můžete přiřadit metodu proměnné odpovídajícího typu delegáta.
* Řádek `Console.WriteLine(rev("a string"));` ukazuje, jak použít proměnnou typu delegáta k vyvolání delegáta.

Za účelem zjednodušení procesu vývoje obsahuje rozhraní .NET sadu typů delegátů, které mohou programátoři znovu použít a nemusí vytvářet nové typy. Jedná `Func<>`se `Action<>` `Predicate<>`o , a , a mohou být použity na různých místech v rámci rozhraní API .NET bez nutnosti definovat nové typy delegátů. Samozřejmě, tam jsou některé rozdíly mezi těmito třemi, jak uvidíte v jejich podpisy, které většinou mají co do činění s tím, jak byly určeny k použití:

* `Action<>`se používá, když je potřeba provést akci pomocí argumentů delegáta. Metoda zapouzdřuje nevrátí hodnotu.
* `Func<>`se obvykle používá, když máte transformace na skladě, to znamená, že je třeba transformovat argumenty delegáta do jiného výsledku. Projekce jsou toho ukázkovým příkladem. Metoda, kterou zapouzdřuje vrátí zadanou hodnotu.
* `Predicate<>`se používá, když potřebujete zjistit, zda argument splňuje podmínku delegáta. Může být také zapsán `Func<T, bool>`jako , což znamená, že metoda vrátí logickou hodnotu.

Nyní můžeme vzít náš příklad výše a `Func<>` přepsat jej pomocí delegáta namísto vlastního typu. Program bude pokračovat v spuštění přesně stejný.

```csharp
using System;
using System.Linq;

public class Program
{
    static string ReverseString(string s)
    {
        return new string(s.Reverse().ToArray());
    }

    static void Main(string[] args)
    {
        Func<string, string> rev = ReverseString;

        Console.WriteLine(rev("a string"));
    }
}
```

Pro tento jednoduchý příklad, s metodou `Main` definovanou mimo metodu se zdá být trochu nadbytečné. Je to proto, že rozhraní .NET Framework 2.0 představil koncept **anonymních delegátů**. S jejich podporou můžete vytvořit "inline" delegáty bez nutnosti zadávat další typ nebo metodu. Jednoduše zařazujete definici delegáta tam, kde ji potřebujete.

Například ji přepneme a použijeme anonymního delegáta k odfiltrování seznamu pouze sudých čísel a jejich vytištění do konzole.

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main(string[] args)
    {
        List<int> list = new List<int>();

        for (int i = 1; i <= 100; i++)
        {
            list.Add(i);
        }

        List<int> result = list.FindAll(
          delegate (int no)
          {
              return (no % 2 == 0);
          }
        );

        foreach (var item in result)
        {
            Console.WriteLine(item);
        }
    }
}
```

Jak můžete vidět, tělo delegáta je jen sada výrazů, jako každý jiný delegát. Ale místo toho, aby to byla samostatná definice, zavedli jsme <xref:System.Collections.Generic.List%601.FindAll%2A?displayProperty=nameWithType> ji _ad hoc_ v našem volání k metodě.

Nicméně, i s tímto přístupem, je stále mnoho kódu, který můžeme vyhodit. To je místo, kde **lambda výrazy** přicházejí do hry.

Lambda výrazy, nebo jen "lambdas" v krátkosti, byly zavedeny nejprve v Jazyce C# 3.0, jako jeden z základních stavebních bloků jazyka integrovaný dotaz (LINQ). Jsou to jen pohodlnější syntaxe pro použití delegátů. Deklarují podpis a tělo metody, ale nemají vlastní formální identitu, pokud nejsou přiřazeny delegátovi. Na rozdíl od delegátů mohou být přímo přiřazeny jako levá strana registrace událostí nebo v různých klauzulích a metodách LINQ.

Vzhledem k tomu, že výraz lambda je pouze dalším způsobem určení delegáta, měli bychom být schopni přepsat výše uvedenou ukázku tak, aby místo anonymního delegáta použilvýraz lambda.

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main(string[] args)
    {
        List<int> list = new List<int>();

        for (int i = 1; i <= 100; i++)
        {
            list.Add(i);
        }

        List<int> result = list.FindAll(i => i % 2 == 0);

        foreach (var item in result)
        {
            Console.WriteLine(item);
        }
    }
}
```

V předchozím příkladu je `i => i % 2 == 0`použitý výraz lambda . Opět je to jen **velmi** výhodná syntaxe pro použití delegátů, takže to, co se děje pod kryty, je podobné tomu, co se děje s anonymním delegátem.

Opět lambdas jsou pouze delegáti, což znamená, že mohou být použity jako obslužná rutina události bez problémů, jak ukazuje následující fragment kódu.

```csharp
public MainWindow()
{
    InitializeComponent();

    Loaded += (o, e) =>
    {
        this.Title = "Loaded";
    };
}
```

Operátor `+=` v tomto kontextu se používá k odběru [události](../../docs/csharp/language-reference/keywords/event.md). Další informace naleznete v tématu [Jak se přihlásit k odběru a odhlásit z odběru událostí](../../docs/csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).

## <a name="further-reading-and-resources"></a>Další čtení a zdroje

* [Delegáty](../../docs/csharp/programming-guide/delegates/index.md)
* [Anonymní funkce](../../docs/csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)
* [Výrazy lambda](../../docs/csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
