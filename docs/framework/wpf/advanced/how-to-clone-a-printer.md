---
title: 'Postupy: Klonování tiskárny'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- print queues [WPF]
- cloning printers [WPF]
- printers [WPF], cloning
- print queues [WPF], cloning
- cloning print queues [WPF]
ms.assetid: dd6997c9-fe04-40f8-88a6-92e3ac0889eb
ms.openlocfilehash: e6af8d6410c4e383990bdaa27f97cc698be71719
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649203"
---
# <a name="how-to-clone-a-printer"></a>Postupy: Klonování tiskárny
Většina podniků v určitém okamžiku koupit více tiskáren stejného modelu. Obvykle tyto jsou nainstalovány s nastavením konfigurace prakticky totožný. Instalace tiskárny, může být časově náročné a náchylné k chybám. <xref:System.Printing.IndexedProperties?displayProperty=nameWithType> Obor názvů a <xref:System.Printing.PrintServer.InstallPrintQueue%2A> třídu, která jsou přístupné pomocí rozhraní Microsoft .NET Framework umožňuje okamžitě nainstalovat libovolný počet dalších tiskové fronty, které se klonují z existující tiskovou frontu.  
  
## <a name="example"></a>Příklad  
 V následujícím příkladu je druhý tiskovou frontu naklonovali z existující tiskovou frontu. Druhý se liší od první pouze v jeho název, umístění, port a sdílený stav. Hlavní kroky tohoto postupu jsou následující.  
  
1. Vytvoření <xref:System.Printing.PrintQueue> objektu, která se má klonovat existující tiskárny.  
  
2. Vytvoření <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> z <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> z <xref:System.Printing.PrintQueue>. <xref:System.Collections.DictionaryEntry.Value%2A> Vlastností pro každou položku ve slovníku je objekt jednoho z typů odvozených z <xref:System.Printing.IndexedProperties.PrintProperty>. Existují dva způsoby, jak nastavit hodnotu položky ve slovníku.  
  
    - Použití slovníku **odebrat** a <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.Add%2A> metody odeberte položku a poté znovu přidejte požadovanou hodnotu.  
  
    - Použití slovníku <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.SetProperty%2A> metody.  
  
     Následující příklad znázorňuje oba způsoby.  
  
3. Vytvoření <xref:System.Printing.IndexedProperties.PrintBooleanProperty> objektu a nastavte jeho <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> na "IsShared" a jeho <xref:System.Printing.IndexedProperties.PrintBooleanProperty.Value%2A> k `true`.  
  
4. Použití <xref:System.Printing.IndexedProperties.PrintBooleanProperty> objekt má být hodnota <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>na položku "IsShared".  
  
5. Vytvoření <xref:System.Printing.IndexedProperties.PrintStringProperty> objektu a nastavte jeho <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> na "ShareName" a jeho <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> na odpovídající <xref:System.String>.  
  
6. Použití <xref:System.Printing.IndexedProperties.PrintStringProperty> objekt má být hodnota <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>na položku "ShareName".  
  
7. Vytvořte další <xref:System.Printing.IndexedProperties.PrintStringProperty> objektu a nastavte jeho <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> "Umístění" a jeho <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> na odpovídající <xref:System.String>.  
  
8. Použijte druhý <xref:System.Printing.IndexedProperties.PrintStringProperty> objekt má být hodnota <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>na položku "Umístění".  
  
9. Vytvoření pole <xref:System.String>s. Každá položka je název portu na serveru.  
  
10. Použití <xref:System.Printing.PrintServer.InstallPrintQueue%2A> k instalaci nové tiskárny s novými hodnotami.  
  
 Příkladem je níže.  
  
 [!code-csharp[ClonePrinter#ClonePrinter](~/samples/snippets/csharp/VS_Snippets_Wpf/ClonePrinter/CSharp/Program.cs#cloneprinter)]
 [!code-vb[ClonePrinter#ClonePrinter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClonePrinter/visualbasic/program.vb#cloneprinter)]  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Printing.IndexedProperties>
- <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.PrintQueue>
- <xref:System.Collections.DictionaryEntry>
- [Dokumenty v platformě WPF](documents-in-wpf.md)
- [Přehled tisku](printing-overview.md)
