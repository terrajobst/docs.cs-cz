---
title: 'Postupy: Podpora zprostředkovatele komunikace s objekty COM zobrazením formuláře Windows pomocí metody ShowDialog'
ms.date: 03/30/2017
helpviewer_keywords:
- COM [Windows Forms]
- Windows Forms, unmanaged
- COM interop [Windows Forms], calling methods
- ActiveX controls [Windows Forms], COM interop
- Windows Forms, interop
ms.assetid: 87aac8ad-3c04-43b3-9b0c-d0b00df9ee74
ms.openlocfilehash: f2fb48e07243694b14904b240bdcb0739175c2fc
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593526"
---
# <a name="how-to-support-com-interop-by-displaying-a-windows-form-with-the-showdialog-method"></a>Postupy: Podpora zprostředkovatele komunikace s objekty COM zobrazením formuláře Windows pomocí metody ShowDialog
Vyřešíte problémy vzájemná funkční spolupráce modelu COM (Component Object) zobrazením formuláře Windows ve smyčce zprávy rozhraní .NET Framework, která je vytvořena pomocí <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> metody.  
  
 Chcete-li formuláře fungovat správně z klientské aplikace modelu COM, musíte ho spustit na smyčku zpráv Windows Forms. K tomuto účelu použijte jednu z následujících postupů:  
  
- Použití <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metodu pro zobrazení formuláři Windows.  
  
- Každý formulář Windows pro zobrazení na samostatném vlákně. Další informace najdete v tématu [jak: Podpora komunikace s objekty COM zobrazením jednotlivých formulářů Windows ve vlastním vlákně](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md).  
  
## <a name="procedure"></a>Postup  
 Použití <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metoda může být nejjednodušší způsob, jak zobrazit formulář ve smyčce zpráv rozhraní .NET Framework, protože všechny přístupy, vyžaduje nejmenší kód pro implementaci.  
  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> Metody pozastaví smyčky zpráv nespravovaná aplikace a zobrazí formulář jako dialogové okno. Protože smyčky zpráv hostitelská aplikace je pozastavená, <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metoda vytvoří nový smyčky zpráv rozhraní .NET Framework pro zpracování zpráv formuláře.  
  
 Nevýhodou použití <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metody je, že formulář se otevřou jako modální dialogové okno. Toto chování bloky uživatelského rozhraní (UI) v volající aplikace při otevřeném formuláři Windows. Když uživatel zavře formulář, ukončí smyčku zpráv rozhraní .NET Framework a smyčky zpráv starší aplikace znovu spustí.  
  
 Můžete vytvořit knihovnu tříd ve Windows Forms, který obsahuje metodu k zobrazení formuláře a následně vytvořit knihovnu tříd pro spolupráci s COM. Tento soubor knihovny DLL v jazyce Visual Basic 6.0 nebo Microsoft Foundation Classes (MFC) můžete použít, a pomocí kteréhokoli z těchto prostředí můžete volat <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metody k zobrazení formuláře.  
  
#### <a name="to-support-com-interop-by-displaying-a-windows-form-with-the-showdialog-method"></a>Pro podporu komunikace s objekty COM zobrazením windows form pomocí metody ShowDialog  
  
- Nahraďte všechna volání <xref:System.Windows.Forms.Form.Show%2A?displayProperty=nameWithType> metodu volání <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> metoda v rozhraní .NET Framework komponentě.  
  
## <a name="see-also"></a>Viz také:

- [Vystavení komponent architektury .NET Framework pro COM](../../interop/exposing-dotnet-components-to-com.md)
- [Postupy: Podpora komunikace s objekty COM zobrazením jednotlivých formulářů Windows ve vlastním vlákně](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)
- [Model Windows Forms a nespravované aplikace](windows-forms-and-unmanaged-applications.md)
