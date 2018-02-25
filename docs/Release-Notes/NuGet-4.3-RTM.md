---
title: Note sulla versione per NuGet 4.3 RTM | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 4.3 RTM incluse informazioni su problemi noti, correzioni di bug, funzionalità aggiunte e DCR."
keywords: "Note sulla versione per NuGet 4.3 RTM, correzioni di bug, problemi noti, funzionalità aggiunte, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: a2b61d854f4a5f1490832dab9a272c3a13b56adf
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="0179b-104">Note sulla versione per NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="0179b-104">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="0179b-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.3 RTM, che aggiunge il supporto per nuovi scenari, ad esempio.NET Standard 2.0/.NET Core 2.0, contiene varie correzioni di qualità e migliora le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="0179b-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="0179b-106">Questa versione introduce anche vari miglioramenti, come il supporto della versione 2.0.0 del versionamento semantico, l'integrazione in MSBuild degli avvisi e degli errori di NuGet e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="0179b-106">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0179b-107">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="0179b-107">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="0179b-108">In determinati casi il ripristino di NuGet gestisce le origini pacchetto disabilitate come se fossero abilitate</span><span class="sxs-lookup"><span data-stu-id="0179b-108">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="0179b-109">Problema</span><span class="sxs-lookup"><span data-stu-id="0179b-109">Issue</span></span>

