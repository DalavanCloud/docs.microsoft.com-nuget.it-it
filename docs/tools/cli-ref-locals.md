---
title: Comando locals NuGet CLI
description: Informazioni di riferimento per il comando locals nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545028"
---
# <a name="locals-command-nuget-cli"></a>Comando locals (interfaccia della riga di comando di NuGet)

**Si applica a:** consumo del pacchetto &bullet; **le versioni supportate:** 3.3 +

Cancella o elenca risorse NuGet locali, ad esempio la *http-cache*, *global-packages* cartella e la cartella temporanea. Il `locals` comando può essere utilizzato anche per visualizzare un elenco di queste posizioni. Per altre informazioni, vedere [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Utilizzo

```cli
nuget locals <folder> [options]
```

in cui `<folder>` è uno dei `all`, `http-cache`, `packages-cache` *(3.5 e versioni precedenti)*, `global-packages`, `temp` *(3.4 +)*, e `plugins-cache` *(4.8)*.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| Cancella | Cancella la cartella specificata. |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| List | Elenca il percorso della cartella specificata o i percorsi di tutte le cartelle quando abbinata *tutti*. |
| Non interattive | Elimina richieste di input o conferme dell'utente. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Esempi

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Per altri esempi, vedere [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).
