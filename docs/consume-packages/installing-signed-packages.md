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
# <a name="install-a-signed-package"></a>Installare un pacchetto firmato

Non sono richieste azioni specifiche per l'installazione di pacchetti firmati. Tuttavia, se il contenuto è stato modificato dopo la firma, l'installazione viene bloccata con l'[errore NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> I pacchetti firmati con certificati non attendibili vengono considerati non firmati e installati senza eventuali avvisi o errori come qualsiasi altro pacchetto non firmato.

## <a name="configure-package-signature-requirements"></a>Configurare i requisiti di firma del pacchetto

> [!Note]
> Richiede NuGet 4.9.0+ e Visual Studio 15.9 o versioni successive su Windows

Per configurare come i client NuGet verificano le firme dei pacchetti, impostare `signatureValidationMode` su `require` nel file [nuget.config](../reference/nuget-config-file) utilizzando il comando [`nuget config`](../tools/cli-ref-config).

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Questa modalità verifica che tutti i pacchetti siano firmati da uno dei certificati attendibili nel file `nuget.config`. Questo file consente di specificare gli autori e/o i repository attendibili in base all'impronta digitale del certificato.

### <a name="trust-package-author"></a>Considerare attendibile l'autore del pacchetto

Per considerare attendibili i pacchetti in base alla firma dell'autore, usare il comando [`trusted-signers`](..tools/cli-ref-trusted-signers) per impostare la proprietà `author` in nuget.config.

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
>Usare il [comando verify](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) di `nuget.exe` per ottenere il valore `SHA256` dell'impronta digitale del certificato.


### <a name="trust-all-packages-from-a-repository"></a>Considerare attendibili tutti i pacchetti di un archivio

Per considerare attendibili i pacchetti in base alla firma del repository, usare l'elemento `repository`:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Considerare attendibili i proprietari del pacchetto

Le firme di repository includono metadati aggiuntivi che consentono di determinare i proprietari del pacchetto al momento dell'invio. È possibile limitare i pacchetti provenienti da un repository in funzione di un elenco di proprietari:

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

Se un pacchetto ha più proprietari e uno di questi è presente nell'elenco degli elementi attendibili, l'installazione del pacchetto avrà esito positivo.

### <a name="untrusted-root-certificates"></a>Certificati radice non attendibili

In alcune situazioni può essere opportuno abilitare la verifica usando certificati non concatenati a una radice attendibile del computer locale. Per personalizzare questo comportamento è possibile usare l'attributo `allowUntrustedRoot`.

### <a name="sync-repository-certificates"></a>Sincronizzazione dei certificati del repository

I repository dei pacchetti devono annunciare i certificati usati nel loro [indice dei servizi](https://docs.microsoft.com/en-us/nuget/api/service-index). Prima o poi, il repository aggiornerà questi certificati, ad esempio, allo scadere del certificato. Quando ciò avviene, i client con criteri specifici richiederanno un aggiornamento della configurazione per includere il certificato appena aggiunto. I firmatari attendibili associati a un repository possono essere aggiornati facilmente usando il `nuget.exe` [comando trusted-signers sync](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).

### <a name="schema-reference"></a>Riferimento allo schema

Il riferimento allo schema completo per i criteri client è reperibile in [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section) (Informazioni di riferimento su nuget.config)

## <a name="related-articles"></a>Articoli correlati

- [Diversi modi per installare un pacchetto NuGet](ways-to-install-a-package.md)
- [Firma di pacchetti NuGet](../create-packages/Sign-a-Package.md)
- [Informazioni di riferimento sui pacchetti firmati](../reference/Signed-Packages-Reference.md)
