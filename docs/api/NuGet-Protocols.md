---
title: Protocolli di NuGet.org
description: I protocolli di nuget.org in continua evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="a94db-103">protocolli di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a94db-103">nuget.org protocols</span></span>

<span data-ttu-id="a94db-104">Per interagire con nuget.org, è necessario seguire alcuni protocolli client.</span><span class="sxs-lookup"><span data-stu-id="a94db-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="a94db-105">Poiché questi protocolli mantengono in evoluzione, i client devono identificare la versione del protocollo che usano durante la chiamata API di nuget.org specifico.</span><span class="sxs-lookup"><span data-stu-id="a94db-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="a94db-106">In questo modo nuget.org introdurre modifiche in modo non è importante per i client precedenti.</span><span class="sxs-lookup"><span data-stu-id="a94db-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="a94db-107">Le API illustrate in questa pagina sono specifiche di nuget.org e vi è alcuna aspettativa per altre implementazioni di server NuGet introdurre tali API.</span><span class="sxs-lookup"><span data-stu-id="a94db-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="a94db-108">Per informazioni sull'API NuGet implementato su vasta scala nell'ecosistema NuGet, vedere il [panoramica dell'API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a94db-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="a94db-109">Questo argomento elenca i vari protocolli come e quando si collegano a esistenza.</span><span class="sxs-lookup"><span data-stu-id="a94db-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="a94db-110">Versione del protocollo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="a94db-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="a94db-111">Il 4.1.0 protocollo specifica l'utilizzo di chiavi di ambito verificare per interagire con i servizi diversi da nuget.org, per convalidare un pacchetto con un account di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a94db-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="a94db-112">Si noti che il `4.1.0` versione numero è una stringa opaca, ma si verifica in genere coincidano con la prima versione del client NuGet ufficiale che questo protocollo è supportato.</span><span class="sxs-lookup"><span data-stu-id="a94db-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="a94db-113">La convalida garantisce che le chiavi API creati dall'utente vengono utilizzate solo con nuget.org e che altri verifica o convalida da un servizio di terze parti viene gestita tramite una chiave di ambito verificare usato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="a94db-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="a94db-114">Queste chiavi ambito verificare utilizzabile per convalidare che il pacchetto appartiene a un determinato utente (account) in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a94db-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="a94db-115">Requisiti client</span><span class="sxs-lookup"><span data-stu-id="a94db-115">Client requirement</span></span>

<span data-ttu-id="a94db-116">I client devono passare l'intestazione seguente quando si effettuano chiamate API per **push** pacchetti nuget.org:</span><span class="sxs-lookup"><span data-stu-id="a94db-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="a94db-117">Si noti che il `X-NuGet-Client-Version` intestazione semantica è simile, ma è riservato a essere utilizzato solo dal client NuGet ufficiale.</span><span class="sxs-lookup"><span data-stu-id="a94db-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="a94db-118">I client di terze parti devono utilizzare il `X-NuGet-Protocol-Version` intestazione e il valore.</span><span class="sxs-lookup"><span data-stu-id="a94db-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="a94db-119">Il **push** protocollo stesso è descritto nella documentazione per il [ `PackagePublish` risorse](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a94db-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="a94db-120">Se un client interagisce con servizi esterni è necessario per convalidare un pacchetto appartiene a un determinato utente (account), deve utilizzare il protocollo seguente ed utilizzare le chiavi di verifica all'ambito e non le chiavi API di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a94db-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="a94db-121">API per richiedere una chiave di verifica dell'ambito</span><span class="sxs-lookup"><span data-stu-id="a94db-121">API to request a verify-scope key</span></span>

<span data-ttu-id="a94db-122">Questa API viene usata per ottenere una chiave di verifica con ambito di un autore di nuget.org convalidare un pacchetto di proprietà di quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="a94db-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="a94db-123">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="a94db-123">Request parameters</span></span>

<span data-ttu-id="a94db-124">nome</span><span class="sxs-lookup"><span data-stu-id="a94db-124">Name</span></span>           | <span data-ttu-id="a94db-125">In</span><span class="sxs-lookup"><span data-stu-id="a94db-125">In</span></span>     | <span data-ttu-id="a94db-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="a94db-126">Type</span></span>   | <span data-ttu-id="a94db-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a94db-127">Required</span></span> | <span data-ttu-id="a94db-128">Note</span><span class="sxs-lookup"><span data-stu-id="a94db-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a94db-129">Id</span><span class="sxs-lookup"><span data-stu-id="a94db-129">ID</span></span>             | <span data-ttu-id="a94db-130">URL</span><span class="sxs-lookup"><span data-stu-id="a94db-130">URL</span></span>    | <span data-ttu-id="a94db-131">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-131">string</span></span> | <span data-ttu-id="a94db-132">sì</span><span class="sxs-lookup"><span data-stu-id="a94db-132">yes</span></span>      | <span data-ttu-id="a94db-133">Identidier il pacchetto per il quale viene richiesta la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="a94db-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="a94db-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="a94db-134">VERSION</span></span>        | <span data-ttu-id="a94db-135">URL</span><span class="sxs-lookup"><span data-stu-id="a94db-135">URL</span></span>    | <span data-ttu-id="a94db-136">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-136">string</span></span> | <span data-ttu-id="a94db-137">No</span><span class="sxs-lookup"><span data-stu-id="a94db-137">no</span></span>       | <span data-ttu-id="a94db-138">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a94db-138">The package version</span></span>
<span data-ttu-id="a94db-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a94db-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a94db-140">Header</span><span class="sxs-lookup"><span data-stu-id="a94db-140">Header</span></span> | <span data-ttu-id="a94db-141">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-141">string</span></span> | <span data-ttu-id="a94db-142">sì</span><span class="sxs-lookup"><span data-stu-id="a94db-142">yes</span></span>      | <span data-ttu-id="a94db-143">Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="a94db-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="a94db-144">Risposta</span><span class="sxs-lookup"><span data-stu-id="a94db-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="a94db-145">API per verificare la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="a94db-145">API to verify the verify scope key</span></span>

<span data-ttu-id="a94db-146">Questa API viene usata per convalidare una chiave di verifica ambito per il pacchetto dall'autore del nuget.org di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a94db-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="a94db-147">Parametri della richiesta</span><span class="sxs-lookup"><span data-stu-id="a94db-147">Request parameters</span></span>

<span data-ttu-id="a94db-148">nome</span><span class="sxs-lookup"><span data-stu-id="a94db-148">Name</span></span>           | <span data-ttu-id="a94db-149">In</span><span class="sxs-lookup"><span data-stu-id="a94db-149">In</span></span>     | <span data-ttu-id="a94db-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="a94db-150">Type</span></span>   | <span data-ttu-id="a94db-151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a94db-151">Required</span></span> | <span data-ttu-id="a94db-152">Note</span><span class="sxs-lookup"><span data-stu-id="a94db-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="a94db-153">Id</span><span class="sxs-lookup"><span data-stu-id="a94db-153">ID</span></span>             | <span data-ttu-id="a94db-154">URL</span><span class="sxs-lookup"><span data-stu-id="a94db-154">URL</span></span>    | <span data-ttu-id="a94db-155">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-155">string</span></span> | <span data-ttu-id="a94db-156">sì</span><span class="sxs-lookup"><span data-stu-id="a94db-156">yes</span></span>      | <span data-ttu-id="a94db-157">L'identificatore del pacchetto per il quale viene richiesta la chiave di verifica ambito</span><span class="sxs-lookup"><span data-stu-id="a94db-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="a94db-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="a94db-158">VERSION</span></span>        | <span data-ttu-id="a94db-159">URL</span><span class="sxs-lookup"><span data-stu-id="a94db-159">URL</span></span>    | <span data-ttu-id="a94db-160">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-160">string</span></span> | <span data-ttu-id="a94db-161">No</span><span class="sxs-lookup"><span data-stu-id="a94db-161">no</span></span>       | <span data-ttu-id="a94db-162">La versione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a94db-162">The package version</span></span>
<span data-ttu-id="a94db-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a94db-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a94db-164">Header</span><span class="sxs-lookup"><span data-stu-id="a94db-164">Header</span></span> | <span data-ttu-id="a94db-165">stringa</span><span class="sxs-lookup"><span data-stu-id="a94db-165">string</span></span> | <span data-ttu-id="a94db-166">sì</span><span class="sxs-lookup"><span data-stu-id="a94db-166">yes</span></span>      | <span data-ttu-id="a94db-167">Ad esempio, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="a94db-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="a94db-168">Questa chiave API ambito verifica scadenza ora del giorno o al primo utilizzo, qualunque si verifichi prima.</span><span class="sxs-lookup"><span data-stu-id="a94db-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="a94db-169">Risposta</span><span class="sxs-lookup"><span data-stu-id="a94db-169">Response</span></span>

<span data-ttu-id="a94db-170">Codice di stato</span><span class="sxs-lookup"><span data-stu-id="a94db-170">Status Code</span></span> | <span data-ttu-id="a94db-171">Significato</span><span class="sxs-lookup"><span data-stu-id="a94db-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="a94db-172">200</span><span class="sxs-lookup"><span data-stu-id="a94db-172">200</span></span>         | <span data-ttu-id="a94db-173">La chiave API è valida</span><span class="sxs-lookup"><span data-stu-id="a94db-173">The API key is valid</span></span>
<span data-ttu-id="a94db-174">403</span><span class="sxs-lookup"><span data-stu-id="a94db-174">403</span></span>         | <span data-ttu-id="a94db-175">La chiave API non è valido o non autorizzato per effettuare il push per il pacchetto</span><span class="sxs-lookup"><span data-stu-id="a94db-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="a94db-176">404</span><span class="sxs-lookup"><span data-stu-id="a94db-176">404</span></span>         | <span data-ttu-id="a94db-177">Il pacchetto a cui fa riferimento a `ID` e `VERSION` (facoltativo) non esiste</span><span class="sxs-lookup"><span data-stu-id="a94db-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>