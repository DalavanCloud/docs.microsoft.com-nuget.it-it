---
title: Query per recuperare tutti i pacchetti pubblicati su nuget.org | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/2/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d017cd4-3d75-4341-ba90-3c57be093b7d
description: "Tramite l'API NuGet, è possibile eseguire una query per recuperare tutti i pacchetti pubblicati su nuget.org e rimanere aggiornati nel tempo."
keywords: "Enumerazione di tutti i pacchetti tramite l'API NuGet, replica dei pacchetti tramite l'API NuGet, pacchetti più recenti pubblicati su nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50a5be4cb0405ad78a72d0497612781a4b346060
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="874f4-104">Query per recuperare tutti i pacchetti pubblicati su nuget.org</span><span class="sxs-lookup"><span data-stu-id="874f4-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="874f4-105">Un modello di query comune sull'API OData V2 legacy prevedeva l'enumerazione di tutti i pacchetti pubblicati su nuget.org, ordinati in base alla data di pubblicazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="874f4-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="874f4-106">Gli scenari che richiedono questo tipo di query su nuget.org variano notevolmente:</span><span class="sxs-lookup"><span data-stu-id="874f4-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="874f4-107">Replica completa di nuget.org</span><span class="sxs-lookup"><span data-stu-id="874f4-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="874f4-108">Individuazione del rilascio di nuove versioni di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="874f4-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="874f4-109">Ricerca di pacchetti che dipendono dal pacchetto in uso</span><span class="sxs-lookup"><span data-stu-id="874f4-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="874f4-110">La modalità legacy di esecuzione di questa operazione dipendeva dall'ordinamento dell'entità del pacchetto OData in base a un timestamp e dallo spostamento all'interno del set di risultati di dimensioni elevate usando i parametri `skip` e `top` (dimensioni della pagina).</span><span class="sxs-lookup"><span data-stu-id="874f4-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="874f4-111">Sfortunatamente, questo approccio presenta alcuni svantaggi:</span><span class="sxs-lookup"><span data-stu-id="874f4-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="874f4-112">Possibilità di pacchetti mancanti, dal momento che le query sono effettuate su dati che spesso cambiano ordine</span><span class="sxs-lookup"><span data-stu-id="874f4-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="874f4-113">Tempi di risposta delle query rallentati, poiché le query non sono ottimizzate (le query più ottimizzate sono quelle che supportano uno scenario principale per il client NuGet ufficiale)</span><span class="sxs-lookup"><span data-stu-id="874f4-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="874f4-114">Uso di API deprecate e non documentate, il che significa che il supporto di tali query in futuro non è garantito</span><span class="sxs-lookup"><span data-stu-id="874f4-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="874f4-115">Impossibilità di riprodurre la cronologia nell'ordine esatto in cui si è verificata</span><span class="sxs-lookup"><span data-stu-id="874f4-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="874f4-116">Per questo motivo, è possibile fare riferimento alla guida seguente per gestire gli scenari menzionati in precedenza in modo più affidabile e valido sia oggi che in futuro.</span><span class="sxs-lookup"><span data-stu-id="874f4-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="874f4-117">Panoramica</span><span class="sxs-lookup"><span data-stu-id="874f4-117">Overview</span></span>

