---
title: Odvození textu elementu
ms.date: 03/30/2017
ms.assetid: 789799e5-716f-459f-a168-76c5cf22178b
ms.openlocfilehash: 3fdd110a14ddfd6065ed552171a8d76ef64e2fb5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784536"
---
# <a name="inferring-element-text"></a>Odvození textu elementu
Pokud element obsahuje text a nemá odvoditelné žádné podřízené prvky jako tabulky (například elementy s atributy nebo opakujícími se prvky), přidá se do tabulky, která je odvozena pro prvek, nový sloupec s názvem **TableName_Text** . Text obsažený v elementu se přidá do řádku v tabulce a uloží se do nového sloupce. Vlastnost **ColumnMapping** nového sloupce bude nastavena na **MappingType. SimpleContent**.  
  
 Zvažte například následující kód XML.  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1">Text1</Element1>  
</DocumentElement>  
```  
  
 Proces odvození vytvoří tabulku s názvem **Element1** se dvěma sloupci: **attr1** a **Element1_Text**. Vlastnost **ColumnMapping** sloupce **attr1** bude nastavena na **MappingType. Attribute**. Vlastnost **ColumnMapping** sloupce **Element1_Text** bude nastavena na **MappingType. SimpleContent**.  
  
 **Integrován** DocumentElement  
  
 **Stolní** Element1  
  
|attr1|Element1_Text|  
|-----------|--------------------|  
|Hodnota1|Text1|  
  
 Pokud element obsahuje text, ale také obsahuje podřízené prvky, které obsahují text, sloupec nebude přidán do tabulky, aby ukládal text obsažený v elementu. Text obsažený v elementu bude ignorován, zatímco text v podřízených prvcích je zahrnut do řádku v tabulce. Zvažte například následující kód XML.  
  
```xml  
<Element1>  
  Text1  
  <ChildElement1>Text2</ChildElement1>  
  Text3  
</Element1>  
```  
  
 Proces odvození vytvoří tabulku s názvem **Element1** s jedním sloupcem s názvem **ChildElement1**. Text elementu **ChildElement1** bude zahrnut do řádku v tabulce. Druhý text bude ignorován. Vlastnost **ColumnMapping** sloupce **ChildElement1** bude nastavena na **MappingType. element**.  
  
 **Integrován** DocumentElement  
  
 **Stolní** Element1  
  
|ChildElement1|  
|-------------------|  
|Text2|  
  
## <a name="see-also"></a>Viz také:

- [Odvození relační struktury datové sady z XML](inferring-dataset-relational-structure-from-xml.md)
- [Načtení datové sady z XML](loading-a-dataset-from-xml.md)
- [Načtení informací o schématu datové sady z XML](loading-dataset-schema-information-from-xml.md)
- [Použití XML v datové sadě](using-xml-in-a-dataset.md)
- [Datové sady, datové tabulky a datová zobrazení](index.md)
- [Přehled ADO.NET](../ado-net-overview.md)
