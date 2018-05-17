---
title: Versioni non definitive nei pacchetti NuGet
description: Linee guida per la compilazione di versioni non definitive dei pacchetti
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a4540d29d9ca01f98ee5d1786e8a175ee0ea79f4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="e267e-103">Compilazione di versioni non definitive dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="e267e-103">Building pre-release packages</span></span>

<span data-ttu-id="e267e-104">Ogni volta che si rilascia un pacchetto aggiornato con un nuovo numero di versione, NuGet considera tale versione l'ultima versione stabile, come illustrato, ad esempio, nell'interfaccia utente di Gestione pacchetti all'interno di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e267e-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Interfaccia utente di Gestione pacchetti che mostra l'ultima versione stabile](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="e267e-106">Una versione stabile è una versione considerata sufficientemente affidabile da poter essere usata in ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e267e-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="e267e-107">L'ultima versione stabile è anche quella che verrà installata come aggiornamento del pacchetto oppure durante il ripristino del pacchetto (soggetto a vincoli, come descritto in [Reinstallazione e aggiornamento di pacchetti](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="e267e-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="e267e-108">Per supportare il ciclo di vita di rilascio del software, NuGet 1.6 e versioni successive consentono la distribuzione di pacchetti in versione non definitiva, in cui il numero di versione include un suffisso per il controllo delle versioni semantico, ad esempio `-alpha`, `-beta` o `-rc`.</span><span class="sxs-lookup"><span data-stu-id="e267e-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="e267e-109">Per altre informazioni, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="e267e-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="e267e-110">È possibile specificare tali versioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="e267e-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="e267e-111">File `.nuspec`: includere il suffisso di versione semantico nell'elemento `version`:</span><span class="sxs-lookup"><span data-stu-id="e267e-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="e267e-112">Attributi dell'assembly: quando si compila un pacchetto da un progetto di Visual Studio (`.csproj` o `.vbproj`), usare `AssemblyInformationalVersionAttribute` per specificare la versione:</span><span class="sxs-lookup"><span data-stu-id="e267e-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="e267e-113">NuGet preleva questo valore anziché quello specificato nell'attributo `AssemblyVersion`, che non supporta il versionamento semantico.</span><span class="sxs-lookup"><span data-stu-id="e267e-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="e267e-114">Quando si è pronti per rilasciare una versione stabile, è sufficiente rimuovere il suffisso e il pacchetto ottiene la precedenza rispetto a qualsiasi altra versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="e267e-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="e267e-115">Vedere di nuovo [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="e267e-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="e267e-116">Installazione e aggiornamento di pacchetti in versione non definitiva</span><span class="sxs-lookup"><span data-stu-id="e267e-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="e267e-117">Per impostazione predefinita, NuGet non include le versioni non definitive quando si lavora con i pacchetti, ma è possibile modificare questo comportamento come segue:</span><span class="sxs-lookup"><span data-stu-id="e267e-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="e267e-118">**Interfaccia utente di Gestione pacchetti in Visual Studio**: nell'interfaccia utente di **Gestisci pacchetti NuGet** selezionare la casella di controllo **Includi versione preliminare**:</span><span class="sxs-lookup"><span data-stu-id="e267e-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Casella di controllo Includi versione preliminare in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="e267e-120">La selezione o la deselezione di questa casella di controllo aggiorna l'interfaccia utente di Gestione pacchetti e l'elenco delle versioni disponibili che è possibile installare.</span><span class="sxs-lookup"><span data-stu-id="e267e-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="e267e-121">**Console di Gestione pacchetti**: usare l'opzione `-IncludePrerelease` con i comandi `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="e267e-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="e267e-122">Vedere [Informazioni di riferimento su PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e267e-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="e267e-123">**Interfaccia della riga di comando di NuGet**: usare l'opzione `-prerelease` con i comandi `install`, `update`, `delete` e `mirror`.</span><span class="sxs-lookup"><span data-stu-id="e267e-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="e267e-124">Vedere [NuGet CLI reference](../tools/nuget-exe-cli-reference.md) (Informazioni di riferimento sull'interfaccia della riga di comando di NuGet).</span><span class="sxs-lookup"><span data-stu-id="e267e-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="e267e-125">Versionamento semantico</span><span class="sxs-lookup"><span data-stu-id="e267e-125">Semantic versioning</span></span>

<span data-ttu-id="e267e-126">La [convenzione di versionamento semantico o SemVer](http://semver.org/spec/v1.0.0.html) descrive come usare le stringhe nei numeri di versione per indicare il significato del codice sottostante.</span><span class="sxs-lookup"><span data-stu-id="e267e-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="e267e-127">In questa convenzione, ogni versione è composta di tre parti, `Major.Minor.Patch`, con il significato seguente:</span><span class="sxs-lookup"><span data-stu-id="e267e-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="e267e-128">`Major`: modifiche importanti</span><span class="sxs-lookup"><span data-stu-id="e267e-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="e267e-129">`Minor`: nuove funzionalità, ma compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="e267e-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="e267e-130">`Patch`: solo correzioni di bug compatibili con le versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="e267e-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="e267e-131">Le versioni non definitive vengono quindi contrassegnate aggiungendo un trattino e una stringa dopo il numero di patch.</span><span class="sxs-lookup"><span data-stu-id="e267e-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="e267e-132">Tecnicamente, è possibile usare *qualsiasi* stringa dopo il trattino e NuGet considererà il pacchetto come in versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="e267e-132">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="e267e-133">NuGet visualizza quindi il numero di versione completo nell'interfaccia utente applicabile, lasciando ai consumer l'interpretazione del significato.</span><span class="sxs-lookup"><span data-stu-id="e267e-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="e267e-134">Tenendo conto di questo aspetto, è in genere consigliabile seguire convenzioni di denominazione riconosciute, come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="e267e-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="e267e-135">`-alpha`: versione alfa, usata in genere per lavori in corso e sperimentazione</span><span class="sxs-lookup"><span data-stu-id="e267e-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="e267e-136">`-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.</span><span class="sxs-lookup"><span data-stu-id="e267e-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="e267e-137">`-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.</span><span class="sxs-lookup"><span data-stu-id="e267e-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="e267e-138">NuGet 4.3.0+ supporta il [versionamento semantico v2.0.0](http://semver.org/spec/v2.0.0.html), ovvero numeri di versione non definitiva con la notazione con punto, come in `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="e267e-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="e267e-139">La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="e267e-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="e267e-140">Nelle versioni precedenti di NuGet è possibile usare un formato come `1.0.1-build23`, ma viene sempre considerato una versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="e267e-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="e267e-141">Indipendentemente dai suffissi usati, tuttavia, NuGet stabilirà sempre la precedenza in ordine alfabetico inverso:</span><span class="sxs-lookup"><span data-stu-id="e267e-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="e267e-142">Come illustrato, la versione senza suffisso avrà sempre la precedenza rispetto alle versioni non definitive.</span><span class="sxs-lookup"><span data-stu-id="e267e-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="e267e-143">Si noti inoltre che se si usano suffissi numerici con i tag di versione non definitiva che potrebbero usare numeri a due cifre (o più), è buona norma usare zeri iniziali come in beta01 e beta05 per assicurare un ordinamento corretto con l'aumentare dei numeri.</span><span class="sxs-lookup"><span data-stu-id="e267e-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>