<span data-ttu-id="874f4-118">Al centro di questa guida si trova una risorsa dell'[API NuGet](../../api/overview.md) chiamata **catalogo**.</span><span class="sxs-lookup"><span data-stu-id="874f4-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="874f4-119">Il catalogo è un'API a solo accodamento che consente al chiamante di visualizzare una cronologia completa di pacchetti aggiunti, modificati ed eliminati da nuget.org. Se si è interessati a tutti i pacchetti pubblicati su nuget.org o anche solo a un subset, il catalogo costituisce una valida soluzione per mantenersi aggiornati nel tempo con il set di pacchetti attualmente disponibili.</span><span class="sxs-lookup"><span data-stu-id="874f4-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="874f4-120">Questa guida è da intendersi come una presentazione generale, ma se si è interessati a informazioni più dettagliate sul catalogo, vedere il relativo [documento di riferimento per l'API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="874f4-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="874f4-121">I passaggi seguenti possono essere implementati in qualsiasi linguaggio di programmazione scelto.</span><span class="sxs-lookup"><span data-stu-id="874f4-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="874f4-122">Se si vuole un esempio completo in esecuzione, prendere in considerazione l'[esempio in C#](#c-sample-code) menzionato di seguito.</span><span class="sxs-lookup"><span data-stu-id="874f4-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="874f4-123">In caso contrario, attenersi alla guida seguente per creare un lettore del catalogo affidabile.</span><span class="sxs-lookup"><span data-stu-id="874f4-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="874f4-124">Inizializzare un cursore</span><span class="sxs-lookup"><span data-stu-id="874f4-124">Initialize a cursor</span></span>

<span data-ttu-id="874f4-125">Il primo passaggio per la creazione di un lettore del catalogo affidabile consiste nell'implementazione di un cursore.</span><span class="sxs-lookup"><span data-stu-id="874f4-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="874f4-126">Per i dettagli completi sulla progettazione di un cursore del catalogo, vedere il [documento di riferimento per il catalogo](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="874f4-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="874f4-127">In breve, il cursore è un punto nel tempo fino al quale sono stati elaborati gli eventi nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="874f4-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="874f4-128">Gli eventi nel catalogo rappresentano le pubblicazioni dei pacchetti e altre modifiche dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="874f4-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="874f4-129">Se si è interessati a tutti i pacchetti pubblicati in NuGet fin dall'inizio, è necessario inizializzare il cursore su un timestamp di "valore minimo" (ad esempio `DateTime.MinValue` in .NET).</span><span class="sxs-lookup"><span data-stu-id="874f4-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="874f4-130">Se si è interessati solo ai pacchetti pubblicati a partire dalla data odierna, è possibile usare il timestamp corrente come valore del cursore iniziale.</span><span class="sxs-lookup"><span data-stu-id="874f4-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="874f4-131">In questa guida il cursore sarà inizializzato su un timestamp risalente a un'ora prima.</span><span class="sxs-lookup"><span data-stu-id="874f4-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="874f4-132">Per il momento, il timestamp verrà semplicemente salvato in memoria.</span><span class="sxs-lookup"><span data-stu-id="874f4-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="874f4-133">Determinare l'URL dell'indice del catalogo</span><span class="sxs-lookup"><span data-stu-id="874f4-133">Determine catalog index URL</span></span>

