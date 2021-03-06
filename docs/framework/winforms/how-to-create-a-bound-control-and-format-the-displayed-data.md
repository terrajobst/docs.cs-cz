---
title: 'Postupy: Vytvoření připojeného ovládacího prvku a formátování zobrazených dat'
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], formatting
- bound controls [Windows Forms], creating
- bound controls [Windows Forms], formatting data
ms.assetid: d5a56228-899d-41d9-8af8-87b3f4ec2f94
ms.openlocfilehash: 543775894994c518d6069f697b145cedaa7af5b0
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015651"
---
# <a name="how-to-create-a-bound-control-and-format-the-displayed-data"></a>Postupy: Vytvoření připojeného ovládacího prvku a formátování zobrazených dat

Pomocí model Windows Forms datové vazby můžete naformátovat data zobrazená v ovládacím prvku vázaného na data pomocí dialogového okna **formátování a rozšířené vazby** .

## <a name="to-bind-a-control-and-format-the-displayed-data"></a>Navázání ovládacího prvku a formátování zobrazených dat

1. Připojte se ke zdroji dat. Další informace najdete v tématu [připojení ke zdroji dat](../data/adonet/connecting-to-a-data-source.md).

2. V aplikaci Visual Studio vyberte ovládací prvek ve formuláři a poté otevřete okno **vlastnosti** .

3. Rozbalte vlastnost **(DataBindings)** a pak v poli **(rozšířeném)** klikněte na tlačítko se třemi tečkami (![tlačítko se třemi tečkami (...) v okno Vlastnosti sady Visual](./media/how-to-create-a-bound-control-and-format-the-displayed-data/visual-studio-ellipsis-button.png)Studio) a zobrazte **formátování a rozšířené možnosti.** Dialogové okno vazby, které obsahuje úplný seznam vlastností pro tento ovládací prvek.

4. Vyberte vlastnost, kterou chcete svázat, a pak vyberte šipku **vazby** .

     Zobrazí se seznam dostupných zdrojů dat.

5. Rozbalte zdroj dat, ke kterému chcete vytvořit vazby, dokud nenajdete jeden datový prvek, který chcete.

     Pokud například vytváříte vazbu k hodnotě sloupce v tabulce datové sady, rozbalíte název datové sady a potom rozbalíte název tabulky pro zobrazení názvů sloupců.

6. Vyberte název prvku, ke kterému se má vytvořit vazba.

7. V poli **typ formátu** vyberte formát, který chcete použít pro data zobrazená v ovládacím prvku.

     V každém případě můžete zadat hodnotu zobrazenou v ovládacím prvku, pokud zdroj dat obsahuje <xref:System.DBNull>. V opačném případě se možnosti mírně liší v závislosti na zvoleném typu formátu. V následující tabulce jsou uvedeny typy a možnosti formátu.

    |Typ formátu|Možnost formátování|
    |-----------------|-----------------------|
    |Žádné formátování|Žádné možnosti.|
    |Numeric|Určete počet desetinných míst pomocí ovládacího prvku **desetinná místa** .|
    |Měna|Určete počet desetinných míst pomocí ovládacího prvku **desetinná místa** .|
    |Datum a čas|Vyberte, jak se má datum a čas zobrazit výběrem jedné z položek v poli Výběr **typu** .|
    |Odbornou|Určete počet desetinných míst pomocí ovládacího prvku **desetinná místa** .|
    |Vlastní|Zadejte řetězec vlastního formátu pomocí.<br /><br /> Další informace najdete v tématu [formátování typů](../../standard/base-types/formatting-types.md). **Poznámka:**  Řetězce vlastního formátu nejsou zaručené k úspěšnému zacyklení cest mezi zdrojem dat a vázaným ovládacím prvkem. Místo toho zpracujte <xref:System.Windows.Forms.Binding.Parse> událost <xref:System.Windows.Forms.Binding.Format> nebo pro vazbu a použijte vlastní formátování v kódu pro zpracování událostí.|

8. Kliknutím na **tlačítko OK** zavřete dialogové okno **formátování a rozšířené vazby** a vraťte se do okno Vlastnosti.

## <a name="see-also"></a>Viz také:

- [Postupy: Vytvoření jednoduchého ovládacího prvku vázaného na formuláři Windows](how-to-create-a-simple-bound-control-on-a-windows-form.md)
- [Ověřování uživatelského vstupu ve Windows Forms](user-input-validation-in-windows-forms.md)
- [Windows Forms – datová vazba](windows-forms-data-binding.md)
