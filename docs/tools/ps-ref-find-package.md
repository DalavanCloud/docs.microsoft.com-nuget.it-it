---
title: Riferimento di PowerShell di NuGet. Find-Package
description: Riferimento per il comando di PowerShell di Find-Package nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f4640-103">Find-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f4640-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f4640-104">*Versione 3.0; questo argomento viene descritto il comando all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows. Per il comando di PowerShell. Find-Package generico, vedere il [riferimento di PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f4640-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f4640-105">Ottiene il set di pacchetti remoti con parole chiave o un ID specificato dall'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f4640-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="f4640-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f4640-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f4640-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="f4640-107">Parameters</span></span>

| <span data-ttu-id="f4640-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="f4640-108">Parameter</span></span> | <span data-ttu-id="f4640-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f4640-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4640-110">ID &lt;parole chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="f4640-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="f4640-111">(Obbligatorio) Parole chiave per la ricerca dell'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f4640-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="f4640-112">Utilizzare - ExactMatch per restituire solo i pacchetti il cui ID di pacchetto consente di ricercare le parole chiave.</span><span class="sxs-lookup"><span data-stu-id="f4640-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="f4640-113">Se nessuna parola chiave vengono specificata, `Find-Package` restituisce un elenco dei pacchetti primi 20 tramite download o il numero specificato da - prima.</span><span class="sxs-lookup"><span data-stu-id="f4640-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="f4640-114">Si noti che - Id è facoltativo e nessuna operazione.</span><span class="sxs-lookup"><span data-stu-id="f4640-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="f4640-115">Origine</span><span class="sxs-lookup"><span data-stu-id="f4640-115">Source</span></span> | <span data-ttu-id="f4640-116">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="f4640-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f4640-117">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="f4640-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f4640-118">Se omesso, `Find-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="f4640-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f4640-119">Completaversioni</span><span class="sxs-lookup"><span data-stu-id="f4640-119">AllVersions</span></span> | <span data-ttu-id="f4640-120">Visualizza tutte le versioni disponibili di ogni pacchetto anziché solo la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="f4640-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f4640-121">First</span><span class="sxs-lookup"><span data-stu-id="f4640-121">First</span></span> | <span data-ttu-id="f4640-122">Il numero di pacchetti da restituire dall'inizio dell'elenco. il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="f4640-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="f4640-123">Skip</span><span class="sxs-lookup"><span data-stu-id="f4640-123">Skip</span></span> | <span data-ttu-id="f4640-124">Omette il primo &lt;int&gt; pacchetti nell'elenco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="f4640-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f4640-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f4640-125">IncludePrerelease</span></span> | <span data-ttu-id="f4640-126">Include i pacchetti non definitiva nei risultati.</span><span class="sxs-lookup"><span data-stu-id="f4640-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f4640-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="f4640-127">ExactMatch</span></span> | <span data-ttu-id="f4640-128">Specificato da utilizzare &lt;parole chiave&gt; come un ID pacchetto tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="f4640-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="f4640-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="f4640-129">StartWith</span></span> | <span data-ttu-id="f4640-130">Restituisce pacchetti con pacchetto ID inizia con &lt;parole chiave&gt;.</span><span class="sxs-lookup"><span data-stu-id="f4640-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="f4640-131">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="f4640-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f4640-132">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="f4640-132">Common Parameters</span></span>

<span data-ttu-id="f4640-133">`Find-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f4640-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f4640-134">Esempi</span><span class="sxs-lookup"><span data-stu-id="f4640-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```