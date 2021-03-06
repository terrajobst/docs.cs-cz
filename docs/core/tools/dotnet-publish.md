---
title: dotnet publikovat, příkaz
description: Příkaz publikování dotnet publikuje projekt nebo řešení .NET Core do adresáře.
ms.date: 02/24/2020
ms.openlocfilehash: ed5b87b3343210ca81486ef4b9a9d70d1b534464
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80110968"
---
# <a name="dotnet-publish"></a>dotnet publish

**Tento článek se týká:** ✔️ .NET Core 2.1 SDK a novější verze

## <a name="name"></a>Name (Název)

`dotnet publish`- Publikuje aplikaci a její závislosti do složky pro nasazení do hostitelského systému.

## <a name="synopsis"></a>Synopse

```dotnetcli
dotnet publish [<PROJECT>|<SOLUTION>] [-c|--configuration]
    [-f|--framework] [--force] [--interactive] [--manifest]
    [--no-build] [--no-dependencies] [--no-restore] [--nologo]
    [-o|--output] [-r|--runtime] [--self-contained]
    [--no-self-contained] [-v|--verbosity] [--version-suffix]

dotnet publish [-h|--help]
```

## <a name="description"></a>Popis

`dotnet publish`zkompiluje aplikaci, pročte její závislosti zadané v souboru projektu a publikuje výslednou sadu souborů do adresáře. Výstup zahrnuje následující aktiva:

- Kód zprostředkujícího jazyka (IL) v sestavení s rozšířením *dll.*
- Soubor *.deps.json,* který obsahuje všechny závislosti projektu.
- Soubor *.runtimeconfig.json,* který určuje sdílený runtime, který aplikace očekává, stejně jako další možnosti konfigurace pro runtime (například typ uvolňování paměti).
- Závislosti aplikace, které jsou zkopírovány z mezipaměti NuGet do výstupní složky.

Výstup `dotnet publish` příkazu je připraven k nasazení do hostitelského systému (například server, PC, Mac, notebook) pro spuštění. Je to jediný oficiálně podporovaný způsob, jak připravit aplikaci pro nasazení. V závislosti na typu nasazení, který projekt určuje, může nebo nemusí mít hostitelský systém na něm nainstalovanou sdílenou runtime .NET Core.

## <a name="arguments"></a>Argumenty

