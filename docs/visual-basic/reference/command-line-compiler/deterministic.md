---
title: -deterministic
ms.date: 04/11/2018
helpviewer_keywords:
- deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
- -deterministic compiler option [Visual Basic]
ms.openlocfilehash: 9b611a72656bdd570eccec8a0585bf5ce6fa55f6
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716793"
---
# <a name="-deterministic"></a>-deterministic

Způsobí, že kompilátor sestaví sestavení, jejichž výstup Byte-byte je stejný v rámci kompilací pro stejné vstupy.

## <a name="syntax"></a>Syntaxe

```console
-deterministic
```

## <a name="remarks"></a>Poznámky

Ve výchozím nastavení je výstup kompilátoru z dané sady vstupů jedinečný, protože kompilátor přidá časové razítko a identifikátor GUID, který je vygenerován z náhodných čísel. Použijete možnost `-deterministic` k vytvoření *deterministického sestavení*, jehož binární obsah je identický v rámci kompilací, pokud vstup zůstává stejný.

Kompilátor považuje za účel determinismem následující vstupy:

- Sekvence parametrů příkazového řádku.
- Obsah souboru odpovědí kompilátoru. rsp
- Byla použita přesná verze kompilátoru a jejich odkazovaná sestavení.
- Cesta k aktuálnímu adresáři.
- Binární obsah všech souborů explicitně předaných kompilátoru buď přímo, nebo nepřímo, včetně:
  - Zdrojové soubory
  - Odkazovaná sestavení
  - Odkazované moduly
  - Prostředky
  - Soubor klíče se silným názvem
  - soubory @ Response
  - Analyzátory
  - Rulesets
  - Další soubory, které mohou používat analyzátory
- Aktuální jazyková verze (pro jazyk, ve kterém se vytvářejí zprávy o diagnostice a výjimkách).
- Výchozí kódování (nebo aktuální znaková stránka), pokud kódování není zadáno.
- Existence, neexistence a obsah souborů v cestách pro hledání kompilátoru (určené například pomocí `-lib` nebo `-recurse`).
- Platforma CLR, na které je kompilátor spuštěn.
- Hodnota `%LIBPATH%`, která může ovlivnit načítání závislostí analyzátoru.

Pokud jsou zdroje veřejně dostupné, lze použít deterministické kompilace k určení, zda binární soubor je zkompilován z důvěryhodného zdroje. Může být také užitečné v souvislém systému sestavení pro určení, zda jsou kroky sestavení závislé na změnách binárních souborů nutné provést.

## <a name="see-also"></a>Viz také:

- [Visual Basic Kompilátor příkazového řádku](../../../visual-basic/reference/command-line-compiler/index.md)
- [Příkazové řádky ukázkové kompilace](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
