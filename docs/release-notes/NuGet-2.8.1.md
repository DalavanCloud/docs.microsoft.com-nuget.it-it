---
title: Note sulla versione di NuGet 2.8.1
description: Note sulla versione per l'inclusione di NuGet 2.8.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="e307d-103">Note sulla versione di NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="e307d-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="e307d-104">[Note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md) | [note sulla versione di NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="e307d-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="e307d-105">È stata rilasciata NuGet 2.8.1 2 aprile 2014.</span><span class="sxs-lookup"><span data-stu-id="e307d-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="e307d-106">Importanti funzionalità nella versione</span><span class="sxs-lookup"><span data-stu-id="e307d-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="e307d-107">Supporto per i progetti Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e307d-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="e307d-108">Questa versione supporta ora i moniker seguente nuovo framework di destinazione che possono essere utilizzato per i progetti di destinazione Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="e307d-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="e307d-109">WindowsPhone81 / WP81 (per i progetti di Windows Phone basate su Silverlight)</span><span class="sxs-lookup"><span data-stu-id="e307d-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="e307d-110">WindowsPhoneApp81 / WPA81 (per i progetti di App di Windows Phone basate su WinRT)</span><span class="sxs-lookup"><span data-stu-id="e307d-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="e307d-111">Aggiornamento dell'estensione di WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="e307d-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="e307d-112">Questa versione aggiorna il client NuGet trovato in WebMatrix per [sono](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e la porta con comprende, ad esempio trasformazioni XDT.</span><span class="sxs-lookup"><span data-stu-id="e307d-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="e307d-113">Ancora più importante, la 2.6.1 aggiornamento core consente al client di WebMatrix installare i pacchetti NuGet che contengono le versioni più recenti del `.nuspec` schema, che include i pacchetti NuGet di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e307d-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="e307d-114">Per ulteriori informazioni sull'aggiornamento dell'estensione di WebMatrix, vedere parametri specifici [note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="e307d-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="e307d-115">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="e307d-115">Bug Fixes</span></span>
<span data-ttu-id="e307d-116">Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="e307d-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="e307d-117">Si sono verificati problemi di totali 16 risolti nella versione.</span><span class="sxs-lookup"><span data-stu-id="e307d-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="e307d-118">Per un elenco completo delle operazioni gli elementi corretti in NuGet, 2.8.1 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="e307d-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="e307d-119">Reshipping con Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="e307d-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="e307d-120">Nella versione CTP di Visual Studio "14" rilasciata a giugno 2014 3rd NuGet 2.8.1 viene fornito nella casella.</span><span class="sxs-lookup"><span data-stu-id="e307d-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="e307d-121">Le funzionalità supportano restano in pari con altri 2.8.1 VSIXes ad esempio quello per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="e307d-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>