---
title: Entwerfen einer an Microservice orientierten Anwendung
description: .NET-Microservicesarchitektur für .NET-Containeranwendungen | Entwerfen einer an Microservice orientierten Anwendung
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 6cbe4512c8ed89540599d1257046bd080b464165
ms.sourcegitcommit: 979597cd8055534b63d2c6ee8322938a27d0c87b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2018
ms.locfileid: "37105958"
---
# <a name="designing-a-microservice-oriented-application"></a>Entwerfen einer an Microservice orientierten Anwendung

Dieser Abschnitt konzentriert sich auf das Entwickeln einer hypothetischen serverseitigen Unternehmensanwendung.

## <a name="application-specifications"></a>Anwendungsspezifikationen

Die hypothetische Anwendung verarbeitet Anforderungen, indem sie Geschäftslogik ausführt, auf Datenbanken zugreift und anschließend HTML-, JSON- oder XML-Antworten zurückgibt. Die Anwendung soll eine Vielzahl von Clients unterstützen, einschließlich Desktopbrowsern, die Einzelseitenanwendungen (Single Page Applications, SPAs) ausführen, herkömmlichen Web-Apps, mobilen Web-Apps und nativen Web-Apps. Die Anwendung könnte auch eine API verfügbar machen, die von Drittanbietern verwendet werden kann. Sie sollte zudem in der Lage sein, ihre Microservices oder externen Anwendungen asynchron zu integrieren, sodass dieser Ansatz im Fall von Teilfehlern für eine bessere Stabilität der Microservices sorgt.

Die Anwendung soll aus den folgenden Typen von Komponenten bestehen:

-   Präsentationskomponenten. Diese sind für die Verarbeitung der Benutzeroberfläche sowie die Verwendung von Remotediensten verantwortlich.

-   Domänen- oder Geschäftslogik. Dabei handelt es sich um die Domänenlogik der Anwendung.

-   Datenbankzugriffslogik. Diese besteht aus Datenzugriffskomponenten, die für den Zugriff auf Datenbanken verantwortlich sind (SQL oder NoSQL).

-   Anwendungsintegrationslogik. Diese beinhaltet einen Nachrichtenkanal, der hauptsächlich auf Nachrichtenbroker basiert.

Die Anwendung erfordert eine hohe Skalierbarkeit, wobei sie den vertikalen Subsystemen ermöglichen muss, unabhängig horizontal hochzuskalieren, da einige Subsysteme eine höhere Skalierbarkeit erfordern als andere.

Die Anwendung muss in mehreren Infrastrukturumgebungen (mehreren öffentlichen Clouds und lokalen Umgebungen) bereitgestellt werden können und idealerweise plattformübergreifend sein, damit ein Verschieben von Linux nach Windows (oder umgekehrt) einfach möglich ist.

## <a name="development-team-context"></a>Kontext des Entwicklungsteams

Für den Entwicklungsprozess der Anwendung wird außerdem Folgendes angenommen:

-   Sie verfügen über mehrere Entwicklungsteams, die sich auf unterschiedliche Geschäftsbereiche der Anwendung konzentrieren.

-   Neue Teammitglieder müssen sich schnell einarbeiten, und die Anwendung muss einfach zu verstehen und zu bearbeiten sein.

-   Die Anwendung wird langfristig weiterentwickelt und weist Geschäftsregeln, die stetig verändert werden.

-   Sie benötigen eine gute, langfristige Wartbarkeit, d.h. Flexibilität beim Implementieren neuer Änderungen in der Zukunft, wobei es möglich sein muss, dass mehrere Subsysteme ohne größeren Einfluss auf die anderen Subsysteme aktualisiert werden.

-   Sie möchten Continuous Integration und Continuous Deployment der Anwendung ausüben.

-   Sie möchten bei der Weiterentwicklung Ihrer Anwendung von neuen Technologien (Frameworks, Programmiersprachen usw.) profitieren. Sie möchten bei der Umstellung auf neue Technologien keine vollständigen Migrationen der Anwendung durchführen, da dies zu hohen Kosten führen würde und sich negativ auf die Vorhersagbarkeit und die Stabilität der Anwendung auswirken würde.

## <a name="choosing-an-architecture"></a>Auswählen einer Architektur

