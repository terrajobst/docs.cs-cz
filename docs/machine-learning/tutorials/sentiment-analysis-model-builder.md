---
title: 'Kurz: Analyzovat klasifikaci mínění-Binary'
description: V tomto kurzu se dozvíte, jak vytvořit aplikaci Razor Pages, která klasifikuje mínění z komentářů k webu a provede příslušnou akci. Binární mínění klasifikátoru používá tvůrce modelů v aplikaci Visual Studio.
ms.date: 09/13/2019
author: luisquintanilla
ms.author: luquinta
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c6184e097daf4604173db9e2a34606e68eb0fdc8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054319"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-in-a-web-application-using-mlnet-model-builder"></a>Kurz: Analýza mínění komentářů k webu ve webové aplikaci pomocí Tvůrce modelů ML.NET

Naučte se analyzovat mínění z komentářů v reálném čase uvnitř webové aplikace.

V tomto kurzu se dozvíte, jak vytvořit aplikaci ASP.NET Core Razor Pages, která klasifikuje mínění z komentářů k webům v reálném čase.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření aplikace ASP.NET Core Razor Pages
> * Příprava a pochopení dat
> * Zvolit scénář
> * Načtení dat
> * Trénování modelu
> * Vyhodnocení modelu
> * Použití modelu pro předpovědi

> [!NOTE]
> Tvůrce modelů je aktuálně ve verzi Preview.

