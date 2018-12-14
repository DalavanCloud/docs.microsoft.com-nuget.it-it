---
title: Installare un pacchetto NuGet firmato
description: Viene descritto il processo di installazione di pacchetti NuGet firmati e di configurazione delle impostazioni di attendibilità della firma dei pacchetti.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977835"
---
# <a name="install-a-signed-package"></a><span data-ttu-id="fd99c-103">Installare un pacchetto firmato</span><span class="sxs-lookup"><span data-stu-id="fd99c-103">Install a signed package</span></span>

<span data-ttu-id="fd99c-104">Non sono richieste azioni specifiche per l'installazione di pacchetti firmati. Tuttavia, se il contenuto è stato modificato dopo la firma, l'installazione viene bloccata con l'[errore NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="fd99c-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="fd99c-105">I pacchetti firmati con certificati non attendibili vengono considerati non firmati e installati senza eventuali avvisi o errori come qualsiasi altro pacchetto non firmato.</span><span class="sxs-lookup"><span data-stu-id="fd99c-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="fd99c-106">Configurare i requisiti di firma del pacchetto</span><span class="sxs-lookup"><span data-stu-id="fd99c-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="fd99c-107">Richiede NuGet 4.9.0+ e Visual Studio 15.9 o versioni successive su Windows</span><span class="sxs-lookup"><span data-stu-id="fd99c-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="fd99c-108">Per configurare come i client NuGet verificano le firme dei pacchetti, impostare `signatureValidationMode` su `require` nel file [nuget.config](../reference/nuget-config-file) utilizzando il comando [`nuget config`](../tools/cli-ref-config).</span><span class="sxs-lookup"><span data-stu-id="fd99c-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="fd99c-109">Questa modalità verifica che tutti i pacchetti siano firmati da uno dei certificati attendibili nel file `nuget.config`.</span><span class="sxs-lookup"><span data-stu-id="fd99c-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="fd99c-110">Questo file consente di specificare gli autori e/o i repository attendibili in base all'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="fd99c-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="fd99c-111">Considerare attendibile l'autore del pacchetto</span><span class="sxs-lookup"><span data-stu-id="fd99c-111">Trust package author</span></span>

<span data-ttu-id="fd99c-112">Per considerare attendibili i pacchetti in base alla firma dell'autore, usare il comando [`trusted-signers`](..tools/cli-ref-trusted-signers) per impostare la proprietà `author` in nuget.config.</span><span class="sxs-lookup"><span data-stu-id="fd99c-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
><span data-ttu-id="fd99c-113">Usare il [comando verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) di `nuget.exe` per ottenere il valore `SHA256` dell'impronta digitale del certificato.</span><span class="sxs-lookup"><span data-stu-id="fd99c-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="fd99c-114">Considerare attendibili tutti i pacchetti di un archivio</span><span class="sxs-lookup"><span data-stu-id="fd99c-114">Trust all packages from a repository</span></span>

<span data-ttu-id="fd99c-115">Per considerare attendibili i pacchetti in base alla firma del repository, usare l'elemento `repository`:</span><span class="sxs-lookup"><span data-stu-id="fd99c-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="fd99c-116">Considerare attendibili i proprietari del pacchetto</span><span class="sxs-lookup"><span data-stu-id="fd99c-116">Trust Package Owners</span></span>

<span data-ttu-id="fd99c-117">Le firme di repository includono metadati aggiuntivi che consentono di determinare i proprietari del pacchetto al momento dell'invio.</span><span class="sxs-lookup"><span data-stu-id="fd99c-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="fd99c-118">È possibile limitare i pacchetti provenienti da un repository in funzione di un elenco di proprietari:</span><span class="sxs-lookup"><span data-stu-id="fd99c-118">You can restrict packages from a repository based on a list of owners:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

<span data-ttu-id="fd99c-119">Se un pacchetto ha più proprietari e uno di questi è presente nell'elenco degli elementi attendibili, l'installazione del pacchetto avrà esito positivo.</span><span class="sxs-lookup"><span data-stu-id="fd99c-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="fd99c-120">Certificati radice non attendibili</span><span class="sxs-lookup"><span data-stu-id="fd99c-120">Untrusted Root certificates</span></span>

<span data-ttu-id="fd99c-121">In alcune situazioni può essere opportuno abilitare la verifica usando certificati non concatenati a una radice attendibile del computer locale.</span><span class="sxs-lookup"><span data-stu-id="fd99c-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="fd99c-122">Per personalizzare questo comportamento è possibile usare l'attributo `allowUntrustedRoot`.</span><span class="sxs-lookup"><span data-stu-id="fd99c-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="fd99c-123">Sincronizzazione dei certificati del repository</span><span class="sxs-lookup"><span data-stu-id="fd99c-123">Sync repository certificates</span></span>

<span data-ttu-id="fd99c-124">I repository dei pacchetti devono annunciare i certificati usati nel loro [indice dei servizi](https://docs.microsoft.com/en-us/nuget/api/service-index).</span><span class="sxs-lookup"><span data-stu-id="fd99c-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="fd99c-125">Prima o poi, il repository aggiornerà questi certificati, ad esempio, allo scadere del certificato.</span><span class="sxs-lookup"><span data-stu-id="fd99c-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="fd99c-126">Quando ciò avviene, i client con criteri specifici richiederanno un aggiornamento della configurazione per includere il certificato appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="fd99c-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="fd99c-127">I firmatari attendibili associati a un repository possono essere aggiornati facilmente usando il `nuget.exe` [comando trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span><span class="sxs-lookup"><span data-stu-id="fd99c-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="fd99c-128">Riferimento allo schema</span><span class="sxs-lookup"><span data-stu-id="fd99c-128">Schema reference</span></span>

<span data-ttu-id="fd99c-129">Il riferimento allo schema completo per i criteri client è reperibile in [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section) (Informazioni di riferimento su nuget.config)</span><span class="sxs-lookup"><span data-stu-id="fd99c-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="fd99c-130">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="fd99c-130">Related articles</span></span>

- [<span data-ttu-id="fd99c-131">Diversi modi per installare un pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="fd99c-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="fd99c-132">Firma di pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="fd99c-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="fd99c-133">Informazioni di riferimento sui pacchetti firmati</span><span class="sxs-lookup"><span data-stu-id="fd99c-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)