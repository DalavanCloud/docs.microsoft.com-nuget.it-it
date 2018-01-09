---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b70326a0-5bfc-4b7c-881d-7a7d5ebeeed5
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
keywords: Ripristinare pacchetti NuGet, ripristino di pacchetti, risoluzione dei problemi, risolvere problemi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c23a9ed2b7cffbf904018a089ccde000adaa517f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="a509a-104">Risoluzione degli errori relativi al ripristino dei pacchetti in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a509a-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="a509a-105">Questa pagina è dedicata agli errori comuni durante il ripristino dei pacchetti in Visual Studio e alle procedure per risolverli.</span><span class="sxs-lookup"><span data-stu-id="a509a-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="a509a-106">Per istruzioni su come ripristinare i pacchetti, vedere [Ripristino di pacchetti](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="a509a-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="a509a-107">Per impostazione predefinita, quando si compila un progetto in Visual Studio vengono ripristinati automaticamente i pacchetti NuGet a cui si fa riferimento nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a509a-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="a509a-108">Tuttavia, le compilazioni avranno esito negativo se il ripristino dei pacchetti è disabilitato nelle impostazioni **Strumenti > Opzioni > Gestione pacchetti NuGet > Ripristino pacchetto** e i pacchetti necessari non sono disponibili nel computer.</span><span class="sxs-lookup"><span data-stu-id="a509a-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="a509a-109">In questi casi potrebbero essere visualizzati gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a509a-109">In these cases you may see the following errors:</span></span>

```
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

<span data-ttu-id="a509a-110">Per abilitare il ripristino dei pacchetti, aprire **Strumenti > Opzioni > Gestione pacchetti NuGet** e selezionare le opzioni **Consenti a NuGet di scaricare i pacchetti mancanti** e **Verificare in automatico i pacchetti mancanti durante il build in Visual Studio**:</span><span class="sxs-lookup"><span data-stu-id="a509a-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../Consume-Packages/media/restore-01-autorestoreoptions.png)
