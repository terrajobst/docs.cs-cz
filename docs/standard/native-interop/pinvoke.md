---
title: Vyvolání platformy (nespravovaného)
description: Zjistěte, jak volat nativní funkce prostřednictvím P/Invoke v rozhraní .NET.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: f243fee2b246afff36732d469c6295d7e4b2fd87
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2019
ms.locfileid: "54416223"
---
# <a name="platform-invoke-pinvoke"></a><span data-ttu-id="2afc0-103">Vyvolání platformy (nespravovaného)</span><span class="sxs-lookup"><span data-stu-id="2afc0-103">Platform Invoke (P/Invoke)</span></span>

<span data-ttu-id="2afc0-104">P/Invoke je technologie, která umožňuje přístup ke strukturám, zpětná volání a funkce v nespravovaných knihoven ze spravovaného kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-104">P/Invoke is a technology that allows you to access structs, callbacks, and functions in unmanaged libraries from your managed code.</span></span> <span data-ttu-id="2afc0-105">Většina nespravovaného rozhraní API je součástí dva obory názvů: `System` a `System.Runtime.InteropServices`.</span><span class="sxs-lookup"><span data-stu-id="2afc0-105">Most of the P/Invoke API is contained in two namespaces: `System` and `System.Runtime.InteropServices`.</span></span> <span data-ttu-id="2afc0-106">Tyto dva obory názvů pomocí získáte všechny nástroje k popisu způsobu komunikovat s nativní součást.</span><span class="sxs-lookup"><span data-stu-id="2afc0-106">Using these two namespaces give you the tools to describe how you want to communicate with the native component.</span></span>

<span data-ttu-id="2afc0-107">Začněme od Nejběžnějším příkladem a, který je volání nespravovaných funkcí ve spravovaném kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-107">Let’s start from the most common example, and that is calling unmanaged functions in your managed code.</span></span> <span data-ttu-id="2afc0-108">Pojďme zobrazit okno se zprávou z aplikace příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="2afc0-108">Let’s show a message box from a command-line application:</span></span>

```csharp
using System.Runtime.InteropServices;

public class Program {

    // Import user32.dll (containing the function we need) and define
    // the method corresponding to the native function.
    [DllImport("user32.dll")]
    public static extern int MessageBox(IntPtr hWnd, String text, String caption, int options);

    public static void Main(string[] args) {
        // Invoke the function as a regular managed method.
        MessageBox(IntPtr.Zero, "Command-line message box", "Attention!", 0);
    }
}
```

<span data-ttu-id="2afc0-109">V předchozím příkladu je jednoduché, ale je předvést, co je potřeba k volání nespravovaných funkcí ze spravovaného kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-109">The previous example is simple, but it does show off what's needed to invoke unmanaged functions from managed code.</span></span> <span data-ttu-id="2afc0-110">Projděme si příklad:</span><span class="sxs-lookup"><span data-stu-id="2afc0-110">Let’s step through the example:</span></span>

*   <span data-ttu-id="2afc0-111">Řádek #1 ukazuje na pomocí příkazu pro `System.Runtime.InteropServices` obor názvů, který obsahuje všechny položky, které jsou potřeba.</span><span class="sxs-lookup"><span data-stu-id="2afc0-111">Line #1 shows the using statement for the `System.Runtime.InteropServices` namespace that holds all the items needed.</span></span>
*   <span data-ttu-id="2afc0-112">Představuje řádek #7 `DllImport` atribut.</span><span class="sxs-lookup"><span data-stu-id="2afc0-112">Line #7 introduces the `DllImport` attribute.</span></span> <span data-ttu-id="2afc0-113">Tento atribut je zásadní, protože říká modul runtime, že by se měly načíst nespravovaná knihovna DLL.</span><span class="sxs-lookup"><span data-stu-id="2afc0-113">This attribute is crucial, as it tells the runtime that it should load the unmanaged DLL.</span></span> <span data-ttu-id="2afc0-114">Předaný řetězec je knihovna DLL je náš cíl funkce v.</span><span class="sxs-lookup"><span data-stu-id="2afc0-114">The string passed in is the DLL our target function is in.</span></span>
*   <span data-ttu-id="2afc0-115">Řádek #8 je jádrem pracovní P/Invoke.</span><span class="sxs-lookup"><span data-stu-id="2afc0-115">Line #8 is the crux of the P/Invoke work.</span></span> <span data-ttu-id="2afc0-116">Definuje spravované metody, která má **přesně stejnou signaturu** jako nespravovaný.</span><span class="sxs-lookup"><span data-stu-id="2afc0-116">It defines a managed method that has the **exact same signature** as the unmanaged one.</span></span> <span data-ttu-id="2afc0-117">Deklarace má nové klíčové slovo, můžete si všimnete, `extern`, který dává pokyn modulu runtime to je externí metoda a že při vyvolání jeho, modul runtime měl nacházet v knihovny DLL určené v `DllImport` atribut.</span><span class="sxs-lookup"><span data-stu-id="2afc0-117">The declaration has a new keyword that you can notice, `extern`, which tells the runtime this is an external method, and that when you invoke it, the runtime should find it in the DLL specified in `DllImport` attribute.</span></span>

