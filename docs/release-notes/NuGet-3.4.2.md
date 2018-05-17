---
title: Note sulla versione di sezione 3.4.2 NuGet
description: Note sulla versione per l'inclusione di NuGet sezione 3.4.2 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="46e80-103">Note sulla versione di sezione 3.4.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="46e80-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="46e80-104">[Note sulla versione di NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [note sulla versione di NuGet la versione 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="46e80-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="46e80-105">È stata rilasciata NuGet sezione 3.4.2 8 aprile 2016 a risolvere alcuni problemi che sono stati identificati i 3.4 e 3.4.1 rilasciare.</span><span class="sxs-lookup"><span data-stu-id="46e80-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="46e80-106">NuGet.exe sezione 3.4.2 RC è ora disponibile</span><span class="sxs-lookup"><span data-stu-id="46e80-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="46e80-107">È possibile scaricare la versione finale candidata di nuget.exe sezione 3.4.2 [qui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="46e80-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="46e80-108">Aggiornamenti e miglioramenti</span><span class="sxs-lookup"><span data-stu-id="46e80-108">Updates and Improvements</span></span>

* <span data-ttu-id="46e80-109">Sono stati migliorati in modo significativo le prestazioni degli aggiornamenti in uno scenario specifico, in cui gli aggiornamenti per i pacchetti con grafici delle dipendenze completa richiede molto tempo e blocco di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46e80-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="46e80-110">il ripristino NuGet senza il traffico di rete è 2.5 x – 3 più veloce in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46e80-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="46e80-111">Oltre a questa modifica, è stato risolto un problema in cui si stava raggiunge la rete due volte quando l'aggiornamento di recupero contare nell'interfaccia utente di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46e80-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="46e80-112">Questo è stato parzialmente responsabile di alcuni clienti di problemi di timeout nella 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="46e80-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="46e80-113">Aggiunta del supporto per l'impostazione no_proxy</span><span class="sxs-lookup"><span data-stu-id="46e80-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="46e80-114">Correzioni</span><span class="sxs-lookup"><span data-stu-id="46e80-114">Fixes</span></span>

* <span data-ttu-id="46e80-115">Risolto un problema in nuget.org origine era mancante nella configurazione o impostazioni NuGet dopo l'aggiornamento a 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="46e80-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="46e80-116">Risolto un problema in cui una modifica di maiuscole e minuscole a FindPackagesById in 3.4.1 interruzioni Artifactory.</span><span class="sxs-lookup"><span data-stu-id="46e80-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="46e80-117">Correggere un problema con FIPS che ha generato errori con il ripristino NuGet con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="46e80-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="46e80-118">Correzione di un arresto anomalo durante l'esplorazione delle origini con l'URL dell'icona non valido.</span><span class="sxs-lookup"><span data-stu-id="46e80-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="46e80-119">Risoluzione dei problemi con l'unione delle versioni e le voci da 'Tutte le origini'.</span><span class="sxs-lookup"><span data-stu-id="46e80-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="46e80-120">Problemi noti nella sezione 3.4.2 riga di comando di Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="46e80-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="46e80-121">Questi problemi verranno risolti prima settimana successiva prima viene raggiunto RTM.</span><span class="sxs-lookup"><span data-stu-id="46e80-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="46e80-122">Ripristino nuget in esecuzione su una soluzione avrà esito negativo se il file della soluzione viene inserito in una gerarchia di cartelle inferiore rispetto ai file di progetto.</span><span class="sxs-lookup"><span data-stu-id="46e80-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="46e80-123">Eseguire il comando di eliminazione nuget in un pacchetto utilizzando il feed V2 avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="46e80-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="46e80-124">In alternativa, usare feed V3.</span><span class="sxs-lookup"><span data-stu-id="46e80-124">Use V3 feed instead.</span></span>


<span data-ttu-id="46e80-125">Per l'elenco completo delle correzioni e miglioramenti in questa versione, consultare l'elenco dei problemi [qui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="46e80-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>