---
title: -target
ms.date: 03/13/2018
helpviewer_keywords:
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
ms.openlocfilehash: d186670489ada51fced67ff9adeb73b14909b664
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716691"
---
# <a name="-target-visual-basic"></a>-Target (Visual Basic)

Určuje formát výstupu kompilátoru.

## <a name="syntax"></a>Syntaxe

```console
-target:{exe | library | module | winexe | appcontainerexe | winmdobj}
```

## <a name="remarks"></a>Poznámky

Následující tabulka shrnuje efekt možnosti `-target`.

|**Možnost**|**Chování**|
|----------------|------------------|
|`-target:exe`|Způsobí, že kompilátor vytvoří spustitelnou konzolovou aplikaci.<br /><br /> Toto je výchozí možnost, pokud není zadána možnost `-target`. Spustitelný soubor se vytvoří s příponou. exe.<br /><br /> Pokud není uvedeno jinak s možností `-out`, název výstupního souboru převezme název vstupního souboru, který obsahuje `Sub Main` postup.<br /><br /> V souborech zdrojového kódu, které jsou zkompilovány do souboru. exe, je vyžadována pouze jedna `Sub Main` procedura. Pomocí možnosti kompilátoru `-main` určete, která třída obsahuje `Sub Main` postup.|
|`-target:library`|Způsobí, že kompilátor vytvoří dynamickou knihovnu (DLL).<br /><br /> Soubor dynamické knihovny je vytvořen s příponou. dll.<br /><br /> Pokud není uvedeno jinak s možností `-out`, název výstupního souboru převezme název prvního vstupního souboru.<br /><br /> Při sestavování knihovny DLL není nutná `Sub Main` procedura.|
|`-target:module`|Způsobí, že kompilátor vygeneruje modul, který lze přidat do sestavení.<br /><br /> Výstupní soubor je vytvořen s příponou. netmodule.<br /><br /> Modul CLR (Common Language Runtime) .NET nemůže načíst soubor, který nemá sestavení. Takový soubor však lze začlenit do manifestu sestavení sestavení pomocí `-reference`.<br /><br /> Když kód v jednom modulu odkazuje na interní typy v jiném modulu, oba moduly musí být začleněny do manifestu sestavení pomocí `-reference`.<br /><br /> Možnost [-addmodule –](../../../visual-basic/reference/command-line-compiler/addmodule.md) Importuje metadata z modulu.|
|`-target:winexe`|Způsobí, že kompilátor vytvoří spustitelnou aplikaci založenou na Windows.<br /><br /> Spustitelný soubor se vytvoří s příponou. exe. Aplikace pro systém Windows je taková, která poskytuje uživatelské rozhraní z knihovny tříd .NET Framework nebo pomocí rozhraní API systému Windows.<br /><br /> Pokud není uvedeno jinak s možností `-out`, název výstupního souboru převezme název vstupního souboru, který obsahuje `Sub Main` postup.<br /><br /> V souborech zdrojového kódu, které jsou zkompilovány do souboru. exe, je vyžadována pouze jedna `Sub Main` procedura. V případech, kdy má váš kód více než jednu třídu, která má `Sub Main` proceduru, použijte možnost kompilátoru `-main` k určení, která třída obsahuje `Sub Main` proceduru.|
|`-target:appcontainerexe`|Způsobí, že kompilátor vytvoří spustitelnou aplikaci pro Windows, která musí být spuštěna v kontejneru aplikace. Toto nastavení je určeno pro použití pro aplikace Windows 8. x Store.<br /><br /> Nastavení **appcontainerexe** nastaví bit v poli vlastností [přenositelného spustitelného](/windows/desktop/Debug/pe-format) souboru. Tento bit znamená, že aplikace musí být spuštěná v kontejneru aplikace. Pokud je tento bit nastaven, dojde k chybě, pokud se metoda `CreateProcess` pokusí spustit aplikaci mimo kontejner aplikace. Kromě tohoto bitového nastavení **-target: appcontainerexe** je ekvivalentní k **target: winexe**.<br /><br /> Spustitelný soubor se vytvoří s příponou. exe.<br /><br /> Pokud neurčíte jinak pomocí možnosti `-out`, název výstupního souboru převezme název vstupního souboru, který obsahuje `Sub Main` postup.<br /><br /> V souborech zdrojového kódu, které jsou zkompilovány do souboru. exe, je vyžadována pouze jedna `Sub Main` procedura. Pokud váš kód obsahuje více než jednu třídu, která má `Sub Main` proceduru, použijte možnost kompilátoru `-main` k určení, která třída obsahuje `Sub Main` proceduru.|
|`-target:winmdobj`|Způsobí, že kompilátor vytvoří zprostředkující soubor, který lze převést na soubor prostředí Windows Runtime binární (. winmd). Soubor. winmd lze kromě spravovaných jazykových programů spotřebovat pomocí JavaScriptu a C++ programů.<br /><br /> Zprostředkující soubor se vytvoří s příponou. winmdobj.<br /><br /> Pokud neurčíte jinak pomocí možnosti `-out`, název výstupního souboru vezme název prvního vstupního souboru. Postup `Sub Main` není povinný.<br /><br /> Soubor. winmdobj je navržený tak, aby se použil jako vstup pro nástroj <xref:Microsoft.Build.Tasks.WinMDExp>ho exportu k vytvoření souboru Windows metadata (WinMD). Soubor WinMD má příponu. winmd a obsahuje jak kód z původní knihovny, tak definice WinMD, které JavaScript, C++a prostředí Windows Runtime použít.|

Pokud nezadáte `-target:module`, `-target` způsobí přidání manifestu .NET Framework sestavení do výstupního souboru.

Každá instance nástroje Vbc. exe vytváří nejvýše jeden výstupní soubor. Zadáte-li možnost kompilátoru, jako je například `-out` nebo `-target` více než jednou, bude poslední proces kompilátoru zaveden v platnost. Do manifestu jsou přidány informace o všech souborech v kompilaci. Všechny výstupní soubory kromě těch, které byly vytvořeny pomocí `-target:module` obsahují metadata sestavení v manifestu. K zobrazení metadat ve výstupním souboru použijte [Ildasm. exe (IL Disassembler)](../../../framework/tools/ildasm-exe-il-disassembler.md) .

Krátká forma `-target` je `-t`.

### <a name="to-set--target-in-the-visual-studio-ide"></a>Nastavení cíle v integrovaném vývojovém prostředí sady Visual Studio

1. Máte projekt vybraný v **Průzkumník řešení**. V nabídce **projekt** klikněte na příkaz **vlastnosti**.

2. Klikněte na kartu **aplikace** .

3. Upravte hodnotu v poli **Typ aplikace** .

## <a name="example"></a>Příklad

Následující kód zkompiluje `in.vb`a vytvoří `in.dll`:

```console
vbc -target:library in.vb
```

## <a name="see-also"></a>Viz také:

- [Visual Basic Kompilátor příkazového řádku](../../../visual-basic/reference/command-line-compiler/index.md)
- [-main](../../../visual-basic/reference/command-line-compiler/main.md)
- [-out (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)
- [-Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
- [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)
- [-moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)
- [Sestavení v .NET](../../../standard/assembly/index.md)
- [Příkazové řádky ukázkové kompilace](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