<span data-ttu-id="2afc0-118">Zbývající část v příkladu je právě volání metody, stejně jako jiné spravované metody.</span><span class="sxs-lookup"><span data-stu-id="2afc0-118">The rest of the example is just invoking the method as you would any other managed method.</span></span>

<span data-ttu-id="2afc0-119">Vzorek je podobný pro macOS.</span><span class="sxs-lookup"><span data-stu-id="2afc0-119">The sample is similar for macOS.</span></span> <span data-ttu-id="2afc0-120">Název knihovny `DllImport` atributů je potřeba změnit, protože s macOS má jiné schéma názvů dynamické knihovny.</span><span class="sxs-lookup"><span data-stu-id="2afc0-120">The name of the library in the `DllImport` attribute needs to change since macOS has a different scheme of naming dynamic libraries.</span></span> <span data-ttu-id="2afc0-121">Následující ukázkový používá `getpid(2)` funkce, která se získat ID procesu aplikace a vytiskne ji do konzoly:</span><span class="sxs-lookup"><span data-stu-id="2afc0-121">The following sample uses the `getpid(2)` function to get the process ID of the application and print it out to the console:</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libSystem shared library and define the method corresponding to the native function.
        [DllImport("libSystem.dylib")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}
```

<span data-ttu-id="2afc0-122">Je to podobné v Linuxu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-122">It is also similar on Linux.</span></span> <span data-ttu-id="2afc0-123">Název funkce je stejný, protože `getpid(2)` je standard [POSIX](https://en.wikipedia.org/wiki/POSIX) volání systému.</span><span class="sxs-lookup"><span data-stu-id="2afc0-123">The function name is the same, since `getpid(2)` is a standard [POSIX](https://en.wikipedia.org/wiki/POSIX) system call.</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libc shared library and define the method corresponding to the native function.
        [DllImport("libc.so.6")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}
```

## <a name="invoking-managed-code-from-unmanaged-code"></a><span data-ttu-id="2afc0-124">Volání spravovaného kódu z nespravovaného kódu</span><span class="sxs-lookup"><span data-stu-id="2afc0-124">Invoking managed code from unmanaged code</span></span>

<span data-ttu-id="2afc0-125">Modul runtime povoluje komunikaci probíhaly v obou směrech, umožňuje volat zpět do spravovaného kódu z nativní funkce pomocí ukazatelů na funkce.</span><span class="sxs-lookup"><span data-stu-id="2afc0-125">The runtime allows communication to flow in both directions, enabling you to call back into managed code from native functions by using function pointers.</span></span> <span data-ttu-id="2afc0-126">Je nejbližší věcí s ukazatelem na funkci ve spravovaném kódu **delegovat**, takže je to, co se používá k povolení zpětných volání z nativního kódu do spravovaného kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-126">The closest thing to a function pointer in managed code is a **delegate**, so this is what is used to allow callbacks from native code into managed code.</span></span>

<span data-ttu-id="2afc0-127">Způsob, jak používat tuto funkci je podobný jako spravované do nativní popsaných výše.</span><span class="sxs-lookup"><span data-stu-id="2afc0-127">The way to use this feature is similar to the managed to native process previously described.</span></span> <span data-ttu-id="2afc0-128">Pro dané zpětné volání definovat delegáta, která odpovídá podpisu a předat ho do externí metody.</span><span class="sxs-lookup"><span data-stu-id="2afc0-128">For a given callback, you define a delegate that matches the signature and pass that into the external method.</span></span> <span data-ttu-id="2afc0-129">Modul runtime se postará o všechno ostatní.</span><span class="sxs-lookup"><span data-stu-id="2afc0-129">The runtime will take care of everything else.</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

namespace ConsoleApplication1 {

    class Program {

        // Define a delegate that corresponds to the unmanaged function.
        delegate bool EnumWC(IntPtr hwnd, IntPtr lParam);

        // Import user32.dll (containing the function we need) and define
        // the method corresponding to the native function.
        [DllImport("user32.dll")]
        static extern int EnumWindows(EnumWC lpEnumFunc, IntPtr lParam);

