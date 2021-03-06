---
title: 'Návod: Použití jen uložených procedur (C#)'
ms.date: 03/30/2017
ms.assetid: ecde4bf2-fa4d-4252-b5e4-96a46b9e097d
ms.openlocfilehash: f980402c976db9ee327a7b726e36a0a4d9d6d73f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792113"
---
# <a name="walkthrough-using-only-stored-procedures-c"></a>Návod: Použití jen uložených procedur (C#)

Tento názorný postup poskytuje základní kompletní [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] scénář pro přístup k datům, a to provedením uložených procedur. Tento přístup často používají správci databáze k omezení způsobu přístupu k úložišti dat.

> [!NOTE]
> Uložené procedury v [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] aplikacích můžete použít také k přepsání výchozího chování, zejména pro `Create`procesy, `Update`a `Delete` . Další informace najdete v tématu [přizpůsobení operací vložení, aktualizace a odstranění](customizing-insert-update-and-delete-operations.md).

Pro účely tohoto Názorného postupu použijete dvě metody, které byly namapovány na uložené procedury v ukázkové databázi Northwind: CustOrdersDetail a CustOrderHist. Mapování probíhá při spuštění nástroje příkazového řádku SqlMetal pro vygenerování C# souboru. Další informace najdete v části požadavky dále v tomto návodu.

