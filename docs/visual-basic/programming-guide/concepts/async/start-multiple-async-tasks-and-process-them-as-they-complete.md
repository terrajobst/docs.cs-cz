---
title: Zahájení více úloh s modifikátorem Async a jejich zpracování po dokončení
ms.date: 07/20/2015
ms.assetid: 57ffb748-af40-4794-bedd-bdb7fea062de
ms.openlocfilehash: b14171196a95e9a6a12f6b13f6f17d3cfe352bce
ms.sourcegitcommit: 43d10ef65f0f1fd6c3b515e363bde11a3fcd8d6d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/04/2020
ms.locfileid: "78266843"
---
# <a name="start-multiple-async-tasks-and-process-them-as-they-complete-visual-basic"></a>Spuštění více asynchronních úloh a jejich zpracování po dokončení (Visual Basic)
Pomocí <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>aplikace můžete spustit více úkolů najednou a zpracovat je jeden po druhém při jejich dokončení, nikoli je zpracovat v pořadí, ve kterém jsou spuštěny.  
  
 Následující příklad používá dotaz k vytvoření kolekce úkolů. Každý úkol stáhne obsah zadaného webu. V každé iteraci smyčky while očekávané `WhenAny` volání vrátí úlohu v kolekci úkolů, které dokončí jeho stažení jako první. Tato úloha je odebrána z kolekce a zpracována. Smyčka se opakuje, dokud kolekce neobsahuje žádné další úkoly.  
  
> [!NOTE]
> Chcete-li spustit příklady, musíte mít Visual Studio 2012 nebo novější a rozhraní .NET Framework 4.5 nebo novější nainstalován v počítači.  
  
## <a name="downloading-the-example"></a>Stažení příkladu  
 Můžete si stáhnout celý projekt Windows Presentation Foundation (WPF) z [ukázky asynchronní: Jemné doladění aplikace](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) a postupujte takto.  
  
1. Dekomprimujte soubor, který jste stáhli, a spusťte Visual Studio.  
  
2. Na řádku nabídek zvolte **Soubor**, **Otevřít**, **Projekt/Řešení**.  
  
3. V dialogovém okně **Otevřít projekt** otevřete složku obsahující ukázkový kód, který jste dekomprimovali, a potom otevřete soubor řešení (.sln) pro AsyncFineTuningVB.  
  
4. V **Průzkumníku řešení**otevřete místní nabídku projektu **ProcessTasksAsTheyFinish** a pak zvolte **Nastavit jako počáteční projekt**.  
  
5. Zvolte klávesu F5 pro spuštění projektu.  
  
     Zvolte klávesy Ctrl+F5 pro spuštění projektu bez jeho ladění.  
  
6. Spusťte projekt několikrát a ověřte, zda se stažené délky nevždy zobrazují ve stejném pořadí.  
  
 Pokud nechcete stáhnout projekt, můžete zkontrolovat mainwindow.xaml.vb soubor na konci tohoto tématu.  
  
