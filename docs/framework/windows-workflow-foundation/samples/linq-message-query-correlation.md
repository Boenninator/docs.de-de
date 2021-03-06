---
title: LINQ-Meldungsabfragekorrelation
ms.date: 03/30/2017
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
ms.openlocfilehash: 5b215764f7e02f07873f63872f4ac8c3fcaffbcc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33515842"
---
# <a name="linq-message-query-correlation"></a>LINQ-Meldungsabfragekorrelation
Dieses Beispiel veranschaulicht, wie die inhaltsbasierte Korrelation mithilfe einer benutzerdefinierten <xref:System.ServiceModel.Dispatcher.MessageQuery>-Implementierung im Gegensatz zu der vom System bereitgestellten <xref:System.ServiceModel.XPathMessageQuery> erfolgt.  
  
## <a name="demonstrates"></a>Veranschaulicht  
 Benutzerdefinierte <xref:System.ServiceModel.Dispatcher.MessageQuery>, inhaltsbasierte Korrelation.  
  
## <a name="discussion"></a>Diskussion  
 In diesem Beispiel wird veranschaulicht, wie zum Zwecke der Korrelation eine Erweiterung von der <xref:System.ServiceModel.Dispatcher.MessageQuery>-Basisklasse durchgeführt wird. Die benutzerdefinierte Implementierung, `LinqMessageQuery`, ermöglicht es Benutzern, einen XName anzugeben, der innerhalb der Meldung mit XLinq gesucht werden soll. Die von der Abfrage abgerufenen Daten werden verwendet, um den Korrelationsschlüssel zu bilden, mit dem Meldungen an die entsprechende Workflowinstanz weitergeleitet werden.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Dieses Beispiel macht einen Workflowdienst mithilfe von HTTP-Endpunkten verfügbar. Ausführung dieser Beispiele, die richtige URL-ACLs hinzugefügt werden muss (finden Sie unter [Configuring HTTP and HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353) Details), durch Ausführen von Visual Studio als Administrator oder durch Ausführen des folgenden Befehls an einer Eingabeaufforderung mit erhöhten Rechten auf die entsprechenden ACLs hinzugefügt. Stellen Sie sicher, dass die Domäne und der Benutzername ersetzt werden.  
  
    ```  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2.  Sobald die URL-ACLs hinzugefügt wurden, führen Sie die folgenden Schritte aus.  
  
    1.  Erstellen Sie die Projektmappe.  
  
    2.  Mehrere Startprojekte festlegen, indem Sie die Projektmappe mit der rechten Maustaste und auswählen **Startprojekte festlegen**. Hinzufügen **Service** und **Client** (in dieser Reihenfolge) als mehrere Startprojekte.  
  
    3.  Führen Sie die Anwendung aus. Die Clientkonsole zeigt einen Workflow, der eine Bestellung sendet und die Bestell-ID empfängt und dann daraufhin den Auftrag bestätigt. Das Fenster "Dienst" zeigt die Anforderungen, die verarbeitet werden.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, fahren Sie mit [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) aller Windows Communication Foundation (WCF) herunterladen und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`
