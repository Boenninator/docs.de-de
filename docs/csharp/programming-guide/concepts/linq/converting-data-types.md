---
title: Konvertieren von Datentypen (C#)
ms.date: 07/20/2015
ms.assetid: 46e5682f-77a1-4302-8f93-a2b53c408808
ms.openlocfilehash: 374ce15b8329c02c6b496a276a40fd9a60596e1f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33335821"
---
# <a name="converting-data-types-c"></a>Konvertieren von Datentypen (C#)
Konvertierungsmethoden ändern den Typ von Eingabeobjekten.  
  
 Konvertierungsvorgänge in LINQ-Abfragen sind in vielen Anwendungen nützlich. Nachstehend sind einige Beispiele aufgeführt:  
  
-   Die <xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=nameWithType>-Methode kann zum Ausblenden einer benutzerdefinierten Implementierung eines Standardabfrageoperators eines Typs verwendet werden.  
  
-   Die <xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType>-Methode kann verwendet werden, um nicht parametrisierte Auflistungen für LINQ-Abfragen zu ermöglichen.  
  
-   Die Methoden <xref:System.Linq.Enumerable.ToArray%2A?displayProperty=nameWithType>, <xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=nameWithType>, <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> und <xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType> können verwendet werden, um die sofortige Ausführung einer Abfrage zu erzwingen, statt sie zu verzögern, bis die Abfrage enumeriert wurde.  
  
## <a name="methods"></a>Methoden  
 Die folgende Tabelle enthält die Standardabfrageoperator-Methoden, die Datentypumwandlungen ausführen.  
  
 Die Konvertierungsmethoden in dieser Tabelle, deren Namen mit „As“ beginnen, ändern den statischen Typ der Quellauflistung, listen ihn jedoch nicht auf. Die Methoden, deren Namen mit „To“ anfangen, listen die Quellauflistung auf und verschieben die Elemente in den entsprechenden Auflistungstyp.  
  
|Methodenname|description|C#-Abfrageausdruckssyntax|Weitere Informationen|  
|-----------------|-----------------|---------------------------------|----------------------|  
|AsEnumerable|Gibt die Eingabe als <xref:System.Collections.Generic.IEnumerable%601> typisiert zurück|Nicht zutreffend.|<xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=nameWithType>|  
|AsQueryable|Konvertiert ein (generisches) <xref:System.Collections.IEnumerable>-Element in ein (generisches) <xref:System.Linq.IQueryable>-Element|Nicht zutreffend.|<xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=nameWithType>|  
|Typumwandlung|Kopiert die Elemente einer Auflistung in einen bestimmten Typ.|Verwenden Sie eine explizit typisierte Bereichsvariable. Zum Beispiel:<br /><br /> `from string str in words`|<xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Cast%2A?displayProperty=nameWithType>|  
|OfType|Filtert Werte, je nach ihrer Fähigkeit, die in einen angegebenen Typ umgewandelt werden sollen.|Nicht zutreffend.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|  
|ToArray|Konvertiert eine Auflistung in ein Array. Diese Methode erzwingt die Ausführung der Abfrage.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ToArray%2A?displayProperty=nameWithType>|  
|ToDictionary|Platziert Elemente in ein <xref:System.Collections.Generic.Dictionary%602> auf Grundlage einer Schlüsselauswahlfunktion. Diese Methode erzwingt die Ausführung der Abfrage.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=nameWithType>|  
|ToList|Konvertiert eine Auflistung in eine <xref:System.Collections.Generic.List%601>. Diese Methode erzwingt die Ausführung der Abfrage.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType>|  
|ToLookup|Platziert Elemente, basierend auf einer Schlüsselauswahlfunktion, in ein <xref:System.Linq.Lookup%602> (one-to-many-Wörterbuch) ein. Diese Methode erzwingt die Ausführung der Abfrage.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Beispiel für die Abfrageausdruckssyntax  
 Das folgende Codebeispiel verwendet eine explizit typisierte Bereichsvariable, um einen Typ vor dem Zugriff auf ein Element, das nur im Untertyp verfügbar ist, in einen Untertyp umzuwandeln.  
  
```csharp  
class Plant  
{  
    public string Name { get; set; }  
}  
  
class CarnivorousPlant : Plant  
{  
    public string TrapType { get; set; }  
}  
  
static void Cast()  
{  
    Plant[] plants = new Plant[] {  
        new CarnivorousPlant { Name = "Venus Fly Trap", TrapType = "Snap Trap" },  
        new CarnivorousPlant { Name = "Pitcher Plant", TrapType = "Pitfall Trap" },  
        new CarnivorousPlant { Name = "Sundew", TrapType = "Flypaper Trap" },  
        new CarnivorousPlant { Name = "Waterwheel Plant", TrapType = "Snap Trap" }  
    };  
  
    var query = from CarnivorousPlant cPlant in plants  
                where cPlant.TrapType == "Snap Trap"  
                select cPlant;  
  
    foreach (Plant plant in query)  
        Console.WriteLine(plant.Name);  
  
    /* This code produces the following output:  
  
        Venus Fly Trap  
        Waterwheel Plant  
    */  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Linq>  
 [Standard Query Operators Overview (C#) (Übersicht der Standardabfrageoperatoren (C#))](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
 [from-Klausel](../../../../csharp/language-reference/keywords/from-clause.md)  
 [LINQ-Abfrageausdrücke](../../../../csharp/programming-guide/linq-query-expressions/index.md)  
 [How to: Query an ArrayList with LINQ (C#) (Vorgehensweise: Abfragen von ArrayList mit LINQ (C#))](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)