## <a name="building-the-example"></a>Vytvoření příkladu  
 Tento příklad přidá ke kódu, který je vyvinut v [zrušit zbývající asynchronní úkoly po dokončení jednoho (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md) a používá stejné ui.  
  
 Chcete-li vytvořit příklad sami, krok za krokem postupujte podle pokynů v části "Stažení příkladu", ale zvolte **CancelAfterOneTask** jako **projekt Spuštění**. Přidejte změny v tomto `AccessTheWebAsync` tématu k metodě v tomto projektu. Změny jsou označeny hvězdičkami.  
  
 Projekt **CancelAfterOneTask** již obsahuje dotaz, který při spuštění vytvoří kolekci úkolů. Každé volání `ProcessURLAsync` v následujícím kódu <xref:System.Threading.Tasks.Task%601> `TResult` vrátí kde je celé číslo.  
  
```vb  
Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
    From url In urlList Select ProcessURLAsync(url, client, ct)  
```  
  
 V souboru MainWindow.xaml.vb projektu proveďte následující `AccessTheWebAsync` změny metody.  
  
- Spusťte dotaz <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> použitím <xref:System.Linq.Enumerable.ToArray%2A>namísto .  
  
    ```vb  
    Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
    ```  
  
- Přidejte smyčku while, která provádí následující kroky pro každou úlohu v kolekci.  
  
    1. Čeká na volání `WhenAny` k identifikaci první úkol v kolekci k dokončení jeho stažení.  
  
        ```vb  
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
        ```  
  
    2. Odebere tento úkol z kolekce.  
  
        ```vb  
        downloadTasks.Remove(firstFinishedTask)  
        ```  
  
    3. Čeká `firstFinishedTask`, který je vrácen voláním `ProcessURLAsync`. Proměnná `firstFinishedTask` je <xref:System.Threading.Tasks.Task%601> `TReturn` kde je celé číslo. Úloha je již dokončena, ale čekáte na to, abyste načetli délku staženého webu, jak ukazuje následující příklad.  
  
        ```vb  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        ```  
  
 Projekt byste měli spustit několikrát, abyste ověřili, že stažené délky se nevždy zobrazují ve stejném pořadí.  
  
> [!CAUTION]
> Můžete použít `WhenAny` ve smyčce, jak je popsáno v příkladu, k řešení problémů, které zahrnují malý počet úkolů. Jiné přístupy jsou však efektivnější, pokud máte velký počet úkolů ke zpracování. Další informace a příklady naleznete [v tématu Zpracování úloh při jejich dokončení](https://devblogs.microsoft.com/pfxteam/processing-tasks-as-they-complete/).  
  
## <a name="complete-example"></a>Kompletní příklad  
 Následující kód je úplný text mainwindow.xaml.vb souboru pro příklad. Hvězdičky označují prvky, které byly přidány pro tento příklad.  
  
 Všimněte si, že <xref:System.Net.Http>je nutné přidat odkaz pro .  
  
 Projekt si můžete stáhnout z [ukázky aplikace Async: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea).  
  
```vb  
' Add an Imports directive and a reference for System.Net.Http.  
Imports System.Net.Http  
  
' Add the following Imports directive for System.Threading.  
Imports System.Threading  
  
Class MainWindow  
  
    ' Declare a System.Threading.CancellationTokenSource.  
    Dim cts As CancellationTokenSource  
  
    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
  
        ' Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
  
        resultsTextBox.Clear()  
  
        Try  
            Await AccessTheWebAsync(cts.Token)  
            resultsTextBox.Text &= vbCrLf & "Downloads complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf  
        End Try  
  
        ' Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' You can still include a Cancel button if you want to.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' Provide a parameter for the CancellationToken.  
    ' Change the return type to Task because the method has no return statement.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
        Dim client As HttpClient = New HttpClient()  
  
        ' Call SetUpURLList to make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToList to execute the query and start the download tasks.
        Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
  
        ' ***Add a loop to process the tasks one at a time until none remain.  
        While downloadTasks.Count > 0  
            ' ***Identify the first task that completes.  
            Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
            ' ***Remove the selected task from the list so that you don't  
            ' process it more than once.  
            downloadTasks.Remove(firstFinishedTask)  
  
            ' ***Await the first completed task and display the results.  
            Dim length = Await firstFinishedTask  
            resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        End While  
  
    End Function  
  
    ' Bundle the processing steps for a website into one async method.  
    Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        Return urlContents.Length  
    End Function  
  
    ' Add a method that creates a list of web addresses.  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "https://msdn.microsoft.com",  
                "https://msdn.microsoft.com/library/hh290138.aspx",  
                "https://msdn.microsoft.com/library/hh290140.aspx",  
                "https://msdn.microsoft.com/library/dd470362.aspx",  
                "https://msdn.microsoft.com/library/aa578028.aspx",  
                "https://msdn.microsoft.com/library/ms404677.aspx",  
                "https://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
    End Function  
  
End Class  
  
' Sample output:  
  
' Length of the download:  226093  
' Length of the download:  412588  
' Length of the download:  175490  
' Length of the download:  204890  
' Length of the download:  158855  
' Length of the download:  145790  
' Length of the download:  44908  
' Downloads complete.  
```  
  
## <a name="see-also"></a>Viz také

- <xref:System.Threading.Tasks.Task.WhenAny%2A>
- [Jemné doladění asynchronní aplikace (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)
- [Asynchronní programování s asynchronní a čeká (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)
- [Asynchronní ukázka: Jemné doladění aplikace](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)
