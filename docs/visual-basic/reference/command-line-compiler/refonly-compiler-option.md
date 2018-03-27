---
title: -Refonly (Visual Basic)
ms.date: 03/16/2018
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- -refonly
helpviewer_keywords:
- /refonly compiler option [Visual Basic]
- -refonly compiler option [Visual Basic]
- refonly compiler option [Visual Basic]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f5135ef4d33ddde27416e48c28425aa5b029237b
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="-refonly-visual-basic"></a><span data-ttu-id="d183f-102">-Refonly (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d183f-102">-refonly (Visual Basic)</span></span>

<span data-ttu-id="d183f-103">Die **- Refonly** Option gibt an, dass die primäre Ausgabe von der Kompilierung anstelle einer Implementierung Assembly eine Verweisassembly werden soll.</span><span class="sxs-lookup"><span data-stu-id="d183f-103">The **-refonly** option indicates that the primary output of the compilation should be a reference assembly instead of an implementation assembly.</span></span> <span data-ttu-id="d183f-104">Der Parameter `-refonly` deaktiviert im Hintergrund die Ausgabe von PDBs, da Verweisassemblys nicht ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="d183f-104">The `-refonly` parameter silently disables outputting PDBs, as reference assemblies cannot be executed.</span></span>

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]

## <a name="syntax"></a><span data-ttu-id="d183f-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="d183f-105">Syntax</span></span>

```console
-refonly
```

## <a name="remarks"></a><span data-ttu-id="d183f-106">Hinweise</span><span class="sxs-lookup"><span data-stu-id="d183f-106">Remarks</span></span>

<span data-ttu-id="d183f-107">Visual Basic unterstützt die `-refout` ab Version 15.3 wechseln.</span><span class="sxs-lookup"><span data-stu-id="d183f-107">Visual Basic supports the `-refout` switch starting with version 15.3.</span></span>

<span data-ttu-id="d183f-108">Verweisassemblys sind reine Assemblys, die Metadaten, aber keinen Implementierungscode enthalten.</span><span class="sxs-lookup"><span data-stu-id="d183f-108">Reference assemblies are metadata-only assemblies that contain metadata but no implementation code.</span></span> <span data-ttu-id="d183f-109">Typ- und Memberdaten Angaben für alles mit Ausnahme von anonymen Typen enthalten.</span><span class="sxs-lookup"><span data-stu-id="d183f-109">They include type and member information for everything except anonymous types.</span></span> <span data-ttu-id="d183f-110">Der Grund für die Verwendung von `throw null`-Texten (im Gegensatz zu keinen Texten) ist, dass PEVerify erfolgreich ausgeführt werden kann (und so wird die Vollständigkeit der Metadaten überprüft).</span><span class="sxs-lookup"><span data-stu-id="d183f-110">The reason for using `throw null` bodies (as opposed to no bodies) is so that PEVerify could run and pass (thus validating the completeness of the metadata).</span></span>

<span data-ttu-id="d183f-111">Verweisassemblys enthalten eine Assemblyebene [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) Attribut.</span><span class="sxs-lookup"><span data-stu-id="d183f-111">Reference assemblies include an assembly-level [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) attribute.</span></span> <span data-ttu-id="d183f-112">Dieses Attribut kann in der Quelle angegeben werden (dann muss der Compiler es nicht künstlich erstellen).</span><span class="sxs-lookup"><span data-stu-id="d183f-112">This attribute may be specified in source (then the compiler won't need to synthesize it).</span></span> <span data-ttu-id="d183f-113">Aufgrund dieses Attribut Laufzeiten lehnt Verweisassemblys für Ausführung geladen (aber dennoch können Sie in einem reflektionsbezogenen Kontext geladen werden).</span><span class="sxs-lookup"><span data-stu-id="d183f-113">Because of this attribute, runtimes will refuse to load reference assemblies for execution (but they can still be loaded in a reflection-only context).</span></span> <span data-ttu-id="d183f-114">Tools, mit die Assemblys entsprechen müssen sicherstellen, dass sie Verweisassemblys als reflektionsbezogenen geladen; Andernfalls löst die Laufzeit eine <xref:System.BadImageFormatException>.</span><span class="sxs-lookup"><span data-stu-id="d183f-114">Tools that reflect on assemblies need to ensure they load reference assemblies as reflection-only; otherwise, the runtime throws a <xref:System.BadImageFormatException>.</span></span>

<span data-ttu-id="d183f-115">Die Optionen `-refonly` und [`-refout`](refout-compiler-option.md) schließen sich gegenseitig aus.</span><span class="sxs-lookup"><span data-stu-id="d183f-115">The `-refonly` and [`-refout`](refout-compiler-option.md) options are mutually exclusive.</span></span>

## <a name="see-also"></a><span data-ttu-id="d183f-116">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="d183f-116">See also</span></span>
<span data-ttu-id="d183f-117">[-refout](refout-compiler-option.md) </span><span class="sxs-lookup"><span data-stu-id="d183f-117">[-refout](refout-compiler-option.md) </span></span>  
[<span data-ttu-id="d183f-118">Visual Basic-Befehlszeilencompiler</span><span class="sxs-lookup"><span data-stu-id="d183f-118">Visual Basic Command-Line Compiler</span></span>](index.md)  
[<span data-ttu-id="d183f-119">Beispiele für Kompilierungsbefehlszeilen</span><span class="sxs-lookup"><span data-stu-id="d183f-119">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)   