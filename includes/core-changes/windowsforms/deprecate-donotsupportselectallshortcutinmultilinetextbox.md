---
ms.openlocfilehash: a9d0fe3516ade04bc38b804268a9d989f6891d80
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71181767"
---
### <a name="switchsystemwindowsformsdonotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported"></a><span data-ttu-id="857ac-101">Přepínač kompatibility. System. Windows. Forms. DoNotSupportSelectAllShortcutInMultilineTextBox není podporovaný.</span><span class="sxs-lookup"><span data-stu-id="857ac-101">Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported</span></span>

<span data-ttu-id="857ac-102">Přepínač `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` kompatibility, který byl představen v .NET Framework 4.6.1, není podporován v model Windows Forms .NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="857ac-102">The `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` compatibility switch, which was introduced in .NET Framework 4.6.1, is not supported in Windows Forms on .NET Core 3.0.</span></span>

#### <a name="change-description"></a><span data-ttu-id="857ac-103">Změnit popis</span><span class="sxs-lookup"><span data-stu-id="857ac-103">Change description</span></span>

<span data-ttu-id="857ac-104">Počínaje .NET Framework 4.6.1 vyberete <kbd>klávesovou</kbd> + <kbd>zkratku</kbd> CTRL v <xref:System.Windows.Forms.TextBox> ovládacím prvku vybraný veškerý text.</span><span class="sxs-lookup"><span data-stu-id="857ac-104">Starting with .NET Framework 4.6.1, selecting the <kbd>Ctrl</kbd> + <kbd>A</kbd> shortcut key in a <xref:System.Windows.Forms.TextBox> control selected all text.</span></span> <span data-ttu-id="857ac-105">V .NET Framework 4,6 a předchozích verzích se při výběru <kbd>klávesy CTRL</kbd> + <kbd>a klávesové zkratky</kbd> nepovedlo vybrat veškerý text, pokud by vlastnost <xref:System.Windows.Forms.TextBox.Multiline?displayProperty=nameWithType> [TextBox. ShortcutsEnabled](xref:System.Windows.Forms.TextBoxBase.ShortcutsEnabled) a Properties `true`byla obě nastavená na.</span><span class="sxs-lookup"><span data-stu-id="857ac-105">In .NET Framework 4.6 and previous versions, selecting the <kbd>Ctrl</kbd> + <kbd>A</kbd> shortcut key failed to select all text if the [Textbox.ShortcutsEnabled](xref:System.Windows.Forms.TextBoxBase.ShortcutsEnabled) and <xref:System.Windows.Forms.TextBox.Multiline?displayProperty=nameWithType> properties were both set to `true`.</span></span> <span data-ttu-id="857ac-106">Přepínač `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` kompatibility byl představen v .NET Framework 4.6.1 za účelem zachování původního chování.</span><span class="sxs-lookup"><span data-stu-id="857ac-106">The `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` compatibility switch was introduced in .NET Framework 4.6.1 to retain the original behavior.</span></span> <span data-ttu-id="857ac-107">Další informace najdete v <xref:System.Windows.Forms.TextBox.ProcessCmdKey%2A?displayProperty=nameWithType>tématu.</span><span class="sxs-lookup"><span data-stu-id="857ac-107">For more information see <xref:System.Windows.Forms.TextBox.ProcessCmdKey%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="857ac-108">V rozhraní .NET Core `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` není přepínač podporován.</span><span class="sxs-lookup"><span data-stu-id="857ac-108">In .NET Core, the `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` switch is not supported.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="857ac-109">Představená verze</span><span class="sxs-lookup"><span data-stu-id="857ac-109">Version introduced</span></span>

<span data-ttu-id="857ac-110">3,0 Preview 9</span><span class="sxs-lookup"><span data-stu-id="857ac-110">3.0 Preview 9</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="857ac-111">Doporučená akce</span><span class="sxs-lookup"><span data-stu-id="857ac-111">Recommended action</span></span>

<span data-ttu-id="857ac-112">Odeberte přepínač.</span><span class="sxs-lookup"><span data-stu-id="857ac-112">Remove the switch.</span></span> <span data-ttu-id="857ac-113">Přepínač není podporován a nejsou k dispozici žádné alternativní funkce.</span><span class="sxs-lookup"><span data-stu-id="857ac-113">The switch is not supported, and no alternative functionality is available.</span></span>

#### <a name="category"></a><span data-ttu-id="857ac-114">Kategorie</span><span class="sxs-lookup"><span data-stu-id="857ac-114">Category</span></span>

<span data-ttu-id="857ac-115">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="857ac-115">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="857ac-116">Ovlivněná rozhraní API</span><span class="sxs-lookup"><span data-stu-id="857ac-116">Affected APIs</span></span>

- <span data-ttu-id="857ac-117">Žádné</span><span class="sxs-lookup"><span data-stu-id="857ac-117">None</span></span>

<!-- 

### Affected APIs

- Not detectable via API analysis

-->