---
ms.openlocfilehash: 1721d32f8cdc9b6ea4b4732e38afa56a8a532600
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62088470"
---
### <a name="dbparameterprecision-and-dbparameterscale-are-now-public-virtual-members"></a>DbParameter.Precision a DbParameter.Scale jsou teď virtuální veřejné členy

|   |   |
|---|---|
|Podrobnosti|<xref:System.Data.Common.DbParameter.Precision> a <xref:System.Data.Common.DbParameter.Scale> jsou implementovány jako virtuální veřejné vlastnosti. Nahrazují odpovídající implementace explicitního rozhraní <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Precision> a <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Scale>.|
|Doporučení|Při opětovné sestavování databáze poskytovatele ADO.NET, bude vyžadovat tyto rozdíly – klíčové slovo 'override' má použít u vlastnosti hodnot Precision a Scale. To je jenom nutné, když znovu sestavení součástí; existující binární soubory budou nadále fungovat.|
|Rozsah|Vedlejší|
|Version|4.5.1|
|Type|Změna cílení|
|Ovlivněná rozhraní API|<ul><li><xref:System.Data.Common.DbParameter.Precision?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbParameter.Scale?displayProperty=nameWithType></li></ul>|
