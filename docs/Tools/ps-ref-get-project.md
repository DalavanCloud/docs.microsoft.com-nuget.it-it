---
title: Riferimento di PowerShell di NuGet. Get-progetto | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Riferimento per il comando GetProject PowerShell nella Console di gestione pacchetti NuGet in Visual Studio.
keywords: Console di gestione, i comandi di Powershell di NuGet, riferimento di Powershell di NuGet, Get-progetto del pacchetto NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="bc554-104">Get-progetto (Console di gestione dei pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bc554-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bc554-105">*Disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="bc554-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="bc554-106">Visualizza informazioni sul valore predefinito o il progetto specificato.</span><span class="sxs-lookup"><span data-stu-id="bc554-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="bc554-107">`Get-Project` in particolare, restituisce un riferimento per l'oggetto di Visual Studio DTE (Development Tools Environment) per il progetto.</span><span class="sxs-lookup"><span data-stu-id="bc554-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="bc554-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="bc554-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bc554-109">Parametri</span><span class="sxs-lookup"><span data-stu-id="bc554-109">Parameters</span></span>

| <span data-ttu-id="bc554-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="bc554-110">Parameter</span></span> | <span data-ttu-id="bc554-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bc554-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc554-112">nome</span><span class="sxs-lookup"><span data-stu-id="bc554-112">Name</span></span> | <span data-ttu-id="bc554-113">Specifica il progetto da visualizzare, verrà utilizzato per il progetto predefinito selezionato nella Console di gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bc554-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="bc554-114">-Il nome del parametro è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="bc554-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="bc554-115">Tutti</span><span class="sxs-lookup"><span data-stu-id="bc554-115">All</span></span> | <span data-ttu-id="bc554-116">Visualizza informazioni per ogni progetto nella soluzione. l'ordine dei progetti non è deterministico.</span><span class="sxs-lookup"><span data-stu-id="bc554-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="bc554-117">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="bc554-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bc554-118">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="bc554-118">Common Parameters</span></span>

<span data-ttu-id="bc554-119">`Get-Project` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bc554-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bc554-120">Esempi</span><span class="sxs-lookup"><span data-stu-id="bc554-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```