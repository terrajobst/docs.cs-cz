---
ms.openlocfilehash: cf1a8169351e29c18d85303fb32d4394877448f4
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/18/2019
ms.locfileid: "59803713"
---
### <a name="log-file-name-created-by-the-objectcontextcreatedatabase-method-has-changed-to-match-sql-server-specifications"></a>Změnil se název souboru protokolu vytvořené metodou ObjectContext.CreateDatabase tak, aby odpovídaly specifikace serveru SQL Server

|   |   |
|---|---|
|Podrobnosti|Když <xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=name> metoda je volána buď přímo nebo pomocí Code First se zprostředkovatelem SqlClient a je hodnota AttachDBFilename připojovacího řetězce, vytvoří soubor protokolu s názvem filename_log.ldf místo filename.ldf (kde název_souboru je název soubor určený hodnotou AttachDBFilename). Tato změna zlepšuje ladění poskytnutím souboru protokolu s názvem podle specifikace serveru SQL Server.|
|Doporučení|Pokud název souboru protokolu je důležité pro aplikace, aplikace se musí aktualizovat můžete očekávat formát názvu souboru standardní _log.ldf.|
|Rozsah|Edge|
|Version|4.5|
|Type|Modul runtime|
|Ovlivněná rozhraní API|<ul><li><xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=nameWithType></li></ul>|