Zdrojový kód pro tento kurz najdete v úložišti [dotnet/machinelearning-Samples](https://github.com/dotnet/machinelearning-samples) .

## <a name="pre-requisites"></a>Požadavky

Seznam požadavků a pokyny k instalaci najdete v [Průvodci instalací modelu modelů](../how-to-guides/install-model-builder.md).

## <a name="create-a-razor-pages-application"></a>Vytvoření aplikace Razor Pages

1. Vytvořte **aplikaci ASP.NET Core Razor Pages**.

    1. Otevřete Visual Studio a v řádku nabídek vyberte **soubor > nový > projekt** . 
    1. V dialogovém okně Nový projekt vyberte uzel  **C# vizuálu** následovaný **webovým** uzlem. 
    1. Pak vyberte šablonu projektu **ASP.NET Core webové aplikace** . 
    1. Do textového pole **název** zadejte "SentimentRazor".
    1. Zaškrtávací políčko **vytvořit adresář pro řešení** by mělo být ve výchozím nastavení zaškrtnuté. Pokud tomu tak není, ověřte ji. 
    1. Vyberte tlačítko **OK**.
    1. Zvolte **Webová aplikace** v okně, které zobrazuje různé typy ASP.NET Core projektů, a pak vyberte tlačítko **OK** .

## <a name="prepare-and-understand-the-data"></a>Příprava a pochopení dat

Stáhněte si [datovou sadu Detox Wikipedii](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv). Po otevření webové stránky klikněte na ni pravým tlačítkem myši, vyberte **Uložit jako** a uložte soubor kdekoli v počítači. 

Každý řádek v datové sadě *Wikipedii-Detox-250-line-data. TSV* představuje jinou revizi, kterou si uživatel na Wikipedii nanechal. První sloupec představuje mínění textu (0 je non-toxický, 1 je toxický) a druhý sloupec představuje komentář, který opustil uživatel. Sloupce jsou oddělené kartami. Data vypadají jako následující:

| Mínění | SentimentText |
| :---: | :---: |
1 | = = HRUBÉ = = Dude, jste hrubé nahráli obrázek Carl, nebo jiný.
1 | = = OK! = = IM VANDALIZE VOLNĚ ŽIJÍCÍ NA WIKIWEBU A POTOM!!!
0 | Doufám, že vám to pomůže.

## <a name="choose-a-scenario"></a>Zvolit scénář

![](./media/sentiment-analysis-model-builder/model-builder-screen.png)

Abyste mohli model vyškolit, musíte si vybrat ze seznamu dostupných scénářů strojového učení, které poskytuje tvůrce modelů. 

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt *SentimentRazor* a vyberte **Přidat** > **Machine Learning**.
1. V této ukázce je scénář analýzou mínění. V kroku *scénář* nástroje Tvůrce modelů vyberte **Analýza mínění** scénář.

## <a name="load-the-data"></a>Načtení dat

Tvůrce modelů přijímá data ze dvou zdrojů, SQL Server databáze nebo místního souboru ve `csv` formátu nebo. `tsv`

1. V kroku dat nástroje Tvůrce modelů vyberte v rozevíracím seznamu zdroj dat **soubor** .
1. Vyberte tlačítko vedle textového pole **Vybrat soubor** a pomocí Průzkumníka souborů vyhledejte a vyberte soubor *Wikipedii-Detox-250-line-data. TSV* .
1. Výběr **mínění** v rozevíracím seznamu **popisek nebo sloupec pro předpověď**
1. Vyberte odkaz **výuka** , který se přesune k dalšímu kroku v nástroji Tvůrce modelů.

## <a name="train-the-model"></a>Trénování modelu

Úkolem strojového učení, který se používá k výuce modelu předpovědi cen v tomto kurzu, je binární klasifikace. V průběhu procesu školení modelů vlacích sestavuje samostatné modely pomocí různých binárních algoritmů klasifikace a nastavení, aby bylo možné najít nejlepší model pro datovou sadu.

Čas potřebný ke školení modelu je úměrný množství dat. Tvůrce modelů automaticky vybere výchozí hodnotu pro **čas do výuky (sekundy)** na základě velikosti zdroje dat. 

1. I když tvůrce modelů nastaví hodnotu **času na vlak (sekundy)** až 10 sekund, narůstá na 30 sekund. Školení po delší dobu umožňuje tvůrci modelů prozkoumat větší počet algoritmů a kombinaci parametrů při hledání nejlepšího modelu.
1. Vyberte **Spustit školení**.

    V průběhu procesu školení se data o průběhu zobrazují v `Progress` části kroku výuka.

    - Stav zobrazuje stav dokončení procesu školení.
    - Nejlepší přesnost zobrazuje přesnost nejlepšího modelu, kterou najde tvůrce modelů, zatím. Vyšší přesnost znamená, že model se v testovacích datech podrobnějším způsobem vypovídat.
    - Nejlepší algoritmus zobrazuje název nejlepšího výkonu, který našel tvůrce modelů, zatím.
    - Poslední algoritmus zobrazuje název algoritmu naposledy, který tvůrce modelů použil k vytvoření výukového modelu.

1. Po dokončení školení vyberte odkaz **vyhodnotit** , který se přesune k dalšímu kroku.

## <a name="evaluate-the-model"></a>Vyhodnocení modelu

Výsledkem kroku školení bude jeden model, který má nejlepší výkon. V kroku vyhodnocení nástroje pro sestavování modelů bude v sekci výstup obsahovat algoritmus používaný modelem nejlepšího provádění v **nejlepším záznamu modelu** spolu se metrikami v **nejlepší kvalitě modelu (RSquared)** . Navíc Souhrnná tabulka obsahující pět modelů a jejich metriky.

Pokud nejste spokojeni s metrikami přesnosti, můžou vám některé jednoduché způsoby, jak zkusit a zlepšit přesnost modelu, zvýšit množství času pro výuku modelu nebo použít víc dat. V opačném případě vyberte odkaz **kód** , který se přesune k poslednímu kroku v nástroji Tvůrce modelů.

## <a name="add-the-code-to-make-predictions"></a>Přidejte kód, který provede předpovědi

V důsledku školicího procesu se vytvoří dva projekty.

### <a name="reference-the-trained-model"></a>Odkaz na školený model

1. V kroku *kód* nástroje Tvůrce modelů vyberte **Přidat projekty** a přidejte do řešení automaticky generované projekty.

    Následující projekty by se měly zobrazit v **Průzkumník řešení**:

    - *SentimentRazorML. ConsoleApp*: Konzolová aplikace .NET Core, která obsahuje kód pro školení a předpověď modelu.
    - *SentimentRazorML. model*: .NET Standard knihovny tříd obsahující datové modely, které definují schéma vstupních a výstupních dat modelu a také trvalou verzi modelu nejlepšího provádění během školení.

    Pro tento kurz je použit pouze projekt *SentimentRazorML. model* , protože předpovědi bude vytvořen ve webové aplikaci *SentimentRazor* , nikoli v konzole nástroje. I když se *SentimentRazorML. ConsoleApp* nebude používat pro vyhodnocování, dá se použít k reučení modelu pomocí nových dat později. Přeškolení je mimo rámec tohoto kurzu, ale.

1. Chcete-li použít trained model uvnitř vaší aplikace Razor Pages, přidejte odkaz na projekt *SentimentRazorML. model* .

    1. Klikněte pravým tlačítkem na projekt **SentimentRazor** . 
    1. Vyberte **přidat > odkaz**. 
    1. Vyberte **projekty > uzel řešení** a ze seznamu ověřte projekt **SentimentRazorML. model** .
    1. Vyberte **OK**.

### <a name="configure-the-predictionengine-pool"></a>Konfigurace PredictionEngine fondu

K provedení jedné předpovědi použijte [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602). Aby bylo možné použít [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) aplikaci v aplikaci, je nutné ji v případě potřeby vytvořit. V takovém případě je osvědčeným postupem použití injektáže závislostí.

> [!WARNING]
> [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)není bezpečná pro přístup z více vláken. Pro zlepšení výkonu a bezpečnosti vláken použijte `PredictionEnginePool` službu, která [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) vytvoří `PredictionEngine` objekty pro použití aplikací. Další informace o [vytváření a používání `PredictionEngine` fondů objektů v ASP.NET Core](https://devblogs.microsoft.com/cesardelatorre/how-to-optimize-and-run-ml-net-models-on-scalable-asp-net-core-webapis-or-web-apps/)najdete v tomto blogovém příspěvku. 

1. Nainstalujte balíček NuGet *Microsoft.Extensions.ml* :

    1. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**. 
    1. Jako zdroj balíčku vyberte "nuget.org". 
    1. Vyberte kartu **Procházet** a vyhledejte **Microsoft.Extensions.ml**. 
    1. Vyberte balíček v seznamu a klikněte na tlačítko **instalovat** . 
    1. V dialogovém okně **Náhled změn** klikněte na tlačítko **OK** .
    1. Pokud souhlasíte s licenčními podmínkami pro uvedené balíčky, v dialogu pro **přijetí licence** vyberte tlačítko **přijmout** . 

1. Otevřete soubor *Startup.cs* v projektu *SentimentRazor* .
1. Přidejte následující příkazy using pro odkazování na balíček NuGet *Microsoft.Extensions.ml* a projekt *SentimentRazorML. model* :

    [!code-csharp [StartupUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L12-L14)]        

1. Vytvořte globální proměnnou pro uložení umístění trained modelového souboru.

    [!code-csharp [ModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L20)]

1. Soubor modelu je uložen v adresáři buildu spolu se soubory sestavení vaší aplikace. Aby byl přístup snazší, vytvořte pomocnou metodu volanou `GetAbsolutePath` `Configure` za metodou.

    [!code-csharp [GetAbsolutePathMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L66-L73)]

1. Použijte metodu v konstruktoru`_modelPath`třídypronastavení. `Startup` `GetAbsolutePath`

    [!code-csharp [InitModelPath](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L25)]

1. Nakonfigurujte pro aplikaci v `ConfigureServices`metodě: `PredictionEnginePool`

    [!code-csharp [InitPredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Startup.cs#L42)]

### <a name="create-sentiment-analysis-handler"></a>Vytvořit obslužnou rutinu analýzy mínění

Předpovědi se provede uvnitř hlavní stránky aplikace. Proto metoda, která přijímá vstup uživatele a používá `PredictionEnginePool` k vrácení předpovědi, je nutné přidat.

1. Otevřete soubor *index.cshtml.cs* umístěný v adresáři *stránky* a přidejte následující příkazy using:

    [!code-csharp [IndexUsings](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L7-L8)]

    Aby bylo možné použít `PredictionEnginePool` konfiguraci `Startup` ve třídě, je nutné ji vložit do konstruktoru modelu, kde jej chcete použít. 

1. Přidejte proměnnou pro odkazování `PredictionEnginePool` `IndexModel` uvnitř třídy.

    [!code-csharp [PredEnginePool](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L14)]

1. Vytvořte ve `IndexModel` třídě konstruktor a `PredictionEnginePool` založit do něj službu.

    [!code-csharp [IndexConstructor](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L16-L19)]

1. Vytvořte obslužnou rutinu metody, která `PredictionEnginePool` používá k vytvoření předpovědi ze vstupu uživatele přijatého z webové stránky.

    1. `OnGet` Pod metodou vytvořte novou metodu s názvem.`OnGetAnalyzeSentiment`

        ```csharp
        public IActionResult OnGetAnalyzeSentiment([FromQuery] string text)
        {

        }
        ```

    1. V rámci metody vrátí neutrální mínění, pokud je vstup od uživatele prázdný nebo má hodnotu null. `OnGetAnalyzeSentiment`

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L28)] 
    
    1. Když je zadaný platný vstup, vytvoří se nová instance `ModelInput`. 

        [!code-csharp [InitInput](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L29)] 

    1. `PredictionEnginePool` Použijte k předpovídání mínění.

        [!code-csharp [MakePrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L30)] 

    1. Převeďte předpovězenou `bool` hodnotu na toxické nebo netoxické pomocí následujícího kódu.

        [!code-csharp [ConvertPrediction](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L31)]

    1. Nakonec vraťte mínění zpět na webovou stránku.

        [!code-csharp [ReturnSentiment](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml.cs#L32)]

### <a name="configure-the-web-page"></a>Konfigurace webové stránky

Výsledky vrácené nástrojem `OnGetAnalyzeSentiment` budou dynamicky zobrazeny `Index` na webové stránce.

1. Otevřete soubor *index. cshtml* v adresáři *stránky* a nahraďte jeho obsah následujícím kódem: 

    [!code-cshtml [IndexPage](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml)]

1. Pak na konec stránky *. CSS* v adresáři *wwwroot\css* přidejte kód CSS stylu:

    [!code-css [CssStyling](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/css/site.css#L61-L105)]

1. Pak přidejte kód, který odešle vstupy z webové stránky do `OnGetAnalyzeSentiment` obslužné rutiny.

    1. V souboru *site. js* v adresáři *wwwroot\js* vytvořte funkci s názvem `getSentiment` , která vytvoří požadavek GET http `OnGetAnalyzeSentiment` s uživatelským vstupem k obslužné rutině.

        [!code-javascript [GetSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L5-L10)]

    1. Níže přidejte další funkci nazvanou `updateMarker` , která dynamicky aktualizuje pozici značky na webové stránce, protože mínění je předpovězeno.

        [!code-javascript [UpdateMarkerMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L12-L15)]

    1. Vytvořte funkci obslužné rutiny události `updateSentiment` volanou k získání vstupu z uživatele, odešlete ji `OnGetAnalyzeSentiment` funkci pomocí `getSentiment` funkce a aktualizujte značku pomocí `updateMarker` funkce.

        [!code-javascript [UpdateSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L17-L34)]

    1. Nakonec zaregistrujte obslužnou rutinu události a navažte `textarea` ji na element `id=Message` s atributem.

        [!code-javascript [UpdateSentimentEvtHandler](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L36)]

## <a name="run-the-application"></a>Spuštění aplikace

Teď, když je vaše aplikace nastavená, spusťte aplikaci, která by se měla spustit ve vašem prohlížeči.

Až se aplikace spustí, zadejte *Tvůrce modelů.* do textové oblasti. Zobrazený předpokládaný mínění by neměl být *toxický*.

![](./media/sentiment-analysis-model-builder/web-app.png)

Pokud potřebujete odkazovat na projekty vygenerované tvůrcem modelu později v jiném řešení, můžete je najít v `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` adresáři.

## <a name="next-steps"></a>Další postup

V tomto kurzu jste se naučili:
> [!div class="checklist"]
> * Vytvoření aplikace ASP.NET Core Razor Pages
> * Příprava a pochopení dat
> * Zvolit scénář
> * Načtení dat
> * Trénování modelu
> * Vyhodnocení modelu
> * Použití modelu pro předpovědi

### <a name="additional-resources"></a>Další prostředky

Další informace o tématech uvedených v tomto kurzu najdete v následujících zdrojích informací:

- [Scénáře tvůrce modelů](../automate-training-with-model-builder.md#scenarios)
- [Binární klasifikace](../resources/glossary.md#binary-classification)
- [Metriky modelu binární klasifikace](../resources/metrics.md#metrics-for-binary-classification)