        // Define the implementation of the delegate; here, we simply output the window handle.
        static bool OutputWindow(IntPtr hwnd, IntPtr lParam) {
            Console.WriteLine(hwnd.ToInt64());
            return true;
        }

        static void Main(string[] args) {
            // Invoke the method; note the delegate as a first parameter.
            EnumWindows(OutputWindow, IntPtr.Zero);
        }
    }
}
```

<span data-ttu-id="2afc0-130">Před provede v příkladu, je vhodné zkontrolovat podpisy nespravované funkce, které potřebujete pro práci s.</span><span class="sxs-lookup"><span data-stu-id="2afc0-130">Before walking through the example, it's good to review the signatures of the unmanaged functions you need to work with.</span></span> <span data-ttu-id="2afc0-131">Funkce, která se dá zavolat, aby vypisovat výčet všech oken má následující podpis: `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`</span><span class="sxs-lookup"><span data-stu-id="2afc0-131">The function to be called to enumerate all of the windows has the following signature: `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`</span></span>

<span data-ttu-id="2afc0-132">První parametr je zpětné volání.</span><span class="sxs-lookup"><span data-stu-id="2afc0-132">The first parameter is a callback.</span></span> <span data-ttu-id="2afc0-133">Uvedené zpětné volání má následující podpis: `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`</span><span class="sxs-lookup"><span data-stu-id="2afc0-133">The said callback has the following signature: `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`</span></span>

<span data-ttu-id="2afc0-134">Nyní projděme si příklad:</span><span class="sxs-lookup"><span data-stu-id="2afc0-134">Now, let’s walk through the example:</span></span>

*   <span data-ttu-id="2afc0-135">Řádek #9 v příkladu definuje delegáta, který se shoduje se signaturou zpětného volání z nespravovaného kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-135">Line #9 in the example defines a delegate that matches the signature of the callback from unmanaged code.</span></span> <span data-ttu-id="2afc0-136">Všimněte si, jak jsou reprezentovány typy LPARAM a HWND pomocí `IntPtr` ve spravovaném kódu.</span><span class="sxs-lookup"><span data-stu-id="2afc0-136">Notice how the LPARAM and HWND types are represented using `IntPtr` in the managed code.</span></span>
*   <span data-ttu-id="2afc0-137">Zavést řádky #13 a #14 `EnumWindows` funkce z knihovny user32.dll.</span><span class="sxs-lookup"><span data-stu-id="2afc0-137">Lines #13 and #14 introduce the `EnumWindows` function from the user32.dll library.</span></span>
*   <span data-ttu-id="2afc0-138">Řádky #17 20 implementaci delegáta.</span><span class="sxs-lookup"><span data-stu-id="2afc0-138">Lines #17 - 20 implement the delegate.</span></span> <span data-ttu-id="2afc0-139">Tento jednoduchý příklad my chceme jenom výstupní popisovač do konzoly.</span><span class="sxs-lookup"><span data-stu-id="2afc0-139">For this simple example, we just want to output the handle to the console.</span></span>
*   <span data-ttu-id="2afc0-140">Nakonec v řádku #24 externí metoda je volána a předaný delegátovi.</span><span class="sxs-lookup"><span data-stu-id="2afc0-140">Finally, in line #24, the external method is called and passed in the delegate.</span></span>

<span data-ttu-id="2afc0-141">Níže jsou uvedeny příklady operačních systémů Linux a macOS.</span><span class="sxs-lookup"><span data-stu-id="2afc0-141">The Linux and macOS examples are shown below.</span></span> <span data-ttu-id="2afc0-142">Pro ně používáme `ftw` funkce, která lze nalézt v `libc`, knihovna C.</span><span class="sxs-lookup"><span data-stu-id="2afc0-142">For them, we use the `ftw` function that can be found in `libc`, the C library.</span></span> <span data-ttu-id="2afc0-143">Tato funkce slouží k procházení hierarchie adresáře a bere ukazatel na funkci jako jeden ze svých parametrů.</span><span class="sxs-lookup"><span data-stu-id="2afc0-143">This function is used to traverse directory hierarchies and it takes a pointer to a function as one of its parameters.</span></span> <span data-ttu-id="2afc0-144">Uvedení funkce má následující podpis: `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`.</span><span class="sxs-lookup"><span data-stu-id="2afc0-144">The said function has the following signature: `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`.</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

            // Define a delegate that has the same signature as the native function.
            delegate int DirClbk(string fName, StatClass stat, int typeFlag);

            // Import the libc and define the method to represent the native function.
            [DllImport("libc.so.6")]
            static extern int ftw(string dirpath, DirClbk cl, int descriptors);

            // Implement the above DirClbk delegate;
            // this one just prints out the filename that is passed to it.
            static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                    Console.WriteLine(fName);
                    return 0;
            }

            public static void Main(string[] args){
                    // Call the native function.
                    // Note the second parameter which represents the delegate (callback).
                    ftw(".", DisplayEntry, 10);
            }
    }

    // The native callback takes a pointer to a struct. The below class
    // represents that struct in managed code. You can find more information
    // about this in the section on marshalling below.
    [StructLayout(LayoutKind.Sequential)]
    public class StatClass {
            public uint DeviceID;
            public uint InodeNumber;
            public uint Mode;
            public uint HardLinks;
            public uint UserID;
            public uint GroupID;
            public uint SpecialDeviceID;
            public ulong Size;
            public ulong BlockSize;
            public uint Blocks;
            public long TimeLastAccess;
            public long TimeLastModification;
            public long TimeLastStatusChange;
    }
}
```

