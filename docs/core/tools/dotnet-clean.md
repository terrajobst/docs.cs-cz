---
title: dotnet clean, příkaz
description: Příkaz dotnet clean vyčistí aktuální adresář.
ms.date: 02/14/2020
ms.openlocfilehash: 186f1ea07718a8e178f88c3d079cf6e2f1f8660b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/14/2020
ms.locfileid: "77503751"
---
# <a name="dotnet-clean"></a>dotnet clean

**Tento článek se týká:** ✔️ .NET Core 2.x SDK a novější verze

## <a name="name"></a>Name (Název)

`dotnet clean`- Čistí výstup projektu.

## <a name="synopsis"></a>Synopse

```dotnetcli
dotnet clean [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--interactive]
    [--nologo] [-o|--output] [-r|--runtime] [-v|--verbosity]
dotnet clean [-h|--help]
```

## <a name="description"></a>Popis

Příkaz `dotnet clean` vyčistí výstup předchozísestavení. Je implementován jako [cíl MSBuild](/visualstudio/msbuild/msbuild-targets), takže projekt je vyhodnocen při spuštění příkazu. Pouze výstupy vytvořené během sestavení jsou vyčištěny. Obě střední (*obj*) a konečný výstup (*bin*) složky jsou vyčištěny.

## <a name="arguments"></a>Argumenty

`PROJECT | SOLUTION`

MSBuild projektu nebo řešení k čištění. Pokud není zadán soubor projektu nebo řešení, MSBuild vyhledá aktuální pracovní adresář pro soubor, který má příponu souboru, která končí *na proj* nebo *sln*, a použije tento soubor.

## <a name="options"></a>Možnosti

* **`-c|--configuration <CONFIGURATION>`**

  Definuje konfiguraci sestavení. Výchozí hodnota pro `Debug`většinu projektů je , ale můžete přepsat nastavení konfigurace sestavení v projektu. Tato možnost je vyžadována pouze při čištění, pokud jste ji zadali během doby sestavení.

* **`-f|--framework <FRAMEWORK>`**

  [Rámec,](../../standard/frameworks.md) který byl zadán v době sestavení. Rámec musí být definován v [souboru projektu](csproj.md). Pokud jste zadali rozhraní v době sestavení, je nutné zadat rámec při čištění.

* **`-h|--help`**

  Vytiskne krátkou nápovědu pro příkaz.

* **`--interactive`**

  Umožňuje příkazu zastavit a čekat na vstup uživatele nebo akci. Například k dokončení ověřování. K dispozici od .NET Core 3.0 SDK.

* **`--nologo`**

  Nezobrazuje spouštěcí banner ani zprávu o autorských právech. K dispozici od .NET Core 3.0 SDK.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Adresář, který obsahuje artefakty sestavení k čištění. Zadejte `-f|--framework <FRAMEWORK>` přepínač s přepínačem výstupního adresáře, pokud jste zadali rámec při projektu byl vytvořen.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Vyčistí výstupní složku zadaného běhu. Používá se při [vytvoření samostatného nasazení.](../deploying/index.md#publish-self-contained)

* **`-v|--verbosity <LEVEL>`**

  Nastaví úroveň podrobností MSBuild. Povolené hodnoty `q[uiet]` `m[inimal]`jsou `n[ormal]` `d[etailed]`, `diag[nostic]`, , a . Výchozí formát je `normal`.

## <a name="examples"></a>Příklady

* Vyčistit výchozí sestavení projektu:

  ```dotnetcli
  dotnet clean
  ```

* Vyčistěte projekt vytvořený pomocí konfigurace vydání:

  ```dotnetcli
  dotnet clean --configuration Release
  ```
