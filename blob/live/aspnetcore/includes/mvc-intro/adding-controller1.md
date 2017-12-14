<span data-ttu-id="7d797-101">Wzorzec architektury Model-widok-kontroler (MVC) dzieli aplikację na trzy główne składniki: **M**odelu, **V**widoku, a **C**ontroller.</span><span class="sxs-lookup"><span data-stu-id="7d797-101">The Model-View-Controller (MVC) architectural pattern separates an app into three main components: **M**odel, **V**iew, and **C**ontroller.</span></span> <span data-ttu-id="7d797-102">Wzorzec MVC pomaga w tworzeniu aplikacji, które są bardziej testować i łatwiejsze do zaktualizowania niż tradycyjne aplikacje wbudowanymi.</span><span class="sxs-lookup"><span data-stu-id="7d797-102">The MVC pattern helps you create apps that are more testable and easier to update than traditional monolithic apps.</span></span> <span data-ttu-id="7d797-103">Aplikacji MVC zawiera:</span><span class="sxs-lookup"><span data-stu-id="7d797-103">MVC-based apps contain:</span></span>

* <span data-ttu-id="7d797-104">**M**odels: klasy reprezentujące dane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d797-104">**M**odels: Classes that represent the data of the app.</span></span> <span data-ttu-id="7d797-105">Klasy modeli umożliwia logikę weryfikacji wymuszania reguł biznesowych dla tych danych.</span><span class="sxs-lookup"><span data-stu-id="7d797-105">The model classes use validation logic to enforce business rules for that data.</span></span> <span data-ttu-id="7d797-106">Zazwyczaj obiekty modelu pobrać i przechowywanie stanu modelu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7d797-106">Typically, model objects retrieve and store model state in a database.</span></span> <span data-ttu-id="7d797-107">W tym samouczku `Movie` modelu pobiera filmu dane z bazy danych, przekazuje go do widoku lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7d797-107">In this tutorial, a `Movie` model retrieves movie data from a database, provides it to the view or updates it.</span></span> <span data-ttu-id="7d797-108">Zaktualizowane dane są zapisywane w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7d797-108">Updated data is written to a database.</span></span>

* <span data-ttu-id="7d797-109">**V**iews: widoki są składnikami wyświetlającymi interfejs użytkownika aplikacji (UI).</span><span class="sxs-lookup"><span data-stu-id="7d797-109">**V**iews: Views are the components that display the app's user interface (UI).</span></span> <span data-ttu-id="7d797-110">Ogólnie rzecz biorąc to interfejs użytkownika wyświetla dane modelu.</span><span class="sxs-lookup"><span data-stu-id="7d797-110">Generally, this UI displays the model data.</span></span>

* <span data-ttu-id="7d797-111">**C**ontrollers: klasy, które obsługuje żądania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="7d797-111">**C**ontrollers: Classes that handle browser requests.</span></span> <span data-ttu-id="7d797-112">Pobierają dane z modelu i wywołać szablonów widoków, które zwracają odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="7d797-112">They retrieve model data and call view templates that return a response.</span></span> <span data-ttu-id="7d797-113">W aplikacji MVC widoku wyświetlane są tylko informacje; Kontroler obsługuje i ma odpowiadać na dane wejściowe użytkownika i interakcja.</span><span class="sxs-lookup"><span data-stu-id="7d797-113">In an MVC app, the view only displays information; the controller handles and responds to user input and interaction.</span></span> <span data-ttu-id="7d797-114">Na przykład kontroler obsługuje wartości danych i ciągu zapytania trasy i przekazuje te wartości do modelu.</span><span class="sxs-lookup"><span data-stu-id="7d797-114">For example, the controller handles route data and query-string values, and passes these values to the model.</span></span> <span data-ttu-id="7d797-115">Model może użyć tych wartości, aby w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7d797-115">The model might use these values to query the database.</span></span> <span data-ttu-id="7d797-116">Na przykład `http://localhost:1234/Home/About` zawiera dane trasy z `Home` (kontrolera) i `About` (metoda akcji do wywołania w domu kontrolera).</span><span class="sxs-lookup"><span data-stu-id="7d797-116">For example, `http://localhost:1234/Home/About` has route data of `Home` (the controller) and `About` (the action method to call on the home controller).</span></span> <span data-ttu-id="7d797-117">`http://localhost:1234/Movies/Edit/5`to żądanie, aby edytować filmu o identyfikatorze = 5, korzystając z kontrolera filmu.</span><span class="sxs-lookup"><span data-stu-id="7d797-117">`http://localhost:1234/Movies/Edit/5` is a request to edit the movie with ID=5 using the movie controller.</span></span>  <span data-ttu-id="7d797-118">Będzie omawianiu dane trasy później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="7d797-118">We'll talk about route data later in the tutorial.</span></span>

<span data-ttu-id="7d797-119">Wzorzec MVC pomaga w tworzeniu aplikacji, których różne aspekty aplikacji (logika danych wejściowych, logika biznesowa i logika interfejsu użytkownika), zapewniając luźne powiązanie między tymi elementami.</span><span class="sxs-lookup"><span data-stu-id="7d797-119">The MVC pattern helps you create apps that separate the different aspects of the app (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="7d797-120">Wzorzec Określa, gdzie każdy rodzaj logiki powinien znajdować się w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d797-120">The pattern specifies where each kind of logic should be located in the app.</span></span> <span data-ttu-id="7d797-121">Logika interfejsu użytkownika należy w widoku.</span><span class="sxs-lookup"><span data-stu-id="7d797-121">The UI logic belongs in the view.</span></span> <span data-ttu-id="7d797-122">Logika danych wejściowych jest powiązana z kontrolerem.</span><span class="sxs-lookup"><span data-stu-id="7d797-122">Input logic belongs in the controller.</span></span> <span data-ttu-id="7d797-123">Logika biznesowa jest powiązana w modelu.</span><span class="sxs-lookup"><span data-stu-id="7d797-123">Business logic belongs in the model.</span></span> <span data-ttu-id="7d797-124">Taki rozdział pomaga w zarządzaniu złożonością podczas tworzenia aplikacji, ponieważ umożliwia ona działać na jednym aspekcie implementacji jednocześnie bez wpływu na kod innego.</span><span class="sxs-lookup"><span data-stu-id="7d797-124">This separation helps you manage complexity when you build an app, because it enables you to work on one aspect of the implementation at a time without impacting the code of another.</span></span> <span data-ttu-id="7d797-125">Na przykład można pracować w widoku kodu bez stosownie do kodu logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="7d797-125">For example, you can work on the view code without depending on the business logic code.</span></span>

<span data-ttu-id="7d797-126">Firma Microsoft opisano te pojęcia związane z tego samouczka serii i opisano, jak ich używać do tworzenia aplikacji filmu.</span><span class="sxs-lookup"><span data-stu-id="7d797-126">We cover these concepts in this tutorial series and show you how to use them to build a movie app.</span></span> <span data-ttu-id="7d797-127">Projekt MVC zawiera foldery *kontrolerów* i *widoków*.</span><span class="sxs-lookup"><span data-stu-id="7d797-127">The MVC project contains folders for the *Controllers* and *Views*.</span></span>