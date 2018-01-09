---
title: Risoluzione delle controversie sui nomi dei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: Processo per la risoluzione delle controversie tra gli autori di pacchetti NuGet correlate alla personalizzazione, ai marchi e ad altre situazioni conflittuali.
keywords: Controversie sui pacchetti NuGet, risoluzione delle controversie per NuGet, processo di risoluzione delle controversie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="83675-104">Risoluzione delle controversie sui nomi dei pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="83675-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="83675-105">Questo documento contiene il processo consigliato per i membri della community per la risoluzione delle controversie con altri autori di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="83675-105">This document is a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>  

<span data-ttu-id="83675-106">Si supponga ad esempio che Northwind Traders realizzi un sistema CRM per cui fornisce driver client sotto forma di un file MSI scaricabile dal proprio sito Web.</span><span class="sxs-lookup"><span data-stu-id="83675-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="83675-107">Nancy, uno sviluppatore indipendente, intende rendere più accessibile la libreria client di Northwind e la trasforma in un pacchetto NuGet chiamato `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="83675-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="83675-108">In un secondo momento, Northwind vuole produrre un proprio pacchetto NuGet ufficiale della libreria client e pertanto contesta la proprietà del nome del pacchetto da parte di Nancy.</span><span class="sxs-lookup"><span data-stu-id="83675-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="83675-109">In questo scenario Nancy non sembra essere animata da cattive intenzioni, ma supporta gli strumenti e i clienti di Northwind offrendo il proprio contributo in termini di tempo e codice.</span><span class="sxs-lookup"><span data-stu-id="83675-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="83675-110">Allo stesso tempo, Northwind è il legittimo proprietario del nome Northwind.</span><span class="sxs-lookup"><span data-stu-id="83675-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="83675-111">Seguendo il processo riportato di seguito, Northwind e Nancy possono collaborare a una risoluzione appropriata, perché entrambi sono interessati a offrire il proprio contributo alla community di sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="83675-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="83675-112">Di solito non è necessario che il team di NuGet sia coinvolto, in genere la collaborazione è la scelta migliore.</span><span class="sxs-lookup"><span data-stu-id="83675-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="83675-113">In effetti, tutte le controversie portate finora all'attenzione del team di NuGet sono state risolte senza che il team abbia dovuto esprimere il suo giudizio.</span><span class="sxs-lookup"><span data-stu-id="83675-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>


## <a name="process"></a><span data-ttu-id="83675-114">Processo</span><span class="sxs-lookup"><span data-stu-id="83675-114">Process</span></span>

1. <span data-ttu-id="83675-115">Contattare i proprietari del pacchetto per cui è sorta la controversia usando il collegamento **Contact Owners** (Contatta proprietari) nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="83675-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="83675-116">Spiegare il problema in modo diretto e cortese.</span><span class="sxs-lookup"><span data-stu-id="83675-116">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="83675-117">Inviare una copia del messaggio all'indirizzo [support@nuget.org](mailto:support@nuget.org) in modo che NuGet e .NET Foundation siano al corrente della controversia.</span><span class="sxs-lookup"><span data-stu-id="83675-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="83675-118">Attendere un massimo di 30 giorni per la risoluzione, dopodiché segnalare nuovamente il problema all'indirizzo [support@nuget.org](mailto:support@nuget.org).</span><span class="sxs-lookup"><span data-stu-id="83675-118">Wait a maximum of 30 days for a resolution, after which notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="83675-119">Il team di supporto di nuget.org verrà contattato e tenterà di risolvere la controversia collaborando con entrambe le parti.</span><span class="sxs-lookup"><span data-stu-id="83675-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>