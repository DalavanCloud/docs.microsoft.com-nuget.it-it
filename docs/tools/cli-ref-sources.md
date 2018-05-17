---
title: NuGet CLI origini comando
description: Riferimento per il nuget.exe origini comando
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d588ff09075ad75b76b7dd3645f3cdff29f6f093
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="62e60-103">Comando sources (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="62e60-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="62e60-104">**Si applica a:** il consumo di pacchetti, pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="62e60-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="62e60-105">Gestisce l'elenco delle origini nel file di configurazione di ambito di utente o un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="62e60-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="62e60-106">Il file di configurazione di ambito di utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac o Linux).</span><span class="sxs-lookup"><span data-stu-id="62e60-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="62e60-107">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="62e60-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="62e60-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="62e60-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="62e60-109">dove `<operation>` è uno dei *elenco, aggiungere, rimuovere, attivare, disattivare* o *aggiornamento*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="62e60-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="62e60-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="62e60-110">Options</span></span>

| <span data-ttu-id="62e60-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="62e60-111">Option</span></span> | <span data-ttu-id="62e60-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62e60-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="62e60-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="62e60-113">ConfigFile</span></span> | <span data-ttu-id="62e60-114">Il file di configurazione NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="62e60-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="62e60-115">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="62e60-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="62e60-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="62e60-116">ForceEnglishOutput</span></span> | <span data-ttu-id="62e60-117">*(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="62e60-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="62e60-118">Formato</span><span class="sxs-lookup"><span data-stu-id="62e60-118">Format</span></span> | <span data-ttu-id="62e60-119">Si applica al `list` azione e può essere `Detailed` (impostazione predefinita) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="62e60-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="62e60-120">?</span><span class="sxs-lookup"><span data-stu-id="62e60-120">Help</span></span> | <span data-ttu-id="62e60-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="62e60-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="62e60-122">Non interattivo</span><span class="sxs-lookup"><span data-stu-id="62e60-122">NonInteractive</span></span> | <span data-ttu-id="62e60-123">Elimina richieste per l'input dell'utente o le conferme.</span><span class="sxs-lookup"><span data-stu-id="62e60-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="62e60-124">Password</span><span class="sxs-lookup"><span data-stu-id="62e60-124">Password</span></span> | <span data-ttu-id="62e60-125">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="62e60-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="62e60-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="62e60-126">StorePasswordInClearText</span></span> | <span data-ttu-id="62e60-127">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di archiviazione di un formato crittografato.</span><span class="sxs-lookup"><span data-stu-id="62e60-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="62e60-128">UserName</span><span class="sxs-lookup"><span data-stu-id="62e60-128">UserName</span></span> | <span data-ttu-id="62e60-129">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="62e60-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="62e60-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="62e60-130">Verbosity</span></span> | <span data-ttu-id="62e60-131">Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="62e60-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="62e60-132">Assicurarsi di aggiungere password delle origini nel contesto dell'utente stesso come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="62e60-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="62e60-133">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente come è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="62e60-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="62e60-134">Ad esempio quando si utilizza un server di compilazione per il ripristino dei pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows in cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="62e60-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="62e60-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="62e60-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="62e60-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="62e60-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```