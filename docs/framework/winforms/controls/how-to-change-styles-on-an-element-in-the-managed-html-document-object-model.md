---
title: 'Postupy: Změna stylů v elementu v modelu spravovaného objektu dokumentu HTML'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- managed HTML DOM [Windows Forms], changing styles on elements
ms.assetid: 154e8d9f-3e2d-4e8b-a6f3-c85a070e9cc1
ms.openlocfilehash: 728bc77db959e25fe31d2ff37288b2359dca852e
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424595"
---
# <a name="how-to-change-styles-on-an-element-in-the-managed-html-document-object-model"></a>Postupy: Změna stylů v elementu v modelu spravovaného objektu dokumentu HTML

Styly ve formátu HTML můžete řídit vzhled dokument a jeho elementy. <xref:System.Windows.Forms.HtmlDocument> a <xref:System.Windows.Forms.HtmlElement> podporují <xref:System.Windows.Forms.HtmlElement.Style%2A> vlastnosti, které přijímají řetězce styl v následujícím formátu:

`name1:value1;...;nameN:valueN;`

Tady je `DIV` řetězcem styl, který nastaví na Arial a veškerý text tučné písmo:

```html
<DIV style="font-face:arial;font-weight:bold;">
Hello, world!
</DIV>
```

Problém s manipulace s použitím stylů <xref:System.Windows.Forms.HtmlElement.Style%2A> vlastnost je, že může být velmi náročná na přidání a odebrání nastavení jednotlivých stylu z řetězce. Například jej by se mohla stát složité postup vykreslit předchozí text kurzívou pokaždé, když se uživatel se umístí kurzor nad `DIV`a využijte kurzíva vypnout, když ukazatel opustí `DIV`. Čas by stát problémem, pokud potřebujete pracovat s velký počet styly tímto způsobem.

Následující postup obsahuje kód, který vám umožní snadno pracovat s styly u dokumentů HTML a prvky. Postup vyžaduje, že víte, jak provádět základní úlohy ve Windows Forms, jako je například vytvoření nového projektu a přidání ovládacího prvku na formulář.

### <a name="to-process-style-changes-in-a-windows-forms-application"></a>Ke zpracování změn stylů v aplikaci Windows Forms

1. Vytvoření nového projektu Windows Forms.

2. Vytvořte nový soubor třídy končící na rozšíření, které jsou vhodné pro vaše programovací jazyk.

3. Kopírovat `StyleGenerator` třídy do souboru třídy kód v oddíle Příklad tohoto tématu a uložit kód.

4. Následující kód HTML uložte do souboru s názvem Test.htm.

    ```html
    <HTML>
        <BODY>

            <DIV style="font-face:arial;font-weight:bold;">
                Hello, world!
            </DIV><P>

            <DIV>
                Hello again, world!
            </DIV><P>

        </BODY>
    </HTML>
    ```

5. Přidat <xref:System.Windows.Forms.WebBrowser> ovládací prvek s názvem `webBrowser1` hlavního formuláře do projektu.

6. Přidejte následující kód do souboru kódu projektu.

    > [!IMPORTANT]
    > Ujistěte se, že `webBrowser1_DocumentCompleted` obslužná rutina události je nakonfigurovaný jako naslouchací proces pro <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> událostí. V sadě Visual Studio, poklepejte na <xref:System.Windows.Forms.WebBrowser> ovládací prvek; v textovém editoru, nakonfigurujte naslouchací proces prostřednictvím kódu programu.

     [!code-csharp[ManagedDOMStyles#2](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/Form1.cs#2)]
     [!code-vb[ManagedDOMStyles#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/Form1.vb#2)]

7. Spusťte projekt. Spustit ukazatel myši nad první `DIV` chcete sledovat účinky kód.

## <a name="example"></a>Příklad

Následující příklad kódu ukazuje celý kód pro `StyleGenerator` třídu, která analyzuje existující hodnotu stylu, podporuje přidání, změně a odebrání styly a vrátí novou hodnotu stylu s požadované změny.

[!code-csharp[ManagedDOMStyles#1](~/samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/StyleGenerator.cs#1)]
[!code-vb[ManagedDOMStyles#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/StyleGenerator.vb#1)]

## <a name="see-also"></a>Viz také:

- <xref:System.Windows.Forms.HtmlElement>
