---
title: Sub – procedury
ms.date: 07/20/2015
helpviewer_keywords:
- Sub procedures [Visual Basic], about Sub procedures
- statement blocks
- Sub procedures [Visual Basic], calling
- procedures [Visual Basic], calling
- Sub procedures [Visual Basic], syntax
- Sub procedures
- procedures [Visual Basic], Sub
- syntax [Visual Basic], Sub procedures
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
ms.openlocfilehash: 9ca1d302a0bc8e989e0b2dddf8cce68e89211d57
ms.sourcegitcommit: 5d769956a04b6d68484dd717077fabc191c21da5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2020
ms.locfileid: "76163810"
---
# <a name="sub-procedures-visual-basic"></a>Procedury Sub (Visual Basic)

Procedura `Sub` je série Visual Basic příkazů, které jsou uzavřeny příkazy `Sub` a `End Sub`. Procedura `Sub` provede úlohu a vrátí řízení volajícímu kódu, ale nevrátí hodnotu volajícímu kódu.

Pokaždé, když je procedura volána, její příkazy jsou spouštěny, počínaje prvním spustitelným příkazem po příkazu `Sub` a končící prvním `End Sub`, `Exit Sub`nebo `Return`m příkazem.

Můžete definovat `Sub` proceduru v modulech, třídách a strukturách. Ve výchozím nastavení je `Public`, což znamená, že ho můžete volat odkudkoli v aplikaci, která má přístup k modulu, třídě nebo struktuře, ve které jste ji definovali. Pojem *Metoda* popisuje `Sub` nebo `Function` postup, který je k dispozici vně jeho definujícího modulu, třídy nebo struktury. Další informace najdete v tématu [postupy](./index.md).

`Sub` procedura může přebírat argumenty, jako jsou konstanty, proměnné nebo výrazy, které jsou předány volajícím kódem.

## <a name="declaration-syntax"></a>Syntaxe deklarace

Syntaxe pro deklaraci `Sub` postup je následující:

```vb
[modifiers] Sub SubName[(parameterList)]
    ' Statements of the Sub procedure.
End Sub
```

`modifiers` může určovat úroveň přístupu a informace o přetížení, přepsání, sdílení a stínování. Další informace naleznete v tématu [Sub Statement](../../../language-reference/statements/sub-statement.md).

## <a name="parameter-declaration"></a>Deklarace parametru

Každý parametr procedury deklarujete podobně, jak deklarujete proměnnou, zadáním názvu parametru a datového typu. Můžete také zadat mechanismus předávání a to, zda je parametr volitelný, nebo pole parametrů.

Syntaxe pro každý parametr v seznamu parametrů je následující:

```vb
[Optional] [ByVal | ByRef] [ParamArray] parameterName As DataType
```

Pokud je parametr volitelný, musíte také zadat výchozí hodnotu jako součást její deklarace. Syntaxe pro určení výchozí hodnoty je následující:

```vb
Optional [ByVal | ByRef]  parameterName As DataType = defaultValue
```

### <a name="parameters-as-local-variables"></a>Parametry jako lokální proměnné

Při předání řízení proceduře je každý parametr považován za místní proměnnou. To znamená, že jeho životnost je stejná jako procedura a jeho rozsah je celý postup.

## <a name="calling-syntax"></a>Syntaxe volání

Vyvoláte `Sub` proceduru explicitně pomocí příkazu samostatného volání. Nemůžete ji volat pomocí jejího názvu ve výrazu. Je nutné zadat hodnoty pro všechny argumenty, které nejsou volitelné, a je třeba uzavřít seznam argumentů v závorkách. Pokud nejsou zadány žádné argumenty, můžete volitelně vynechat závorky. Použití klíčového slova `Call` je volitelné, ale nedoporučuje se.

Syntaxe pro volání `Sub` postup je následující:

```vb
[Call] SubName[(argumentlist)]
```

Metodu `Sub` můžete volat vně třídy, která ji definuje. Nejdříve je nutné použít klíčové slovo `New` pro vytvoření instance třídy nebo volání metody, která vrací instanci třídy. Další informace najdete v tématu [New operator](../../../language-reference/operators/new-operator.md). Pak můžete použít následující syntaxi pro volání metody `Sub` objektu instance:

```vb
object.MethodName[(argumentList)]
```

### <a name="illustration-of-declaration-and-call"></a>Ilustrace deklarace a volání

Následující postup `Sub` informuje operátora počítače, který úkol aplikace provede, a také zobrazí časové razítko. Namísto duplikování tohoto kódu na začátku každé úlohy aplikace volá pouze `tellOperator` z různých umístění. Každé volání předá řetězec v argumentu `task`, který identifikuje spuštěnou úlohu.

[!code-vb[VbVbcnProcedures#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#2)]

Následující příklad ukazuje typické volání `tellOperator`.

[!code-vb[VbVbcnProcedures#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#3)]

## <a name="see-also"></a>Viz také:

- [Procedury](./index.md)
- [Procedury funkce](./function-procedures.md)
- [Procedury vlastnosti](./property-procedures.md)
- [Procedury operátoru](./operator-procedures.md)
- [Parametry a argumenty procedury](./procedure-parameters-and-arguments.md)
- [Příkaz Sub](../../../language-reference/statements/sub-statement.md)
- [Postupy: Volání procedury, která nevrací hodnotu](./how-to-call-a-procedure-that-does-not-return-a-value.md)
- [Postupy: volání obslužné rutiny události v Visual Basic](./how-to-call-an-event-handler.md)