<span data-ttu-id="874f4-134">Il percorso di ogni risorsa (endpoint) nell'API NuGet deve essere individuato tramite l'[indice del servizio](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="874f4-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="874f4-135">Poiché questa guida è incentrata su nuget.org, verrà usato l'indice del servizio di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="874f4-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="874f4-136">Il documento del servizio è un documento JSON contenente tutte le risorse su nuget.org. Cercare la risorsa con il valore della proprietà `@type` pari a `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="874f4-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="874f4-137">Il valore della proprietà `@id` associato è l'URL per l'indice del catalogo stesso.</span><span class="sxs-lookup"><span data-stu-id="874f4-137">The associated `@id` property value is the URL to the catalog index itself.</span></span>

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="874f4-138">Trovare nuovi elementi foglia del catalogo</span><span class="sxs-lookup"><span data-stu-id="874f4-138">Find new catalog leaves</span></span>

<span data-ttu-id="874f4-139">Usando il valore della proprietà `@id` individuato nel passaggio precedente, scaricare l'indice del catalogo:</span><span class="sxs-lookup"><span data-stu-id="874f4-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="874f4-140">Deserializzare l'[indice del catalogo](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="874f4-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="874f4-141">Applicare un filtro per escludere tutti gli [oggetti della pagina del catalogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) con `commitTimeStamp` minore o uguale al valore del cursore corrente.</span><span class="sxs-lookup"><span data-stu-id="874f4-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="874f4-142">Per ogni pagina del catalogo rimanente, scaricare il documento completo usando la proprietà `@id`.</span><span class="sxs-lookup"><span data-stu-id="874f4-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="874f4-143">Deserializzare la [pagina del catalogo](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="874f4-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="874f4-144">Applicare un filtro per escludere tutti gli [oggetti foglia del catalogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) con `commitTimeStamp` minore o uguale al valore del cursore corrente.</span><span class="sxs-lookup"><span data-stu-id="874f4-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="874f4-145">Dopo avere scaricato tutte le pagine di catalogo non escluse tramite l'applicazione del filtro, sarà disponibile un set di oggetti foglia del catalogo che rappresentano i pacchetti che sono stati pubblicati, rimossi dall'elenco, elencati o eliminati nel periodo di tempo trascorso tra il timestamp del cursore e il momento attuale.</span><span class="sxs-lookup"><span data-stu-id="874f4-145">After you have downloaded all of the catalog pages not filtered out, you will have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="874f4-146">Elaborare gli elementi foglia del catalogo</span><span class="sxs-lookup"><span data-stu-id="874f4-146">Process catalog leaves</span></span>

<span data-ttu-id="874f4-147">A questo punto, è possibile eseguire qualsiasi operazione di elaborazione personalizzata sugli elementi del catalogo.</span><span class="sxs-lookup"><span data-stu-id="874f4-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="874f4-148">Se si ha bisogno dell'ID e della versione del pacchetto, è possibile esaminare le proprietà `nuget:id` e `nuget:version` degli oggetti elemento del catalogo trovati nelle pagine.</span><span class="sxs-lookup"><span data-stu-id="874f4-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="874f4-149">Assicurarsi di esaminare la proprietà `@type` per sapere se l'elemento del catalogo riguarda un pacchetto esistente o un pacchetto eliminato.</span><span class="sxs-lookup"><span data-stu-id="874f4-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="874f4-150">Se si è interessati ai metadati sul pacchetto (come la descrizione, le dipendenze, le dimensioni del pacchetto .nupkg e così via), è possibile recuperare il [documento foglia del catalogo](../../api/catalog-resource.md#catalog-leaf) usando la proprietà `@id`.</span><span class="sxs-lookup"><span data-stu-id="874f4-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="874f4-151">Questo documento contiene tutti i metadati inclusi nella [risorsa dei metadati del pacchetto](../../api/registration-base-url-resource.md) e molto altro.</span><span class="sxs-lookup"><span data-stu-id="874f4-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="874f4-152">Questo è il passaggio in cui viene implementata la logica personalizzata.</span><span class="sxs-lookup"><span data-stu-id="874f4-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="874f4-153">Gli altri passaggi in questa guida vengono implementati all'incirca in modo analogo, indipendentemente dalle operazioni eseguite sugli elementi foglia del catalogo.</span><span class="sxs-lookup"><span data-stu-id="874f4-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="874f4-154">Download del pacchetto .nupkg</span><span class="sxs-lookup"><span data-stu-id="874f4-154">Downloading the .nupkg</span></span>

<span data-ttu-id="874f4-155">Se si è interessati al download del pacchetto .nupkg per i pacchetti individuati nel catalogo, è possibile usare la [risorsa di contenuto del pacchetto](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="874f4-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="874f4-156">Tuttavia, si noti che sussiste un breve ritardo tra quando viene rilevato un pacchetto nel catalogo e quando è disponibile nella risorsa di contenuto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="874f4-156">However, note that there is a short delay between when a package is found in catalog and when it is available in the package content resource.</span></span> <span data-ttu-id="874f4-157">Pertanto, se si verifica l'errore `404 Not Found` mentre si tenta di scaricare un pacchetto .nupkg per un pacchetto rilevato nel catalogo, è sufficiente ripetere il tentativo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="874f4-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="874f4-158">La correzione di questo ritardo è registrata nel problema GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="874f4-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="874f4-159">Spostare in avanti il cursore</span><span class="sxs-lookup"><span data-stu-id="874f4-159">Move the cursor forward</span></span>

<span data-ttu-id="874f4-160">Dopo avere elaborato correttamente gli elementi del catalogo, è necessario determinare il nuovo valore del cursore da salvare.</span><span class="sxs-lookup"><span data-stu-id="874f4-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="874f4-161">A tale scopo, trovare il valore `commitTimeStamp` massimo (il più recente in ordine cronologico) di tutti gli elementi del catalogo elaborati.</span><span class="sxs-lookup"><span data-stu-id="874f4-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="874f4-162">Questo è il nuovo valore del cursore.</span><span class="sxs-lookup"><span data-stu-id="874f4-162">This is your new cursor value.</span></span> <span data-ttu-id="874f4-163">Salvarlo in una risorsa di archiviazione permanente, come un database, un file system o un archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="874f4-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="874f4-164">Se si vogliono ottenere altri elementi del catalogo, partire semplicemente dal [primo passaggio](#initialize-a-cursor) inizializzando il valore del cursore da questo archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="874f4-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="874f4-165">Se l'applicazione genera errori o un'eccezione, non spostare in avanti il cursore.</span><span class="sxs-lookup"><span data-stu-id="874f4-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="874f4-166">Spostare in avanti il cursore significa che non è più necessario elaborare gli elementi del catalogo prima del cursore.</span><span class="sxs-lookup"><span data-stu-id="874f4-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="874f4-167">Se per qualche motivo è presente un bug nella modalità di elaborazione degli elementi figlio del catalogo, è possibile semplicemente spostare il cursore indietro nel tempo e consentire al codice di rielaborare gli elementi del catalogo precedenti.</span><span class="sxs-lookup"><span data-stu-id="874f4-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="874f4-168">Codice di esempio in C#</span><span class="sxs-lookup"><span data-stu-id="874f4-168">C# sample code</span></span>

<span data-ttu-id="874f4-169">Poiché il catalogo è un set di documenti JSON disponibili tramite HTTP, è possibile interagire con esso tramite qualsiasi linguaggio di programmazione che disponga di un client HTTP e di un deserializzatore JSON.</span><span class="sxs-lookup"><span data-stu-id="874f4-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="874f4-170">Gli esempi in C# sono disponibili nel [repository NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="874f4-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="874f4-171">SDK del catalogo</span><span class="sxs-lookup"><span data-stu-id="874f4-171">Catalog SDK</span></span>

<span data-ttu-id="874f4-172">Il modo più semplice per utilizzare il catalogo consiste nell'usare la versione preliminare del pacchetto SDK del catalogo .NET: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="874f4-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span>
<span data-ttu-id="874f4-173">Questo pacchetto è disponibile nel feed MyGet `nuget-build`, per cui si usa l'URL di origine del pacchetto NuGet `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="874f4-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="874f4-174">È possibile installare questo pacchetto in un progetto compatibile con `netstandard1.3` o versione successiva, come NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="874f4-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="874f4-175">Un esempio che usa questo pacchetto è disponibile su GitHub nel [progetto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="874f4-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="874f4-176">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="874f4-176">Sample output</span></span>

```
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="874f4-177">Esempio minimo</span><span class="sxs-lookup"><span data-stu-id="874f4-177">Minimal sample</span></span>

<span data-ttu-id="874f4-178">Per un esempio con un numero minore di dipendenze che illustra l'interazione con il catalogo in maggiore dettaglio, vedere il [progetto di esempio CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="874f4-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span>
<span data-ttu-id="874f4-179">Il progetto ha come destinazione `netcoreapp2.0` e dipende da [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (per la risoluzione dell'indice del servizio) e da [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (per la deserializzazione JSON).</span><span class="sxs-lookup"><span data-stu-id="874f4-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="874f4-180">La logica principale del codice è visibile nel [file Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="874f4-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="874f4-181">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="874f4-181">Sample output</span></span>

```
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```