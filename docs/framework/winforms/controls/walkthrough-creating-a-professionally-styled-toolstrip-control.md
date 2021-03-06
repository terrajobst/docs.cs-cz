---
title: 'Návod: Vytvoření ovládacího prvku ToolStrip s profesionálním vzhledem'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStripRenderer class [Windows Forms]
- toolbars [Windows Forms], walkthroughs
- ToolStrip control [Windows Forms], creating professionally styled controls
ms.assetid: b52339ae-f1d3-494e-996e-eb455614098a
ms.openlocfilehash: 226e805d0240236899ee0cc290f1060a3b0aa391
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211761"
---
# <a name="walkthrough-creating-a-professionally-styled-toolstrip-control"></a>Návod: Vytvoření ovládacího prvku ToolStrip s profesionálním vzhledem

Aplikace můžete udělit <xref:System.Windows.Forms.ToolStrip> řídí profesionální vzhled a chování napsáním vlastní třídy odvozené od <xref:System.Windows.Forms.ToolStripProfessionalRenderer> typu.

Tento návod ukazuje, jak používat <xref:System.Windows.Forms.ToolStrip> ovládací prvky pro vytvoření složeného ovládacího prvku, který se podobá **navigačním podokně** poskytované Microsoft Outlook®. Tyto úlohy jsou uvedené v tomto návodu:

- Vytvoření projektu knihovny ovládacích prvků Windows.

- Návrh StackView ovládacího prvku.

- Implementace vlastní zobrazovací jednotky.

Až budete hotovi, budete mít opakovaně použitelné vlastní ovládací prvek s profesionální vzhled aplikace Microsoft Office® XP ovládacího prvku.

Pokud chcete zkopírovat kód v tomto tématu jako jeden seznam, naleznete v tématu [jak: Vytvoření ovládacího prvku ToolStrip s profesionálním](how-to-create-a-professionally-styled-toolstrip-control.md).

## <a name="prerequisites"></a>Požadavky

Visual Studio k dokončení tohoto návodu budete potřebovat.

## <a name="create-the-control-library-project"></a>Vytvoření projektu knihovny ovládacích prvků

1. V sadě Visual Studio vytvořte nový projekt knihovny ovládacích prvků Windows s názvem `StackViewLibrary`.

2. V **Průzkumníka řešení**, odstraňte výchozí ovládací prvek projektu tak, že odstraníte zdrojový soubor s názvem "UserControl1.cs" nebo "UserControl1.vb", v závislosti na vámi zvolený jazyk.

     Další informace najdete v tématu [jak: Odebrat, odstranit a vyloučit položky](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100)).

3. Přidat nový <xref:System.Windows.Forms.UserControl> položkou **StackViewLibrary** projektu. Zadejte základní název nového zdrojového souboru `StackView`.

## <a name="design-the-stackview-control"></a>Návrh StackView ovládacího prvku

`StackView` Složeného ovládacího prvku s jeden podřízený prvek je ovládací prvek <xref:System.Windows.Forms.ToolStrip> ovládacího prvku. Další informace o složených ovládacích prvků naleznete v tématu [typy Custom Controls](varieties-of-custom-controls.md).

1. Z **nástrojů**, přetáhněte <xref:System.Windows.Forms.ToolStrip> ovládací prvek na návrhovou plochu.

2. V **vlastnosti** okno, nastaveno <xref:System.Windows.Forms.ToolStrip> ovládacího prvku vlastnosti podle následující tabulky.

    |Vlastnost|Value|
    |--------------|-----------|
    |Name|`stackStrip`|
    |CanOverflow.|`false`|
    |Ukotvení|<xref:System.Windows.Forms.DockStyle.Bottom>|
    |Písma|`Tahoma, 10pt, style=Bold`|
    |GripStyle|<xref:System.Windows.Forms.ToolStripGripStyle.Hidden>|
    |LayoutStyle|<xref:System.Windows.Forms.ToolStripLayoutStyle.VerticalStackWithOverflow>|
    |Padding|`0, 7, 0, 0`|
    |RenderMode|<xref:System.Windows.Forms.ToolStripRenderMode.Professional>|

