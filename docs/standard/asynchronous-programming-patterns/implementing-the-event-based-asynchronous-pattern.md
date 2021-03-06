---
title: Implementieren des ereignisbasierten asynchronen Entwurfsmusters
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
ms.openlocfilehash: 89de0690c0f9788120f7805b0b63c22ecafa6b9c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33577358"
---
# <a name="implementing-the-event-based-asynchronous-pattern"></a>Implementieren des ereignisbasierten asynchronen Entwurfsmusters
Wenn Sie eine Klasse mit Vorgängen schreiben, die nennenswerte Verzögerungen verursachen können, sollten Sie die Klasse mit einer asynchronen Funktionalität ausstatten, indem Sie das ereignisbasierte asynchrone Muster implementieren. Informationen zu diesem Muster finden Sie unter [Übersicht über ereignisbasierte asynchrone Muster](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  
  
 Das ereignisbasierte asynchrone Muster bietet eine standardisierte Möglichkeit zum Verpacken einer Klasse, die asynchrone Features hat. Ist eine Klasse mit Hilfsklassen wie <xref:System.ComponentModel.AsyncOperationManager> implementiert, funktioniert sie unter jedem beliebigen Anwendungsmodell ordnungsgemäß, einschließlich [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], Konsolenanwendungen und Windows Forms-Anwendungen.  
  
 Ein Beispiel, in dem das ereignisbasierte asynchrone Muster implementiert ist, finden Sie unter [Gewusst wie: Implementieren einer Komponente, die das ereignisbasierte asynchrone Muster unterstützt](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
 Für einfache asynchrone Vorgänge ist möglicherweise die Komponente <xref:System.ComponentModel.BackgroundWorker> gut geeignet. Weitere Informationen zu <xref:System.ComponentModel.BackgroundWorker> finden Sie unter [Gewusst wie: Ausführen eines Vorgangs im Hintergrund](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md).  
  
 In der folgenden Liste sind die Features des ereignisbasierten asynchronen Musters aufgeführt, die in diesem Thema beschrieben sind.  
  
-   Gelegenheiten für Implementieren des ereignisbasierten asynchronen Entwurfsmusters  
  
-   Benennen von asynchronen Methoden  
  
-   Optionales Unterstützen von Abbruch  
  
-   Optionales Unterstützen der „IsBusy“-Eigenschaft  
  
-   Optionales Unterstützen von Statusberichterstellung  
  
-   Optionales Unterstützen der Rückgabe von inkrementellen Ergebnissen  
  
-   Verarbeiten von „out“- und „ref“-Parametern in Methoden  
  
## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a>Gelegenheiten für Implementieren des ereignisbasierten asynchronen Entwurfsmusters  
 Implementieren des ereignisbasierten asynchronen Entwurfsmusters bietet sich an, wenn Folgendes zutrifft:  
  
-   Clients einer Klasse benötigen keine <xref:System.Threading.WaitHandle>- und <xref:System.IAsyncResult>-Objekte, die für asynchrone Vorgänge verfügbar sind, d.h. Abfragen und <xref:System.Threading.WaitHandle.WaitAll%2A> oder <xref:System.Threading.WaitHandle.WaitAny%2A> müssen vom Client erzeugt werden.  
  
-   Asynchrone Vorgänge sollen vom Client mit dem vertrauten Ereignis/Delegat-Modell verwaltet werden.  
  
 Jeder Vorgang ist ein Kandidat für eine asynchrone Implementierung, aber ein Vorgang, für den Sie lange Wartezeiten erwarten, sollte auf alle Fälle berücksichtigt werden. Besonders geeignet sind Vorgänge, in denen Clients eine Methode aufrufen und bei Abschluss benachrichtigt werden, ohne dass weiteres Eingreifen erforderlich ist. Geeignet sind außerdem Vorgänge, die durchgängig ausgeführt werden und dabei Clients regelmäßig über Fortschritte, inkrementelle Ergebnisse oder Zustandsänderungen benachrichtigen.  
  
 Weitere Informationen dazu, wie entschieden werden soll, ob das ereignisbasierte asynchrone Muster unterstützt werden sollte, finden Sie unter [Gründe für das Implementieren des ereignisbasierten asynchronen Musters](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md).  
  
## <a name="naming-asynchronous-methods"></a>Benennen von asynchronen Methoden  
 Definieren Sie für jede synchrone Methode *MethodName*, für die Sie ein asynchrones Gegenstück bereitstellen möchten, Folgendes:  
  
 Definieren Sie eine *MethodName***Async**-Methode, die:  
  
-   Gibt `void`zurück.  
  
-   Dieselben Parameter hat wie die *MethodName*-Methode.  
  
-   Mehrere Aufrufe akzeptiert.  
  
 Definieren Sie optional eine *MethodName***Async**-Überladung, die mit *MethodName***Async** identisch ist, aber einen zusätzlichen Objektparameter namens `userState` hat. Dies sollten Sie tun, wenn Sie mehrere gleichzeitige Aufrufe der Methode verwalten möchten. In diesem Fall wird der `userState`-Wert an alle Ereignishandler zurückgegeben, um die Aufrufe der Methode zu unterscheiden. Diese Vorgehensweise bietet sich auch an, wenn Sie einfach einen Platz haben möchten, in dem der Benutzerstatus für spätere Abrufe gespeichert werden soll.  
  
 Definieren Sie für jede einzelne *MethodName***Async**-Methodensignatur:  
  
1.  Das folgende Ereignis in derselben Klasse wie die Methode:  
  
    ```vb  
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler  
    ```  
  
    ```csharp  
    public event MethodNameCompletedEventHandler MethodNameCompleted;  
    ```  
  
2.  Den folgenden Delegaten und <xref:System.ComponentModel.AsyncCompletedEventArgs>. Diese sind wahrscheinlich außerhalb der Klasse selbst, aber im selben Namespace definiert.  
  
    ```vb  
    Public Delegate Sub MethodNameCompletedEventHandler( _  
        ByVal sender As Object, _  
        ByVal e As MethodNameCompletedEventArgs)  
  
    Public Class MethodNameCompletedEventArgs  
        Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As MyReturnType  
    End Property  
    ```  
  
    ```csharp  
    public delegate void MethodNameCompletedEventHandler(object sender,   
        MethodNameCompletedEventArgs e);  
  
    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
    {  
        public MyReturnType Result { get; }  
    }  
    ```  
  
    -   Stellen Sie sicher, dass die *MethodName***CompletedEventArgs**-Klasse ihre Elemente als schreibgeschützte Eigenschaften verfügbar macht, und nicht als Felder, weil Felder Datenbindungen verhindern.  
  
    -   Definieren Sie keine <xref:System.ComponentModel.AsyncCompletedEventArgs>-abgeleitete Klassen für Methoden, die keine Ergebnisse erzeugen. Verwenden Sie einfach eine Instanz von <xref:System.ComponentModel.AsyncCompletedEventArgs> selbst.  
  
        > [!NOTE]
        >  Es ist durchaus akzeptabel, wenn machbar und angemessen, Delegaten und <xref:System.ComponentModel.AsyncCompletedEventArgs>-Typen wiederzuverwenden. In diesem Fall ist die Benennung nicht so konsistent wie mit dem Methodennamen, da ein bestimmter Delegat und <xref:System.ComponentModel.AsyncCompletedEventArgs> nicht an eine einzelne Methode gebunden sind.  
  
## <a name="optionally-support-cancellation"></a>Optionales Unterstützen von Abbruch  
 Wenn Ihre Klasse das Abbrechen von asynchronen Vorgängen unterstützt, sollte Abbruch so für den Client verfügbar gemacht werden, wie dies weiter unten beschrieben ist. Es gibt zwei Entscheidungspunkte, die erreicht sein müssen, bevor Abbruchunterstützung definiert wird:  
  
-   Hat die Klasse, einschließlich zukünftiger zu erwartender Erweiterungen, nur einen asynchronen Vorgang, der Abbruch unterstützt?  
  
-   Können die asynchronen Vorgänge, die Abbruch unterstützen, mehrere ausstehende Vorgänge unterstützen? Das heißt, hat die *MethodName***Async**-Methode den `userState`-Parameter akzeptiert und lässt sie mehrere Aufrufe zu, bevor sie für jeden auf dessen Beendigung wartet?  
  
 Entscheiden Sie anhand der Antworten auf die beiden Fragen in der folgenden Tabelle, welche Signatur für die Abbruchmethode zu verwenden ist.  
  
### <a name="visual-basic"></a>Visual Basic  
  
||Mehrere gleichzeitige Vorgänge unterstützt|Nur immer jeweils ein Vorgang|  
|------|------------------------------------------------|----------------------------------|  
|Ein asynchroner Vorgang in der gesamten Klasse|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|  
|Mehrere asynchrone Vorgänge in der Klasse|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|  
  
### <a name="c"></a>C#  
  
||Mehrere gleichzeitige Vorgänge unterstützt|Nur immer jeweils ein Vorgang|  
|------|------------------------------------------------|----------------------------------|  
|Ein asynchroner Vorgang in der gesamten Klasse|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|  
|Mehrere asynchrone Vorgänge in der Klasse|`void CancelAsync(object userState);`|`void CancelAsync();`|  
  
 Wenn Sie die `CancelAsync(object userState)`-Methode definieren, müssen Clients bei der Auswahl ihrer Statuswerte vorsichtig sein, damit sie in der Lage sind, zwischen allen für das Objekt aufgerufenen asynchronen Methoden, nicht nur zwischen allen Aufrufen einer einzigen asynchronen Methode zu unterscheiden.  
  
 Es wurde entschieden, die Version mit einzelnem asynchronen Vorgang als *MethodName***AsyncCancel** zu benennen, um die Methode in einer Entwurfsumgebung wie Visual Studios IntelliSense einfacher erkennen zu können. Dadurch werden die zusammengehörenden Member gruppiert und lassen sich von anderen Membern unterscheiden, die nichts mit der asynchronen Funktionalität zu tun haben. Wenn Sie davon ausgehen, dass in späteren Versionen weitere asynchrone Vorgänge hinzugefügt werden, sollten Sie `CancelAsync` definieren.  
  
 Definieren Sie nicht mehrere Methoden aus der obigen Tabelle in derselben Klasse. Dies ist nicht sinnvoll oder führt dazu, dass in der Klassenschnittstelle unnötig viele Methoden bereitgestellt werden.  
  
 Diese Methoden führen üblicherweise sofort eine Rückkehr aus, und der Vorgang wird möglicherweise tatsächlich abgebrochen (oder nicht). Im Ereignishandler für das *MethodName***Completed**-Ereignis enthält das *MethodName***CompletedEventArgs**-Objekt ein `Cancelled`-Feld, anhand dessen Clients ermitteln können, ob der Abbruch aufgetreten ist.  
  
 Halten Sie sich an die Abbruchsemantik, die unter [Bewährte Verfahrensweisen für das Implementieren des ereignisbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md) beschrieben ist.  
  
## <a name="optionally-support-the-isbusy-property"></a>Optionales Unterstützen der „IsBusy“-Eigenschaft  
 Unterstützt die Klasse nicht mehrere gleichzeitige Aufrufe, sollten Sie eine `IsBusy`-Eigenschaft verfügbar machen. Dies ermöglicht Entwicklern, zu bestimmen, ob eine *MethodName**Async**-Methode ausgeführt wird, ohne eine Ausnahme von der *MethodName***Async**-Methode abzufangen.  
  
 Halten Sie sich an die `IsBusy`-Semantik, die unter [Bewährte Verfahrensweisen für das Implementieren des ereignisbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md) beschrieben ist.  
  
## <a name="optionally-provide-support-for-progress-reporting"></a>Optionales Unterstützen von Statusberichterstellung  
 Es ist häufig wünschenswert, dass ein asynchroner Vorgang während seiner Ausführung den Status mitteilt. Das ereignisbasierte asynchrone Muster stellt eine Richtlinie dafür bereit.  
  
-   Definieren Sie optional ein Ereignis, das vom asynchronen Vorgang ausgelöst und im entsprechenden Thread aufgerufen wird. Das <xref:System.ComponentModel.ProgressChangedEventArgs>-Objekt enthält eine Statusanzeige mit Ganzzahlwert, der zwischen 0 und 100 liegt.  
  
-   Benennen Sie dieses Ereignis wie folgt:  
  
    -   `ProgressChanged`, wenn die Klasse mehrere asynchrone Vorgänge hat (oder vermutlich so erweitert wird, dass sie in zukünftigen Versionen mehrere asynchrone Vorgänge haben wird)  
  
    -   *MethodName***ProgressChanged**, wenn die Klasse einen einzelnen asynchronen Vorgang hat.  
  
     Diese Benennungskonvention entspricht derjenigen für die Abbruchmethode, wie im Abschnitt „Optionales Unterstützen von Abbruch“ beschrieben.  
  
 Dieses Ereignis sollte die <xref:System.ComponentModel.ProgressChangedEventHandler>-Signatur des Delegaten und die <xref:System.ComponentModel.ProgressChangedEventArgs>-Klasse verwenden. Für den Fall, dass eine bereichsspezifischere Statusanzeige bereitgestellt werden kann (beispielsweise gelesene Bytes und die Gesamtanzahl der Bytes für einen Downloadvorgang), sollten Sie eine abgeleitete Klasse von <xref:System.ComponentModel.ProgressChangedEventArgs> definieren.  
  
 Beachten Sie, dass es nur ein `ProgressChanged`- oder *MethodName***ProgressChanged**-Ereignis für die Klasse gibt, unabhängig davon, wie viele asynchrone Methoden sie unterstützt. Für Clients wird vorausgesetzt, dass sie das `userState`-Objekt verwenden, das an die *MethodName***Async**-Methoden übergeben wird, um zwischen Statusupdates bei mehreren gleichzeitigen Vorgängen zu unterscheiden.  
  
 Es kann Situationen geben, in denen mehrere Vorgänge einen Status unterstützen und jeder Vorgang einen anderen Indikator für den Status zurückgibt. In diesem Fall ist ein einzelnes `ProgressChanged`-Ereignis nicht geeignet, und Sie sollten Unterstützung für mehrere `ProgressChanged`-Ereignisse erwägen. Verwenden Sie für diesen Fall das Benennungsmuster *MethodName***ProgressChanged** für jede *MethodName***Async**-Methode.  
  
 Halten Sie sich an die Statusberichte-Semantik, die unter [Bewährte Verfahrensweisen für das Implementieren des ereignisbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md) beschrieben ist.  
  
## <a name="optionally-provide-support-for-returning-incremental-results"></a>Optionales Unterstützen der Rückgabe von inkrementellen Ergebnissen  
 Möglicherweise gibt ein asynchroner Vorgang vor seiner Beendigung inkrementelle Ergebnisse zurück. Zur Unterstützung dieses Szenarios gibt es eine Reihe von Optionen, die verwendet werden können. Es folgen einige Beispiele.  
  
### <a name="single-operation-class"></a>Klasse mit einem einzigen Vorgang  
 Unterstützt die Klasse nur einen einzigen asynchronen Vorgang, und kann dieser Vorgang inkrementelle Ergebnisse zurückgeben, dann gehen Sie wie folgt vor:  
  
-   Erweitern Sie den <xref:System.ComponentModel.ProgressChangedEventArgs>-Typ, damit er die Daten eines inkrementellen Ergebnisses aufnehmen kann, und definieren Sie ein *MethodName***ProgressChanged**-Ereignis mit diesen erweiterten Daten.  
  
-   Lösen Sie dieses *MethodName***ProgressChanged**-Ereignis aus, sobald ein zu berichtendes inkrementelles Ergebnis vorliegt.  
  
 Diese Lösung ist speziell für eine Klasse mit einzelnem asynchronen Vorgang anwendbar, weil es kein Problem damit gibt, dass dasselbe auftretende Ereignis inkrementelle Ergebnisse für „alle Vorgänge“ zurückgibt, denn das *MethodName***ProgressChanged**-Ereignis erledigt dies.  
  
### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a>Klasse mit mehreren Vorgängen und homogenen inkrementellen Ergebnissen  
 In diesem Fall unterstützt die Klasse mehrere asynchrone Methoden, von denen jede inkrementelle Ergebnisse zurückgeben kann, wobei diese inkrementellen Ergebnisse alle denselben Datentyp haben.  
  
 Gehen Sie entsprechend dem oben beschriebenen Modell für Klassen mit einzelnem Vorgang vor, da die gleiche <xref:System.EventArgs>-Struktur für alle inkrementellen Ergebnisse funktioniert. Definieren Sie ein `ProgressChanged`-Ereignis anstelle eines *MethodName***ProgressChanged**-Ereignisses, weil es für mehrere asynchrone Methoden gilt.  
  
### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a>Klasse mit mehreren Vorgängen und heterogenen inkrementellen Ergebnissen  
 Wenn die Klasse mehrere asynchrone Methoden unterstützt, wobei jede Methode Daten eines anderen Typs zurückgibt, sollten Sie wie folgt vorgehen:  
  
-   Trennen Sie die Mitteilungen über inkrementelle Ergebnisse von den Statusmitteilungen.  
  
-   Definieren Sie für jede asynchrone Methode ein eigenes *MethodName***ProgressChanged**-Ereignis mit entsprechenden <xref:System.EventArgs>, um die Daten eines inkrementellen Ergebnisses dieser Methode zu verarbeiten.  
  
 Rufen Sie diesen Ereignishandler für den entsprechenden Thread auf, wie dies unter [Bewährte Verfahrensweisen für das Implementieren des ereignisbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md) beschrieben ist.  
  
## <a name="handling-out-and-ref-parameters-in-methods"></a>Verarbeiten von „out“- und „ref“-Parametern in Methoden  
 Grundsätzlich wird davon abgeraten, `out` und `ref` in .NET Framework zu verwenden. Sind diese aber vorhanden, sollten die folgenden Regeln beachtet werden:  
  
 Angenommen, es gibt die synchrone Methode *MethodName*:  
  
-   `out`-Parameter für *MethodName* dürfen keine Bestandteile von *MethodName***Async** sein. Stattdessen müssen sie Bestandteile von *MethodName***CompletedEventArgs** mit denselben Namen wie ihre Parametergegenstücke in *MethodName* sein (es sei denn, es gibt geeignetere Namen).  
  
-   `ref`-Parameter für *MethodName* müssen als Bestandteile von *MethodName***Async** und als Bestandteile von *MethodName***CompletedEventArgs** mit denselben Namen wie ihre Parametergegenstücke in *MethodName* vorhanden sein (es sei denn, es gibt geeignetere Namen).  
  
 Angenommen, dies liegt vor:  
  
```vb  
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer  
```  
  
```csharp  
public int MethodName(string arg1, ref string arg2, out string arg3);  
```  
  
 Die asynchrone Methode und die zugehörige <xref:System.ComponentModel.AsyncCompletedEventArgs>-Klasse würde wie folgt aussehen:  
  
```vb  
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)  
  
Public Class MethodNameCompletedEventArgs  
    Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As Integer   
    End Property  
    Public ReadOnly Property Arg2() As String   
    End Property  
    Public ReadOnly Property Arg3() As String   
    End Property  
End Class  
```  
  
```csharp  
public void MethodNameAsync(string arg1, string arg2);  
  
public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
{  
    public int Result { get; };  
    public string Arg2 { get; };  
    public string Arg3 { get; };  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ComponentModel.ProgressChangedEventArgs>  
 <xref:System.ComponentModel.AsyncCompletedEventArgs>  
 [Gewusst wie: Implementieren einer Komponente, die das ereignisbasierte asynchrone Muster unterstützt](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)  
 [Gewusst wie: Ausführen eines Vorgangs im Hintergrund](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
 [Vorgehensweise: Implementieren eines Formulars, das eine Hintergrundoperation verwendet](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)  
 [Deciding When to Implement the Event-based Asynchronous Pattern (Gründe für das Implementieren des ereignisbasierten asynchronen Musters)](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 [Multithreadprogrammierung mit dem ereignisbasierten asynchronen Muster](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)  
 [Bewährte Verfahrensweisen für das Implementieren des ereignisbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
