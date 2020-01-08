---
title: Odinstalační nástroj
description: Přehled nástroje pro odinstalaci rozhraní .NET Core, což je průvodce nástrojem, který umožňuje řízené vyčištění sad .NET Core SDK a modulů runtime.
author: sfoslund
ms.date: 12/17/2019
ms.openlocfilehash: 5a1a419d5ad09643a7063cc03ec727c547268cc6
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75443545"
---
# <a name="net-core-uninstall-tool"></a>Nástroj pro odinstalaci .NET Core

[Nástroj pro odinstalaci .NET Core](https://github.com/dotnet/cli-lab/releases) (`dotnet-core-uninstall`) umožňuje odebrat sady .NET Core SDK a moduly runtime ze systému. K dispozici je kolekce možností, které určují verze, které chcete odinstalovat.

Nástroj podporuje Windows a macOS. Linux není aktuálně podporován.

V systému Windows může nástroj odinstalovat pouze sady SDK a moduly runtime, které byly nainstalovány pomocí jednoho z následujících instalačních programů:

- Instalační program .NET Core SDK a modulu runtime.
- Instalační program sady Visual Studio ve verzích starších než Visual Studio 2019 verze 16,3.

V macOS může nástroj odinstalovat jenom sady SDK a moduly runtime umístěné ve složce */usr/local/share/dotnet* .

Z důvodu těchto omezení nemusí nástroj na počítači odinstalovat všechny sady .NET Core SDK a moduly runtime. Pomocí příkazu `dotnet --info` můžete vyhledat všechny nainstalované sady SDK a moduly runtime .NET Core, včetně sad SDK a modulů runtime, které tento nástroj nemůže odebrat. Příkaz `dotnet-core-uninstall list` zobrazuje, které sady SDK je možné odinstalovat pomocí nástroje.

## <a name="install-the-tool"></a>Instalace nástroje

Nástroj pro odinstalaci .NET Core si můžete stáhnout z úložiště GitHubu [dotnet/CLI-Lab](https://github.com/dotnet/cli-lab/releases) .

> [!NOTE]
> Tento nástroj vyžaduje zvýšení oprávnění k odinstalování sad SDK a modulů runtime .NET Core. Proto by měl být nainstalován v adresáři chráněném zápisem, například *C:\Program Files* ve Windows nebo */usr/local/bin* na MacOS. Viz také [zvýšený přístup pro příkazy dotnet](../tools/elevated-access.md). Podrobné pokyny k instalaci jsou k dispozici na [stránce verze GitHubu](https://github.com/dotnet/cli-lab/releases).

## <a name="run-the-tool"></a>Spusťte nástroj

Následující kroky ukazují doporučený postup pro spuštění nástroje pro odinstalaci:

- [Krok 1 – zobrazení nainstalovaných sad SDK a modulů runtime .NET Core](#step-1---display-installed-net-core-sdks-and-runtimes)
- [Krok 2 – provedení suchého běhu](#step-2---do-a-dry-run)
- [Krok 3 – odinstalace sad SDK a modulů runtime .NET Core](#step-3---uninstall-net-core-sdks-and-runtimes)
- [Krok 4 – odstranění záložní složky NuGet (volitelné)](#step-4---delete-the-nuget-fallback-folder-optional)

### <a name="step-1---display-installed-net-core-sdks-and-runtimes"></a>Krok 1 – zobrazení nainstalovaných sad SDK a modulů runtime .NET Core

Příkaz `dotnet-core-uninstall list` vypíše nainstalované sady .NET Core SDK a moduly runtime, které lze pomocí tohoto nástroje odebrat. Aplikace Visual Studio může vyžadovat některé sady SDK a moduly runtime, které se zobrazí s poznámkou, proč není doporučeno je odinstalovat.

**dotnet – základní – seznam odinstalování**

#### <a name="synopsis"></a>Stručný obsah

```console
dotnet-core-uninstall list [options]
```

#### <a name="options"></a>Možnosti

## <a name="windowstabwindows"></a>[Windows](#tab/windows)

* **`--aspnet-runtime`**

  Zobrazí seznam všech ASP.NET Core Runtime, které lze pomocí tohoto nástroje odinstalovat.

* **`--hosting-bundle`**

  Zobrazí seznam všech modulů runtime .NET Core a hostitelských sad, které se dají odinstalovat pomocí tohoto nástroje.

* **`--runtime`**

  Zobrazí seznam všech modulů runtime .NET Core, které se dají odinstalovat pomocí tohoto nástroje.

* **`--sdk`**

  Zobrazí seznam všech sad SDK .NET Core, které se dají odinstalovat pomocí tohoto nástroje.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.

* **`--x64`**

  Obsahuje seznam všech sad SDK a modulů runtime x64 .NET Core, které je možné odinstalovat pomocí tohoto nástroje.

* **`--x86`**

  Obsahuje seznam všech sad SDK a modulů runtime x86 .NET Core, které je možné odinstalovat pomocí tohoto nástroje.

## <a name="macostabmacos"></a>[macOS](#tab/macos)

* **`--runtime`**

  Zobrazí seznam všech modulů runtime .NET Core, které se dají odinstalovat pomocí tohoto nástroje.

* **`--sdk`**

  Zobrazí seznam všech sad SDK .NET Core, které se dají odinstalovat pomocí tohoto nástroje.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.
  
---

#### <a name="examples"></a>Příklady

* Vypíše všechny sady SDK a moduly runtime .NET Core, které je možné odebrat pomocí tohoto nástroje:

  ```console
  dotnet-core-uninstall list
  ```

* Vypíše všechny sady SDK a moduly runtime x64 .NET Core:

  ```console
  dotnet-core-uninstall list --x64
  ```

* Vypíše všechny sady SDK x86 .NET Core:

  ```console
  dotnet-core-uninstall list --sdk --x86
  ```

### <a name="step-2---do-a-dry-run"></a>Krok 2 – provedení suchého běhu

Příkazy `dotnet-core-uninstall dry-run` a `dotnet-core-uninstall whatif` zobrazují sady SDK a moduly runtime .NET Core, které se odeberou na základě možností, které jsou k dispozici bez provedení odinstalace. Tyto příkazy jsou synonyma.

**dotnet-Core – odinstalace suchého běhu a dotnet-Core-Uninstall whatIf**

#### <a name="synopsis"></a>Stručný obsah

```console
dotnet-core-uninstall dry-run [options] [<VERSION>...]

dotnet-core-uninstall whatif [options] [<VERSION>...]
```

#### <a name="arguments"></a>Arguments

* **`VERSION`**

  Zadaná verze, která se má odinstalovat Po druhém můžete zobrazit několik verzí, které jsou oddělené mezerami. Podporovány jsou také soubory odpovědí.

  > [!TIP]
  > Soubory odpovědí jsou alternativou k umístění všech verzí do příkazového řádku.
  > Jedná se o textové soubory, obvykle s příponou \*. rsp a každá verze je uvedena na samostatném řádku.
  > Chcete-li zadat soubor odpovědí pro argument `VERSION`, použijte znak \@ ihned následovaný názvem souboru odpovědi.

#### <a name="options"></a>Možnosti

## <a name="windowstabwindows"></a>[Windows](#tab/windows)

* **`--all`**

  Odebere všechny sady SDK a moduly runtime .NET Core.

* **`--all-below <VERSION>`**

  Odebere jenom sady SDK a modul runtime .NET Core s verzí nižší, než je zadaná verze. Zadaná verze zůstane nainstalovaná.

* **`--all-but <VERSIONS>`**

  Odebere všechny sady SDK a moduly runtime .NET Core s výjimkou uvedených verzí.

* **`--all-but-latest`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou jedné nejvyšší verze.

* **`--all-lower-patches`**

  Odebere sady SDK a moduly runtime .NET Core nahrazené vyššími opravami. Tato možnost chrání Global. JSON.

* **`--all-previews`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy.

* **`--all-previews-but-latest`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy kromě nejvyšší verze Preview.

* **`--aspnet-runtime`**

  Odebere pouze moduly runtime ASP.NET Core.

* **`--hosting-bundle`**

  Odebere jenom modul runtime .NET Core a hostitelské sady.

* **`--major-minor <MAJOR_MINOR>`**

  Odebere sady SDK a moduly runtime .NET Core, které odpovídají zadané verzi `major.minor`.

* **`--runtime`**

  Odebere jenom modul runtime .NET Core.

* **`--sdk`**

  Odebere jenom sady .NET Core SDK.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.

* **`--x64`**

  Se musí použít s `--sdk`, `--runtime`a `--aspnet-runtime` k odebrání sad nebo runtime sady x64.

* **`--x86`**

  Se musí použít s `--sdk`, `--runtime`a `--aspnet-runtime` k odebrání sad SDK nebo modulů runtime x86.

* **`--force`** Vynutí odebrání verzí, které mohou být použity v aplikaci Visual Studio.

Poznámky:

1. Je vyžadován právě jeden z `--sdk`, `--runtime`, `--aspnet-runtime`a `--hosting-bundle`.
2. `--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`a `[<VERSION>...]` jsou exkluzivní.
3. Pokud nejsou zadány `--x64` nebo `--x86`, budou odebrány obě platformy x64 i x86.

## <a name="macostabmacos"></a>[macOS](#tab/macos)

* **`--all`**

  Odebere všechny sady SDK a moduly runtime .NET Core.

* **`--all-below <VERSION>`**

  Odebere sady SDK a moduly runtime .NET Core pod zadanou verzí. Zadaná verze zůstane.

* **`--all-but <VERSIONS>`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou uvedených verzí.

* **`--all-but-latest`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou jedné nejvyšší verze.

* **`--all-lower-patches`**

  Odebere sady SDK a moduly runtime .NET Core nahrazené vyššími opravami. Tato možnost chrání Global. JSON.

* **`--all-previews`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy.

* **`--all-previews-but-latest`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy kromě nejvyšší verze Preview.

* **`--major-minor <MAJOR_MINOR>`**

  Odebere sady SDK a moduly runtime .NET Core, které odpovídají zadané verzi `major.minor`.

* **`--runtime`**

  Odebere jenom modul runtime .NET Core.

* **`--sdk`**

  Odebere jenom sady .NET Core SDK.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.
  
* **`--force`** Vynutí odebrání verzí, které mohou být použity v aplikaci Visual Studio nebo sadách SDK.

Poznámky:

1. Je vyžadován právě jeden z `--sdk` a `--runtime`.
2. `--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`a `[<VERSION>...]` jsou exkluzivní.

---

#### <a name="examples"></a>Příklady

> [!NOTE]
> Ve výchozím nastavení nejsou sady .NET Core SDK a moduly runtime, které mohou být vyžadovány aplikací Visual Studio nebo jinými sadami SDK, obsaženy v `dotnet-core-uninstall dry-run`m výstupu. V následujících příkladech nemusí být některé ze zadaných sad SDK a modulu runtime zahrnuty ve výstupu v závislosti na stavu počítače. Pokud chcete zahrnout všechny sady SDK a moduly runtime, uveďte je explicitně jako argumenty nebo použijte možnost `--force`.

* Suché spuštění odebrání všech modulů runtime .NET Core, které byly nahrazeny vyššími opravami:

  ```console
  dotnet-core-uninstall dry-run --all-lower-patches --runtime
  ```

* Suché spuštění odebrání všech sad .NET Core SDK pod verzí `2.2.301`:

  ```console
  dotnet-core-uninstall whatif --all-below 2.2.301 --sdk
  ```

### <a name="step-3---uninstall-net-core-sdks-and-runtimes"></a>Krok 3 – odinstalace sad SDK a modulů runtime .NET Core

`dotnet-core-uninstall remove` odinstaluje sady SDK a moduly runtime .NET Core, které jsou určené kolekcí možností. Tento nástroj se nedá použít k odinstalování sad SDK a běhových prostředí s verzí 5,0 nebo vyšší.

Vzhledem k tomu, že tento nástroj má destruktivní chování, **důrazně** doporučujeme, abyste před spuštěním příkazu Remove nepoužívali suché spuštění. V suchém běhu se zobrazí informace o tom, jaké sady .NET Core SDK a moduly runtime budou odebrány při použití příkazu `remove`. Informace o tom, jak [mám odebrat verzi?](../versions/remove-runtime-sdk-versions.md#should-i-remove-a-version) informace o tom, které sady SDK a moduly runtime je bezpečné odebrat.

> [!CAUTION]
> Pamatujte na následující upozornění:
>
>- Tento nástroj může odinstalovat verze .NET Core SDK, které jsou vyžadovány soubory `global.json` na vašem počítači. Sady .NET Core SDK můžete přeinstalovat ze stránky [stáhnout jádro .NET Core](https://dotnet.microsoft.com/download/dotnet-core) .
>- Tento nástroj může odinstalovat verze modulu runtime .NET Core, které jsou vyžadovány závislými aplikacemi architektury na vašem počítači. Moduly runtime .NET Core můžete přeinstalovat na stránce [stáhnout jádro .NET Core](https://dotnet.microsoft.com/download/dotnet-core) .
>- Tento nástroj může odinstalovat verze .NET Core SDK a modulu runtime, na kterém se aplikace Visual Studio spoléhá. Pokud přerušíte instalaci sady Visual Studio, spusťte v instalačním programu sady Visual Studio "opravit" a vraťte se do funkčního stavu.

Ve výchozím nastavení všechny příkazy udržují sady SDK a moduly runtime .NET Core, které mohou být vyžadovány aplikací Visual Studio nebo jinými sadami SDK. Tyto sady SDK a moduly runtime můžete odinstalovat tak, že je explicitně uvedete jako argumenty nebo pomocí možnosti `--force`.

Tento nástroj vyžaduje zvýšení oprávnění k odinstalování sad SDK a modulů runtime .NET Core. Spusťte nástroj z příkazového řádku správce ve Windows a pomocí `sudo` v macOS. Příkazy `dry-run` a `whatif` nevyžadují zvýšení oprávnění.

**dotnet – jádro – odebrání odinstalace**

#### <a name="synopsis"></a>Stručný obsah

```console
dotnet-core-uninstall remove [options] [<VERSION>...]
```

#### <a name="arguments"></a>Arguments

* **`VERSION`**

  Zadaná verze, která se má odinstalovat Po druhém můžete zobrazit několik verzí, které jsou oddělené mezerami. Podporovány jsou také soubory odpovědí.

  > [!TIP]
  > Soubory odpovědí jsou alternativou k umístění všech verzí do příkazového řádku.
  > Jedná se o textové soubory, obvykle s příponou \*. rsp a každá verze je uvedena na samostatném řádku.
  > Chcete-li zadat soubor odpovědí pro argument `VERSION`, použijte znak \@ ihned následovaný názvem souboru odpovědi.

#### <a name="options"></a>Možnosti

## <a name="windowstabwindows"></a>[Windows](#tab/windows)

* **`--all`**

  Odebere všechny sady SDK a moduly runtime .NET Core.

* **`--all-below <VERSION>`**

  Odebere jenom sady SDK a modul runtime .NET Core s verzí nižší, než je zadaná verze. Zadaná verze zůstane nainstalovaná.

* **`--all-but <VERSIONS>`**

  Odebere všechny sady SDK a moduly runtime .NET Core s výjimkou uvedených verzí.

* **`--all-but-latest`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou jedné nejvyšší verze.

* **`--all-lower-patches`**

  Odebere sady SDK a moduly runtime .NET Core nahrazené vyššími opravami. Tato možnost chrání Global. JSON.

* **`--all-previews`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy.

* **`--all-previews-but-latest`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy kromě nejvyšší verze Preview.

* **`--aspnet-runtime`**

  Odebere pouze moduly runtime ASP.NET Core.

* **`--hosting-bundle`**

  Odebere jenom modul runtime .NET Core a hostitelské sady.

* **`--major-minor <MAJOR_MINOR>`**

  Odebere sady SDK a moduly runtime .NET Core, které odpovídají zadané verzi `major.minor`.

* **`--runtime`**

  Odebere jenom modul runtime .NET Core.

* **`--sdk`**

  Odebere jenom sady .NET Core SDK.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.

* **`--x64`**

  Se musí použít s `--sdk`, `--runtime`a `--aspnet-runtime` k odebrání sad nebo runtime sady x64.

* **`--x86`**

  Se musí použít s `--sdk`, `--runtime`a `--aspnet-runtime` k odebrání sad SDK nebo modulů runtime x86.

* **`-y, --yes`** Provede příkaz bez nutnosti potvrzení Ano nebo ne.

* **`--force`** Vynutí odebrání verzí, které mohou být použity v aplikaci Visual Studio.

Poznámky:

1. Je vyžadován právě jeden z `--sdk`, `--runtime`, `--aspnet-runtime`a `--hosting-bundle`.
2. `--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`a `[<VERSION>...]` jsou exkluzivní.
3. Pokud nejsou zadány `--x64` nebo `--x86`, budou odebrány obě platformy x64 i x86.

## <a name="macostabmacos"></a>[macOS](#tab/macos)

* **`--all`**

  Odebere všechny sady SDK a moduly runtime .NET Core.

* **`--all-below <VERSION>`**

  Odebere sady SDK a moduly runtime .NET Core pod zadanou verzí. Zadaná verze zůstane.

* **`--all-but <VERSIONS>`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou uvedených verzí.

* **`--all-but-latest`**

  Odebere sady SDK a moduly runtime .NET Core s výjimkou jedné nejvyšší verze.

* **`--all-lower-patches`**

  Odebere sady SDK a moduly runtime .NET Core nahrazené vyššími opravami. Tato možnost chrání Global. JSON.

* **`--all-previews`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy.

* **`--all-previews-but-latest`**

  Odebere sady .NET Core SDK a moduly runtime označené jako náhledy kromě nejvyšší verze Preview.

* **`--major-minor <MAJOR_MINOR>`**

  Odebere sady SDK a moduly runtime .NET Core, které odpovídají zadané verzi `major.minor`.

* **`--runtime`**

  Odebere jenom modul runtime .NET Core.

* **`--sdk`**

  Odebere jenom sady .NET Core SDK.

* **`-v, --verbosity <LEVEL>`**

  Nastaví úroveň podrobností. Povolené hodnoty jsou `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`a `diag[nostic]`. Výchozí hodnota je `normal`.

* **`-y, --yes`** Provede příkaz bez potvrzení hodnoty Y/n.
  
* **`--force`** Vynutí odebrání verzí, které mohou být použity v aplikaci Visual Studio nebo sadách SDK.

Poznámky:

1. Je vyžadován právě jeden z `--sdk` a `--runtime`.
2. `--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`a `[<VERSION>...]` jsou exkluzivní.

---

#### <a name="examples"></a>Příklady

> [!NOTE]
> Ve výchozím nastavení jsou zachovány sady .NET Core SDK a moduly runtime, které mohou být vyžadovány aplikací Visual Studio nebo jinými sadami SDK. V následujících příkladech mohou některé ze zadaných sad SDK a modulu runtime zůstat v závislosti na stavu počítače. Pokud chcete odebrat všechny sady SDK a moduly runtime, uveďte je explicitně jako argumenty nebo použijte možnost `--force`.

* Odeberte všechny běhové moduly runtime x86 .NET s výjimkou `3.0.0-preview6-27804-01` verze, aniž by bylo nutné potvrzovat a/n:

  ```console
  dotnet-core-uninstall remove --all-but 3.0.0-preview6-27804-01 --runtime --yes
  ```

* Odeberte všechny sady SDK .NET Core 1,1, aniž by bylo nutné potvrzovat a/n:

  ```console
  dotnet-core-uninstall remove --sdk --major-minor 1.1 -y
  ```

* Odebrání sady .NET Core 1.1.11 SDK bez výstupu konzoly:

  ```console
  dotnet-core-uninstall remove 1.1.11 --sdk --yes -verbosity q
  ```

* Odeberte všechny sady SDK .NET Core, které je možné bezpečně odebrat tímto nástrojem:

  ```console
  dotnet-core-uninstall remove --all --sdk
  ```

* Odebrat všechny sady .NET Core SDK, které mohou být tímto nástrojem odebrány, včetně sad SDK, které mohou být vyžadovány aplikací Visual Studio (nedoporučuje se):

  ```console
  dotnet-core-uninstall remove --all --sdk --force
  ```

* Odeberte všechny sady .NET Core SDK, které jsou zadané v souboru odpovědí `versions.rsp`

  ```console
  dotnet-core-uninstall remove --sdk @versions.rsp
  ```

  Obsah *verze. rsp* je následující:
  
  ```text
  2.2.300
  2.1.700
  ```

### <a name="step-4---delete-the-nuget-fallback-folder-optional"></a>Krok 4 – odstranění záložní složky NuGet (volitelné)

V některých případech už `NuGetFallbackFolder` nepotřebujete a budete ho chtít odstranit. Další informace o odstranění této složky najdete v tématu [Odebrání NuGetFallbackFolder](../versions/remove-runtime-sdk-versions.md#remove-the-nuget-fallback-folder).

## <a name="uninstall-the-tool"></a>Odinstalace nástroje

## <a name="windowstabwindows"></a>[Windows](#tab/windows)

1. Otevřete panel **Přidat nebo odebrat programy**.
2. Vyhledejte `Microsoft .NET Core SDK Uninstall Tool`.
3. Vyberte **Odinstalovat**.

## <a name="macostabmacos"></a>[macOS](#tab/macos)

Odstraňte stažený soubor *dotnet-Core-Uninstall. tar. gz* z adresáře, kam byl nainstalován. Pokud rozdělíte obsah tohoto souboru do jiného adresáře, nezapomeňte tento obsah také odstranit.

---