3. V Návrháři formulářů Windows, klikněte na tlačítko <xref:System.Windows.Forms.ToolStrip> ovládacího prvku **přidat** tlačítko a přidat <xref:System.Windows.Forms.ToolStripButton> k `stackStrip` ovládacího prvku.

4. V **vlastnosti** okno, nastaveno <xref:System.Windows.Forms.ToolStripButton> ovládacího prvku vlastnosti podle následující tabulky.

    |Vlastnost|Hodnota|
    |--------------|-----------|
    |Name|`mailStackButton`|
    |CheckOnClick|true|
    |– CheckState|<xref:System.Windows.Forms.CheckState.Checked>|
    |DisplayStyle|<xref:System.Windows.Forms.ToolStripItemDisplayStyle.ImageAndText>|
    |ImageAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|
    |ImageScaling|<xref:System.Windows.Forms.ToolStripItemImageScaling.None>|
    |ImageTransparentColor|`238, 238, 238`|
    |Okraj|`0, 0, 0, 0`|
    |Padding|`3, 3, 3, 3`|
    |Text|**e-mailu**|
    |TextAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|

5. Opakujte krok 7 pro tři další <xref:System.Windows.Forms.ToolStripButton> ovládacích prvků.

     Ovládací prvky pojmenujte `calendarStackButton`, `contactsStackButton`, a `tasksStackButton`. Nastavte hodnotu <xref:System.Windows.Forms.Control.Text%2A> vlastnost **kalendáře**, **kontakty**, a **úlohy**v uvedeném pořadí.

## <a name="handle-events"></a>Zpracování událostí

Dvě události jsou důležité, aby `StackView` ovládací prvek se chovají správně. Zpracování <xref:System.Windows.Forms.UserControl.Load> událost pro umístění ovládacího prvku správně. Zpracování <xref:System.Windows.Forms.ToolStripItem.Click> událost pro každou <xref:System.Windows.Forms.ToolStripButton> poskytnout `StackView` řídit chování stavu podobně jako <xref:System.Windows.Forms.RadioButton> ovládacího prvku.

1. V Návrháři formulářů Windows, vyberte `StackView` ovládacího prvku.

2. V **vlastnosti** okna, klikněte na tlačítko **události**.

3. Poklikáním na událost zatížení ke generování `StackView_Load` obslužné rutiny události.

4. V `StackView_Load` obslužná rutina události, zkopírujte a vložte následující kód.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#3)]

5. V Návrháři formulářů Windows, vyberte `mailStackButton` ovládacího prvku.

6. V **vlastnosti** okna, klikněte na tlačítko **události**.

7. Dvakrát klikněte na událost Click.

     Generuje Návrhář formulářů Windows `mailStackButton_Click` obslužné rutiny události.

8. Přejmenovat `mailStackButton_Click` obslužnou rutinu události `stackButton_Click`.

     Další informace najdete v tématu [kódu symbol refaktoring pro přejmenování](/visualstudio/ide/reference/rename).

9. Vložte následující kód do `stackButton_Click` obslužné rutiny události.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#4)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#4)]

10. V Návrháři formulářů Windows, vyberte `calendarStackButton` ovládacího prvku.

11. V **vlastnosti** okně, nastavte na hodnotu událost Click `stackButton_Click` obslužné rutiny události.

12. Opakujte kroky 10 a 11 pro `contactsStackButton` a `tasksStackButton` ovládací prvky.

## <a name="define-icons"></a>Definování ikony