- **`PROJECT|SOLUTION`**

  Projekt nebo řešení publikovat.
  
  * `PROJECT`je cesta a název souboru projektu [jazyka C#](csproj.md), F# nebo Visual Basic nebo cesta k adresáři, který obsahuje soubor projektu Jazyka C#, F# nebo Visual Basic. Pokud adresář není zadán, je výchozí pro aktuální adresář.

  * `SOLUTION`je cesta a název souboru řešení (*přípona .sln)* nebo cesta k adresáři, který obsahuje soubor řešení. Pokud adresář není zadán, je výchozí pro aktuální adresář. K dispozici od .NET Core 3.0 SDK.

## <a name="options"></a>Možnosti

- **`-c|--configuration <CONFIGURATION>`**

  Definuje konfiguraci sestavení. Výchozí hodnota pro `Debug`většinu projektů je , ale můžete přepsat nastavení konfigurace sestavení v projektu.

- **`-f|--framework <FRAMEWORK>`**

  Publikuje aplikaci pro zadaný [cílový rámec](../../standard/frameworks.md). Je nutné zadat cílovou architekturu v souboru projektu.

- **`--force`**

  Vynutí vyřešení všech závislostí, i když bylo poslední obnovení úspěšné. Zadání tohoto příznaku je stejné jako odstranění souboru *project.assets.json.*

- **`-h|--help`**

  Vytiskne krátkou nápovědu pro příkaz.

- **`--interactive`**

  Umožňuje příkazu zastavit a čekat na vstup uživatele nebo akci. Například k dokončení ověřování. K dispozici od .NET Core 3.0 SDK.

- **`--manifest <PATH_TO_MANIFEST_FILE>`**

  Určuje jeden nebo více [cílových manifestů,](../deploying/runtime-store.md) které se mají použít k oříznutí sady balíčků publikovaných s aplikací. Soubor manifestu je součástí výstupu [ `dotnet store` příkazu](dotnet-store.md). Chcete-li zadat více `--manifest` manifestů, přidejte možnost pro každý manifest.

- **`--no-build`**

  Nesestavuje projekt před publikováním. Také implicitně nastaví příznak. `--no-restore`

- **`--no-dependencies`**

  Ignoruje odkazy projektu na projekt a obnoví pouze kořenový projekt.

- **`--nologo`**

  Nezobrazuje spouštěcí banner ani zprávu o autorských právech. K dispozici od .NET Core 3.0 SDK.

- **`--no-restore`**

  Nespustí implicitní obnovení při spuštění příkazu.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  Určuje cestu pro výstupní adresář. Pokud není zadán, výchozí hodnota *./bin/[configuration]/[framework]/publish/* pro spustitelný soubor ový soubor a binární soubory mezi platformami. Výchozí hodnota je *./bin/[configuration]/[framework]/[runtime]/publish/* pro samostatný spustitelný soubor.

  Pokud je cesta relativní, je vygenerovaný výstupní adresář relativní k umístění souboru projektu, nikoli k aktuálnímu pracovnímu adresáři.

- **`--self-contained [true|false]`**

  Publikuje zaběhu .NET Core s vaší aplikací, takže runtime nemusí být nainstalován v cílovém počítači. Ve `true` výchozím nastavení je zadán identifikátor za běhu. Další informace naleznete v tématu [publikování a](../deploying/index.md) publikování [aplikací .NET Core pomocí rozhraní .NET Core .](../deploying/deploy-with-cli.md)

- **`--no-self-contained`**

  Odpovídá `--self-contained false`. K dispozici od .NET Core 3.0 SDK.

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Publikuje aplikaci pro daný běhový čas. Seznam identifikátorů modulu Runtime (RID) naleznete v [katalogu RID](../rid-catalog.md). Další informace naleznete v tématu [publikování a](../deploying/index.md) publikování [aplikací .NET Core pomocí rozhraní .NET Core .](../deploying/deploy-with-cli.md)

- **`-v|--verbosity <LEVEL>`**

  Nastaví úroveň podrobností příkazu. Povolené hodnoty `q[uiet]` `m[inimal]`jsou `n[ormal]` `d[etailed]`, `diag[nostic]`, , a . Výchozí hodnota `minimal`je .

- **`--version-suffix <VERSION_SUFFIX>`**

  Definuje příponu verze, která nahradí hvězdičku (`*`) v poli verze souboru projektu.

## <a name="examples"></a>Příklady

- Vytvořte [binární soubor pro běhový čas závislý na více platformách](../deploying/index.md#produce-a-cross-platform-binary) pro projekt v aktuálním adresáři:

  ```dotnetcli
  dotnet publish
  ```

  Počínaje .NET Core 3.0 SDK, tento příklad také vytvoří [spustitelný soubor závislý na modulu runtime](../deploying/index.md#publish-runtime-dependent) pro aktuální platformu.

- Vytvořte [samostatný spustitelný soubor](../deploying/index.md#publish-self-contained) pro projekt v aktuálním adresáři pro konkrétní modul runtime:

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64
  ```

  Rid musí být v souboru projektu.

- Vytvořte [spustitelný soubor závislý na modulu runtime](../deploying/index.md#publish-runtime-dependent) pro projekt v aktuálním adresáři pro konkrétní platformu:

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64 --self-contained false
  ```

  Rid musí být v souboru projektu. Tento příklad platí pro .NET Core 3.0 SDK a novější verze.

- Publikujte projekt v aktuálním adresáři pro konkrétní rozhraní runtime a cílový rámec:

  ```dotnetcli
  dotnet publish --framework netcoreapp3.1 --runtime osx.10.11-x64
  ```

- Publikování zadaného souboru projektu:

  ```dotnetcli
  dotnet publish ~/projects/app1/app1.csproj
  ```

- Publikujte aktuální aplikaci, ale neobnovte odkazy projektu na projekt (P2P), pouze kořenový projekt během operace obnovení:

  ```dotnetcli
  dotnet publish --no-dependencies
  ```

## <a name="see-also"></a>Viz také

- [Přehled publikování aplikace .NET Core](../deploying/index.md)
- [Publikování aplikací .NET Core pomocí rozhraní CLI jádra ROZHRANÍ .NET](../deploying/deploy-with-cli.md)
- [Cílové architektury](../../standard/frameworks.md)
- [Katalog IDentifier (RID) modulu runtime](../rid-catalog.md)
- [Práce s macOS Catalina Notarization](../install/macos-notarization-issues.md)
- [Adresářová struktura publikované aplikace](/aspnet/core/hosting/directory-structure)
