---
title: Datenbindung in einem Windows Presentation Foundation-Client
ms.date: 03/30/2017
ms.assetid: bb8c8293-5973-4aef-9b07-afeff5d3293c
ms.openlocfilehash: 225bdedb67e218092ff3369d4fe742c4fc897fc6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33502545"
---
# <a name="data-binding-in-a-windows-presentation-foundation-client"></a>Datenbindung in einem Windows Presentation Foundation-Client
In diesem Beispiel wird die Verwendung der Datenbindung in einem Windows Presentation Foundation (WPF)-Client veranschaulicht. Das Beispiel verwendet einen Windows Communication Foundation (WCF)-Dienst, der ein Array von Alben zurückzugebenden an den Client nach dem Zufallsprinzip generiert. Jedes Album hat einen Namen, einen Preis und eine Liste von Albumtiteln. Die Albumtitel haben einen Namen und eine Dauer. Die Informationen, die vom Dienst zurückgegeben wird, wird automatisch für die Benutzeroberfläche (UI) von der Windows Presentation Foundation (WPF)-Client bereitgestellt gebunden.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Durch die Datenbindung kann eine Datenquelle automatisch an eine Benutzeroberfläche gebunden werden. Dadurch wird das Programmiermodell vereinfacht, da Sie nicht jedes Element der Benutzeroberfläche programmgesteuert mit den Daten aus einem Datenobjekt oder einem Array von Datenobjekten aktualisieren müssen. Sie können ein Objekt an ein Benutzeroberflächenelement oder ein Array an ein Steuerelement mit mehreren Eingaben binden, beispielsweise `ListBox`. Im folgenden Codebeispiel wird das Binden von Daten an den `DataContext` eines Benutzeroberflächenelements veranschaulicht.  
  
```  
// Event handler executed when call is complete  
void client_GetAlbumListCompleted(object sender, GetAlbumListCompletedEventArgs e)  
{  
    // This is on the UI thread, myPanel can be accessed directly  
    myPanel.DataContext = e.Result;   
}  
```  
  
 Im obigen Beispiel wird der `DataContext` für das `grid`-Layoutelement `myPanel` auf die von der `GetAlbumList`-Methode zurückgegebenen Daten festgelegt. Durch den `DataContext` können Elemente Informationen zu der für die Bindung verwendete Datenquelle sowie andere Merkmale der Bindung (beispielsweise den Pfad) von den übergeordneten Elementen erben. Die Codezeile muss jedes Mal ausgeführt werden, wenn die Daten auf dem Server aktualisiert werden. Sie wird beispielsweise ausgeführt, wenn das Fenster initialisiert wird und wenn ein neues Album hinzugefügt wird.  
  
 Im folgenden XAML-Beispielcode wird `ListBox` von `ItemsSource="{Binding }"` angegeben.  
  
```xml  
<ListBox   
          ItemTemplate="{StaticResource AlbumStyle}"  
          ItemsSource="{Binding }"   
          IsSynchronizedWithCurrentItem="true" />  
```  
  
 Dies gibt an, dass die an das Benutzeroberflächenelement der obersten Ebene gebundenen Daten auch an dieses Steuerelement gebunden werden (d.&#160;h. an das Array von Alben). Außerdem gibt `ItemTemplate="{StaticResource AlbumStyle}"` die Datenvorlage an, die in `ListBox` für jedes Element verwendet werden soll. Sie können auch Datenvorlagen definieren, um anzugeben, wie die Daten formatiert werden sollen. Diese Datenvorlagen können für andere Benutzeroberflächenelemente in der Anwendung wiederverwendet werden. Der Vorteil liegt darin, dass die Datenvorlage an einem Ort definiert und verwaltet wird.  
  
 Die `AlbumStyle`-Datenvorlage definiert ein Raster mit zwei nebeneinanderliegenden `TextBlock`s. In einem wird der Name des Albums angegeben, im anderen die Anzahl der Titel auf dem Album.  
  
```xaml  
<DataTemplate x:Key="AlbumStyle">  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="260" />  
            <ColumnDefinition Width="60" />  
        </Grid.ColumnDefinitions>  
        <TextBlock Grid.Column="0" TextContent="{Binding Path=Title}" />  
        <TextBlock Grid.Column="1" TextContent="{Binding Path=Tracks#.Count}" HorizontalAlignment="Right" />  
    </Grid>  
</DataTemplate>  
```  
  
 Mit dem folgenden XAML-Code wird eine zweite `ListBox` erstellt.  
  
```xaml  
<ListBox Grid.Row="2"   
            Grid.ColumnSpan="2"   
            ItemTemplate="{StaticResource TrackStyle}"  
            ItemsSource="{Binding Path=Tracks}" />  
```  
  
 Im Code wird ein Pfad für `ItemsSource` angegeben. Damit wird angegeben, dass die an dieses Steuerelement gebundenen Daten keine Daten der obersten Ebene, sondern eine Eigenschaft der Daten der obersten Ebene namens `Tracks` sind. Diese Eigenschaft stellt das Array der im Album enthaltenen Titel dar. Außerdem wird eine weitere `DataTemplate` namens `TrackStyle` angegeben. Das Layout der `TrackStyle`-Vorlage entspricht weitgehend dem der `AlbumStyle`-Vorlage, die `TextBlock`s sind jedoch an andere Eigenschaften gebunden. Dies liegt daran, dass die beiden Vorlagen mit unterschiedlichen Datenobjekten verwendet werden.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Setupprozedur für die Windows Communication Foundation-Beispiele zum einmaligen](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Um die C#- oder Visual Basic .NET-Edition der Projektmappe zu erstellen, befolgen Sie die unter [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)aufgeführten Anweisungen.  
  
3.  Um das Beispiel in einer einzelnen oder computerübergreifenden Konfiguration ausführen möchten, folgen Sie den Anweisungen [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WPFDataBinding`  
  
## <a name="see-also"></a>Siehe auch
