---
title: Note sulla versione per NuGet 4.9 RTM
description: Note sulla versione per NuGet 4.9 incluse informazioni su problemi noti, correzioni di bug, nuove funzionalità e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735136"
---
# <a name="nuget-49-release-notes"></a>Note sulla versione per NuGet 4.9

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| **4.9.0** | Visual Studio 2017 versione 15.9.0 | 2.1.500, 2.2.100 |
| **4.9.1** | N/D | N/D |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 versione 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a>Riepilogo: Novità nella versione 4.9.0

* Firma: abilitare ClientPolicies per richiedere l'uso di un set di autori e repository attendibili elencati nel file NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [post di blog](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Creare file ".snupkg" per contenere i simboli nel pacchetto -- ottimizzare il push per fare in modo che il protocollo nuget accetti file snupkg per il server dei simboli - [#6878](https://github.com/NuGet/Home/issues/6878), [post di blog](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Plug-in credenziali NuGet versione 2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Pacchetti NuGet completi - Licenza - [#4628](https://github.com/NuGet/Home/issues/4628), [annuncio](https://github.com/NuGet/Announcements/issues/32)

* Abilitare i metadati "GeneratePathProperty" con consenso esplicito per un PackageReference per generare una proprietà MSBuild per ogni pacchetto per la directory "Foo.Bar\1.0\" - [#6949](https://github.com/NuGet/Home/issues/6949)

* Migliorare la soddisfazione dei clienti con operazioni NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

* Gli avvisi elevati a errori (tramite WarnAsErrors) generati da PackageExtraction non devono mai lasciare in giro il pacchetto estratto - [ #7445](https://github.com/NuGet/Home/issues/7445)

* I pacchetti con firma non valida non devono finire nella cartella dei pacchetti globale - [#7423](https://github.com/NuGet/Home/issues/7423)

* La generazione di reindirizzamenti di binding non deve ignorare gli assembly di facciata - [#7393](https://github.com/NuGet/Home/issues/7393)

* Il metodo Equals di VersionRange non confronta intervalli mobili - [#7324](https://github.com/NuGet/Home/issues/7324)

* Ripristino: regressione delle prestazioni usando il nuovo stack HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)

* L'aggiornamento di un pacchetto non deve modificare PrivateAssets di un PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)

* Firma: la firma deve avere esito negativo se un pacchetto include troppe voci di pacchetto (>65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* Il percorso di codice "dotnet nuget push" deve supportare il nuovo provider di credenziali - [#7233](https://github.com/NuGet/Home/issues/7233)

* Supporto dell'esecuzione dei plug-in con impostazioni cultura inglese non dipendenti da paese/area geografica (come accade in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)

* Il comando nuget sources add non deve eliminare le credenziali da NuGet.Config - [#7200](https://github.com/NuGet/Home/issues/7200)

* L'installazione di un devDependency PackageReference deve usare l'impostazione predefinita excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* Correggere l'opzione migrator in modo da visualizzarla per tutti i progetti e che mostri un errore se il progetto è incompatibile - [#6958](https://github.com/NuGet/Home/issues/6958)

* Il comando "dotnet add package" deve eseguire il commit del ripristino eseguito nel file di asset - [#6928](https://github.com/NuGet/Home/issues/6928)

* Firma: migliorare i messaggi di errore correlati alla firma- [#6906](https://github.com/NuGet/Home/issues/6906)

* [Errore di test] [zh-TW] Stringa "Console di Gestione pacchetti" non localizzata nella Console di Gestione pacchetti - [#6381](https://github.com/NuGet/Home/issues/6381)

* Il messaggio di errore "Impossibile trovare le informazioni sul progetto" deve essere un po' più specifico all'interno di Visual Studio - [#5350](https://github.com/NuGet/Home/issues/5350)

* Messaggio di errore poco utile quando si usa in modo non corretto il tag version per nuspec di nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - firma: supporto del protocollo NuGet: risorsa RepositorySignatures/4.9.0 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR -Il file nupkg.metadata verrà ora creato durante l'estrazione del pacchetto - Contiene "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Verifica authenticode non eseguita per i plug-in durante l'esecuzione in Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Elenco di tutti i problemi corretti nella versione 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Riepilogo: Novità nella versione 4.9.1

* Aggiunta del supporto per la lettura di una scrittura in NuGet.Config tramite un nuovo comando trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

* Correzione della generazione di collegamenti di licenza - [#7515](https://github.com/NuGet/Home/issues/7515)

* Regressione dei codici di errore per la convalida delle firme- [#7492](https://github.com/NuGet/Home/issues/7492)

* Il pacchetto NuGet.Build.Tasks.Pack non include informazioni di licenza - [#7379](https://github.com/NuGet/Home/issues/7379)

[Elenco di tutti i problemi corretti nella versione 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Riepilogo: Novità nella versione 4.9.2

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

* VS/dotnet.exe/nuget.exe/msbuild.exe restore non usa credenziali quando il nome dell'origine contiene uno spazio vuoto - [#7517](https://github.com/NuGet/Home/issues/7517)

* Problemi di accessibilità per LicenseFileWindow e LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)

* Correggere FormatException in DateTime.Parse da DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)

[Elenco di tutti i problemi corretti nella versione 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a>Problemi noti

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive genera un errore in Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problema
L'argomento `--interactive` non viene inoltrato dall'interfaccia della riga di comando dotnet e genera l'errore `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Soluzione alternativa
Eseguire qualsiasi altro comando dotnet con l'opzione interactive, ad esempio `dotnet restore --interactive`, ed eseguire l'autenticazione. L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali. Eseguire quindi `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problema
Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed. Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.

#### <a name="workaround"></a>Soluzione alternativa
Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su un valore vuoto. `<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.
