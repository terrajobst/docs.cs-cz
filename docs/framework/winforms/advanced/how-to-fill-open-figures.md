---
title: 'Postupy: Vyplňování otevřených obrázků'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- open figures [Windows Forms], filling
- figures [Windows Forms], filling
ms.assetid: 5a36b0e4-f1f4-46c0-a85a-22ae98491950
ms.openlocfilehash: 6ecea7d3edb0c3e25fb4e69ff12b88019e530021
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506071"
---
# <a name="how-to-fill-open-figures"></a>Postupy: Vyplňování otevřených obrázků
Můžete přejít k vyplnění cestu předáním <xref:System.Drawing.Drawing2D.GraphicsPath> objektu <xref:System.Drawing.Graphics.FillPath%2A> metoda. <xref:System.Drawing.Graphics.FillPath%2A> Metoda vyplní cestu podle režim vyplnění (alternativní nebo vinutí) aktuálně nastavený pro danou cestu. Pokud cesta obsahuje všechny otevřených obrázků, cesta je vyplněné, jakoby nebyly uzavřeny tyto údaje. Rozhraní GDI + zavře elementu figure podle Kreslení rovné čáry z koncového bodu pro výchozí bod.  
  
## <a name="example"></a>Příklad  
 Následující příklad vytvoří cestu, která má jeden otevřeného elementu figure (oblouku) a jednoho elementu figure uzavřený (Elipsa). <xref:System.Drawing.Graphics.FillPath%2A> Metoda vyplní cestu podle výchozí režim výplně, což je <xref:System.Drawing.Drawing2D.FillMode.Alternate>.  
  
 Následující obrázek znázorňuje výstup tohoto ukázkového kódu. Všimněte si, že ji naplní (podle <xref:System.Drawing.Drawing2D.FillMode.Alternate>) jako kdyby bylo uzavřeno otevřený útvar rovnou linii od její koncový bod pro výchozí bod.  
  
 ![Diagram, který zobrazuje výstup FillPath – metoda](./media/how-to-fill-open-figures/fill-path-alternate-mode.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>Probíhá kompilace kódu  
 V předchozím příkladu je určený k použití pomocí Windows Forms a vyžaduje <xref:System.Windows.Forms.PaintEventArgs> `e`, což je parametr <xref:System.Windows.Forms.Control.Paint> obslužné rutiny události.  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Drawing.Drawing2D.GraphicsPath>
- [Grafické cesty v GDI+](graphics-paths-in-gdi.md)
