---
title: Come gestire la memorizzazione nella cache dei pacchetti in NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: Come gestire le diverse cache per i pacchetti NuGet esistenti in un computer, usate durante l'installazione o il ripristino dei pacchetti.
keywords: Cache dei pacchetti NuGet, memorizzazione nella cache dei pacchetti, cache NuGet, gestione delle cache, cache NuGet locale, cache NuGet globale, comando locals NuGet, cancellazione di una cache
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="4ee44-104">Gestione delle cache NuGet</span><span class="sxs-lookup"><span data-stu-id="4ee44-104">Managing the NuGet cache</span></span>

<span data-ttu-id="4ee44-105">NuGet gestisce varie cache locali per evitare il download di pacchetti già disponibili nel computer e per fornire il supporto offline.</span><span class="sxs-lookup"><span data-stu-id="4ee44-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="4ee44-106">NuGet 2.8 + esegue automaticamente il fallback alla cache durante l'installazione o la reinstallazione dei pacchetti senza una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="4ee44-106">NuGet 2.8+ automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="4ee44-107">Le posizioni delle cache possono essere recuperate tramite il comando [locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="4ee44-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```
nuget locals all -list
```

<span data-ttu-id="4ee44-108">L'output tipico è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4ee44-108">Typical output is as follows:</span></span>

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

<span data-ttu-id="4ee44-109">Se si verificano problemi di installazione dei pacchetti o si vuole essere certi di eseguire l'installazione dei pacchetti da una raccolta remota, usare l'opzione `locals -clear`:</span><span class="sxs-lookup"><span data-stu-id="4ee44-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="4ee44-110">Si noti che la gestione della cache è attualmente supportata solo dalla riga di comando di NuGet e non all'interno di Visual Studio o mediante la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4ee44-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="4ee44-111">La gestione della cache 2. x non è inoltre supportata in NuGet 3.6 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="4ee44-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="4ee44-112">Durante l'uso di `nuget locals` possono verificarsi gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ee44-112">The following errors can occur when using `nuget locals`:</span></span>

* <span data-ttu-id="4ee44-113">**La cancellazione delle risorse locali non è riuscita. Non è possibile eliminare uno o più file.**</span><span class="sxs-lookup"><span data-stu-id="4ee44-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
* <span data-ttu-id="4ee44-114">**La directory non è vuota**</span><span class="sxs-lookup"><span data-stu-id="4ee44-114">**The directory is not empty**</span></span>

<span data-ttu-id="4ee44-115">Questi errori indicano che non si dispone dell'autorizzazione per eliminare i file nella cache o che uno o più file nella cache sono in uso da un altro processo, che deve essere chiuso prima di poter rimuovere tali file.</span><span class="sxs-lookup"><span data-stu-id="4ee44-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the those files can be removed.</span></span>