Každý `StackView` má tlačítko přidružené ikonu. Pro usnadnění práce jednotlivé ikony je vyjádřena jako řetězec s kódováním Base64, který je deserializován před <xref:System.Drawing.Bitmap> se vytvoří z něj. V produkčním prostředí ukládat data rastrového obrázku jako prostředku a ikony se zobrazí v Návrháři formulářů Windows. Další informace najdete v tématu [jak: Přidání obrázků na pozadí do formulářů Windows](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dff9f95f(v=vs.100)).

1. V editoru kódu vložte následující kód do `StackView` definici třídy. Tento kód inicializuje rastrové obrázky pro <xref:System.Windows.Forms.ToolStripButton> ikony.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#2)]

2. Přidejte volání `InitializeImages` metoda ve `StackView` konstruktoru třídy.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]

## <a name="implement-a-custom-renderer"></a>Implementace vlastního rendereru

Můžete přizpůsobit většinu prvků `StackView` řídit Moje implementace, která je odvozena z třídy <xref:System.Windows.Forms.ToolStripRenderer> třídy. V tomto postupu budete implementovat <xref:System.Windows.Forms.ToolStripProfessionalRenderer> třídu, která přizpůsobí úchytu a vykreslí barevného přechodu pozadí <xref:System.Windows.Forms.ToolStripButton> ovládacích prvků.

1. Vložte následující kód do `StackView` definici ovládacího prvku.

     Toto je definice `StackRenderer` třídy, která přepisuje <xref:System.Windows.Forms.ToolStripRenderer.RenderGrip>, <xref:System.Windows.Forms.ToolStripRenderer.RenderToolStripBorder>, a <xref:System.Windows.Forms.ToolStripRenderer.RenderButtonBackground> metody k vytvoření vlastní vzhled.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#10)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#10)]

2. V `StackView` konstruktoru ovládacího prvku, vytvořte novou instanci třídy `StackRenderer` třídy a přiřazení této instance `stackStrip` ovládacího prvku <xref:System.Windows.Forms.ToolStrip.Renderer%2A> vlastnost.

     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]

## <a name="test-the-stackview-control"></a>Testování StackView ovládacího prvku

`StackView` Ovládacího prvku je odvozena z <xref:System.Windows.Forms.UserControl> třídy. Proto můžete otestovat ovládací prvek s **kontejner testu UserControl**. Další informace najdete v tématu [jak: Testování běhového chování UserControl](how-to-test-the-run-time-behavior-of-a-usercontrol.md).

1. Stisknutím klávesy **F5** projekt sestavit a spustit **UserControl – kontejner testů**.

2. Přesuňte ukazatel nad tlačítek `StackView` ovládací prvek a potom klikněte na tlačítko zobrazit vzhled vybraný stav.

## <a name="next-steps"></a>Další kroky

V tomto návodu vytvoříte opakovaně použitelné vlastní ovládací prvek s profesionální vzhled ovládacího prvku Office XP. Můžete použít <xref:System.Windows.Forms.ToolStrip> řady ovládacích prvků pro mnoho dalších důvodů:

- Vytváření místních nabídek pro vaše ovládací prvky s <xref:System.Windows.Forms.ContextMenuStrip>. Další informace najdete v tématu [ContextMenu – přehled komponenty](contextmenu-component-overview-windows-forms.md).

- Vytvoření formuláře se automaticky vyplněná standardní nabídky. Další informace najdete v tématu [názorný postup: Poskytnutí standardních položek nabídky formuláři](walkthrough-providing-standard-menu-items-to-a-form.md).

- Vytvoření více formuláře (MDI interface) dokumentu s ukotvení <xref:System.Windows.Forms.ToolStrip> ovládacích prvků. Další informace najdete v tématu [jak: Vytvoření formuláře MDI s ovládacími prvky ToolStrip a slučování nabídek](how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md).

## <a name="see-also"></a>Viz také:

- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [Ovládací prvek ToolStrip](toolstrip-control-windows-forms.md)
- [Postupy: Zajištění standardních položek nabídky pro formulář](how-to-provide-standard-menu-items-to-a-form.md)