Welche Architektur sollte für die Anwendungsbereitstellung ausgewählt werden? Im Hinblick auf die Spezifikationen für die Anwendung sowie auf den Entwicklungskontext wird dringend empfohlen, dass Sie die Anwendung zur Architektur in Form von zusammenarbeitenden Microservices und Containern (wobei es sich bei einem Microservice um einen Container handelt) in unabhängige Subsysteme zerlegen.

Bei diesem Ansatz implementiert jeder Dienst (Container) mehrere zusammenhängende und eng verwandte Funktionen. Beispielsweise kann eine Anwendung aus Diensten wie dem Katalogdienst, dem Bestelldienst, dem Warenkorbdienst, dem Benutzerprofildienst bestehen.

Microservices kommunizieren mithilfe von Protokollen wie HTTP (REST), nach Möglichkeit jedoch auch asynchron (z.B. über AMQP), insbesondere bei der Weitergabe von Updates bei Integrationsereignissen.

Microservices werden als Container entwickelt und bereitgestellt, die nicht voneinander abhängig sind. Dies bedeutet, dass ein Entwicklungsteam einen bestimmten Microservice ohne Auswirkungen auf andere Subsysteme entwickeln und bereitstellen kann.

Jeder Microservice verfügt über seine eigene Datenbank, wodurch er vollständig von anderen Microservices entkoppelt werden kann. Wenn nötig, kann die Konsistenz zwischen Datenbanken verschiedener Microservices mithilfe von Integrationsereignissen auf Anwendungsebene (über einen logischen Ereignisbus) erreicht werden, wie bei der Command and Query Responsibility Segregation (CQRS). Daher müssen die Geschäftseinschränkungen eine mögliche Konsistenz zwischen den verschiedenen Microservices und verwandten Datenbanken umfassen.

### <a name="eshoponcontainers-a-reference-application-for-net-core-and-microservices-deployed-using-containers"></a>eShopOnContainers: Eine Referenzanwendung für .NET Core und Microservices, die mithilfe von Containern bereitgestellt wurde

