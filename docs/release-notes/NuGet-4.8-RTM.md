---
title: Note sulla versione per NuGet 4.8 RTM
description: Note sulla versione per NuGet 4.8.1 incluse informazioni su problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: d23c4a8874d3d2e1a9ea721c66b15bb458de88a3
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516232"
---
# <a name="nuget-48-rtm-release-notes"></a><span data-ttu-id="88f43-103">Note sulla versione per NuGet 4.8 RTM</span><span class="sxs-lookup"><span data-stu-id="88f43-103">NuGet 4.8 RTM Release Notes</span></span>

<span data-ttu-id="88f43-104">[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include la funzionalità NuGet 4.8.</span><span class="sxs-lookup"><span data-stu-id="88f43-104">[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.8 functionality.</span></span>

<span data-ttu-id="88f43-105">Sono disponibili anche le versioni da riga di comando della stessa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="88f43-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="88f43-106">NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="88f43-106">NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="88f43-107">DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="88f43-107">DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="88f43-108">Riepilogo: Novità di questa versione</span><span class="sxs-lookup"><span data-stu-id="88f43-108">Summary: What's New in this Release</span></span>
* <span data-ttu-id="88f43-109">NuGet.exe supporta ora i nomi lunghi dei file in Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)</span><span class="sxs-lookup"><span data-stu-id="88f43-109">NuGet.exe now supports longfilenames on Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)</span></span>
* <span data-ttu-id="88f43-110">I plug-in di autenticazione possono ora essere usati in MSBuild, DotNet.exe, NuGet.exe e Visual Studio, anche tra più piattaforme.</span><span class="sxs-lookup"><span data-stu-id="88f43-110">Authenication plugins now work across MsBuild, DotNet.exe, NuGet.exe and Visual Studio, including cross platform.</span></span> <span data-ttu-id="88f43-111">La prima generazione di plug-in di autenticazione non era supportata in MSBuild, DotNet.exe.</span><span class="sxs-lookup"><span data-stu-id="88f43-111">The first generation of authentication plugins were not supported in MsBuild, DotNet.exe.</span></span> <span data-ttu-id="88f43-112">Nota: le build di Visual Studio 2017 15.9 Preview includono il plug-in di autenticazione di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="88f43-112">Note: VS 2017 15.9 Preview builds have a VSTS authentication plugin included.</span></span> [<span data-ttu-id="88f43-113">#6486</span><span class="sxs-lookup"><span data-stu-id="88f43-113">#6486</span></span>](https://github.com/NuGet/Home/issues/6486)
* <span data-ttu-id="88f43-114">Il resolver SDK di MSBuild è ora disponibile come parte di NuGet e viene installato con gli strumenti NuGet per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88f43-114">MsBuild's SDK Resolver now builds as part of NuGet and installs with NuGet tools for VS.</span></span> <span data-ttu-id="88f43-115">In questo modo si evitano problemi di sincronizzazione delle versioni. [#6799](https://github.com/NuGet/Home/issues/6799)</span><span class="sxs-lookup"><span data-stu-id="88f43-115">This will avoid versions getting out sync. [#6799](https://github.com/NuGet/Home/issues/6799)</span></span>
* <span data-ttu-id="88f43-116">PackageReference supporta ora i metadati DevelopmentDependency - [#4125](https://github.com/NuGet/Home/issues/4125)</span><span class="sxs-lookup"><span data-stu-id="88f43-116">PackageReference now supports DevelopmentDependency metadata - [#4125](https://github.com/NuGet/Home/issues/4125)</span></span>

## <a name="known-issues"></a><span data-ttu-id="88f43-117">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="88f43-117">Known issues</span></span>
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a><span data-ttu-id="88f43-118">L'installazione di pacchetti firmati in un computer CI o in un ambiente offline richiede più tempo del solito</span><span class="sxs-lookup"><span data-stu-id="88f43-118">Installing signed packages on a CI machine or in an offline environment takes longer than usual</span></span>

#### <a name="issue"></a><span data-ttu-id="88f43-119">Problema</span><span class="sxs-lookup"><span data-stu-id="88f43-119">Issue</span></span>
<span data-ttu-id="88f43-120">Se il computer ha accesso limitato a Internet (ad esempio un computer di compilazione in uno scenario CI/CD), l'installazione o il ripristino di un pacchetto NuGet firmato genererà un avviso ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) dal momento che i server di revoca non sono raggiungibili.</span><span class="sxs-lookup"><span data-stu-id="88f43-120">If the machine has restricted internet access (such as a build machine in a CI/CD scenario), installing/restoring a signed nuget package will result a warning ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) since the revocation servers are not reachable.</span></span> <span data-ttu-id="88f43-121">Si tratta di una condizione prevista.</span><span class="sxs-lookup"><span data-stu-id="88f43-121">This is expected.</span></span> <span data-ttu-id="88f43-122">In alcuni casi, tuttavia, ciò può avere conseguenze impreviste, ad esempio l'installazione o il ripristino del pacchetto richiede più tempo del solito.</span><span class="sxs-lookup"><span data-stu-id="88f43-122">However, in some cases, this may have unintended concequences such as the package install/restore taking longer than usual.</span></span>

#### <a name="workaround"></a><span data-ttu-id="88f43-123">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="88f43-123">Workaround</span></span>
<span data-ttu-id="88f43-124">Eseguire l'aggiornamento a Visual Studio 15.8.4 e NuGet.exe 4.8.1, in cui è stata introdotta una variabile di ambiente per attivare la modalità di controllo delle revoche.</span><span class="sxs-lookup"><span data-stu-id="88f43-124">Update to Visual Studio 15.8.4 and NuGet.exe 4.8.1 where we introduced an environment variable to switch the revocation check mode.</span></span>
<span data-ttu-id="88f43-125">L'impostazione della variabile di ambiente `NUGET_CERT_REVOCATION_MODE` su `offline` forzerà NuGet a controllare lo stato di revoca del certificato solo a fronte dell'elenco di revoche di certificati memorizzato nella cache, pertanto NuGet non tenterà di raggiungere i server di revoca.</span><span class="sxs-lookup"><span data-stu-id="88f43-125">Setting the `NUGET_CERT_REVOCATION_MODE` environment variable to `offline` will force NuGet to check the revocation status of the certificate only against the cached certificate revocation list, and NuGet will not attempt to reach revocation servers.</span></span> <span data-ttu-id="88f43-126">Quando la modalità di controllo delle revoche è impostata su `offline`, verrà effettuato il downgrade dell'avviso a informazione.</span><span class="sxs-lookup"><span data-stu-id="88f43-126">When the revocation check mode is set to `offline`, the warning will be downgraded to an info.</span></span>

> [!Warning]
> <span data-ttu-id="88f43-127">In circostanze normali non è consigliabile impostare la modalità di controllo delle revoche su offline.</span><span class="sxs-lookup"><span data-stu-id="88f43-127">It is not recommended to switch the revocation check mode to offline under normal cirumstances.</span></span> <span data-ttu-id="88f43-128">Così facendo, infatti, NuGet ignorerà il controllo delle revoche online ed eseguirà solo un controllo delle revoche offline a fronte dell'elenco di revoche di certificati memorizzato nella cache, che potrebbe non essere aggiornato.</span><span class="sxs-lookup"><span data-stu-id="88f43-128">Doing so will cause NuGet to skip online revocation check and perform only an offline revocation check against the cached certificate revocation list which may be out of date.</span></span> <span data-ttu-id="88f43-129">Questo significa che i pacchetti in cui è possibile che il certificato di firma sia stato revocato continueranno a essere installati/ripristinati, mentre non avrebbero dovuto superare il controllo delle revoche ed essere installati.</span><span class="sxs-lookup"><span data-stu-id="88f43-129">This means packages where the signing certificate may have been revoked, will continue to be installed/restored, which otherwise would have failed revocation check and would not have been installed.</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="88f43-130">L'opzione `Migrate packages.config to PackageReference...` non è disponibile nel menu di scelta rapida</span><span class="sxs-lookup"><span data-stu-id="88f43-130">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="88f43-131">Problema</span><span class="sxs-lookup"><span data-stu-id="88f43-131">Issue</span></span>

<span data-ttu-id="88f43-132">Alla prima apertura di un progetto, NuGet potrebbe non essere inizializzato fino all'esecuzione di un'operazione NuGet.</span><span class="sxs-lookup"><span data-stu-id="88f43-132">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="88f43-133">Per questo motivo, l'opzione di migrazione non viene visualizzata nel menu di scelta rapida per `packages.config` o `References`.</span><span class="sxs-lookup"><span data-stu-id="88f43-133">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="88f43-134">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="88f43-134">Workaround</span></span>

<span data-ttu-id="88f43-135">Eseguire una delle azioni NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="88f43-135">Perform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="88f43-136">Aprire l'interfaccia utente di Gestione pacchetti - fare clic con il pulsante destro del mouse su `References` e scegliere `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="88f43-136">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="88f43-137">Aprire la console di Gestione pacchetti - Da `Tools > NuGet Package Manager` selezionare `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="88f43-137">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="88f43-138">Eseguire un ripristino NuGet - Fare clic con il pulsante destro del mouse sul nodo della soluzione in Esplora soluzioni e scegliere `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="88f43-138">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="88f43-139">Compilare il progetto, ovvero un altro modo per attivare un ripristino NuGet</span><span class="sxs-lookup"><span data-stu-id="88f43-139">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="88f43-140">A questo punto, l'opzione di migrazione dovrebbe essere visibile.</span><span class="sxs-lookup"><span data-stu-id="88f43-140">You should now be able to see the migration option.</span></span> <span data-ttu-id="88f43-141">Si noti che questa opzione non è supportata e non verrà visualizzata per i tipi di progetto ASP.NET e C++.</span><span class="sxs-lookup"><span data-stu-id="88f43-141">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>
<span data-ttu-id="88f43-142">Nota: questo problema è stato risolto in Visual Studio 2017 15.9 Preview 3.</span><span class="sxs-lookup"><span data-stu-id="88f43-142">Note: This has been fixed in VS 2017 15.9 Preview 3</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="88f43-143">Problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="88f43-143">Issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="88f43-144">Bug</span><span class="sxs-lookup"><span data-stu-id="88f43-144">Bugs</span></span>
#### <a name="signing"></a><span data-ttu-id="88f43-145">Firma</span><span class="sxs-lookup"><span data-stu-id="88f43-145">Signing</span></span>
* <span data-ttu-id="88f43-146">Firma: installazione di un pacchetto firmato in un ambiente offline [#7008](https://github.com/NuGet/Home/issues/7008) - Corretto nella versione 4.8.1</span><span class="sxs-lookup"><span data-stu-id="88f43-146">Signing: Installing signed package in offline environment [#7008](https://github.com/NuGet/Home/issues/7008) -- Fixed in 4.8.1</span></span>
* <span data-ttu-id="88f43-147">Firma: controllo dell'URL non corretto - [#7174](https://github.com/NuGet/Home/issues/7174)</span><span class="sxs-lookup"><span data-stu-id="88f43-147">Signing:  incorrect URL check - [#7174](https://github.com/NuGet/Home/issues/7174)</span></span>
* <span data-ttu-id="88f43-148">Firma: controllo dell'integrità di un pacchetto in RepositorySignatureVerifier quando il pacchetto è controfirmato nel repository - [#6926](https://github.com/NuGet/Home/issues/6926)</span><span class="sxs-lookup"><span data-stu-id="88f43-148">Signing:  check package integrity in RepositorySignatureVerifier when package is repository countersigned - [#6926](https://github.com/NuGet/Home/issues/6926)</span></span>
* <span data-ttu-id="88f43-149">"Il controllo dell'integrità del pacchetto non è riuscito"</span><span class="sxs-lookup"><span data-stu-id="88f43-149">"Package Integrity check failed."</span></span> <span data-ttu-id="88f43-150">dovrebbe includere nel messaggio l'ID pacchetto (e il codice di errore) - [#6944](https://github.com/NuGet/Home/issues/6944)</span><span class="sxs-lookup"><span data-stu-id="88f43-150">should have package ID in message (and error code) - [#6944](https://github.com/NuGet/Home/issues/6944)</span></span>
* <span data-ttu-id="88f43-151">Il controllo del pacchetto firmato nel repository consente pacchetti firmati da un certificato diverso - [#6884](https://github.com/NuGet/Home/issues/6884)</span><span class="sxs-lookup"><span data-stu-id="88f43-151">Repository signed package verification allows packages signed by different certificate - [#6884](https://github.com/NuGet/Home/issues/6884)</span></span>
* <span data-ttu-id="88f43-152">NuGet - Firma - L'URL di timestamp non può essere https:// ?</span><span class="sxs-lookup"><span data-stu-id="88f43-152">NuGet - Signing - Timestamp URL can not be https:// ?</span></span><span data-ttu-id="88f43-153"> - [#6871](https://github.com/NuGet/Home/issues/6871)</span><span class="sxs-lookup"><span data-stu-id="88f43-153"> - [#6871](https://github.com/NuGet/Home/issues/6871)</span></span>
* <span data-ttu-id="88f43-154">Assenza di NullRef in uno scenario di creazione di pacchetti NuSpec, opzioni migliorate - [#6866](https://github.com/NuGet/Home/issues/6866)</span><span class="sxs-lookup"><span data-stu-id="88f43-154">Don't NullRef in NuSpec packing scenario, also improve options - [#6866](https://github.com/NuGet/Home/issues/6866)</span></span>
* <span data-ttu-id="88f43-155">La memoria non è valida durante l'aggiornamento delle informazioni sul firmatario in caso di aggiunta di timestamp alla controfirma - [#6840](https://github.com/NuGet/Home/issues/6840)</span><span class="sxs-lookup"><span data-stu-id="88f43-155">Memory is invalid while updating signer info when adding timestamp to countersignature - [#6840](https://github.com/NuGet/Home/issues/6840)</span></span>
* <span data-ttu-id="88f43-156">Firma: rimuovere le eccezioni CTL - [#6794](https://github.com/NuGet/Home/issues/6794)</span><span class="sxs-lookup"><span data-stu-id="88f43-156">Signing:  remove CTL exceptions - [#6794](https://github.com/NuGet/Home/issues/6794)</span></span>
* <span data-ttu-id="88f43-157">Firma: contentUrl DEVE essere HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)</span><span class="sxs-lookup"><span data-stu-id="88f43-157">Signing:  contentUrl MUST be HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)</span></span>
* <span data-ttu-id="88f43-158">Firma: SignedPackageVerifierSettings.VSClientDefaultPolicy è inutilizzato - [#6601](https://github.com/NuGet/Home/issues/6601)</span><span class="sxs-lookup"><span data-stu-id="88f43-158">Signing:  SignedPackageVerifierSettings.VSClientDefaultPolicy is unused - [#6601](https://github.com/NuGet/Home/issues/6601)</span></span>


#### <a name="pack"></a><span data-ttu-id="88f43-159">Pacchetto</span><span class="sxs-lookup"><span data-stu-id="88f43-159">Pack</span></span>
* <span data-ttu-id="88f43-160">Il ripristino e la compilazione non sono necessari quando si usa dotnet.exe per comprimere nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)</span><span class="sxs-lookup"><span data-stu-id="88f43-160">restore and build should not be needed when using dotnet.exe to pack nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)</span></span>
* <span data-ttu-id="88f43-161">Consentire token di sostituzione vuoti in NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)</span><span class="sxs-lookup"><span data-stu-id="88f43-161">Allow empty replacement tokens in NuspecProperties  - [#6722](https://github.com/NuGet/Home/issues/6722)</span></span>
* <span data-ttu-id="88f43-162">PackTask genera un'eccezione NullReferenceException quando viene specificato NuspecProperties - [#4649](https://github.com/NuGet/Home/issues/4649)</span><span class="sxs-lookup"><span data-stu-id="88f43-162">PackTask throws NullReferenceException when NuspecProperties is specified - [#4649](https://github.com/NuGet/Home/issues/4649)</span></span>

#### <a name="accessibility"></a><span data-ttu-id="88f43-163">Accessibilità</span><span class="sxs-lookup"><span data-stu-id="88f43-163">Accessibility</span></span>
* <span data-ttu-id="88f43-164">[Accessibilità] La stringa "Versione provvisoria" sotto il pulsante del pacchetto è coperta dalla descrizione del pacchetto nell'interfaccia utente di Gestione pacchetti - [#4504](https://github.com/NuGet/Home/issues/4504)</span><span class="sxs-lookup"><span data-stu-id="88f43-164">[Accessibility] String ‘Prerelease’ under package button is covered by its package description in PM UI - [#4504](https://github.com/NuGet/Home/issues/4504)</span></span>
* <span data-ttu-id="88f43-165">[Accessibilità] Il menu a discesa e il pulsante Impostazioni dell'origine del pacchetto sono troncati quando si seleziona "Microsoft Visual Studio Offline Packages" nell'interfaccia utente di Gestione pacchetti - [#4502](https://github.com/NuGet/Home/issues/4502)</span><span class="sxs-lookup"><span data-stu-id="88f43-165">[Accessibility] Package source drop down and settings button truncated when selecting ‘Microsoft Visual Studio Offline Packages’ in PM UI - [#4502](https://github.com/NuGet/Home/issues/4502)</span></span>

#### <a name="powershell-management-console-pmc"></a><span data-ttu-id="88f43-166">Console di gestione di PowerShell (PMC)</span><span class="sxs-lookup"><span data-stu-id="88f43-166">Powershell Management Console (PMC)</span></span>
* <span data-ttu-id="88f43-167">`Update-Package` ignora l'intervallo di versioni PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)</span><span class="sxs-lookup"><span data-stu-id="88f43-167">`Update-Package` ignores PackageReference version range - [#6775](https://github.com/NuGet/Home/issues/6775)</span></span>
* <span data-ttu-id="88f43-168">Problema di reinstallazione a livello di soluzione con `Update-Package -reinstall` - [#3127](https://github.com/NuGet/Home/issues/3127)</span><span class="sxs-lookup"><span data-stu-id="88f43-168">`Update-Package -reinstall` solution wide issue - [#3127](https://github.com/NuGet/Home/issues/3127)</span></span>
* <span data-ttu-id="88f43-169">`Update-Package [packagename] -reinstall` reinstalla tutti i pacchetti anziché solo quello denominato - [#737](https://github.com/NuGet/Home/issues/737)</span><span class="sxs-lookup"><span data-stu-id="88f43-169">`Update-Package [packagename] -reinstall` reinstalls all packages instead of just the named one - [#737](https://github.com/NuGet/Home/issues/737)</span></span>
* <span data-ttu-id="88f43-170">Possibilità di eseguire l'aggiornamento a un pacchetto NuGet non in elenco dalla console di Gestione pacchetti - [#4553](https://github.com/NuGet/Home/issues/4553)</span><span class="sxs-lookup"><span data-stu-id="88f43-170">Can update to unlisted NuGet package from the Package Manager Console - [#4553](https://github.com/NuGet/Home/issues/4553)</span></span>

#### <a name="misc"></a><span data-ttu-id="88f43-171">Varie</span><span class="sxs-lookup"><span data-stu-id="88f43-171">Misc</span></span>
* <span data-ttu-id="88f43-172">Per correggere `NuGet update self` NuGet.Commandline nupkg non deve essere semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)</span><span class="sxs-lookup"><span data-stu-id="88f43-172">To fix `NuGet update self` NuGet.Commandline nupkg should not be semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)</span></span>
* <span data-ttu-id="88f43-173">Migliorare le esperienze con gli errori di installazione di NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)</span><span class="sxs-lookup"><span data-stu-id="88f43-173">Improve experiences with NU1107 install failures - [#7107](https://github.com/NuGet/Home/issues/7107)</span></span>
* <span data-ttu-id="88f43-174">La serializzazione di GetAuthenticationCredentialRequest è errata - [#6983](https://github.com/NuGet/Home/issues/6983)</span><span class="sxs-lookup"><span data-stu-id="88f43-174">The serialization of GetAuthenticationCredentialRequest is incorrect - [#6983](https://github.com/NuGet/Home/issues/6983)</span></span>
* <span data-ttu-id="88f43-175">NuGet Visual Studio AsyncPackage non viene caricato quando è inizializzato all'esterno del thread dell'interfaccia utente - [#6976](https://github.com/NuGet/Home/issues/6976)</span><span class="sxs-lookup"><span data-stu-id="88f43-175">NuGet Visual Studio AsyncPackage fails to load when initialized off the UI thread - [#6976](https://github.com/NuGet/Home/issues/6976)</span></span>
* <span data-ttu-id="88f43-176">Durante il ripristino vengono segnalati errori fuorvianti sulla necessità di project.json - [#6959](https://github.com/NuGet/Home/issues/6959)</span><span class="sxs-lookup"><span data-stu-id="88f43-176">Restore is reporting misleading errors stating project.json is needed - [#6959](https://github.com/NuGet/Home/issues/6959)</span></span>
* <span data-ttu-id="88f43-177">Interfaccia utente di Gestione pacchetti: pulsante OK in Anteprima modifiche non utilizzabile automaticamente dalla tastiera - [#6893](https://github.com/NuGet/Home/issues/6893)</span><span class="sxs-lookup"><span data-stu-id="88f43-177">Package manager UI : preview changes, ok button not automatically useable by keyboard - [#6893](https://github.com/NuGet/Home/issues/6893)</span></span>
* <span data-ttu-id="88f43-178">RestoreSources ignorati per il progetto con riferimenti p2p - [#6776](https://github.com/NuGet/Home/issues/6776)</span><span class="sxs-lookup"><span data-stu-id="88f43-178">RestoreSources are ignored for project with p2p references - [#6776](https://github.com/NuGet/Home/issues/6776)</span></span>
* <span data-ttu-id="88f43-179">La creazione di un progetto di unit test con il modello .NET Framework aprirà un modello di progetto precedente con packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)</span><span class="sxs-lookup"><span data-stu-id="88f43-179">Creating unit test project using .NET Framework template will open older project model with packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)</span></span>
* <span data-ttu-id="88f43-180">Consentire al riferimento progetto di eseguire l'override delle dipendenze del pacchetto - [#6536](https://github.com/NuGet/Home/issues/6536)</span><span class="sxs-lookup"><span data-stu-id="88f43-180">allow project reference to override package dependency - [#6536](https://github.com/NuGet/Home/issues/6536)</span></span>
* <span data-ttu-id="88f43-181">Esporre NoDefaultExcludes nell'attività di MSBuild - [#6450](https://github.com/NuGet/Home/issues/6450)</span><span class="sxs-lookup"><span data-stu-id="88f43-181">Expose NoDefaultExcludes in MSBuild task - [#6450](https://github.com/NuGet/Home/issues/6450)</span></span>
* <span data-ttu-id="88f43-182">Il messaggio di stato per "Cancella tutte le cache NuGet" può essere nascosto nel ridimensionamento della finestra - [#5938](https://github.com/NuGet/Home/issues/5938)</span><span class="sxs-lookup"><span data-stu-id="88f43-182">Status message for "Clear All NuGet Cache(s)" can be hidden on window resize - [#5938](https://github.com/NuGet/Home/issues/5938)</span></span>


[<span data-ttu-id="88f43-183">Elenco di tutti i problemi corretti in questa versione</span><span class="sxs-lookup"><span data-stu-id="88f43-183">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")