---
title: Guida di riferimento di sincronizzazione-pacchetto NuGet PowerShell
description: Riferimento per il comando di PowerShell di sincronizzazione pacchetto nella Console di gestione pacchetti NuGet in Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="bc345-103">Sync-Package (console di Gestione pacchetti in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bc345-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bc345-104">*Versione 3.0; disponibile solo all'interno di [Console di gestione pacchetti NuGet](package-manager-console.md) in Visual Studio in Windows.*</span><span class="sxs-lookup"><span data-stu-id="bc345-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="bc345-105">Ottiene la versione del pacchetto installato dal specificato (o predefinito) del progetto e sincronizza la versione ai restanti progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="bc345-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="bc345-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="bc345-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bc345-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="bc345-107">Parameters</span></span>

| <span data-ttu-id="bc345-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="bc345-108">Parameter</span></span> | <span data-ttu-id="bc345-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bc345-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc345-110">Id</span><span class="sxs-lookup"><span data-stu-id="bc345-110">Id</span></span> | <span data-ttu-id="bc345-111">(Obbligatorio) L'identificatore del pacchetto per la sincronizzazione. -Id switch stesso è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="bc345-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="bc345-112">MSI</span><span class="sxs-lookup"><span data-stu-id="bc345-112">IgnoreDependencies</span></span> | <span data-ttu-id="bc345-113">Installa solo questo pacchetto e non le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bc345-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="bc345-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="bc345-114">ProjectName</span></span> | <span data-ttu-id="bc345-115">Progetto per sincronizzare il pacchetto, verrà utilizzato per il progetto predefinito.</span><span class="sxs-lookup"><span data-stu-id="bc345-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="bc345-116">Versione</span><span class="sxs-lookup"><span data-stu-id="bc345-116">Version</span></span> | <span data-ttu-id="bc345-117">La versione del pacchetto per la sincronizzazione, verrà utilizzato per la versione attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="bc345-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="bc345-118">Origine</span><span class="sxs-lookup"><span data-stu-id="bc345-118">Source</span></span> | <span data-ttu-id="bc345-119">Il percorso URL o una cartella per l'origine del pacchetto da cercare.</span><span class="sxs-lookup"><span data-stu-id="bc345-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="bc345-120">I percorsi di cartella locale possono essere assoluto o relativo della cartella corrente.</span><span class="sxs-lookup"><span data-stu-id="bc345-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="bc345-121">Se omesso, `Sync-Package` Cerca l'origine pacchetto attualmente selezionata.</span><span class="sxs-lookup"><span data-stu-id="bc345-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="bc345-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="bc345-122">IncludePrerelease</span></span> | <span data-ttu-id="bc345-123">Include pacchetti della versione provvisoria della sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="bc345-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="bc345-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="bc345-124">FileConflictAction</span></span> | <span data-ttu-id="bc345-125">L'azione da intraprendere quando viene richiesto di sovrascrivere o ignorare i file esistenti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="bc345-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="bc345-126">I valori possibili sono *sovrascrittura, Ignora, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="bc345-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="bc345-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="bc345-127">DependencyVersion</span></span> | <span data-ttu-id="bc345-128">La versione dei pacchetti di dipendenza da usare, che può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="bc345-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="bc345-129">*Più basso* (impostazione predefinita): la versione minima</span><span class="sxs-lookup"><span data-stu-id="bc345-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="bc345-130">*HighestPatch*: la versione con la patch più basso principale, secondaria più basso, più elevata</span><span class="sxs-lookup"><span data-stu-id="bc345-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="bc345-131">*HighestMinor*: la versione con il minimo principali, patch più alto, minore più alto</span><span class="sxs-lookup"><span data-stu-id="bc345-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="bc345-132">*Più alto* (impostazione predefinita per il pacchetto di aggiornamento senza parametri): la versione più recente</span><span class="sxs-lookup"><span data-stu-id="bc345-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="bc345-133">È possibile impostare il valore predefinito utilizzando il [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) impostazione di `Nuget.Config` file.</span><span class="sxs-lookup"><span data-stu-id="bc345-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="bc345-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="bc345-134">WhatIf</span></span> | <span data-ttu-id="bc345-135">Viene illustrato che cosa accadrebbe eseguendo il comando senza eseguire effettivamente la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="bc345-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="bc345-136">Nessuno di questi parametri accettano caratteri jolly o di input di pipeline.</span><span class="sxs-lookup"><span data-stu-id="bc345-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bc345-137">Parametri comuni</span><span class="sxs-lookup"><span data-stu-id="bc345-137">Common Parameters</span></span>

<span data-ttu-id="bc345-138">`Sync-Package` supporta i seguenti [parametri PowerShell comuni](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, azione di errore, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bc345-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bc345-139">Esempi</span><span class="sxs-lookup"><span data-stu-id="bc345-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```