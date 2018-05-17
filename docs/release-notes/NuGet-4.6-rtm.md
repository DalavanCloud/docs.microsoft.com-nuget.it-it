---
title: Note sulla versione per NuGet 4.6 RTM
description: Note sulla versione per NuGet 4.6.0 incluse informazioni su problemi noti, correzioni di bug e DCR.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: d8fc374167e5c7f601c41887c4844854d0177ccb
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-46-rtm-release-notes"></a><span data-ttu-id="ed626-103">Note sulla versione per NuGet 4.6 RTM</span><span class="sxs-lookup"><span data-stu-id="ed626-103">NuGet 4.6 RTM Release Notes</span></span>

<span data-ttu-id="ed626-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="ed626-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="ed626-105">Riepilogo: Novità di questa versione</span><span class="sxs-lookup"><span data-stu-id="ed626-105">Summary: What's New in this Release</span></span>
* <span data-ttu-id="ed626-106">È stato aggiunto il supporto per [firma dei pacchetti](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).</span><span class="sxs-lookup"><span data-stu-id="ed626-106">We have added support for [signing packages](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).</span></span>  
* <span data-ttu-id="ed626-107">Visual Studio 2017 e nuget.exe ora verificano l'integrità dei pacchetti prima dell'installazione, ripristinando i [pacchetti firmati](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).</span><span class="sxs-lookup"><span data-stu-id="ed626-107">Visual Studio 2017 and nuget.exe now verifies package integrity before installing, restoring packages for [signed packages](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).</span></span>
* <span data-ttu-id="ed626-108">Sono state migliorate le prestazioni dei ripristini successivi.</span><span class="sxs-lookup"><span data-stu-id="ed626-108">We have improved performance of successive restores.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ed626-109">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="ed626-109">Known issues</span></span>
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="ed626-110">Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet</span><span class="sxs-lookup"><span data-stu-id="ed626-110">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="ed626-111">.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="ed626-111">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="ed626-112">[Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="ed626-112">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="ed626-113">Problemi principali corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="ed626-113">Top issues fixed in this release</span></span>

<span data-ttu-id="ed626-114">**Correzioni per le prestazioni**</span><span class="sxs-lookup"><span data-stu-id="ed626-114">**Performance fixes**</span></span>
* <span data-ttu-id="ed626-115">Non scrivere file di asset in assenza di modifiche - [#6491](https://github.com/NuGet/Home/issues/6491)</span><span class="sxs-lookup"><span data-stu-id="ed626-115">Don't write asset files when there is no change - [#6491](https://github.com/NuGet/Home/issues/6491)</span></span>
* <span data-ttu-id="ed626-116">Il ripristino causa valutazioni MSBuild aggiuntive quando il TFM dei progetti figlio non corrisponde a quello del padre del progetto - [#6311](https://github.com/NuGet/Home/issues/6311)</span><span class="sxs-lookup"><span data-stu-id="ed626-116">Restore causes extra MSBuild evaluations when child projects' TFM do not match with the parent project's - [#6311](https://github.com/NuGet/Home/issues/6311)</span></span>
* <span data-ttu-id="ed626-117">Migliorare le prestazioni di ripristino NoOp ottimizzando la creazione della specifica del grafico delle dipendenze - [#6252](https://github.com/NuGet/Home/issues/6252)</span><span class="sxs-lookup"><span data-stu-id="ed626-117">Improve NoOp restore perf by optimizing dependency graph spec creation - [#6252](https://github.com/NuGet/Home/issues/6252)</span></span>

<span data-ttu-id="ed626-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="ed626-118">**Bugs**</span></span>
* <span data-ttu-id="ed626-119">Il push in una cartella locale lascia nupkg bloccato - [#6325](https://github.com/NuGet/Home/issues/6325)</span><span class="sxs-lookup"><span data-stu-id="ed626-119">Push to local folder leaves nupkg locked - [#6325](https://github.com/NuGet/Home/issues/6325)</span></span>
* <span data-ttu-id="ed626-120">Implementazione di plug-in NuGet: più problemi - [#6149](https://github.com/NuGet/Home/issues/6149)</span><span class="sxs-lookup"><span data-stu-id="ed626-120">NuGet Plugin implementation:  multiple issues - [#6149](https://github.com/NuGet/Home/issues/6149)</span></span>
* <span data-ttu-id="ed626-121">UIHang - Rimuovere la chiamata del servizio query dall'inizializzazione MEF in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)</span><span class="sxs-lookup"><span data-stu-id="ed626-121">UIHang - Remove query service call from MEF initialization in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)</span></span>
* <span data-ttu-id="ed626-122">Eccezione di segnalazione errori per l'attività di download del pacchetto annullata - [#6096](https://github.com/NuGet/Home/issues/6096)</span><span class="sxs-lookup"><span data-stu-id="ed626-122">Error reporting exception for cancelled package download task - [#6096](https://github.com/NuGet/Home/issues/6096)</span></span>
* <span data-ttu-id="ed626-123">NuGet.exe sostituisce '+' con '%2B' nel nome di assembly - [#5956](https://github.com/NuGet/Home/issues/5956)</span><span class="sxs-lookup"><span data-stu-id="ed626-123">NuGet.exe replaces '+' with '%2B' in assembly name - [#5956](https://github.com/NuGet/Home/issues/5956)</span></span>
* <span data-ttu-id="ed626-124">Fn+F1 non porta alla pagina della Guida corretta per l'interfaccia utente e la console di Gestione pacchetti - [#5912](https://github.com/NuGet/Home/issues/5912)</span><span class="sxs-lookup"><span data-stu-id="ed626-124">Fn+F1 does not take to the right help page for PM UI and Console - [#5912](https://github.com/NuGet/Home/issues/5912)</span></span>
* <span data-ttu-id="ed626-125">VS NuGet scrive percorsi assoluti nei file di progetto in determinate circostanze - [#5888](https://github.com/NuGet/Home/issues/5888)</span><span class="sxs-lookup"><span data-stu-id="ed626-125">VS NuGet writes absolute paths into project files under specific circumstances - [#5888](https://github.com/NuGet/Home/issues/5888)</span></span>
* <span data-ttu-id="ed626-126">Correzione regressione 4.3 - I segnaposto $product$ e $ $AssemblyGuid non vengono sostituiti nel file di contenuto tramite la trasformazione - [#5880](https://github.com/NuGet/Home/issues/5880)</span><span class="sxs-lookup"><span data-stu-id="ed626-126">Fix 4.3 regression - Placeholders $product$ and $AssemblyGuid$ not replaced in contentfile through transformation - [#5880](https://github.com/NuGet/Home/issues/5880)</span></span>
* <span data-ttu-id="ed626-127">Arresto anomalo di dotnet restore con più origini - [#5817](https://github.com/NuGet/Home/issues/5817)</span><span class="sxs-lookup"><span data-stu-id="ed626-127">dotnet restore with multiple sources crashes - [#5817](https://github.com/NuGet/Home/issues/5817)</span></span>
* <span data-ttu-id="ed626-128">Il comando pack deve valutare nuovamente le versioni di progetto per consentire il controllo delle versioni git - [#4790](https://github.com/NuGet/Home/issues/4790)</span><span class="sxs-lookup"><span data-stu-id="ed626-128">Pack should re-evaluate project versions to allow git versioning - [#4790](https://github.com/NuGet/Home/issues/4790)</span></span>
* <span data-ttu-id="ed626-129">Migliorare errori difficili da capire quando si installa un pacchetto incompatibile - [#4555](https://github.com/NuGet/Home/issues/4555)</span><span class="sxs-lookup"><span data-stu-id="ed626-129">Improve hard to understand errors when you install an incompatible package - [#4555](https://github.com/NuGet/Home/issues/4555)</span></span>
* <span data-ttu-id="ed626-130">Opzione necessaria in TemplateWizard per installare i pacchetti come PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span><span class="sxs-lookup"><span data-stu-id="ed626-130">TemplateWizard needs option to install packages as PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span></span>
* <span data-ttu-id="ed626-131">I file props forniti dal pacchetto vengono ignorati quando MSBuild.exe viene eseguito all'esterno di un prompt dei comandi per sviluppatori - [#4530](https://github.com/NuGet/Home/issues/4530)</span><span class="sxs-lookup"><span data-stu-id="ed626-131">Package-delivered props files ignored when MSBuild.exe is run from outside a Developer Command Prompt - [#4530](https://github.com/NuGet/Home/issues/4530)</span></span>
* <span data-ttu-id="ed626-132">Correggere il messaggio di errore poco comprensibile quando si fa riferimento a una libreria .NET Standard non applicabile al progetto - [#4423](https://github.com/NuGet/Home/issues/4423)</span><span class="sxs-lookup"><span data-stu-id="ed626-132">Fix poor error message when referencing .NET Standard Library that is not applicable to project - [#4423](https://github.com/NuGet/Home/issues/4423)</span></span>
* <span data-ttu-id="ed626-133">Il comando dotnet add package non riesce per un pacchetto destinato a un profilo portatile con scarse indicazioni - [#4349](https://github.com/NuGet/Home/issues/4349)</span><span class="sxs-lookup"><span data-stu-id="ed626-133">dotnet add package fails for package targeting portable profile with little guidance - [#4349](https://github.com/NuGet/Home/issues/4349)</span></span>
* <span data-ttu-id="ed626-134">dotnet pack - suffisso version mancante da ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)</span><span class="sxs-lookup"><span data-stu-id="ed626-134">dotnet pack - version suffix missing from ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)</span></span>
* <span data-ttu-id="ed626-135">Errori di compilazione e arresto anomalo di Visual Studio con modello .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)</span><span class="sxs-lookup"><span data-stu-id="ed626-135">Build errors and VS crash with .NET Core template - [#3973](https://github.com/NuGet/Home/issues/3973)</span></span>
* <span data-ttu-id="ed626-136">Impossibile caricare l'indice del servizio per l'origine https:\* - [#3681](https://github.com/NuGet/Home/issues/3681)</span><span class="sxs-lookup"><span data-stu-id="ed626-136">Unable to load the service index for source https:\* - [#3681](https://github.com/NuGet/Home/issues/3681)</span></span>
* <span data-ttu-id="ed626-137">nuget.exe list -allversions non funziona - [#3441](https://github.com/NuGet/Home/issues/3441)</span><span class="sxs-lookup"><span data-stu-id="ed626-137">nuget.exe list -allversions doesn't work - [#3441](https://github.com/NuGet/Home/issues/3441)</span></span>
* <span data-ttu-id="ed626-138">Messaggio di errore fuorviante per la risoluzione delle dipendenze - [2984 #](https://github.com/NuGet/Home/issues/2984)</span><span class="sxs-lookup"><span data-stu-id="ed626-138">Misleading dependency resolution error message - [#2984](https://github.com/NuGet/Home/issues/2984)</span></span>
* <span data-ttu-id="ed626-139">nuget.exe restore non produce file con estensione props e targets per msbuildproj (regressione nell'aggiornamento v3.3.0-3.4.4) - [#2921](https://github.com/NuGet/Home/issues/2921)</span><span class="sxs-lookup"><span data-stu-id="ed626-139">nuget.exe restore doesn't produce .props and .targets files for .msbuildproj (regression in v3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)</span></span>
* <span data-ttu-id="ed626-140">Ritardo dell'interfaccia utente quando si aggiorna un pacchetto NuGet con apri file XAML - [#2878](https://github.com/NuGet/Home/issues/2878)</span><span class="sxs-lookup"><span data-stu-id="ed626-140">UI delay when updating a NuGet package with XAML file open - [#2878](https://github.com/NuGet/Home/issues/2878)</span></span>
* <span data-ttu-id="ed626-141">Errore del progetto di sito Web da IIS con caratteri non validi nel percorso - [#2798](https://github.com/NuGet/Home/issues/2798)</span><span class="sxs-lookup"><span data-stu-id="ed626-141">WebSite project from IIS fails with illegal characters in path - [#2798](https://github.com/NuGet/Home/issues/2798)</span></span>
* <span data-ttu-id="ed626-142">Blocco di nuget add in CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)</span><span class="sxs-lookup"><span data-stu-id="ed626-142">Nuget add hangs on CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)</span></span>
* <span data-ttu-id="ed626-143">Il ripristino con packagesavemode -nupkg non riesce per json.net - [#2706](https://github.com/NuGet/Home/issues/2706)</span><span class="sxs-lookup"><span data-stu-id="ed626-143">Restore with packagesavemode -nupkg fails for json.net - [#2706](https://github.com/NuGet/Home/issues/2706)</span></span>
* <span data-ttu-id="ed626-144">Filtro di Gestione pacchetti non disponibile nella finestra di output di Visual Studio per il comando restore - [#2704](https://github.com/NuGet/Home/issues/2704)</span><span class="sxs-lookup"><span data-stu-id="ed626-144">Package Manager filter not available in vs output window for restore command - [#2704](https://github.com/NuGet/Home/issues/2704)</span></span>


[<span data-ttu-id="ed626-145">Elenco di tutti i problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="ed626-145">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")