<span data-ttu-id="0179b-110">Le seguenti tecniche della riga di comando per il ripristino gestiscono le origini dei pacchetti disabilitate come abilitate.</span><span class="sxs-lookup"><span data-stu-id="0179b-110">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="0179b-111">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="0179b-111">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="0179b-112">`dotnet restore` (con il file dotnet.exe incluso con Visual Studio o con il file incluso con NetCore SDK 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="0179b-112">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="0179b-113">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="0179b-113">Workaround</span></span>

1. <span data-ttu-id="0179b-114">Usare Visual Studio (2017 15.3 o versioni successive) o NuGet.exe (v4.3.0 o versioni successive)</span><span class="sxs-lookup"><span data-stu-id="0179b-114">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="0179b-115">Eliminare l'origine disabilitata e continuare a usare msbuild o dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="0179b-115">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="0179b-116">Per la soluzione è possibile usare "Clear" in NuGet.config e quindi definire le origini necessarie per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="0179b-116">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="0179b-117">Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni</span><span class="sxs-lookup"><span data-stu-id="0179b-117">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="0179b-118">Problema</span><span class="sxs-lookup"><span data-stu-id="0179b-118">Issue</span></span>

<span data-ttu-id="0179b-119">A volte, nella console di Gestione pacchetti il tasto INVIO non funziona.</span><span class="sxs-lookup"><span data-stu-id="0179b-119">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="0179b-120">Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="0179b-120">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="0179b-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="0179b-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="0179b-122">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="0179b-122">Workaround</span></span>

<span data-ttu-id="0179b-123">Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="0179b-123">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="0179b-124">In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.</span><span class="sxs-lookup"><span data-stu-id="0179b-124">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="0179b-125">Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="0179b-125">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="0179b-126">Problema</span><span class="sxs-lookup"><span data-stu-id="0179b-126">Issue</span></span>

<span data-ttu-id="0179b-127">Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="0179b-127">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="0179b-128">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="0179b-128">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="0179b-129">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="0179b-129">Workaround</span></span>

<span data-ttu-id="0179b-130">È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="0179b-130">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="0179b-131">La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete</span><span class="sxs-lookup"><span data-stu-id="0179b-131">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="0179b-132">Problema</span><span class="sxs-lookup"><span data-stu-id="0179b-132">Issue</span></span>

<span data-ttu-id="0179b-133">Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete.</span><span class="sxs-lookup"><span data-stu-id="0179b-133">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="0179b-134">Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0179b-134">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="0179b-135">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="0179b-135">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="0179b-136">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="0179b-136">Workaround</span></span>

<span data-ttu-id="0179b-137">Eseguire un ripristino manuale.</span><span class="sxs-lookup"><span data-stu-id="0179b-137">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="0179b-138">Problemi risolti nell'intervallo di tempo NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="0179b-138">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="0179b-139">[Note sulla versione per NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) - Vengono elencati tutti i problemi risolti per NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="0179b-139">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="0179b-140">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="0179b-140">Features</span></span>

- <span data-ttu-id="0179b-141">Miglioramento delle prestazioni del ripristino NuGet - Implementazione di NoOp più intelligente per i ripristini dalla riga di comando e VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="0179b-141">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="0179b-142">NET Core 2.0: l'interfaccia della riga di comando di VS/Dotnet deve iniziare a usare funzionalità NuGet esistenti: cartelle di fallback - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="0179b-142">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="0179b-143">NET Core 2.0: consentire agli utenti di ignorare avvisi di ripristino specifici (o elevarli a errore) - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="0179b-143">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="0179b-144">NET Core 2.0: assembly localizzati dell'interfaccia della riga di comando - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="0179b-144">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="0179b-145">NET Core 2.0: registrare tutti gli avvisi/errori nel file degli asset (incluso PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="0179b-145">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="0179b-146">Abilitare il supporto del moniker TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="0179b-146">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="0179b-147">Ridurre il numero di progetti NuGet.Core e NuGet.Client (quindi di DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="0179b-147">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="0179b-148">Aggiungere la possibilità di contrassegnare gli avvisi NuGet come errori - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="0179b-148">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="0179b-149">Bug</span><span class="sxs-lookup"><span data-stu-id="0179b-149">Bugs</span></span>

- <span data-ttu-id="0179b-150">Errore di msbuild /t:pack con il parametro "DevelopmentDependency" non supportato dall'attività "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="0179b-150">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="0179b-151">La struttura di directory per i file di contenuto diventa flat se non si aggiunge il separatore di directory Windows alla fine di PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="0179b-151">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="0179b-152">I progetti netcore non supportano l'impostazione come developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="0179b-152">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="0179b-153">RestoreManagerPackage viene caricato in modo sincrono con conseguente blocco del thread dell'interfaccia utente e deadlock di VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="0179b-153">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="0179b-154">dotnet restore (e quindi msbuild /t:restore) ignora i progetti con una dipendenza esplicita da un progetto nella soluzione [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="0179b-154">dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="0179b-155">Se la soluzione contiene ProjectReference che fanno riferimento allo stesso progetto, con combinazioni di maiuscole/minuscole diverse, il ripristino potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="0179b-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="0179b-156">Questo problema riguarda anche percorsi relativi diversi, senza differenze nella combinazione di maiuscole/minuscole - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="0179b-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="0179b-157">Gli eseguibili ripristinati da pacchetti NuGet non sono più eseguibili con .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="0179b-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="0179b-158">NuGet.exe non visualizza tutti i dettagli dell'eccezione durante l'analisi del file di soluzione - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="0179b-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="0179b-159">Pack inserisce i file di contenuto nella posizione errata se ContentTargetFolders contiene un percorso che termina con '/' in Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="0179b-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="0179b-160">Non è possibile ripristinare un DotNetCliToolReference per un pacchetto di strumenti con destinazione netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="0179b-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="0179b-161">L'interfaccia della riga di comando per l'aggiornamento di NuGet lascia la condizione della versione del pacchetto precedente nel file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="0179b-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0179b-162">DCR</span><span class="sxs-lookup"><span data-stu-id="0179b-162">DCRs</span></span>

- <span data-ttu-id="0179b-163">Lettura di DotnetCliToolTargetFramework dai nomi CPS - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="0179b-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="0179b-164">Il controllo TPMinV dovrebbe funzionare per progetti UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="0179b-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="0179b-165">Migliorare la descrizione dell'interfaccia utente per i pacchetti AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="0179b-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="0179b-166">Il ripristino di NuGet seleziona gli asset di compilazione dalla sezione di runtime.</span><span class="sxs-lookup"><span data-stu-id="0179b-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="0179b-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="0179b-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="0179b-168">Inserire la diagnostica per le dipendenze nel file di blocco - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="0179b-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="0179b-169">Collegamenti ai problemi di GitHub risolti nella versione 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="0179b-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="0179b-170">Elenco dei problemi</span><span class="sxs-lookup"><span data-stu-id="0179b-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")