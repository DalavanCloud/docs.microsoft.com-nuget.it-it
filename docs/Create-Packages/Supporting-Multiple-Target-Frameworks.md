---
title: Multitargeting per i pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet."
keywords: "Selezione di un pacchetto NuGet come destinazione, versioni di .NET Framework, NuGet e .NET, selezione di più framework come destinazione, creazione di pacchetti NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 723dbcc12ecc4e16d2ba4662559f107b9b22e2c2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="89e59-104">Supporto di più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="89e59-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="89e59-105">*Per i progetti .NET Core che usano NuGet 4.0+, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md) per informazioni dettagliate sul crosstargeting.*</span><span class="sxs-lookup"><span data-stu-id="89e59-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="89e59-106">Molte librerie hanno come destinazione una versione specifica di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="89e59-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="89e59-107">Ad esempio, si potrebbe disporre di una versione della libreria specifica per UWP e di un'altra versione che sfrutta le funzionalità di .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="89e59-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="89e59-108">Per far fronte a questa situazione, NuGet supporta l'inserimento di più versioni della stessa libreria in un singolo pacchetto quando si usa il metodo della directory di lavoro basata su convenzioni descritto in [Creazione di un pacchetto](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="89e59-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="89e59-109">Struttura di cartelle della versione del framework</span><span class="sxs-lookup"><span data-stu-id="89e59-109">Framework version folder structure</span></span>

<span data-ttu-id="89e59-110">Quando si compila un pacchetto che contiene solo una versione di una libreria o che ha come destinazione più framework, si creano sempre sottocartelle in `lib` usando nomi di framework diversi con distinzione tra maiuscole e minuscole in base alla convenzione seguente:</span><span class="sxs-lookup"><span data-stu-id="89e59-110">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="89e59-111">Per un elenco completo dei nomi supportati, vedere le [informazioni di riferimento sui framework di destinazione](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="89e59-111">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="89e59-112">Non si deve mai disporre di una versione della libreria che non sia specifica di un framework e che sia inserita direttamente nella cartella `lib` radice</span><span class="sxs-lookup"><span data-stu-id="89e59-112">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="89e59-113">(questa funzionalità è supportata solo con `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="89e59-113">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="89e59-114">Così facendo, la si renderebbe compatibile con qualsiasi framework di destinazione consentendone l'installazione in qualunque posizione, comportando probabilmente errori di runtime imprevisti.</span><span class="sxs-lookup"><span data-stu-id="89e59-114">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="89e59-115">L'aggiunta di assembly nella cartella radice (ad esempio `lib\abc.dll`) o nelle sottocartelle (ad esempio `lib\abc\abc.dll`) è deprecata e viene ignorata quando si usa il formato PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="89e59-115">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="89e59-116">Ad esempio, la struttura di cartelle seguente supporta quattro versioni di un assembly che sono specifiche del framework:</span><span class="sxs-lookup"><span data-stu-id="89e59-116">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="89e59-117">Per includere facilmente tutti i file durante la compilazione del pacchetto, usare un carattere jolly `**` ricorsivo nella sezione `<files>` di `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="89e59-117">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="89e59-118">Cartelle specifiche dell'architettura</span><span class="sxs-lookup"><span data-stu-id="89e59-118">Architecture-specific folders</span></span>

<span data-ttu-id="89e59-119">Se si dispone di assembly specifici dell'architettura, vale a dire assembly distinti che hanno come destinazione ARM, x86 e x64, è necessario inserirli in una cartella denominata `runtimes` all'interno di sottocartelle denominate `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="89e59-119">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="89e59-120">Ad esempio, la struttura di cartelle seguente potrebbe contenere sia DLL native che gestite che hanno come destinazione Windows 10 e il framework `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="89e59-120">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="89e59-121">Vedere [Creare pacchetti UWP](../guides/create-uwp-packages.md) per un esempio di riferimento a questi file nel manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="89e59-121">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="89e59-122">Corrispondenza tra le versioni di assembly e il framework di destinazione in un progetto</span><span class="sxs-lookup"><span data-stu-id="89e59-122">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="89e59-123">Quando NuGet installa un pacchetto che dispone di più versioni di assembly, tenta di associare il nome del framework dell'assembly con il framework di destinazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="89e59-123">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="89e59-124">Se non viene trovata una corrispondenza, NuGet copia l'assembly per la versione più alta inferiore o uguale al framework di destinazione del progetto, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="89e59-124">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="89e59-125">Se non viene trovato un assembly compatibile, NuGet restituisce un messaggio di errore appropriato.</span><span class="sxs-lookup"><span data-stu-id="89e59-125">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="89e59-126">Si consideri ad esempio la struttura di cartelle seguente in un pacchetto:</span><span class="sxs-lookup"><span data-stu-id="89e59-126">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="89e59-127">Quando si installa questo pacchetto in un progetto che ha come destinazione .NET Framework 4.6, NuGet installa l'assembly nella cartella `net45`, trattandosi della versione più alta disponibile inferiore o uguale alla versione 4.6.</span><span class="sxs-lookup"><span data-stu-id="89e59-127">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="89e59-128">Se il progetto ha come destinazione .NET Framework 4.6.1, invece, NuGet installa l'assembly nella cartella `net461`.</span><span class="sxs-lookup"><span data-stu-id="89e59-128">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="89e59-129">Se il progetto ha come destinazione .NET Framework 4.0 e versioni precedenti, NuGet genera un messaggio di errore appropriato per non avere trovato un assembly compatibile.</span><span class="sxs-lookup"><span data-stu-id="89e59-129">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="89e59-130">Raggruppamento di assembly per versione del framework</span><span class="sxs-lookup"><span data-stu-id="89e59-130">Grouping assemblies by framework version</span></span>

<span data-ttu-id="89e59-131">NuGet copia gli assembly solo da una singola cartella di libreria nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="89e59-131">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="89e59-132">Si supponga ad esempio che un pacchetto abbia la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="89e59-132">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="89e59-133">Quando il pacchetto viene installato in un progetto che ha come destinazione .NET Framework 4.5, `MyAssembly.dll` (v2.0) è l'unico assembly installato.</span><span class="sxs-lookup"><span data-stu-id="89e59-133">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="89e59-134">`MyAssembly.Core.dll` (v1.0) non è installato perché non è elencato nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="89e59-134">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="89e59-135">NuGet ha questo comportamento perché `MyAssembly.Core.dll` potrebbe essere stato unito nella versione 2.0 di `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="89e59-135">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="89e59-136">Se si vuole che `MyAssembly.Core.dll` sia installato per .NET Framework 4.5, inserire una copia nella cartella `net45`.</span><span class="sxs-lookup"><span data-stu-id="89e59-136">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="89e59-137">Raggruppamento di assembly per profilo del framework</span><span class="sxs-lookup"><span data-stu-id="89e59-137">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="89e59-138">NuGet supporta anche la selezione di uno specifico profilo del framework come destinazione accodando un trattino e il nome del profilo alla fine della cartella.</span><span class="sxs-lookup"><span data-stu-id="89e59-138">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="89e59-139">I profili supportati sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="89e59-139">The supported profiles are as follows:</span></span>

- <span data-ttu-id="89e59-140">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="89e59-140">`client`: Client Profile</span></span>
- <span data-ttu-id="89e59-141">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="89e59-141">`full`: Full Profile</span></span>
- <span data-ttu-id="89e59-142">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="89e59-142">`wp`: Windows Phone</span></span>
- <span data-ttu-id="89e59-143">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="89e59-143">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="89e59-144">Determinazione della destinazione NuGet da usare</span><span class="sxs-lookup"><span data-stu-id="89e59-144">Determining which NuGet target to use</span></span>

<span data-ttu-id="89e59-145">Quando si inseriscono in un pacchetto librerie che hanno come destinazione la libreria di classi portabile, può essere difficile determinare quale destinazione NuGet usare nei nomi delle cartelle e nel file `.nuspec`, in particolare se la destinazione è solo un subset della libreria di classi portabile.</span><span class="sxs-lookup"><span data-stu-id="89e59-145">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="89e59-146">Le risorse esterne seguenti possono essere di aiuto:</span><span class="sxs-lookup"><span data-stu-id="89e59-146">The following external resources will help you with this:</span></span>

- <span data-ttu-id="89e59-147">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="89e59-147">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="89e59-148">[Profili della libreria di classi portabile](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabella che enumera i profili della libreria di classi portabile e le destinazioni NuGet equivalenti</span><span class="sxs-lookup"><span data-stu-id="89e59-148">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="89e59-149">[Strumento per i profili della libreria di classi portabile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): strumento da riga di comando per determinare i profili della libreria di classi portabile disponibili nel sistema</span><span class="sxs-lookup"><span data-stu-id="89e59-149">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="89e59-150">File di contenuto e script PowerShell</span><span class="sxs-lookup"><span data-stu-id="89e59-150">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="89e59-151">I file di contenuto modificabili e l'esecuzione degli script sono disponibili solo con il formato `packages.config`. Sono deprecati per tutti gli altri formati e non dovrebbero essere usati per i nuovi pacchetti.</span><span class="sxs-lookup"><span data-stu-id="89e59-151">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="89e59-152">Con `packages.config`, i file di contenuto e gli script PowerShell possono essere raggruppati per framework di destinazione usando la stessa convenzione di cartelle all'interno delle cartelle `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="89e59-152">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="89e59-153">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="89e59-153">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="89e59-154">Se una cartella framework viene lasciata vuota, NuGet non aggiunge riferimenti ad assembly o file di contenuto né esegue script PowerShell per tale framework.</span><span class="sxs-lookup"><span data-stu-id="89e59-154">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="89e59-155">Poiché `init.ps1` viene eseguito a livello di soluzione e indipendentemente dal progetto, deve essere inserito direttamente sotto la cartella `tools`.</span><span class="sxs-lookup"><span data-stu-id="89e59-155">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="89e59-156">Viene ignorato se inserito in una cartella framework.</span><span class="sxs-lookup"><span data-stu-id="89e59-156">It's ignored if placed under a framework folder.</span></span>