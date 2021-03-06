---
title: Jak implementovat zjednodušenou třídu s automaticky implementovanými vlastnostmi - C# Programming Guide
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.assetid: 1dc5a8ad-a4f7-4f32-8506-3fc6d8c8bfed
ms.openlocfilehash: 6d121f6be768d41d22ea01d871662913b2daae2b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/14/2020
ms.locfileid: "79170270"
---
# <a name="how-to-implement-a-lightweight-class-with-auto-implemented-properties-c-programming-guide"></a>Jak implementovat zjednodušenou třídu s automaticky implementovanými vlastnostmi (Průvodce programováním jazyka C#)

Tento příklad ukazuje, jak vytvořit neměnné zjednodušené třídy, která slouží pouze k zapouzdření sadu automaticky implementované vlastnosti. Použijte tento druh konstrukce namísto struktury, když je nutné použít sémantiku typu odkazu.

Neměnnou vlastnost můžete vytvořit dvěma způsoby:

- Můžete deklarovat [nastavit](../../language-reference/keywords/set.md) přistupující ho jako [soukromé](../../language-reference/keywords/private.md).  Vlastnost je pouze settable v rámci typu, ale je neměnné pro spotřebitele.

  Při deklarování privátní `set` ho přistupujícího objektu nelze použít inicializační objekt inicializovat vlastnost. Je nutné použít konstruktor nebo metodu výroby.
- Můžete deklarovat pouze [get](../../language-reference/keywords/get.md) přistupující objekt, který umožňuje vlastnost neměnné všude s výjimkou konstruktoru typu.

Následující příklad ukazuje, jak se vlastnost s pouze get accessor liší než s get a private set.

```csharp
class Contact
{
    public string Name { get; }
    public string Address { get; private set; }

    public Contact(string contactName, string contactAddress)
    {
        // Both properties are accessible in the constructor.
        Name = contactName;
        Address = contactAddress;
    }

    // Name isn't assignable here. This will generate a compile error.
    //public void ChangeName(string newName) => Name = newName;

    // Address is assignable here.
    public void ChangeAddress(string newAddress) => Address = newAddress
}
```

## <a name="example"></a>Příklad

Následující příklad ukazuje dva způsoby implementace neměnné třídy, která má automaticky implementované vlastnosti. Každý způsob deklaruje jednu z vlastností s privátní `set` a jednu z vlastností s `get` pouze.  První třída používá konstruktor pouze k inicializaci vlastností a druhá třída používá statickou metodu factory, která volá konstruktor.

```csharp
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// constructor to initialize its properties.
class Contact
{
    // Read-only property.
    public string Name { get; }

    // Read-write property with a private set accessor.
    public string Address { get; private set; }

    // Public constructor.
    public Contact(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }
}

// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// static method and private constructor to initialize its properties.
public class Contact2
{
    // Read-write property with a private set accessor.
    public string Name { get; private set; }

    // Read-only property.
    public string Address { get; }

    // Private constructor.
    private Contact2(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }

    // Public factory method.
    public static Contact2 CreateContact(string name, string address)
    {
        return new Contact2(name, address);
    }
}

public class Program
{
    static void Main()
    {
        // Some simple data sources.
        string[] names = {"Terry Adams","Fadi Fakhouri", "Hanying Feng",
                            "Cesar Garcia", "Debra Garcia"};
        string[] addresses = {"123 Main St.", "345 Cypress Ave.", "678 1st Ave",
                                "12 108th St.", "89 E. 42nd St."};

        // Simple query to demonstrate object creation in select clause.
        // Create Contact objects by using a constructor.
        var query1 = from i in Enumerable.Range(0, 5)
                    select new Contact(names[i], addresses[i]);

        // List elements cannot be modified by client code.
        var list = query1.ToList();
        foreach (var contact in list)
        {
            Console.WriteLine("{0}, {1}", contact.Name, contact.Address);
        }

        // Create Contact2 objects by using a static factory method.
        var query2 = from i in Enumerable.Range(0, 5)
                        select Contact2.CreateContact(names[i], addresses[i]);

        // Console output is identical to query1.
        var list2 = query2.ToList();

        // List elements cannot be modified by client code.
        // CS0272:
        // list2[0].Name = "Eugene Zabokritski";

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

/* Output:
    Terry Adams, 123 Main St.
    Fadi Fakhouri, 345 Cypress Ave.
    Hanying Feng, 678 1st Ave
    Cesar Garcia, 12 108th St.
    Debra Garcia, 89 E. 42nd St.
*/
```

Kompilátor vytvoří záložní pole pro každou automaticky implementovanou vlastnost. Pole nejsou přístupná přímo ze zdrojového kódu.

## <a name="see-also"></a>Viz také

- [Vlastnosti](./properties.md)
- [Struct](../../language-reference/builtin-types/struct.md)
- [Inicializátory objektu a kolekce](./object-and-collection-initializers.md)
