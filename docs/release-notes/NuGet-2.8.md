---
title: Note sulla versione 2.8 di NuGet
description: Note sulla versione per NuGet 2.8 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f472f1370bfedaf04ebe889c0da01155b8aec22
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="bbd4f-103">Note sulla versione 2.8 di NuGet</span><span class="sxs-lookup"><span data-stu-id="bbd4f-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="bbd4f-104">[Note sulla versione di NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="bbd4f-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="bbd4f-105">NuGet 2.8 è stato rilasciato il 29 gennaio 2014.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="bbd4f-106">Riconoscimenti</span><span class="sxs-lookup"><span data-stu-id="bbd4f-106">Acknowledgements</span></span>

1. <span data-ttu-id="bbd4f-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="bbd4f-108">[#3466](https://nuget.codeplex.com/workitem/3466) : quando i pacchetti, verifica dell'Id di pacchetti di dipendenza di compressione.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="bbd4f-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="bbd4f-110">[#2379](https://nuget.codeplex.com/workitem/2379) -rimuovere il suffisso $metadata quando persistening feed credenziali.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="bbd4f-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="bbd4f-112">[#3538](http://nuget.codeplex.com/workitem/3538) - supporto di specifica di file di progetto per il comando di aggiornamento nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="bbd4f-113">Alessandro Gonzalez</span><span class="sxs-lookup"><span data-stu-id="bbd4f-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="bbd4f-114">[#3536](http://nuget.codeplex.com/workitem/3536) -token di sostituzione non passato con - IncludeReferencedProjects.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="bbd4f-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="bbd4f-116">[#3677](http://nuget.codeplex.com/workitem/3677) -correggere nuget.push generando OutOfMemoryException quando il push di pacchetto di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="bbd4f-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="bbd4f-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="bbd4f-118">[#3666](http://nuget.codeplex.com/workitem/3666) -percorso di destinazione non corretto di correzione quando progetto fa riferimento a un altro progetto CLI/C++.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="bbd4f-119">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="bbd4f-120">[#3639](https://nuget.codeplex.com/workitem/3639) -Consenti pacchetti da installare come dipendenze di sviluppo per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="bbd4f-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="bbd4f-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="bbd4f-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="bbd4f-122">[#3717](https://nuget.codeplex.com/workitem/3717) -rimuovere implicita aggiornamento alla versione di patch più recente</span><span class="sxs-lookup"><span data-stu-id="bbd4f-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="bbd4f-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="bbd4f-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="bbd4f-124">Alcune correzioni di bug e miglioramenti per NuGet.Server, il comando di nuget.exe mirror e di altri utenti.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="bbd4f-125">Questa attività sono state eseguite alcuni mesi, con Gregory lavorando con noi la temporizzazione di destra per integrare dati master per 2.8.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="bbd4f-126">Patch di risoluzione delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="bbd4f-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="bbd4f-127">Durante la risoluzione delle dipendenze del pacchetto, NuGet è sempre implementata una strategia di selezionando la versione del pacchetto principale e secondario più bassa che soddisfa le dipendenze del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="bbd4f-128">A differenza delle versioni principale e secondaria, tuttavia, la versione di patch è stato risolto sempre la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="bbd4f-129">Il comportamento è stato malintenzionato, creata una mancanza di determinismo per l'installazione di pacchetti con dipendenze.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="bbd4f-130">Si consideri l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="bbd4f-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="bbd4f-131">In questo esempio, anche se Developer1 e Developer2 installati PackageA@1.0.0, ogni backup terminata con una versione diversa di PackageB.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="bbd4f-132">NuGet 2.8 modifica questo comportamento predefinito in modo che il comportamento di risoluzione delle dipendenze per le versioni di patch sia consistente con il comportamento per le versioni principale e secondarie.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="bbd4f-133">Nell'esempio precedente, quindi, PackageB@1.0.0 verrà installato in seguito all'installazione PackageA@1.0.0, indipendentemente dalla versione di patch più recente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="bbd4f-134">DependencyVersion - opzione</span><span class="sxs-lookup"><span data-stu-id="bbd4f-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="bbd4f-135">Anche se cambia NuGet 2.8 il _predefinito_ comportamento per la risoluzione delle dipendenze, aggiunge anche un controllo più preciso il processo di risoluzione dipendenza tramite l'opzione - DependencyVersion nella console di gestione di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="bbd4f-136">L'opzione consente di risolvere le dipendenze per la versione minima di possibili (comportamento predefinito), la versione più recente, o il minore più alto o la versione di patch.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="bbd4f-137">Questa opzione funziona solo per il pacchetto di installazione del comando di powershell.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-137">This switch only works for install-package in the powershell command.</span></span>

![Opzione DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="bbd4f-139">Attributo DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="bbd4f-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="bbd4f-140">Oltre all'opzione - DependencyVersion sopra descritti, NuGet è inoltre consentito per la possibilità di impostare un nuovo attributo nel file config che definisce che cos'è il valore predefinito, se il parametro - DependencyVersion non viene specificato in una chiamata di pacchetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="bbd4f-141">Questo valore verrà rispettato anche dalla finestra di dialogo Gestione pacchetti NuGet per tutte le operazioni di pacchetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="bbd4f-142">Per impostare questo valore, aggiungere l'attributo di sotto del file NuGet. config:</span><span class="sxs-lookup"><span data-stu-id="bbd4f-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="bbd4f-143">Operazioni di NuGet anteprima con - whatif</span><span class="sxs-lookup"><span data-stu-id="bbd4f-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="bbd4f-144">Alcuni pacchetti NuGet possono avere grafici delle dipendenze complete e di conseguenza, può essere utile durante un'installazione, disinstallare o operazione visualizzare prima di tutto ciò che accadrà di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="bbd4f-145">NuGet 2.8 aggiunge l'opzione - whatif di PowerShell di standard per il pacchetto di installazione, disinstallare-package e comandi di pacchetto di aggiornamento per abilitare la chiusura di pacchetti a cui applicare il comando intera visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="bbd4f-146">Ad esempio, in esecuzione `install-package Microsoft.AspNet.WebApi -whatif` in un Web ASP.NET vuoto applicazione produce il seguente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a><span data-ttu-id="bbd4f-147">Pacchetto di downgrade</span><span class="sxs-lookup"><span data-stu-id="bbd4f-147">Downgrade Package</span></span>

<span data-ttu-id="bbd4f-148">Non è insolito per installare una versione non definitiva di un pacchetto per analizzare nuove funzionalità e si decide di ripristinare l'ultima versione stabile.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="bbd4f-149">Prima di NuGet 2.8, questo è un processo in più passaggi di disinstallare il pacchetto non definitiva e le relative dipendenze e quindi installare la versione precedente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="bbd4f-150">Con NuGet 2.8, tuttavia, il pacchetto di aggiornamento verrà ora eseguito il rollback della chiusura dell'intero pacchetto (ad esempio struttura delle dipendenze del pacchetto) alla versione precedente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="bbd4f-151">Dipendenze di sviluppo</span><span class="sxs-lookup"><span data-stu-id="bbd4f-151">Development Dependencies</span></span>

<span data-ttu-id="bbd4f-152">Molti tipi diversi di funzionalità possono essere recapitati come pacchetti NuGet - tra cui gli strumenti utilizzati per ottimizzare il processo di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="bbd4f-153">Questi componenti, anche se possono essere strumentale lo sviluppo di un nuovo pacchetto, non devono essere considerati una dipendenza del nuovo pacchetto quando viene pubblicato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="bbd4f-154">NuGet 2.8 consente a un pacchetto identificare se stessa nella `.nuspec` file come un developmentDependency.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="bbd4f-155">Durante l'installazione, verranno inoltre aggiunto i metadati per il `packages.config` file del progetto in cui è stato installato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="bbd4f-156">Quando che `packages.config` file viene analizzato in un secondo momento le dipendenze di NuGet durante `nuget.exe pack`, verrà escluso tali dipendenze contrassegnati come dipendenze di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="bbd4f-157">File di singoli file Packages. config per le diverse piattaforme</span><span class="sxs-lookup"><span data-stu-id="bbd4f-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="bbd4f-158">Quando si sviluppano applicazioni per più piattaforme di destinazione, è comune disporre di file di progetto diversi per ognuno degli ambienti di compilazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="bbd4f-159">È inoltre comune per utilizzare i pacchetti NuGet diversi nei file di progetto diverso, come pacchetti con vari livelli di supporto per le diverse piattaforme.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="bbd4f-160">NuGet 2.8 fornisce un supporto migliorato per questo scenario tramite la creazione di diversi `packages.config` file per file di progetto specifico della piattaforma diversi.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![Più file package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="bbd4f-162">Fallback alla Cache locale</span><span class="sxs-lookup"><span data-stu-id="bbd4f-162">Fallback to Local Cache</span></span>

<span data-ttu-id="bbd4f-163">Anche se i pacchetti NuGet vengono in genere utilizzati da una raccolta remota, ad esempio [raccolta NuGet](http://www.nuget.org/) utilizzando una connessione di rete, esistono molti scenari in cui il client non è connesso.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="bbd4f-164">Senza una connessione di rete, il client NuGet non è in grado di installare correttamente i pacchetti, anche quando i pacchetti sono stati già nel computer client nella cache locale NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="bbd4f-165">NuGet 2.8 aggiunge automatica della cache fallback nella console di gestione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="bbd4f-166">Ad esempio, quando la scheda di rete di disconnessione e l'installazione di jQuery, la console mostra quanto segue:</span><span class="sxs-lookup"><span data-stu-id="bbd4f-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="bbd4f-167">La funzionalità di fallback della cache non richiedono alcun argomento di comando specifico.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="bbd4f-168">Inoltre, cache fallback attualmente funziona solo nella console di gestione di pacchetti: il comportamento non funziona nella finestra di dialogo Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="bbd4f-169">Gli aggiornamenti del Client NuGet WebMatrix</span><span class="sxs-lookup"><span data-stu-id="bbd4f-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="bbd4f-170">Insieme a NuGet 2.8, l'estensione NuGet di WebMatrix è stato inoltre aggiornato per includere molte delle principali funzionalità offerte da [NuGet 2.5](../release-notes/nuget-2.5.md).</span><span class="sxs-lookup"><span data-stu-id="bbd4f-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="bbd4f-171">Nuove funzionalità includono quelle, ad esempio 'Update ' al, ' minimo NuGet alla versione' e consentendo la sovrascrittura dei file di contenuto.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="bbd4f-172">Per aggiornare l'estensione Gestione pacchetti NuGet in WebMatrix 3:</span><span class="sxs-lookup"><span data-stu-id="bbd4f-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="bbd4f-173">Aprire WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="bbd4f-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="bbd4f-174">Fare clic sull'icona di estensioni della barra multifunzione</span><span class="sxs-lookup"><span data-stu-id="bbd4f-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="bbd4f-175">Selezionare la scheda di aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="bbd4f-175">Select the Updates tab</span></span>
1. <span data-ttu-id="bbd4f-176">Fare clic per aggiornare Gestione pacchetti NuGet per 2.5.0</span><span class="sxs-lookup"><span data-stu-id="bbd4f-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="bbd4f-177">Chiudere e riavviare WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="bbd4f-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="bbd4f-178">Questo è primo rilascio del team NuGet dell'estensione Gestione pacchetti NuGet per WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="bbd4f-179">Il codice è stato recentemente fornito da Microsoft in NuGet progetto open source.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="bbd4f-180">In precedenza, l'integrazione di NuGet è stato compilato in WebMatrix, e non è possibile aggiornare fuori banda da WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="bbd4f-181">È ora disponibile la funzionalità per aggiornare ulteriormente insieme il resto degli strumenti client di NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bbd4f-182">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="bbd4f-182">Bug Fixes</span></span>

<span data-ttu-id="bbd4f-183">Una delle principali correzioni di bug apportate stato miglioramento delle prestazioni nel pacchetto di aggiornamento-comando.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="bbd4f-184">Oltre a queste funzionalità e risolvere il problema di prestazioni menzionati in precedenza, questa versione di NuGet include anche molte altre correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="bbd4f-185">Si sono verificati problemi di totali 181 risolti nella versione.</span><span class="sxs-lookup"><span data-stu-id="bbd4f-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="bbd4f-186">Per un elenco completo delle operazioni elementi fissa NuGet 2.8,. visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span><span class="sxs-lookup"><span data-stu-id="bbd4f-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>