---
title: Abstrakte Klassen (F#)
description: "Erfahren Sie mehr über f# abstrakte Klassen, die einige oder alle Member, die nicht implementiert lassen und allgemeine Funktionen, die einen unterschiedlichen Satz von Objekttypen darzustellen."
keywords: Visual F#, F#, funktionale Programmierung
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: a3dcc335-433b-4672-ac2d-ae6b11b816f3
ms.openlocfilehash: 209bcca70318db59506011b1f2bb74a09bf3814a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="abstract-classes"></a><span data-ttu-id="2a547-104">Abstrakte Klassen</span><span class="sxs-lookup"><span data-stu-id="2a547-104">Abstract Classes</span></span>

<span data-ttu-id="2a547-105">*Abstrakte Klassen* sind Klassen, die einige oder alle Member, die nicht implementiert ist, lassen, damit Implementierungen von abgeleiteten Klassen bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="2a547-105">*Abstract classes* are classes that leave some or all members unimplemented, so that implementations can be provided by derived classes.</span></span>

## <a name="syntax"></a><span data-ttu-id="2a547-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="2a547-106">Syntax</span></span>

```fsharp
// Abstract class syntax.
[<AbstractClass>]
type [ accessibility-modifier ] abstract-class-name =
[ inherit base-class-or-interface-name ]
[ abstract-member-declarations-and-member-definitions ]

// Abstract member syntax.
abstract member member-name : type-signature
```

## <a name="remarks"></a><span data-ttu-id="2a547-107">Hinweise</span><span class="sxs-lookup"><span data-stu-id="2a547-107">Remarks</span></span>
<span data-ttu-id="2a547-108">In einer objektorientierten Programmierung ist eine abstrakte Klasse dient als Basisklasse einer Hierarchie und stellt allgemeine Funktionen, die einen unterschiedlichen Satz von Objekttypen.</span><span class="sxs-lookup"><span data-stu-id="2a547-108">In object-oriented programming, an abstract class is used as a base class of a hierarchy, and represents common functionality of a diverse set of object types.</span></span> <span data-ttu-id="2a547-109">Wie "Abstract" der Name schon sagt, entsprechen abstrakte Klassen häufig nicht direkt auf konkrete Entitäten in der Problemdomäne.</span><span class="sxs-lookup"><span data-stu-id="2a547-109">As the name "abstract" implies, abstract classes often do not correspond directly onto concrete entities in the problem domain.</span></span> <span data-ttu-id="2a547-110">Sie stellen jedoch dar, was viele unterschiedliche konkrete Entitäten gemeinsam haben.</span><span class="sxs-lookup"><span data-stu-id="2a547-110">However, they do represent what many different concrete entities have in common.</span></span>

<span data-ttu-id="2a547-111">Abstrakte Klassen benötigen die `AbstractClass` Attribut.</span><span class="sxs-lookup"><span data-stu-id="2a547-111">Abstract classes must have the `AbstractClass` attribute.</span></span> <span data-ttu-id="2a547-112">Sie können implementiert und nicht implementierte Member haben.</span><span class="sxs-lookup"><span data-stu-id="2a547-112">They can have implemented and unimplemented members.</span></span> <span data-ttu-id="2a547-113">Die Verwendung des Begriffs *abstrakte* bei Anwendung auf eine Klasse ist dasselbe wie bei anderen; allerdings die Verwendung des Begriffs *abstrakte* bei Anwendung auf Methoden (und Eigenschaften) ist ein wenig anders in f# aus seiner in anderen .NET-Sprachen verwenden.</span><span class="sxs-lookup"><span data-stu-id="2a547-113">The use of the term *abstract* when applied to a class is the same as in other .NET languages; however, the use of the term *abstract* when applied to methods (and properties) is a little different in F# from its use in other .NET languages.</span></span> <span data-ttu-id="2a547-114">In F# erläutert werden, wenn eine Methode mit gekennzeichnet ist die `abstract` -Schlüsselwort, dies gibt an, dass ein Member einen Eintrag, der sogenannten verfügt eine *virtuellen Dispatch-Slot*, in der internen Tabelle virtueller Funktionen für diesen Typ.</span><span class="sxs-lookup"><span data-stu-id="2a547-114">In F#, when a method is marked with the `abstract` keyword, this indicates that a member has an entry, known as a *virtual dispatch slot*, in the internal table of virtual functions for that type.</span></span> <span data-ttu-id="2a547-115">Anders ausgedrückt, ist die Methode virtuell ist, obwohl die `virtual` Schlüsselwort wird nicht in der Sprache f# verwendet.</span><span class="sxs-lookup"><span data-stu-id="2a547-115">In other words, the method is virtual, although the `virtual` keyword is not used in the F# language.</span></span> <span data-ttu-id="2a547-116">Das Schlüsselwort `abstract` dient für virtuelle Methoden unabhängig davon, ob die Methode implementiert wird.</span><span class="sxs-lookup"><span data-stu-id="2a547-116">The keyword `abstract` is used on virtual methods regardless of whether the method is implemented.</span></span> <span data-ttu-id="2a547-117">Die Deklaration einer virtuellen Dispatch-Slots ist getrennt von der Definition einer Methode für diesen Dispatchslot.</span><span class="sxs-lookup"><span data-stu-id="2a547-117">The declaration of a virtual dispatch slot is separate from the definition of a method for that dispatch slot.</span></span> <span data-ttu-id="2a547-118">Aus diesem Grund f# eine virtuelle Methodendeklaration und Definition in einer anderen .NET-Sprache entspricht eine Kombination von einer abstrakten Methodendeklaration und eine separate Definition, entweder mit der `default` Schlüsselwort oder der `override` Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="2a547-118">Therefore, the F# equivalent of a virtual method declaration and definition in another .NET language is a combination of both an abstract method declaration and a separate definition, with either the `default` keyword or the `override` keyword.</span></span> <span data-ttu-id="2a547-119">Weitere Informationen und Beispiele finden Sie unter [Methoden](members/methods.md).</span><span class="sxs-lookup"><span data-stu-id="2a547-119">For more information and examples, see [Methods](members/methods.md).</span></span>

<span data-ttu-id="2a547-120">Eine Klasse gilt als abstrakte nur, wenn es sind abstrakte Methoden, die deklariert, aber nicht definiert.</span><span class="sxs-lookup"><span data-stu-id="2a547-120">A class is considered abstract only if there are abstract methods that are declared but not defined.</span></span> <span data-ttu-id="2a547-121">Daher sind Klassen, die abstrakte Methoden verfügen über nicht zwangsläufig abstrakte Klassen.</span><span class="sxs-lookup"><span data-stu-id="2a547-121">Therefore, classes that have abstract methods are not necessarily abstract classes.</span></span> <span data-ttu-id="2a547-122">Es sei denn, eine Klasse abstrakte Methoden nicht definiert wurde, verwenden Sie nicht die **AbstractClass** Attribut.</span><span class="sxs-lookup"><span data-stu-id="2a547-122">Unless a class has undefined abstract methods, do not use the **AbstractClass** attribute.</span></span>

<span data-ttu-id="2a547-123">In der vorherigen Syntax *Zugriffsmodifizierer* kann `public`, `private` oder `internal`.</span><span class="sxs-lookup"><span data-stu-id="2a547-123">In the previous syntax, *accessibility-modifier* can be `public`, `private` or `internal`.</span></span> <span data-ttu-id="2a547-124">Weitere Informationen finden Sie unter [Zugriffssteuerung](access-control.md).</span><span class="sxs-lookup"><span data-stu-id="2a547-124">For more information, see [Access Control](access-control.md).</span></span>

<span data-ttu-id="2a547-125">Wie bei anderen Arten können abstrakte Klassen eine Basisklasse und eine oder mehrere Basisschnittstellen haben.</span><span class="sxs-lookup"><span data-stu-id="2a547-125">As with other types, abstract classes can have a base class and one or more base interfaces.</span></span> <span data-ttu-id="2a547-126">Jede Basisklasse oder Schnittstelle wird angezeigt, in einer separaten Zeile zusammen mit dem `inherit` Schlüsselwort.</span><span class="sxs-lookup"><span data-stu-id="2a547-126">Each base class or interface appears on a separate line together with the `inherit` keyword.</span></span>

<span data-ttu-id="2a547-127">Die Typdefinition einer abstrakten Klasse kann vollständig definierte Elemente enthalten, aber es kann auch abstrakte Member enthalten.</span><span class="sxs-lookup"><span data-stu-id="2a547-127">The type definition of an abstract class can contain fully defined members, but it can also contain abstract members.</span></span> <span data-ttu-id="2a547-128">Die Syntax für abstrakte Member wird in der vorherigen Syntax separat angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2a547-128">The syntax for abstract members is shown separately in the previous syntax.</span></span> <span data-ttu-id="2a547-129">In dieser Syntax der *Typsignatur* eines Members ist eine Liste mit den Parametertypen in der Reihenfolge und die Rückgabetypen, getrennt durch `->` Token und/oder `*` Token nach Bedarf, um Curry und Tupel Parameter.</span><span class="sxs-lookup"><span data-stu-id="2a547-129">In this syntax, the *type signature* of a member is a list that contains the parameter types in order and the return types, separated by `->` tokens and/or `*` tokens as appropriate for curried and tupled parameters.</span></span> <span data-ttu-id="2a547-130">Die Syntax für Typsignaturen abstrakten Member ist identisch mit, die in der Signatur verwendet und, die von IntelliSense in Visual Studio Code Editor angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2a547-130">The syntax for abstract member type signatures is the same as that used in signature files and that shown by IntelliSense in the Visual Studio Code Editor.</span></span>

<span data-ttu-id="2a547-131">Das folgende Codebeispiel veranschaulicht eine abstrakte Klasse Form, die zwei nicht abstrakte abgeleitete Klassen, Square und Kreis hat.</span><span class="sxs-lookup"><span data-stu-id="2a547-131">The following code illustrates an abstract class Shape, which has two non-abstract derived classes, Square and Circle.</span></span> <span data-ttu-id="2a547-132">Im Beispiel wird gezeigt, wie abstrakte Klassen, Methoden und Eigenschaften verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="2a547-132">The example shows how to use abstract classes, methods, and properties.</span></span> <span data-ttu-id="2a547-133">Im Beispiel stellt die abstrakte Klasse Form die gemeinsamen Elemente von den konkreten Entitäten Kreis oder ein Quadrat.</span><span class="sxs-lookup"><span data-stu-id="2a547-133">In the example, the abstract class Shape represents the common elements of the concrete entities circle and square.</span></span> <span data-ttu-id="2a547-134">Die allgemeinen Funktionen aller Formen (in einem zweidimensionalen Koordinatensystem) werden in der Form "-Klasse abstrahiert: die Position im Raster, einen Drehwinkel um sowie die Bereichs- und Umkreis-Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="2a547-134">The common features of all shapes (in a two-dimensional coordinate system) are abstracted out into the Shape class: the position on the grid, an angle of rotation, and the area and perimeter properties.</span></span> <span data-ttu-id="2a547-135">Diese können, mit Ausnahme der Position, die das Verhalten außer Kraft gesetzt werden der einzelne Formen ändern können.</span><span class="sxs-lookup"><span data-stu-id="2a547-135">These can be overridden, except for position, the behavior of which individual shapes cannot change.</span></span>

<span data-ttu-id="2a547-136">Die Drehungsmethode kann überschrieben werden, wie die Kreis-Klasse, die Drehung invariante aufgrund ihrer Symmetrie ist.</span><span class="sxs-lookup"><span data-stu-id="2a547-136">The rotation method can be overridden, as in the Circle class, which is rotation invariant because of its symmetry.</span></span> <span data-ttu-id="2a547-137">Daher wird in die Kreis-Klasse, die Drehungsmethode mit einer anderen Methode ersetzt, die keine Aktionen ausführt.</span><span class="sxs-lookup"><span data-stu-id="2a547-137">So in the Circle class, the rotation method is replaced by a method that does nothing.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2901.fs)]

<span data-ttu-id="2a547-138">**Ausgabe:**</span><span class="sxs-lookup"><span data-stu-id="2a547-138">**Output:**</span></span>

```
Perimeter of square with side length 10.000000 is 40.000000
Circumference of circle with radius 5.000000 is 31.415927
Area of Square: 100.000000
Area of Circle: 78.539816
```

## <a name="see-also"></a><span data-ttu-id="2a547-139">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2a547-139">See Also</span></span>
[<span data-ttu-id="2a547-140">Klassen</span><span class="sxs-lookup"><span data-stu-id="2a547-140">Classes</span></span>](classes.md)

[<span data-ttu-id="2a547-141">Mitglieder</span><span class="sxs-lookup"><span data-stu-id="2a547-141">Members</span></span>](members/index.md)

[<span data-ttu-id="2a547-142">Methoden</span><span class="sxs-lookup"><span data-stu-id="2a547-142">Methods</span></span>](members/methods.md)

[<span data-ttu-id="2a547-143">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="2a547-143">Properties</span></span>](members/Properties.md)