Damit Sie sich auf die Architektur und die Technologien konzentrieren können, anstatt über eine hypothetische Geschäftsdomäne nachzudenken, mit der Sie sich möglicherweise nicht auskennen, wurde eine bekannte Geschäftsdomäne ausgewählt, nämlich eine vereinfachte E-Commerce-Anwendung (Onlineshop), die einen Katalog von Produkten darstellt, Bestellungen von Kunden entgegennimmt, den Lagerbestand überprüft und weitere Geschäftsfunktionen übernimmt. Dieser containerbasierte Anwendungsquellcode ist im GitHub-Repository [eShopOnContainers](http://aka.ms/MicroservicesArchitecture) verfügbar.

Die Anwendung besteht aus mehreren Subsystemen, einschließlich mehrerer Front-Ends der Shop-Benutzeroberfläche (einer Webanwendung und einer nativen mobilen App), sowie den Back-End-Microservices und -Containern für alle erforderlichen serverseitigen Vorgänge. Abbildung 8-1 zeigt die Architektur der Referenzanwendung.

![](./media/image1.png)

**Abbildung 8-1**. Die Referenzanwendung eShopOnContainers zeigt eine direkte Client-zu-Microservice-Kommunikation und den Ereignisbus.

**Hostumgebung**. In Abbildung 8-1 werden mehrere Container angezeigt, die innerhalb eines einzelnen Docker-Hosts bereitgestellt wurden. Dies wäre bei der Bereitstellung auf einem einzelnen Docker-Host mit dem Befehl „docker-compose up“ der Fall. Wenn Sie jedoch einen Orchestrator- oder Containercluster verwenden, könnte jeder Container auf einem anderen Host(knoten) ausgeführt werden, und jeder Knoten könnte, wie bereits im Abschnitt zur Architektur weiter oben beschrieben, jede beliebige Anzahl von Containern ausführen.

**Kommunikationsarchitektur.** Die Anwendung eShopOnContainers verwendet zwei Kommunikationstypen, abhängig von der Art der funktionalen Aktion (Abfragen im Vergleich zu Updates und Transaktionen):

-   Direkte Kommunikation zwischen Client und Microservice. Diese wird für Abfragen und bei der Annahme von Update- oder Transaktionsbefehlen von den Client-Apps verwendet.

-   Asynchrone, ereignisbasierte Kommunikation. Diese erfolgt über einen Ereignisbus und dient zur Verteilung von Updates zwischen Microservices oder zur Integration in externen Anwendungen. Der Ereignisbus kann mit jeder beliebigen Infrastrukturtechnologie des Nachrichtenbrokers wie RabbitMQ oder mithilfe von Service Bussen höherer Ebene wie Azure Service Bus, NServiceBus, MassTransit oder Brighter implementiert werden.

Die Anwendung wird als eine Reihe von Microservices in der Form von Containern bereitgestellt. Client-Apps können sowohl mit diesen Containern als auch zwischen Microservices kommunizieren. Wie bereits erwähnt, wird bei dieser anfänglichen Architektur eine direkte Client-zu-Microservice-Kommunikationsarchitektur verwendet, wodurch eine Clientanwendung Anforderungen direkt an jeden der Microservices stellen kann. Jeder Microservice weißt einen öffentlichen Endpunkt wie https://servicename.applicationname.companyname auf. Falls erforderlich, kann jeder Microservice einen anderen TCP-Port verwenden. In der Produktionsumgebung wäre diese URL dem Lastenausgleich der Microservices zugeordnet, der Anforderungen auf die verfügbaren Microserviceinstanzen verteilt.

**Wichtiger Hinweis zur API-Gateway im Vergleich zur direkten Kommunikation bei eShopOnContainers.** Wie bereits im Abschnitt zur Architektur in diesem Leitfaden erklärt, kann die direkte Client-zu-Microservice-Architektur Nachteile aufweisen, wenn Sie eine große und komplexe auf Microservices basierte Anwendung erstellen. Sie kann jedoch für eine kleine Anwendung gut genug sein. Beispielsweise für die Anwendung eShopOnContainers, bei der das Ziel ist, den Fokus auf eine einfachere Einsteigeranwendung zu legen, die auf Docker-Containern basiert. Es sollte zudem kein einzelnes monolithisches API-Gateway erstellt werden, das sich auf die Entwicklungsautonomie der Microservices auswirken kann.

Wenn Sie jedoch den Entwurf einer großen auf Microservices basierenden Anwendung mit Dutzenden Microservices planen, wird dringend empfohlen, wie im Abschnitt zur Architektur erklärt das API-Gatewaymuster in Betracht zu ziehen.
Diese Entscheidung für eine Architektur könnte neu überdacht werden, sobald Sie mit dem Gedanken an einsatzbereite Anwendungen und speziell erstellte Fassaden für Remoteclients spielen. Es kann hinsichtlich der unterschiedlichen Datenaggregation pro Client-App von Vorteil sein, wenn Sie über mehrere benutzerdefinierte API-Gateways abhängig vom Formfaktor der Client-Apps verfügen. Zudem können Sie in diesem Fall interne Microservices oder APIs vor den Client-Apps verstecken und die Autorisierung auf dieser einzelnen Ebene vornehmen. 

Vermeiden Sie jedoch, wie bereits erwähnt, große und monolithische API-Gateways, die die Entwicklungsautonomie Ihrer Microservices zerstören könnten.

### <a name="data-sovereignty-per-microservice"></a>Datensouveränität pro Microservice

Bei der Beispielanwendung besitzt jeder Microservice seine eigene Datenbank oder Datenquelle, und jede Datenbank oder Datenquelle wird als ein anderer Container bereitgestellt. Diese Entwurfsentscheidung wurde nur getroffen, um einem Entwickler das Abrufen des Codes aus GitHub, das Klonen dieses Codes und das Öffnen in Visual Studio oder Visual Studio Code zu erleichtern. Alternativ wird dadurch das Kompilieren der benutzerdefinierten Docker-Images mithilfe der .NET Core-CLI und der Docker-CLI sowie die anschließende Bereitstellung und Ausführung dieser in einer Docker-Entwicklungsumgebung erleichtert. So oder so können Entwickler durch die Verwendung von Containern für Datenquellen innerhalb von wenigen Minuten erstellen und bereitstellen, ohne eine externe Datenbank oder eine Datenquelle mit festen Abhängigkeiten von der Infrastruktur (Cloud oder lokal) bereitstellen zu müssen.

In einer echten Produktionsumgebung sollten die Datenbanken für Hochverfügbarkeit und Skalierbarkeit auf Datenbankservern in der Cloud oder lokal, jedoch nicht auf Containern basieren.

Daher handelt es sich bei den Bereitstellungseinheiten für Microservices (und bei dieser Anwendung sogar auch für Datenbanken) um Docker-Container. Außerdem handelt es sich bei der Referenzanwendung um eine Anwendung mit mehreren Containern, die Grundsätze von Microservices umfasst.

### <a name="additional-resources"></a>Zusätzliche Ressourcen

-   **GitHub-Repository „eShopOnContainers“. Quellcode für die Verweisanwendung**
    *https://aka.ms/eShopOnContainers/*

## <a name="benefits-of-a-microservice-based-solution"></a>Vorteile eines auf Microservices basierenden Ansatzes

Ein auf Microservices basierender Ansatz wie dieser hat viele Vorteile:

**Microservices sind relativ klein, einfach zu verwalten und weiterzuentwickeln**. Dies gilt insbesondere in folgenden Fällen:

-   Eine solche Lösung ist für Entwickler leicht verständlich und ermöglicht einen schnellen und produktiven Einstieg.

-   Containers starten schnell, wodurch Entwickler produktiver arbeiten können.

-   In einer integrierten Entwicklungsumgebung wie Visual Studio können kleine Projekte schnell geladen werden, wodurch Entwickler produktiv arbeiten können.

-   Jeder Microservice kann unabhängig von anderen Microservices entworfen, entwickelt und bereitgestellt werden. Dadurch ergibt sich Flexibilität, da die häufige Bereitstellung neuer Versionen von Microservices einfacher durchzuführen ist.

**Es ist möglich, einzelne Bereiche der Anwendung horizontal hochzuskalieren**. Beispielsweise könnte es nötig sein, den Katalog- oder den Warenkorbdienst horizontal hochzuskalieren, jedoch nicht den Bestellprozess. Eine Microserviceinfrastruktur ist im Gegensatz zu einer monolithischen Architektur deutlich effizienter hinsichtlich der verwendeten Ressourcen beim horizontalen Hochskalieren.

**Sie können die Entwicklungsarbeit auf mehrere Teams aufteilen**. Jeder Dienst kann sich im Besitz eines einzigen Entwicklungsteams befinden. Jedes Team kann seinen Dienst unabhängig von den anderen Teams verwalten, entwickeln, bereitstellen und skalieren.

**Probleme sind isolierter**. Wenn bei einem Dienst ein Problem auftritt, ist zunächst einmal nur dieser Dienst davon betroffen (außer wenn der falsche Entwurf verwendet wird, bei dem direkte Abhängigkeiten zwischen den Microservices bestehen), und andere Dienste können weiterhin Anforderungen verarbeiten. Im Gegensatz dazu kann eine fehlerhafte Komponente bei einer monolithischen Bereitstellungsarchitektur das gesamte System zum Ausfall bringen, insbesondere wenn Ressourcen betroffen sind, wie bei einem Arbeitsspeicherverlust. Zudem können Sie, nachdem eine Lösung für ein Problem bei einem Microservice gefunden wurde, nur den betroffenen Microservice bereitstellen, ohne dass der Rest der Anwendung betroffen ist.

**Sie können die neusten Technologien verwenden**. Da Sie unabhängig mit der Entwicklung von Diensten beginnen und diese parallel ausführen können (dank Containern und .NET Core), können Sie die neusten Technologien und Frameworks sinnvoll einsetzen, und Sie müssen für die gesamte Anwendung weiterhin einen älteren Stapel bzw. ein älteres Framework verwenden.

## <a name="downsides-of-a-microservice-based-solution"></a>Nachteile einer auf Microservices basierenden Lösung

Eine auf Microservices basierende Lösung wie diese hat auch einige Nachteile:

**Verteilte Anwendung**. Durch das Verteilen der Anwendung erhöht sich die Komplexität für Entwickler beim Entwerfen und Erstellen der Dienste. Beispielsweise müssen Entwickler die Kommunikation innerhalb des Diensts mithilfe von Protokollen wie HTTP oder AMPQ implementieren, wodurch das Testen und Ausnahmebehandlungen komplexer werden. Außerdem führt dies beim System zu erhöhter Wartezeit.

**Bereitstellungskomplexität**. Eine Anwendung, die über Dutzende Typen von Microservices verfügt und hohe Skalierbarkeit erfordert (sie muss in der Lage sein, viele Instanzen pro Dienst zu erstellen und diese Dienste über mehrere Hosts hinweg auszugleichen), bedeutet einen hohen Grad an Bereitstellungskomplexität in Bezug auf IT-Vorgänge und -Verwaltung. Wenn Sie keine an Microservices orientierte Infrastruktur (wie einen Orchestrator und Scheduler) verwenden, kann der Entwicklungsaufwand für diese zusätzliche Komplexität den Aufwand für die Geschäftsanwendung selbst übersteigen.

**Atomarische Transaktionen**. Atomarische Transaktionen zwischen mehreren Microservices sind üblicherweise nicht möglich. Die Geschäftsanforderungen müssen die eventuelle Konsistenz zwischen mehreren Microservices umfassen.

**Erhöhter Bedarf an globalen Ressourcen** (Gesamtspeicher-, Laufwerk- und Netzwerkressourcen für alle Server oder Hosts). In vielen Fällen übersteigt bei der Umstellung von einer monolithischen Anwendung auf einen Ansatz mit Microservices die Menge der von der neuen auf Microservices basierenden Anwendung benötigten globalen Ressourcen den Bedarf der Infrastruktur der ursprünglichen monolithischen Anwendung. Dies liegt daran, dass das höhere Maß an Granularität und verteilten Diensten mehr globale Ressourcen erfordert. Betrachtet man jedoch die geringen Kosten für Ressourcen im Allgemeinen und den Vorteil, dass nur bestimmte Bereiche der Anwendung horizontal hochskaliert werden können, im Vergleich zu den langfristigen Kosten bei der Weiterentwicklung monolithischer Anwendungen, stellt die verstärkte Verwendung von Ressourcen üblicherweise die bessere Alternative für große, langfristige Anwendungen dar.

**Probleme bei der direkten Kommunikation zwischen Client und Microservice**. Bei einer großen Anwendung mit Dutzenden Microservices ergeben sich Herausforderungen und Einschränkungen, wenn die Anwendung direkte Kommunikation zwischen Client und Microservice erfordert. Ein Problem stellt eine mögliche Diskrepanz zwischen den Anforderungen des Clients und den von jedem der Microservices verfügbar gemachten APIs dar. In einigen Fällen könnte es erforderlich sein, dass die Clientanwendung viele separate Anforderungen stellt, um die Benutzeroberfläche zu bilden. Dies kann über das Internet ineffizient sein und wäre über ein mobiles Netzwerk unpraktisch. Daher sollten Anforderungen von der Clientanwendung an das Back-End-System auf ein Minimum begrenzt werden.

Ein weiteres Problem bei der direkten Kommunikation zwischen Client und Microservice liegt darin, dass einige Microservices möglicherweise Protokolle verwenden, die nicht webfreundlich sind. Ein Dienst verwendet möglicherweise ein binäres Protokoll, während ein anderer Dienst AMQP-Nachrichten verwendet. Diese Protokolle sind nicht Firewall-freundlich und werden am besten intern verwendet. Üblicherweise sollte eine Anwendung Protokolle wie HTTP und WebSockets für die Kommunikation außerhalb der Firewall verwenden.

Ein weiterer Nachteil bei dieser direkten Kommunikation zwischen Client und Dienst ist, dass die Umgestaltung der Verträge für diese Microservices erschwert wird. Im Laufe der Zeit möchten Entwickler möglicherweise ändern, wie das System in Dienste partitioniert wird. Beispielsweise könnten sie zwei Dienste zusammenführen oder einen Dienst in mindestens zwei Dienste aufteilen. Wenn Clients jedoch direkt mit den Diensten kommunizieren, kann diese Art von Umgestaltung dazu führen, dass die Kompatibilität mit Client-Apps nicht mehr gegeben ist.

Wie bereits im Abschnitt zur Architektur erwähnt, sollten Sie beim Entwerfen und Erstellen einer komplexen auf Microservices basierenden Anwendung die Verwendung mehrerer differenzierter API-Gateways in Betracht ziehen, anstatt sich für die einfachere direkte Kommunikation zwischen Client und Microservice zu entscheiden.

**Partitionierung der Microservices.** Schließlich stehen Sie unabhängig davon, für welchen Ansatz Sie sich bei der Architektur der Microservices entscheiden, vor der nächsten Herausforderung: nämlich der Entscheidung, wie Sie eine End-to-End-Anwendung in mehrere Microservices partitionieren wollen. Wie bereits im Abschnitt zur Architektur in diesem Handbuch erwähnt, stehen mehrere Methoden und Ansätze zur Auswahl. Im Grunde müssen Sie Bereiche der Anwendung identifizieren, die von den anderen Bereichen entkoppelt sind und über wenige feste Abhängigkeiten verfügen. In vielen Fällen wird dies je nach Anwendungsfall an die Partitionierung von Diensten angepasst. In der Onlineshopanwendung ist ein Bestelldienst enthalten, der für die gesamte Geschäftslogik im Zusammenhang mit dem Bestellprozess verantwortlich ist. Zudem ist ein Katalogdienst und ein Warenkorbdienst verfügbar, die andere Funktionen implementieren. Idealerweise sollte jeder Dienst nur über wenige Verantwortlichkeiten verfügen. Dies entspricht dem Prinzip der einzigen Verantwortung, das auf Klassen angewendet wird und besagt, dass eine Klasse nur einen Grund zur Änderung haben sollte. In diesem Fall handelt es sich jedoch um Microservices, sodass der Umfang größer ist als bei einer einzelnen Klasse. Vor allem muss ein Microservice vollkommen unabhängig sein (End-to-End), einschließlich der Verantwortung für seine eigenen Datenquellen.

## <a name="external-versus-internal-architecture-and-design-patterns"></a>Externe im Vergleich zu internen Architektur- und Entwurfsmuster

Bei der externen Architektur handelt es sich um die Microservicearchitektur, die sich aus mehreren Diensten zusammensetzt und den im Abschnitt zur Architektur in diesem Handbuch beschriebenen Prinzipien folgt. Jedoch ist es, abhängig von der Art jedes Microservices und unabhängig von der allgemeinen Microservicearchitektur, für die Sie sich entscheiden, üblich und manchmal ratsam, über verschiedene interne Architekturen für verschiedene Microservices zu verfügen, von denen jede auf unterschiedlichen Mustern basiert. Die Microservices können sogar verschiedene Technologien und Programmiersprachen verwenden. In Abbildung 8-2 wird diese Vielfalt dargestellt.

![](./media/image2.png)

**Abbildung 8-2**. Externe im Vergleich zu interner Architektur und Entwurf

Beispielsweise sind in dem Beispiel *eShopOnContainers* die Katalog-, Warenkorb- und Benutzerprofilmicroservices einfach (im Grunde CRUD-Subsysteme). Daher ist deren interne Architektur und der interne Entwurf unkompliziert. Jedoch verfügen Sie möglicherweise über andere Microservices wie den Microservice für Bestellungen, der komplizierter ist und Geschäftsregeln mit einem hohen Grad an Domänenkomplexität darstellt, die sich stetig ändern. In solchen Fällen möchten Sie möglicherweise komplexere Muster innerhalb eines bestimmten Microservices implementieren, z.B. die mit den DDD-Ansätzen (Domain-driven Design) definierten Muster, wie es im Microservice für Bestellungen von *eShopOnContainers* vorgemacht wird. (Diese DDD-Muster wird in einem späteren Abschnitt genauer untersucht, in dem die Implementierung des Microservices für Bestellungen von *eShopOnContainers* erklärt wird).

Ein weiterer Grund für eine unterschiedliche Methode je Microservice könnte die Art jedes Microservices darstellen. Beispielsweise ist es möglicherweise besser, eine funktionale Programmiersprache wie F\# oder sogar eine Sprache wie R zu verwenden, wenn Sie für Domänen für KI und maschinelles Lernen entwickeln, anstelle einer objektorientierten Programmiersprache wie C\#.

Das Fazit ist, dass jeder Microservice über eine andere interne Architektur verfügen kann, die auf unterschiedlichen Entwurfsmustern basiert. Nicht alle Microservices sollten mithilfe von komplexen DDD-Mustern implementiert werden, da sie dadurch unnötig kompliziert gemacht würden. Dementsprechend sollten komplexe Microservices mit sich stets ändernder Geschäftslogik nicht als CRUD-Komponenten implementiert werden, da dies zu Code von geringer Qualität führen könnte.



## <a name="the-new-world-multiple-architectural-patterns-and-polyglot-microservices"></a>Der neue Ansatz: mehrere Architekturmuster und mehrsprachige Microservices

Softwarearchitekten und -entwickler verwenden eine Vielzahl von Architekturmustern. Im Folgenden sind einige davon aufgelistet (wobei sowohl Architekturstile als auch -muster enthalten sind):

-   Einfache CRUD-Architektur, Architektur auf einer einzelnen Ebene

-   [Herkömmliche Architektur mit n Ebenen](https://msdn.microsoft.com/library/ee658109.aspx#Layers)

-   [Domain-Driven Design mit n Ebenen](https://blogs.msdn.microsoft.com/cesardelatorre/2011/07/03/published-first-alpha-version-of-domain-oriented-n-layered-architecture-v2-0/)

-   [Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html) (wie bei [eShopOnWeb](http://aka.ms/WebAppArchitecture) verwendet)

-   [Command and Query Responsibility Segregation](https://martinfowler.com/bliki/CQRS.html) (CQRS)

-   [Ereignisgesteuerte Architektur](https://en.wikipedia.org/wiki/Event-driven_architecture) (Event-Driven Architecture, EDA)

Sie können Microservices auch mit vielen Technologien und Sprachen wie ASP.NET Core-Web-APIs, NancyFx, ASP.NET Core SignalR (verfügbar unter .NET Core 2), F\#, Node.js, Python, Java, C++, GoLang usw. erstellen.

Wichtig ist, dass weder ein bestimmtes Architekturmuster bzw. ein bestimmter Architekturstil noch eine bestimmte Technologie in allen Situationen die richtige Wahl darstellt. Abbildung 8-3 stellt einige Ansätze und Methoden dar (jedoch in keiner bestimmten Reihenfolge), die bei unterschiedlichen Microservices verwendet werden könnten.

![](./media/image3.png)

**Abbildung 8-3**. Die Welt der Muster mit mehreren Architekturen und mehrsprachigen Microservices

Wie in Abbildung 8-3 dargestellt, können Sie bei Anwendungen, die aus vielen Microservices bestehen (begrenzte Kontexte in DDD-Terminologie oder einfach „Subsysteme“ als unabhängige Microservices), jeden Microservice auf eine andere Weise implementieren. Jeder könnte über ein anderes Architekturmuster verfügen und eine andere Sprache sowie andere Datenbanken verwenden, abhängig von der Art, den Geschäftsanforderungen und den Prioritäten der Anwendung. In einigen Fällen können die Microservices ähnlich sein. Dies ist üblicherweise jedoch nicht der Fall, da sich die Kontextgrenze und die Anforderungen jedes Subsystems für gewöhnlich unterscheiden.

Beispielsweise ergäbe es bei einer einfachen CRUD-Wartungsanwendung möglicherweise keinen Sinn, DDD-Muster zu entwerfen und zu implementieren. Jedoch müssen Sie bei Ihrer Kerndomäne bzw. Ihrem Kerngeschäft möglicherweise komplexere Muster verwenden, um mit der Komplexität durch Geschäftsregeln umgehen zu können, die sich stetig ändern.

Insbesondere wenn Sie es mit großen Anwendungen zu tun haben, die aus mehreren Subsystemen bestehen, sollten Sie nicht eine einzige Hauptarchitektur basierend auf einem einzigen Architekturmuster verwenden. Beispielsweise sollte CQRS nicht als Hauptarchitektur für eine gesamte Anwendung verwendet werden, könnte jedoch für einige bestimmte Dienste hilfreich sein.

Es gibt keine Universallösung und kein richtiges Architekturmuster für jeden möglichen Fall. Es gibt kein Architekturmuster, das alle anderen hinfällig macht. Abhängig von den Prioritäten jedes Microservices müssen Sie wie in den folgenden Abschnitten erläutert einen anderen Ansatz für jeden Microservice auswählen.


>[!div class="step-by-step"]
[Zurück](index.md)
[Weiter](data-driven-crud-microservice.md)
