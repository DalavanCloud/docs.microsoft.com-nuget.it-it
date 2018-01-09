---
title: Creazione di pacchetti NuGet nativi | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Informazioni dettagliate sulla creazione di pacchetti NuGet nativi che contengono codice C++ anziché codice gestito, da usare in progetti C++."
keywords: Pacchetti NuGet nativi, pacchetti NuGet C++, pacchetti di codice nativo, progetti C++ di destinazione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a><span data-ttu-id="33b7a-104">Creazione di pacchetti nativi</span><span class="sxs-lookup"><span data-stu-id="33b7a-104">Creating native packages</span></span>

<span data-ttu-id="33b7a-105">Un pacchetto nativo contiene codice C++ nativo invece di codice gestito, in modo che possa essere usato all'interno di progetti C++.</span><span class="sxs-lookup"><span data-stu-id="33b7a-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="33b7a-106">(Vedere [Pacchetti C++ nativi](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) nella sezione Utilizzare i pacchetti.)</span><span class="sxs-lookup"><span data-stu-id="33b7a-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) in the Consume section.)</span></span>

<span data-ttu-id="33b7a-107">Per essere utilizzabile in un progetto C++, un pacchetto deve essere destinato al framework `native`.</span><span class="sxs-lookup"><span data-stu-id="33b7a-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="33b7a-108">Al momento, a questo framework non è assegnato alcun numero di versione perché NuGet considera uguali tutti i progetti C++.</span><span class="sxs-lookup"><span data-stu-id="33b7a-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="33b7a-109">Assicurarsi di includere *native* nella sezione `<tags>` del file `.nuspec` per aiutare gli altri sviluppatori a trovare il pacchetto eseguendo una ricerca in base a tale tag.</span><span class="sxs-lookup"><span data-stu-id="33b7a-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="33b7a-110">I pacchetti NuGet nativi con destinazione `native` forniscono quindi i file nelle cartelle `\build`, `\content` e `\tools`. In questo caso la cartella `\lib` non viene usata (NuGet non può aggiungere direttamente riferimenti a un progetto C++).</span><span class="sxs-lookup"><span data-stu-id="33b7a-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="33b7a-111">Un pacchetto può anche includere file di destinazioni e proprietà in `\build` e tali file verranno importati automaticamente da NuGet nei progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="33b7a-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="33b7a-112">Questi file devono avere lo stesso nome dell'ID di pacchetto con le estensioni `.targets` e/o `.props`.</span><span class="sxs-lookup"><span data-stu-id="33b7a-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="33b7a-113">Ad esempio, il pacchetto [cpprestsdk](https://nuget.org/packages/cpprestsdk/) include un file `cpprestsdk.targets` nella relativa cartella `\build`.</span><span class="sxs-lookup"><span data-stu-id="33b7a-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="33b7a-114">La cartella `\build` può essere usata per tutti i pacchetti NuGet e non solo per i pacchetti nativi.</span><span class="sxs-lookup"><span data-stu-id="33b7a-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="33b7a-115">La cartella `\build` rispetta i framework di destinazione così come le cartelle `\content`, `\lib` e `\tools`.</span><span class="sxs-lookup"><span data-stu-id="33b7a-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="33b7a-116">Questo significa che è possibile creare una cartella `\build\net40` e una cartella `\build\net45` e NuGet importerà i file di proprietà e destinazioni appropriati nel progetto.</span><span class="sxs-lookup"><span data-stu-id="33b7a-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="33b7a-117">Non occorre usare script di PowerShell per importare le destinazioni MSBuild.</span><span class="sxs-lookup"><span data-stu-id="33b7a-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>