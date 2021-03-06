---
title: NuGet Client SDK
description: L'API è in continua evoluzione e non ancora documentato, ma gli esempi sono disponibili nel blog di Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8e612d9f86bcffc99870c5541aa6091e678db512
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547089"
---
# <a name="nuget-client-sdk"></a>NuGet Client SDK

> [!Note]
> Non deve essere confusa con la [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

Il *NuGet Client SDK* fa riferimento a un gruppo di librerie .NET incentrati [NuGet](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), e [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Questi pacchetti sostituiscono la precedente [togliere](https://www.nuget.org/packages/NuGet.Core/) libreria.

Microsoft sta lavorando con una superficie di attacco stabile che è possibile documentare a breve.

## <a name="source-code"></a>Codice sorgente

Il codice sorgente viene pubblicato in GitHub nel progetto [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Documentazione di terze parti

È possibile trovare esempi e documentazione per alcune delle API della serie di blog seguente da Dave Glick, pubblicato 2016:

- [Esplorare le librerie di NuGet v3, parte 1: introduzione e concetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Esplorare le librerie di NuGet v3, parte 2: la ricerca di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Esplorare le librerie di NuGet v3, parte 3: installazione di pacchetti](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Questi post di blog scritti subito dopo il **3.4.3** versione di NuGet sono stati rilasciati pacchetti SDK client.
> Le versioni più recenti dei pacchetti possono essere incompatibili con le informazioni contenute nei post di blog.
