<span data-ttu-id="f555a-101">L'installazione di un pacchetto avviene in tre modi:</span><span class="sxs-lookup"><span data-stu-id="f555a-101">Installing a package happens in three ways:</span></span>

| <span data-ttu-id="f555a-102">Metodo</span><span class="sxs-lookup"><span data-stu-id="f555a-102">Method</span></span> | <span data-ttu-id="f555a-103">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f555a-103">Description</span></span> | <span data-ttu-id="f555a-104">Riferimento</span><span class="sxs-lookup"><span data-stu-id="f555a-104">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f555a-105">Interfaccia della riga di comando di nuget.exe: `nuget install <package_name>`</span><span class="sxs-lookup"><span data-stu-id="f555a-105">nuget.exe CLI: `nuget install <package_name>`</span></span> | <span data-ttu-id="f555a-106">Scarica il pacchetto identificato da \<package_name\> e ne espande il contenuto in una cartella nella directory corrente.</span><span class="sxs-lookup"><span data-stu-id="f555a-106">Downloads the package identified by \<package_name\> and expands its contents into a folder in the current directory.</span></span> <span data-ttu-id="f555a-107">Se non vengono specificati pacchetti, installa tutti i pacchetti elencati nel file `packages.config` del progetto.</span><span class="sxs-lookup"><span data-stu-id="f555a-107">If no packages are specified, installs all packages listed in the project's `packages.config` file.</span></span> <span data-ttu-id="f555a-108">Non vengono apportate modifiche ad alcun file di progetto.</span><span class="sxs-lookup"><span data-stu-id="f555a-108">No changes are made to any project files.</span></span> <span data-ttu-id="f555a-109">Vengono scaricate ed espanse anche le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f555a-109">Dependencies are also downloaded and expanded.</span></span> | [<span data-ttu-id="f555a-110">CLI reference (Informazioni di riferimento sull'interfaccia della riga di comando)</span><span class="sxs-lookup"><span data-stu-id="f555a-110">CLI reference</span></span>](../tools/nuget-exe-CLI-Reference.md) |
| <span data-ttu-id="f555a-111">Console di Gestione pacchetti (Visual Studio): `Install-Package <package_name>`</span><span class="sxs-lookup"><span data-stu-id="f555a-111">Package Manager Console (Visual Studio): `Install-Package <package_name>`</span></span> | <span data-ttu-id="f555a-112">Scarica e installa il pacchetto nel progetto corrente, quindi aggiorna il file di progetto per elencare il pacchetto come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f555a-112">Downloads and installs the package into the current project, then update the project file to list the package as a dependency.</span></span> | [<span data-ttu-id="f555a-113">Package Manager Console Guide (Guida alla console di Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="f555a-113">Package Manager Console Guide</span></span>](../tools/Package-Manager-Console.md) |
| <span data-ttu-id="f555a-114">Interfaccia utente di Gestione pacchetti (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f555a-114">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="f555a-115">Offre un'interfaccia utente tramite la quale è possibile esplorare, selezionare e installare i pacchetti in un progetto.</span><span class="sxs-lookup"><span data-stu-id="f555a-115">Provides a UI through which you can browse, select, and install packages into a project.</span></span> <span data-ttu-id="f555a-116">Aggiorna il file di progetto per elencare il pacchetto come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="f555a-116">Updates the project file to list the package as a dependency.</span></span> | [<span data-ttu-id="f555a-117">Package Manager UI reference (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti)</span><span class="sxs-lookup"><span data-stu-id="f555a-117">Package Manager UI Reference</span></span>](../tools/Package-Manager-UI.md) |