<span data-ttu-id="2afc0-145">macOS příklad používá stejnou funkci, a jediným rozdílem je, že argument `DllImport` atribut, protože udržuje macOS `libc` na jiném místě.</span><span class="sxs-lookup"><span data-stu-id="2afc0-145">macOS example uses the same function, and the only difference is the argument to the `DllImport` attribute, as macOS keeps `libc` in a different place.</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
        public static class Program {

                // Define a delegate that has the same signature as the native function.
                delegate int DirClbk(string fName, StatClass stat, int typeFlag);

                // Import the libc and define the method to represent the native function.
                [DllImport("libSystem.dylib")]
                static extern int ftw(string dirpath, DirClbk cl, int descriptors);

                // Implement the above DirClbk delegate;
                // this one just prints out the filename that is passed to it.
                static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                        Console.WriteLine(fName);
                        return 0;
                }

                public static void Main(string[] args){
                        // Call the native function.
                        // Note the second parameter which represents the delegate (callback).
                        ftw(".", DisplayEntry, 10);
                }
        }

        // The native callback takes a pointer to a struct. The below class
        // represents that struct in managed code.
        [StructLayout(LayoutKind.Sequential)]
        public class StatClass {
                public uint DeviceID;
                public uint InodeNumber;
                public uint Mode;
                public uint HardLinks;
                public uint UserID;
                public uint GroupID;
                public uint SpecialDeviceID;
                public ulong Size;
                public ulong BlockSize;
                public uint Blocks;
                public long TimeLastAccess;
                public long TimeLastModification;
                public long TimeLastStatusChange;
        }
}
```

<span data-ttu-id="2afc0-146">I v předchozích příkladech záviset na parametrech a v obou případech jsou uvedeny parametry, jako spravované typy.</span><span class="sxs-lookup"><span data-stu-id="2afc0-146">Both of the previous examples depend on parameters, and in both cases, the parameters are given as managed types.</span></span> <span data-ttu-id="2afc0-147">Modul runtime dělá "správné věci" a zpracuje do své ekvivalenty na druhé straně.</span><span class="sxs-lookup"><span data-stu-id="2afc0-147">Runtime does the "right thing" and processes these into its equivalents on the other side.</span></span> <span data-ttu-id="2afc0-148">Další informace o tom, jak jsou typy zařazeno do nativního kódu na naší stránce [typu zařazování](type-marshalling.md).</span><span class="sxs-lookup"><span data-stu-id="2afc0-148">Learn about how types are marshalled to native code in our page on [Type marshalling](type-marshalling.md).</span></span>


## <a name="more-resources"></a><span data-ttu-id="2afc0-149">Další materiály</span><span class="sxs-lookup"><span data-stu-id="2afc0-149">More resources</span></span>

*   <span data-ttu-id="2afc0-150">[PInvoke.net wiki](https://www.pinvoke.net/) vynikající Wiki s informacemi o společné rozhraní API systému Win32 a postupu při jejich volání.</span><span class="sxs-lookup"><span data-stu-id="2afc0-150">[PInvoke.net wiki](https://www.pinvoke.net/) an excellent Wiki with information on common Win32 APIs and how to call them.</span></span>
*   [<span data-ttu-id="2afc0-151">P/Invoke na webu MSDN</span><span class="sxs-lookup"><span data-stu-id="2afc0-151">P/Invoke on MSDN</span></span>](https://msdn.microsoft.com/library/zbz07712.aspx)
*   [<span data-ttu-id="2afc0-152">Dokumentace mono na P/Invoke</span><span class="sxs-lookup"><span data-stu-id="2afc0-152">Mono documentation on P/Invoke</span></span>](https://www.mono-project.com/docs/advanced/pinvoke/)