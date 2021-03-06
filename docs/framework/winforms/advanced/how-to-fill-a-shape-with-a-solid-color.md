---
title: 'Postupy: Vyplnění obrazce plnou barvou'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], adding to shapes
- shapes [Windows Forms], filling
ms.assetid: 06088b31-bac9-4ef3-9ebe-06c2c764d6df
ms.openlocfilehash: d6fe7a252029ff80f21d99f7342fabb1d29fbe24
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781287"
---
# <a name="how-to-fill-a-shape-with-a-solid-color"></a>Postupy: Vyplnění obrazce plnou barvou
K vyplnění obrazce plnou barvou, vytvořit <xref:System.Drawing.SolidBrush> objektu a pak předejte, který <xref:System.Drawing.SolidBrush> objektu jako argument pro jednu z metod výplň <xref:System.Drawing.Graphics> třídy. Následující příklad ukazuje, jak vyplnit elipsu s červenou barvu.  
  
## <a name="example"></a>Příklad  
 V následujícím kódu <xref:System.Drawing.SolidBrush.%23ctor%2A> přebírá konstruktor <xref:System.Drawing.Color> objektu jako svůj jediný argument. Hodnot použitých <xref:System.Drawing.Color.FromArgb%2A> metoda představují alfa, červené, zelené a modré součásti barvy. Všechny tyto hodnoty musí být v rozsahu 0 až 255. První 255 znamená, že se barva úplně neprůhledná a druhý 255 znamená, že je hodnota červené na plné intenzity. Dvě nuly znamená, že součásti zelené a modré mít intenzitu zrcadlových 0.  
  
 Předány čtyři číslice (0, 0, 100, 60) <xref:System.Drawing.Graphics.FillEllipse%2A> metody zadejte umístění a velikost ohraničující obdélník elipsy. Obdélník má levého horního rohu (0, 0), 100 šířku a výšku 60.  
  
 [!code-csharp[System.Drawing.UsingABrush#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingABrush#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>Probíhá kompilace kódu  
 V předchozím příkladu je určený k použití pomocí Windows Forms a vyžaduje <xref:System.Windows.Forms.PaintEventArgs> `e`, což je parametr <xref:System.Windows.Forms.Control.Paint> obslužné rutiny události.  
  
## <a name="see-also"></a>Viz také:

- [Použití štětce k vyplnění obrazců](using-a-brush-to-fill-shapes.md)
