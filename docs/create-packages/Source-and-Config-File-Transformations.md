---
title: Trasformazioni di codice sorgente e file di configurazione per i pacchetti NuGet
description: Informazioni dettagliate sulla capacità per i pacchetti NuGet di trasformare il codice sorgente e i file di configurazione (XML) durante l'installazione.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="f5669-103">Trasformazioni di codice sorgente e file di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5669-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="f5669-104">Per i progetti che usano `packages.config`, NuGet supporta la capacità di eseguire trasformazioni del codice sorgente e dei file di configurazione in fase di installazione e disinstallazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f5669-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="f5669-105">Vengono applicate solo le trasformazioni del codice sorgente quando viene installato un pacchetto in un progetto tramite [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="f5669-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="f5669-106">Una **trasformazione di codice sorgente** applica una sostituzione dei token unidirezionale ai file nella cartella `content` o `contentFiles` del pacchetto (`content` per i clienti che usano `packages.config` e `contentFiles` per `PackageReference`) quando il pacchetto viene installato, dove i token fanno riferimento alle [proprietà di progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5669-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="f5669-107">Ciò consente di inserire un file nello spazio dei nomi del progetto o di personalizzare il codice inserito in genere in `global.asax` in un progetto ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f5669-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="f5669-108">Una **trasformazione di file di configurazione** consente di modificare i file già esistenti in un progetto di destinazione, come `web.config` e `app.config`.</span><span class="sxs-lookup"><span data-stu-id="f5669-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="f5669-109">Ad esempio, potrebbe essere necessario aggiungere un elemento per il pacchetto alla sezione `modules` del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5669-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="f5669-110">Questa trasformazione viene eseguita includendo nel pacchetto file speciali che descrivono le sezioni da aggiungere ai file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5669-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="f5669-111">Quando si disinstalla un pacchetto, queste stesse modifiche vengono invertite, rendendola una trasformazione bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="f5669-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="f5669-112">Specifica di trasformazioni di codice sorgente</span><span class="sxs-lookup"><span data-stu-id="f5669-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="f5669-113">I file da inserire dal pacchetto nel progetto devono trovarsi all'interno delle cartelle `content` e `contentFiles` del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="f5669-114">Ad esempio, se si vuole che un file denominato `ContosoData.cs` venga installato in una cartella `Models` del progetto di destinazione, deve trovarsi all'interno delle cartelle `content\Models` e `contentFiles\{lang}\{tfm}\Models` nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="f5669-115">Per indicare a NuGet di applicare la sostituzione dei token in fase di installazione, aggiungere `.pp` al nome file del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="f5669-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="f5669-116">Dopo l'installazione, il file non avrà l'estensione `.pp`.</span><span class="sxs-lookup"><span data-stu-id="f5669-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="f5669-117">Ad esempio, per eseguire trasformazioni in `ContosoData.cs`, denominare il file nel pacchetto `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="f5669-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="f5669-118">Dopo l'installazione verrà visualizzato come `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="f5669-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="f5669-119">Nel file del codice sorgente usare i token senza distinzione tra maiuscole e minuscole nel formato `$token$` per indicare i valori che NuGet deve sostituire con le proprietà del progetto:</span><span class="sxs-lookup"><span data-stu-id="f5669-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="f5669-120">Al momento dell'installazione, NuGet sostituisce `$rootnamespace$` con `Fabrikam` supponendo il progetto di destinazione il cui spazio dei nomi radice è `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="f5669-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="f5669-121">Il token `$rootnamespace$` è la proprietà del progetto usata più di frequente. Tutte le altre sono elencate nelle [proprietà del progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="f5669-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="f5669-122">Tenere in considerazione, naturalmente, che alcune proprietà potrebbero essere specifiche del tipo di progetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="f5669-123">Specifica di trasformazioni di file di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5669-123">Specifying config file transformations</span></span>

<span data-ttu-id="f5669-124">Come descritto nelle sezioni successive, le trasformazioni di file di configurazione possono essere eseguite in due modi:</span><span class="sxs-lookup"><span data-stu-id="f5669-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="f5669-125">Includere i file `app.config.transform` e `web.config.transform` nella cartella `content` del pacchetto, dove l'estensione `.transform` indica a NuGet che questi file contengono il codice XML da unire con i file di configurazione esistenti quando il pacchetto viene installato.</span><span class="sxs-lookup"><span data-stu-id="f5669-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="f5669-126">Quando si disinstalla un pacchetto, lo stesso codice XML viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="f5669-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="f5669-127">Includere i file `app.config.install.xdt` e `web.config.install.xdt` nella cartella `content` del pacchetto usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx) per descrivere le modifiche desiderate.</span><span class="sxs-lookup"><span data-stu-id="f5669-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="f5669-128">Con questa opzione è anche possibile includere un file `.uninstall.xdt` per ripristinare le modifiche quando il pacchetto viene rimosso da un progetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="f5669-129">Le trasformazioni non vengono applicate ai file `.config` a cui si fa riferimento come collegamento in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5669-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="f5669-130">Il vantaggio dell'uso di XDT è dato dal fatto che, invece di unire semplicemente due file statici, fornisce una sintassi per la modifica della struttura di un DOM XML tramite la corrispondenza tra elementi e attributi basata sul supporto XPath completo.</span><span class="sxs-lookup"><span data-stu-id="f5669-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="f5669-131">XDT può quindi aggiungere, aggiornare o rimuovere elementi, inserire nuovi elementi in una posizione specifica oppure sostituire o rimuovere elementi (inclusi i nodi figlio).</span><span class="sxs-lookup"><span data-stu-id="f5669-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="f5669-132">Ciò rende molto semplice creare trasformazioni di disinstallazione che annullano tutte le trasformazioni eseguite durante l'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="f5669-133">Trasformazioni XML</span><span class="sxs-lookup"><span data-stu-id="f5669-133">XML transforms</span></span>

