---
title: 'Postupy: Animace EllipseGeometry'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], EllipseGeometry objects [WPF]
- EllipseGeometry objects [WPF], animating
- graphics [WPF], animation
ms.assetid: 767b9b6e-9cb7-482e-b6c2-fee7750c3995
ms.openlocfilehash: 0f8174a2144435c9ad65904ee587355e8b38e935
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760919"
---
# <a name="how-to-animate-an-ellipsegeometry"></a>Postupy: Animace EllipseGeometry
Tento příklad ukazuje, jak animovat <xref:System.Windows.Media.Geometry> v rámci <xref:System.Windows.Shapes.Path> elementu. V následujícím příkladu <xref:System.Windows.Media.Animation.PointAnimation> je použít pro animaci <xref:System.Windows.Media.EllipseGeometry.Center%2A> ze <xref:System.Windows.Media.EllipseGeometry>.  
  
## <a name="example"></a>Příklad  
 [!code-xaml[animatepath_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/animatepath_snip_XAML/CS/EllipseGeometryExample.xaml#1)]  
  
 [!code-csharp[animatepath_snip#101](~/samples/snippets/csharp/VS_Snippets_Wpf/animatepath_snip/CSharp/EllipseGeometryExample.cs#101)]  
  
 [!code-vb[animatepath_snip#201](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animatepath_snip/VisualBasic/EllipseGeometryExample.vb#201)]  
  
## <a name="see-also"></a>Viz také:

- [Přehled animace](animation-overview.md)
- [Přehled geometrie](geometry-overview.md)