Tento návod nespoléhá na Návrhář relací objektů. Vývojáři, kteří používají Visual Studio, mohou také použít návrháře O/R k implementaci funkcí uložených procedur. Viz [nástroje LINQ to SQL v aplikaci Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

Tento návod byl napsán s použitím nastavení C# vizuálního vývoje.

## <a name="prerequisites"></a>Požadavky

Tento návod vyžaduje následující:

- Tento návod používá pro uchovávání souborů vyhrazenou složku (c:\linqtest7). Před zahájením tohoto návodu vytvořte tuto složku.

- Ukázkovou databázi Northwind

     Pokud tuto databázi ve vývojovém počítači nemáte, můžete si ji stáhnout z webu služby Stažení softwaru společnosti Microsoft. Pokyny najdete v tématu [stažení ukázkových databází](downloading-sample-databases.md). Po stažení databáze zkopírujte soubor northwnd. mdf do složky c:\linqtest7.

- Soubor C# kódu vygenerovaný z databáze Northwind.

     Tento návod byl napsán pomocí nástroje SqlMetal s následujícím příkazovým řádkem:

     **SQLMetal/Code: "c:\linqtest7\northwind.cs"/Language: CSharp "c:\linqtest7\northwnd.mdf"/sprocs/Functions/pluralize**

     Další informace naleznete v tématu [SqlMetal. exe (Nástroj pro generování kódu)](../../../../tools/sqlmetal-exe-code-generation-tool.md).

## <a name="overview"></a>Přehled

Tento názorný postup se skládá ze šesti hlavních úloh:

- [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Nastavení řešení v aplikaci Visual Studio.

- Do projektu se přidává sestavení System. data. Linq.

- Do projektu se přidává soubor s kódem databáze.

- Vytváří se připojení k databázi.

- Nastavení uživatelského rozhraní

- Spuštění a testování aplikace.

## <a name="creating-a-linq-to-sql-solution"></a>Vytvoření řešení LINQ to SQL

V tomto prvním úkolu vytvoříte řešení sady Visual Studio, které obsahuje nezbytné odkazy pro sestavení a spuštění [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] projektu.

### <a name="to-create-a-linq-to-sql-solution"></a>Vytvoření řešení LINQ to SQL

1. V nabídce **soubor** v aplikaci Visual Studio přejděte na **Nový**a klikněte na **projekt**.

2. V podokně **typy projektů** v dialogovém okně **Nový projekt** klikněte na položku **vizuál C#** .

3. V podokně **šablony** klikněte na **model Windows Forms aplikace**.

4. Do pole **název** zadejte **SprocOnlyApp**.

5. V poli **umístění** ověřte, kam chcete uložit soubory projektu.

6. Klikněte na **OK**.

     Otevře se Návrhář formulářů.

## <a name="adding-the-linq-to-sql-assembly-reference"></a>Přidání odkazu na sestavení LINQ to SQL

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Sestavení není zahrnuto do šablony standardní model Windows Forms aplikace. Sestavení bude nutné přidat sami, jak je vysvětleno v následujících krocích:

### <a name="to-add-systemdatalinqdll"></a>To add System.Data.Linq.dll

1. V **Průzkumník řešení**klikněte pravým tlačítkem na **odkazy**a pak klikněte na **Přidat odkaz**.

2. V dialogovém okně **Přidat odkaz** klikněte na položku **.NET**, klikněte na položku sestavení System. data. Linq a pak klikněte na tlačítko **OK**.

     Sestavení je přidáno do projektu.

## <a name="adding-the-northwind-code-file-to-the-project"></a>Přidání souboru s kódem Northwind do projektu

Tento krok předpokládá, že jste použili nástroj SqlMetal k vygenerování souboru kódu z ukázkové databáze Northwind. Další informace najdete v části požadavky výše v tomto návodu.

### <a name="to-add-the-northwind-code-file-to-the-project"></a>Přidání souboru s kódem Northwind do projektu

1. V nabídce **projekt** klikněte na položku **Přidat existující položku**.

2. V dialogovém okně **Přidat existující položku** přejděte na c:\linqtest7\northwind.cs a pak klikněte na **Přidat**.

     Soubor northwind.cs se přidá do projektu.

## <a name="creating-a-database-connection"></a>Vytvoření připojení k databázi

V tomto kroku nadefinujete připojení k ukázkové databázi Northwind. Tento návod používá jako cestu "c:\linqtest7\northwnd.mdf".

### <a name="to-create-the-database-connection"></a>Vytvoření připojení k databázi

1. V **Průzkumník řešení**klikněte pravým tlačítkem na **Form1.cs**a pak klikněte na **Zobrazit kód**.

2. Do `Form1` třídy zadejte následující kód:

     [!code-csharp[DLinqWalk4CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#1)]

## <a name="setting-up-the-user-interface"></a>Nastavení uživatelského rozhraní

V této úloze nastavíte rozhraní tak, aby uživatelé mohli spouštět uložené procedury pro přístup k datům v databázi. V aplikacích, které vyvíjíte pomocí tohoto Názorného postupu, mohou uživatelé získat přístup k datům v databázi pouze pomocí uložených procedur integrovaných v aplikaci.

### <a name="to-set-up-the-user-interface"></a>Nastavení uživatelského rozhraní

1. Vraťte se do Návrhář formulářů (**Form1. cs [Design]** ).

2. V nabídce **zobrazení** klikněte na příkaz **Sada nástrojů**.

     Otevře se panel nástrojů.

    > [!NOTE]
    > Klikněte na ikonu Automatické **skrývání** , aby se panel nástrojů otevřel při provádění zbývajících kroků v této části.

3. Přetáhněte dvě tlačítka, dvě textová pole a dva popisky z panelu nástrojů na **Form1**.

     Uspořádejte ovládací prvky jako v doprovodné ilustraci. Rozbalte **Form1** , aby se ovládací prvky vešly do jednoduchého umístění.

4. Klikněte pravým tlačítkem na **Label1**a pak klikněte na **vlastnosti**.

5. Změňte vlastnost **text** z **Label1** na **ENTER ČísloObjednávky:** .

6. Stejným způsobem jako u **Label2**změňte vlastnost **text** z **Label2** na **ENTER CustomerID:** .

7. Stejným způsobem změňte vlastnost **text** pro **Button1** na **Podrobnosti objednávky**.

8. Změňte vlastnost **text** pro **Button2** na **Seřadit historii**.

     Rozšiřte ovládací prvky tlačítko tak, aby byl veškerý text viditelný.

### <a name="to-handle-button-clicks"></a>Pro zpracování kliknutí na tlačítko

1. Poklikejte na **Podrobnosti objednávky** na **Form1** a otevřete obslužnou rutinu události Button1 v editoru kódu.

2. Do `button1` obslužné rutiny zadejte následující kód:

     [!code-csharp[DLinqWalk4CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#2)]

3. Nyní dvakrát klikněte na položku **Button2** na **Form1** `button2` a otevřete obslužnou rutinu

4. Do `button2` obslužné rutiny zadejte následující kód:

     [!code-csharp[DLinqWalk4CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#3)]

## <a name="testing-the-application"></a>Testování aplikace

Nyní je čas testovat aplikaci. Všimněte si, že váš kontakt s úložištěm dat je omezený na jakékoli akce, které můžou tyto dvě uložené procedury provádět. Tyto akce mají vracet produkty zahrnuté do každé položky ČísloObjednávky, které zadáte, nebo vrátí historii produktů seřazených podle ID zákazníka, které zadáte.

### <a name="to-test-the-application"></a>Testování aplikace

1. Stisknutím klávesy F5 spusťte ladění.

     Zobrazí se Form1.

2. Do pole **Zadejte ČísloObjednávky** zadejte `10249`a potom klikněte na **Seřadit podrobnosti**.

     Okno se zprávou obsahuje seznam produktů obsažených v pořadí 10249.

     Kliknutím na tlačítko **OK** zavřete okno se zprávou.

3. Do pole **Zadejte CustomerID** zadejte `ALFKI`a pak klikněte na **Historie objednávek**.

     Zobrazí se okno se zprávou se seznamem historie objednávek pro zákazníka ALFKI.

     Kliknutím na tlačítko **OK** zavřete okno se zprávou.

4. Do pole **Zadejte ČísloObjednávky** zadejte `123`a potom klikněte na **Seřadit podrobnosti**.

     Zobrazí se okno se zprávou bez výsledků.

     Kliknutím na tlačítko **OK** zavřete okno se zprávou.

5. V nabídce **ladění** klikněte na položku **Zastavit ladění**.

     Ladicí relace se zavře.

6. Pokud jste dokončili experimentování, můžete kliknout na **Zavřít projekt** v nabídce **soubor** a po zobrazení výzvy projekt uložit.

## <a name="next-steps"></a>Další kroky

Tento projekt můžete vylepšit tím, že provedete nějaké změny. Můžete například zobrazit seznam dostupných uložených procedur v seznamu a nechat uživatele vybrat, které procedury provést. Výstup sestav můžete také streamovat do textového souboru.

## <a name="see-also"></a>Viz také:

- [Učení podle návodů](learning-by-walkthroughs.md)
- [Uložené procedury](stored-procedures.md)