<span data-ttu-id="f5669-134">`app.config.transform` e `web.config.transform` nella cartella `content` di un pacchetto contengono solo gli elementi da unire nei file `app.config` e `web.config` esistenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="f5669-135">Ad esempio, si supponga che il progetto contenga inizialmente il contenuto seguente in `web.config`:</span><span class="sxs-lookup"><span data-stu-id="f5669-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-136">Per aggiungere un elemento `MyNuModule` alla sezione `modules` durante l'installazione del pacchetto, creare un file `web.config.transform` nella cartella `content` del pacchetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f5669-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-137">Dopo che NuGet ha installato il pacchetto, NuGet `web.config` avrà l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="f5669-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-138">Si noti che NuGet non ha sostituito la sezione `modules`, ha semplicemente unito la nuova voce al suo interno aggiungendo solo i nuovi elementi e attributi.</span><span class="sxs-lookup"><span data-stu-id="f5669-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="f5669-139">NuGet non modificherà elementi o attributi esistenti.</span><span class="sxs-lookup"><span data-stu-id="f5669-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="f5669-140">Quando il pacchetto viene disinstallato, NuGet esaminerà nuovamente i file `.transform` e rimuoverà gli elementi in esso contenuti dai file `.config` appropriati.</span><span class="sxs-lookup"><span data-stu-id="f5669-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="f5669-141">Si noti che questo processo non avrà effetto sulle righe nel file `.config` modificate dopo l'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="f5669-142">Come esempio più esteso, il pacchetto [Error Logging Modules and Handlers (ELMAH) per ASP.NET](https://www.nuget.org/packages/elmah/) aggiunge molte voci in `web.config`, che vengono nuovamente rimosse quando si disinstalla un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f5669-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="f5669-143">Per esaminare il relativo file `web.config.transform`, scaricare il pacchetto ELMAH dal collegamento precedente, modificare l'estensione del pacchetto da `.nupkg` a `.zip` e quindi aprire `content\web.config.transform` in tale file ZIP.</span><span class="sxs-lookup"><span data-stu-id="f5669-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="f5669-144">Per vedere l'effetto dell'installazione e della disinstallazione del pacchetto, creare un nuovo progetto ASP.NET in Visual Studio (il modello è disponibile in **Visual C# > Web** nella finestra di dialogo Nuovo progetto) e selezionare un'applicazione ASP.NET vuota.</span><span class="sxs-lookup"><span data-stu-id="f5669-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="f5669-145">Aprire `web.config` per visualizzarne lo stato iniziale.</span><span class="sxs-lookup"><span data-stu-id="f5669-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="f5669-146">Quindi fare clic con il pulsante destro del mouse sul progetto, selezionare **Gestisci pacchetti NuGet**, cercare ELMAH su nuget.org e installare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="f5669-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="f5669-147">Notare tutte le modifiche apportate a `web.config`.</span><span class="sxs-lookup"><span data-stu-id="f5669-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="f5669-148">Disinstallare quindi il pacchetto. `web.config` tornerà allo stato precedente.</span><span class="sxs-lookup"><span data-stu-id="f5669-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="f5669-149">Trasformazioni XDT</span><span class="sxs-lookup"><span data-stu-id="f5669-149">XDT transforms</span></span>

<span data-ttu-id="f5669-150">È possibile modificare i file di configurazione usando la [sintassi XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5669-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="f5669-151">È anche possibile fare in modo che NuGet sostituisca i token con le [proprietà del progetto](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) includendo il nome della proprietà all'interno di delimitatori `$` (senza distinzione tra maiuscole e minuscole).</span><span class="sxs-lookup"><span data-stu-id="f5669-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="f5669-152">Ad esempio, il file seguente `app.config.install.xdt` inserirà un elemento `appSettings` in `app.config` contenente i valori `FullPath`, `FileName` e `ActiveConfigurationSettings` dal progetto:</span><span class="sxs-lookup"><span data-stu-id="f5669-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="f5669-153">Per fare un altro esempio, si supponga che il progetto contenga inizialmente il contenuto seguente in `web.config`:</span><span class="sxs-lookup"><span data-stu-id="f5669-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-154">Per aggiungere un elemento `MyNuModule` alla sezione `modules` durante l'installazione del pacchetto, il file `web.config.install.xdt` del pacchetto dovrebbe contenere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f5669-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-155">Dopo l'installazione del pacchetto, `web.config` sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f5669-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f5669-156">Per rimuovere solo l'elemento `MyNuModule` durante la disinstallazione del pacchetto, il file `web.config.uninstall.xdt` dovrebbe contenere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f5669-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```