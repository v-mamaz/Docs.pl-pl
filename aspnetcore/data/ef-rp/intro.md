---
title: Stron razor z Entity Framework Core - 1 samouczka 8
author: rick-anderson
description: "Pokazuje, jak utworzyć aplikację stron Razor przy użyciu programu Entity Framework Core"
keywords: Samouczek platformy ASP.NET Core Entity Framework Core,
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/intro
ms.openlocfilehash: 571d683636244565b184cfec49061ec656377f11
ms.sourcegitcommit: 198fb0488e961048bfa376cf58cb853ef1d1cb91
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="getting-started-with-razor-pages-and-entity-framework-core-using-visual-studio-1-of-8"></a><span data-ttu-id="45bb4-104">Wprowadzenie do stron Razor i Entity Framework Core za pomocą programu Visual Studio (1 8)</span><span class="sxs-lookup"><span data-stu-id="45bb4-104">Getting started with Razor Pages and Entity Framework Core using Visual Studio (1 of 8)</span></span>

<span data-ttu-id="45bb4-105">Przez [Dykstra Tomasz](https://github.com/tdykstra) i [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="45bb4-105">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="45bb4-106">Przykładową aplikację sieci web firmy Contoso University przedstawia sposób tworzenia aplikacji sieci web platformy ASP.NET Core 2.0 MVC za pomocą Core Entity Framework (EF) 2.0 i programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="45bb4-106">The Contoso University sample web app demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="45bb4-107">Przykładowa aplikacja jest witryną sieci web dla fikcyjnej uniwersytetu Contoso.</span><span class="sxs-lookup"><span data-stu-id="45bb4-107">The sample app is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="45bb4-108">Obejmuje funkcje, takie jak wprowadzenia studentów, tworzenie kursu i instruktora przypisania.</span><span class="sxs-lookup"><span data-stu-id="45bb4-108">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="45bb4-109">Ta strona jest to pierwszy z serii samouczków, które opisują sposób kompilowania aplikacji przykładowej Contoso University.</span><span class="sxs-lookup"><span data-stu-id="45bb4-109">This page is the first in a series of tutorials that explain how to build the Contoso University sample app.</span></span>

[<span data-ttu-id="45bb4-110">Pobrania lub wyświetlenia ukończonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-110">Download or view the completed app.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) <span data-ttu-id="45bb4-111">[Instrukcje pobierania](xref:tutorials/index#how-to-download-a-sample).</span><span class="sxs-lookup"><span data-stu-id="45bb4-111">[Download instructions](xref:tutorials/index#how-to-download-a-sample).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45bb4-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="45bb4-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="45bb4-113">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="45bb4-113">Troubleshooting</span></span>

<span data-ttu-id="45bb4-114">Jeśli napotkasz problem, nie można rozpoznać zwykle można znaleźć rozwiązania na podstawie porównania ilości kodu do [ukończone etap](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) lub [projektu zakończone](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span><span class="sxs-lookup"><span data-stu-id="45bb4-114">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) or [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu-final).</span></span> <span data-ttu-id="45bb4-115">Aby uzyskać listę typowych błędów i sposobów ich rozwiązania, zobacz [sekcji rozwiązywania problemów ostatniego samouczek z tej serii](xref:data/ef-mvc/advanced#common-errors).</span><span class="sxs-lookup"><span data-stu-id="45bb4-115">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](xref:data/ef-mvc/advanced#common-errors).</span></span> <span data-ttu-id="45bb4-116">Nie można znaleźć, muszą, możesz wysłać zapytanie do StackOverflow.com dla [platformy ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) lub [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span><span class="sxs-lookup"><span data-stu-id="45bb4-116">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP]
> <span data-ttu-id="45bb4-117">Tej serii samouczków opiera się na czynności wykonane w starszych samouczki.</span><span class="sxs-lookup"><span data-stu-id="45bb4-117">This series of tutorials builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="45bb4-118">Warto zapisać kopię projektu po każdym pomyślnym ukończeniu samouczka.</span><span class="sxs-lookup"><span data-stu-id="45bb4-118">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="45bb4-119">Jeśli wystąpiły problemy, możesz zacząć od nowa z poprzednich samouczek zamiast po powrocie do początku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-119">If you run into problems, you can start over from the previous tutorial instead of going back to the beginning.</span></span> <span data-ttu-id="45bb4-120">Alternatywnie możesz pobrać [ukończone etap](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) i zacząć od nowa przy użyciu etap ukończone.</span><span class="sxs-lookup"><span data-stu-id="45bb4-120">Alternatively, you can download a [completed stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots) and start over using the completed stage.</span></span>

## <a name="the-contoso-university-web-app"></a><span data-ttu-id="45bb4-121">Aplikacja sieci web firmy Contoso University</span><span class="sxs-lookup"><span data-stu-id="45bb4-121">The Contoso University web app</span></span>

<span data-ttu-id="45bb4-122">Aplikacji utworzony w tych samouczkach jest witryną sieci web university podstawowe.</span><span class="sxs-lookup"><span data-stu-id="45bb4-122">The app built in these tutorials is a basic university web site.</span></span>

<span data-ttu-id="45bb4-123">Użytkownicy mogą wyświetlać i uczniów, kursu i informacje o wykładowcach aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-123">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="45bb4-124">Poniżej przedstawiono kilka ekranów utworzone w samouczku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-124">Here are a few of the screens created in the tutorial.</span></span>

![Strona indeksu uczniów lub studentów](intro/_static/students-index.png)

![Strona Edytuj uczniów lub studentów](intro/_static/student-edit.png)

<span data-ttu-id="45bb4-127">Styl interfejsu użytkownika w tej lokacji jest bliski co to jest generowany przez wbudowane szablony.</span><span class="sxs-lookup"><span data-stu-id="45bb4-127">The UI style of this site is close to what's generated by the built-in templates.</span></span> <span data-ttu-id="45bb4-128">Samouczek koncentruje się na podstawowych EF Razor strony, nie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="45bb4-128">The tutorial focus is on EF Core with Razor Pages, not the UI.</span></span>

## <a name="create-a-razor-pages-web-app"></a><span data-ttu-id="45bb4-129">Tworzenie aplikacji sieci web Razor strony</span><span class="sxs-lookup"><span data-stu-id="45bb4-129">Create a Razor Pages web app</span></span>

* <span data-ttu-id="45bb4-130">W programie Visual Studio **pliku** menu, wybierz opcję **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="45bb4-130">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="45bb4-131">Utwórz nową aplikację sieci Web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="45bb4-131">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="45bb4-132">Nazwij projekt **ContosoUniversity**.</span><span class="sxs-lookup"><span data-stu-id="45bb4-132">Name the project **ContosoUniversity**.</span></span> <span data-ttu-id="45bb4-133">Ważne jest, aby nazwa projektu *ContosoUniversity* tak dopasuj przestrzenie nazw, jeśli kod jest skopiowane i wklejone.</span><span class="sxs-lookup"><span data-stu-id="45bb4-133">It's important to name the project *ContosoUniversity* so the namespaces match when code is copy/pasted.</span></span>
 <span data-ttu-id="45bb4-134">![nową aplikację sieci Web Core ASP.NET](intro/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="45bb4-134">![new ASP.NET Core Web Application](intro/_static/np.png)</span></span>
* <span data-ttu-id="45bb4-135">Wybierz **ASP.NET Core 2.0** w listy rozwijanej, a następnie wybierz **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="45bb4-135">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>
 <span data-ttu-id="45bb4-136">![Aplikacja sieci Web (Razor strony)](../../mvc/razor-pages/index/_static/np2.png)</span><span class="sxs-lookup"><span data-stu-id="45bb4-136">![Web Application (Razor Pages)](../../mvc/razor-pages/index/_static/np2.png)</span></span>

<span data-ttu-id="45bb4-137">Naciśnij klawisz **F5** do uruchomienia aplikacji w trybie debugowania lub **Ctrl-F5** działać bez dołączanie debugera</span><span class="sxs-lookup"><span data-stu-id="45bb4-137">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="45bb4-138">Ustawianie stylów lokacji</span><span class="sxs-lookup"><span data-stu-id="45bb4-138">Set up the site style</span></span>

<span data-ttu-id="45bb4-139">Kilka zmian ustawienia lokacji menu, układu i strony głównej.</span><span class="sxs-lookup"><span data-stu-id="45bb4-139">A few changes set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="45bb4-140">Otwórz *Pages/_Layout.cshtml* i wprowadź następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="45bb4-140">Open *Pages/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="45bb4-141">Zmienić każde wystąpienie "ContosoUniversity" na "University firmy Contoso".</span><span class="sxs-lookup"><span data-stu-id="45bb4-141">Change each occurrence of "ContosoUniversity" to "Contoso University."</span></span> <span data-ttu-id="45bb4-142">Istnieją trzy wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="45bb4-142">There are three occurrences.</span></span>

* <span data-ttu-id="45bb4-143">Dodaj elementy menu dla **studentów**, **kursów**, **instruktorów**, i **działów**i Usuń **skontaktuj się z** wpisu menu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-143">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="45bb4-144">Zmiany zostały wyróżnione.</span><span class="sxs-lookup"><span data-stu-id="45bb4-144">The changes are highlighted.</span></span>

[!code-html[](intro/samples/cu/Pages/_Layout.cshtml?highlight=6,29,35-38,47&range=1-50)]

<span data-ttu-id="45bb4-145">W *Pages/Index.cshtml*, Zastąp zawartość pliku następującym kodem, aby zastąpić tekst o ASP.NET i MVC tekst o tej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="45bb4-145">In *Pages/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this app:</span></span>

[!code-html[](intro/samples/cu/Pages/Index.cshtml)]

<span data-ttu-id="45bb4-146">Naciśnij klawisze CTRL + F5, aby uruchomić projekt.</span><span class="sxs-lookup"><span data-stu-id="45bb4-146">Press CTRL+F5 to run the project.</span></span> <span data-ttu-id="45bb4-147">Strona główna jest wyświetlana z kartami utworzone w następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="45bb4-147">The home page is displayed with tabs created in the following tutorials:</span></span>

![Strona główna University firmy Contoso](intro/_static/home-page.png)

## <a name="create-the-data-model"></a><span data-ttu-id="45bb4-149">Tworzenie modelu danych</span><span class="sxs-lookup"><span data-stu-id="45bb4-149">Create the data model</span></span>

<span data-ttu-id="45bb4-150">Tworzenie klas jednostek dla aplikacji Contoso University.</span><span class="sxs-lookup"><span data-stu-id="45bb4-150">Create entity classes for the Contoso University app.</span></span> <span data-ttu-id="45bb4-151">Rozpocząć następujące trzy jednostki:</span><span class="sxs-lookup"><span data-stu-id="45bb4-151">Start with the following three entities:</span></span>

![Diagram modelu danych kursu-rejestracji — dla użytkowników domowych](intro/_static/data-model-diagram.png)

<span data-ttu-id="45bb4-153">Brak relacji jeden do wielu między `Student` i `Enrollment` jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-153">There's a one-to-many relationship between `Student` and `Enrollment` entities.</span></span> <span data-ttu-id="45bb4-154">Brak relacji jeden do wielu między `Course` i `Enrollment` jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-154">There's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="45bb4-155">Gdy uczniowie mogą rejestrować się w dowolnej liczby kursów.</span><span class="sxs-lookup"><span data-stu-id="45bb4-155">A student can enroll in any number of courses.</span></span> <span data-ttu-id="45bb4-156">Kursu może mieć dowolną liczbę studentów zarejestrowane w nim.</span><span class="sxs-lookup"><span data-stu-id="45bb4-156">A course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="45bb4-157">W poniższych sekcjach utworzeniu klasy dla każdego z tych obiektów.</span><span class="sxs-lookup"><span data-stu-id="45bb4-157">In the following sections, a class for each one of these entities is created.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="45bb4-158">Jednostki dla użytkowników domowych</span><span class="sxs-lookup"><span data-stu-id="45bb4-158">The Student entity</span></span>

![Diagram jednostek dla użytkowników domowych](intro/_static/student-entity.png)

<span data-ttu-id="45bb4-160">Utwórz *modele* folderu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-160">Create a *Models* folder.</span></span> <span data-ttu-id="45bb4-161">W *modele* folderu, Utwórz plik klasy o nazwie *Student.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="45bb4-161">In the *Models* folder, create a class file named *Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="45bb4-162">`ID` Właściwości staje się kolumna klucza podstawowego tabeli bazy danych (bazy danych), która odnosi się do tej klasy.</span><span class="sxs-lookup"><span data-stu-id="45bb4-162">The `ID` property becomes the primary key column of the database (DB) table that corresponds to this class.</span></span> <span data-ttu-id="45bb4-163">Domyślnie EF rdzenie będą interpretowane przez właściwość o nazwie `ID` lub `classnameID` jako klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="45bb4-163">By default, EF Core interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="45bb4-164">`Enrollments` Właściwość jest właściwością nawigacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-164">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="45bb4-165">Właściwości nawigacji, połącz się z innymi obiektami, które są powiązane z tą jednostką.</span><span class="sxs-lookup"><span data-stu-id="45bb4-165">Navigation properties link to other entities that are related to this entity.</span></span> <span data-ttu-id="45bb4-166">W takim przypadku `Enrollments` właściwość `Student entity` przechowuje wszystkie `Enrollment` jednostek, które są powiązane z których `Student`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-166">In this case, the `Enrollments` property of a `Student entity` holds all of the `Enrollment` entities that are related to that `Student`.</span></span> <span data-ttu-id="45bb4-167">Na przykład, jeśli wiersz uczniów w bazie danych ma dwa powiązane wiersze rejestracji `Enrollments` właściwość nawigacji zawiera tych dwóch `Enrollment` jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-167">For example, if a Student row in the DB has two related Enrollment rows, the `Enrollments` navigation property contains those two `Enrollment` entities.</span></span> <span data-ttu-id="45bb4-168">Powiązane `Enrollment` wiersz jest wierszem zawiera Studenta dla tej wartości klucza podstawowego w `StudentID` kolumny.</span><span class="sxs-lookup"><span data-stu-id="45bb4-168">A related `Enrollment` row is a row that contains that student's primary key value in the `StudentID` column.</span></span> <span data-ttu-id="45bb4-169">Na przykład, załóżmy, że uczniów o identyfikatorze = 1 ma dwa wiersze `Enrollment` tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-169">For example, suppose the student with ID=1 has two rows in the `Enrollment` table.</span></span> <span data-ttu-id="45bb4-170">`Enrollment` Tabela zawiera dwa wiersze z `StudentID` = 1.</span><span class="sxs-lookup"><span data-stu-id="45bb4-170">The `Enrollment` table has two rows with `StudentID` = 1.</span></span> <span data-ttu-id="45bb4-171">`StudentID`jest to kolumna klucza obcego w `Enrollment` tabeli określający student w `Student` tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-171">`StudentID` is a foreign key in the `Enrollment` table that specifies the student in the `Student` table.</span></span>

<span data-ttu-id="45bb4-172">Jeśli właściwość nawigacji może zawierać wiele jednostek, właściwość nawigacji musi być typem listy, takich jak `ICollection<T>`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-172">If a navigation property can hold multiple entities, the navigation property must be a list type, such as `ICollection<T>`.</span></span> <span data-ttu-id="45bb4-173">`ICollection<T>`można określić, takie jak typ lub `List<T>` lub `HashSet<T>`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-173">`ICollection<T>` can be specified, or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="45bb4-174">Gdy `ICollection<T>` jest używana, tworzy EF Core `HashSet<T>` kolekcji domyślnie.</span><span class="sxs-lookup"><span data-stu-id="45bb4-174">When `ICollection<T>` is used, EF Core creates a `HashSet<T>` collection by default.</span></span> <span data-ttu-id="45bb4-175">Właściwości nawigacji, które zawierają wiele jednostek pochodzą z relacji wiele do wielu oraz jeden do wielu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-175">Navigation properties that hold multiple entities come from many-to-many and one-to-many relationships.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="45bb4-176">Jednostka rejestracji</span><span class="sxs-lookup"><span data-stu-id="45bb4-176">The Enrollment entity</span></span>

![Diagram jednostek rejestracji](intro/_static/enrollment-entity.png)

<span data-ttu-id="45bb4-178">W *modele* folderu, Utwórz *Enrollment.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="45bb4-178">In the *Models* folder, create *Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="45bb4-179">`EnrollmentID` Właściwość jest kluczem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="45bb4-179">The `EnrollmentID` property is the primary key.</span></span> <span data-ttu-id="45bb4-180">Używa tej jednostki `classnameID` wzorca zamiast `ID` jak `Student` jednostki.</span><span class="sxs-lookup"><span data-stu-id="45bb4-180">This entity uses the `classnameID` pattern instead of `ID` like the `Student` entity.</span></span> <span data-ttu-id="45bb4-181">Zwykle programiści wybierz jeden wzorzec i używać go w modelu danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-181">Typically developers choose one pattern and use it throughout the data model.</span></span> <span data-ttu-id="45bb4-182">W samouczku nowsze za pomocą Identyfikatora bez classname przedstawiono ułatwiające wdrażanie dziedziczenia w modelu danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-182">In a later tutorial, using ID without classname is shown to make it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="45bb4-183">`Grade` Jest właściwość `enum`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-183">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="45bb4-184">Znak zapytania po `Grade` deklaracji typu wskazuje, że `Grade` właściwość dopuszcza wartość null.</span><span class="sxs-lookup"><span data-stu-id="45bb4-184">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="45bb4-185">Ma wartość null, która różni się od zera klasy — wartość null oznacza, że klasa nie jest znana lub nie została jeszcze przypisana.</span><span class="sxs-lookup"><span data-stu-id="45bb4-185">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="45bb4-186">`StudentID` Właściwość jest kluczem obcym i odpowiednią właściwość nawigacji jest `Student`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-186">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="45bb4-187">`Enrollment` Jednostka jest skojarzony z jednym `Student` jednostki, więc ta właściwość zawiera jeden `Student` jednostki.</span><span class="sxs-lookup"><span data-stu-id="45bb4-187">An `Enrollment` entity is associated with one `Student` entity, so the property contains a single `Student` entity.</span></span> <span data-ttu-id="45bb4-188">`Student` Jednostki różni się od `Student.Enrollments` właściwość nawigacji, która zawiera wiele `Enrollment` jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-188">The `Student` entity differs from the `Student.Enrollments` navigation property, which contains multiple `Enrollment` entities.</span></span>

<span data-ttu-id="45bb4-189">`CourseID` Właściwość jest kluczem obcym i odpowiednią właściwość nawigacji jest `Course`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-189">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="45bb4-190">`Enrollment` Jednostka jest skojarzony z jednym `Course` jednostki.</span><span class="sxs-lookup"><span data-stu-id="45bb4-190">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="45bb4-191">EF Core interpretuje właściwość jako klucz obcy, jeśli jest o nazwie `<navigation property name><primary key property name>`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-191">EF Core interprets a property as a foreign key if it's named `<navigation property name><primary key property name>`.</span></span> <span data-ttu-id="45bb4-192">Na przykład`StudentID` dla `Student` właściwość nawigacji, ponieważ `Student` klucza podstawowego jednostki jest `ID`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-192">For example,`StudentID` for the `Student` navigation property, since the `Student` entity's primary key is `ID`.</span></span> <span data-ttu-id="45bb4-193">Właściwości klucza obcego może również być nazwany `<primary key property name>`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-193">Foreign key properties can also be named `<primary key property name>`.</span></span> <span data-ttu-id="45bb4-194">Na przykład `CourseID` ponieważ `Course` klucza podstawowego jednostki jest `CourseID`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-194">For example, `CourseID` since the `Course` entity's primary key is `CourseID`.</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="45bb4-195">Jednostki ciągu</span><span class="sxs-lookup"><span data-stu-id="45bb4-195">The Course entity</span></span>

![Diagram jednostek kursu](intro/_static/course-entity.png)

<span data-ttu-id="45bb4-197">W *modele* folderu, Utwórz *Course.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="45bb4-197">In the *Models* folder, create *Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="45bb4-198">`Enrollments` Właściwość jest właściwością nawigacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-198">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="45bb4-199">A `Course` jednostka może być powiązane z dowolną liczbę `Enrollment` jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-199">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="45bb4-200">`DatabaseGenerated` Atrybutu umożliwia aplikacji określenie klucza podstawowego, a nie bazy danych o jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-200">The `DatabaseGenerated` attribute allows the app to specify the primary key rather than having the DB generate it.</span></span>

## <a name="create-the-schoolcontext-db-context"></a><span data-ttu-id="45bb4-201">Tworzenie kontekstu SchoolContext DB</span><span class="sxs-lookup"><span data-stu-id="45bb4-201">Create the SchoolContext DB context</span></span>

<span data-ttu-id="45bb4-202">Klasy głównym, która koordynuje EF podstawową funkcjonalność o dany model danych jest klasa kontekstu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-202">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="45bb4-203">Kontekst danych jest określana na podstawie `Microsoft.EntityFrameworkCore.DbContext`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-203">The data context is derived from `Microsoft.EntityFrameworkCore.DbContext`.</span></span> <span data-ttu-id="45bb4-204">Kontekst danych określa jednostki, które znajdują się w modelu danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-204">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="45bb4-205">W tym projekcie klasy o nazwie `SchoolContext`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-205">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="45bb4-206">W folderze projektu Utwórz folder o nazwie *danych*.</span><span class="sxs-lookup"><span data-stu-id="45bb4-206">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="45bb4-207">W *danych* Utwórz folder *SchoolContext.cs* następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="45bb4-207">In the *Data* folder create *SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="45bb4-208">Ten kod tworzy `DbSet` właściwości dla każdego zestawu jednostek.</span><span class="sxs-lookup"><span data-stu-id="45bb4-208">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="45bb4-209">W terminologii EF rdzeni:</span><span class="sxs-lookup"><span data-stu-id="45bb4-209">In EF Core terminology:</span></span>

* <span data-ttu-id="45bb4-210">Zwykle zestawu jednostek odnosi się do tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-210">An entity set typically corresponds to a DB table.</span></span>
* <span data-ttu-id="45bb4-211">Jednostka odpowiada wiersza w tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-211">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="45bb4-212">`DbSet<Enrollment>`i `DbSet<Course>` można pominąć.</span><span class="sxs-lookup"><span data-stu-id="45bb4-212">`DbSet<Enrollment>` and `DbSet<Course>` can be omitted.</span></span> <span data-ttu-id="45bb4-213">Podstawowe EF są uwzględniane niejawnie ponieważ `Student` odwołań do jednostek `Enrollment` jednostki i `Enrollment` odwołań do jednostek `Course` jednostki.</span><span class="sxs-lookup"><span data-stu-id="45bb4-213">EF Core includes them implicitly because the `Student` entity references the `Enrollment` entity, and the `Enrollment` entity references the `Course` entity.</span></span> <span data-ttu-id="45bb4-214">W tym samouczku, Zachowaj `DbSet<Enrollment>` i `DbSet<Course>` w `SchoolContext`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-214">For this tutorial, keep `DbSet<Enrollment>` and `DbSet<Course>` in the `SchoolContext`.</span></span>

<span data-ttu-id="45bb4-215">Po utworzeniu bazy danych EF Core tworzy tabele, które mają taki sam, jak nazwy `DbSet` nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="45bb4-215">When the DB is created, EF Core creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="45bb4-216">Nazwy właściwości w kolekcji są zwykle w liczbie mnogiej (studentów zamiast uczniów).</span><span class="sxs-lookup"><span data-stu-id="45bb4-216">Property names for collections are typically plural (Students rather than Student).</span></span> <span data-ttu-id="45bb4-217">Deweloperzy nie zgadzają się o czy nazwy tabeli powinien być w liczbie mnogiej.</span><span class="sxs-lookup"><span data-stu-id="45bb4-217">Developers disagree about whether table names should be plural.</span></span> <span data-ttu-id="45bb4-218">Te samouczki domyślne zachowanie jest zastępowany przez określenie nazw pojedynczej tabeli w DbContext.</span><span class="sxs-lookup"><span data-stu-id="45bb4-218">For these tutorials, the default behavior is overridden by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="45bb4-219">Do określenia nazwy w liczbie pojedynczej tabeli, Dodaj następujący wyróżniony kod:</span><span class="sxs-lookup"><span data-stu-id="45bb4-219">To specify singular table names, add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="45bb4-220">Zarejestruj kontekście iniekcji zależności</span><span class="sxs-lookup"><span data-stu-id="45bb4-220">Register the context with dependency injection</span></span>

<span data-ttu-id="45bb4-221">Obejmuje platformy ASP.NET Core [iniekcji zależności](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="45bb4-221">ASP.NET Core includes [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="45bb4-222">Usługi (takie jak kontekst danych podstawowych EF) są zarejestrowane w usłudze iniekcji zależności podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-222">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="45bb4-223">Składniki, które wymagają tych usług (takich jak strony Razor) są udostępniane tych usług za pomocą parametrów konstruktora.</span><span class="sxs-lookup"><span data-stu-id="45bb4-223">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="45bb4-224">Kod konstruktora, który pobiera wystąpienia kontekstu db przedstawiono w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="45bb4-224">The constructor code that gets a db context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="45bb4-225">Aby zarejestrować `SchoolContext` jako usługa, otwórz *Startup.cs*i Dodaj wyróżnione wiersze do `ConfigureServices` metody.</span><span class="sxs-lookup"><span data-stu-id="45bb4-225">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="45bb4-226">Nazwa ciągu połączenia jest przekazywany do kontekstu przez wywołanie metody `DbContextOptionsBuilder` obiektu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-226">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="45bb4-227">Dla wdrożenia lokalnego [systemu konfiguracji platformy ASP.NET Core](xref:fundamentals/configuration/index) odczytuje parametry połączenia z *appsettings.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-227">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="45bb4-228">Dodaj `using` instrukcje dla `ContosoUniversity.Data` i `Microsoft.EntityFrameworkCore` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="45bb4-228">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces.</span></span> <span data-ttu-id="45bb4-229">Skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="45bb4-229">Build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="45bb4-230">Otwórz *appsettings.json* i dodaj ciąg połączenia, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="45bb4-230">Open the *appsettings.json* file and add a connection string as shown in the following code:</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

<span data-ttu-id="45bb4-231">Poprzednie parametry połączenia używane `ConnectRetryCount=0` zapobiegające [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) z wiszące.</span><span class="sxs-lookup"><span data-stu-id="45bb4-231">The preceding connection string uses `ConnectRetryCount=0` to prevent [SQLClient](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/sqlclient-for-the-entity-framework) from hanging.</span></span>

### <a name="sql-server-express-localdb"></a><span data-ttu-id="45bb4-232">SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="45bb4-232">SQL Server Express LocalDB</span></span>

<span data-ttu-id="45bb4-233">Parametry połączenia wskazują bazy danych LocalDB programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="45bb4-233">The connection string specifies a SQL Server LocalDB DB.</span></span> <span data-ttu-id="45bb4-234">LocalDB jest wersja programu SQL Server Express aparatu bazy danych i jest przeznaczony do tworzenia aplikacji, a nie do użytku produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="45bb4-234">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for app development, not production use.</span></span> <span data-ttu-id="45bb4-235">LocalDB rozpoczyna się na żądanie i działa w trybie użytkownika, więc nie ma żadnych złożonych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-235">LocalDB starts on demand and runs in user mode, so there is no complex configuration.</span></span> <span data-ttu-id="45bb4-236">Domyślnie tworzy LocalDB *.mdf* pliki bazy danych w `C:/Users/<user>` katalogu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-236">By default, LocalDB creates *.mdf* DB files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-db-with-test-data"></a><span data-ttu-id="45bb4-237">Dodaj kod, aby zainicjować bazy danych z danych testowych</span><span class="sxs-lookup"><span data-stu-id="45bb4-237">Add code to initialize the DB with test data</span></span>

<span data-ttu-id="45bb4-238">Podstawowe EF tworzy puste bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-238">EF Core creates an empty DB.</span></span> <span data-ttu-id="45bb4-239">W tej sekcji *inicjatora* zapisywana jest metoda wypełnić je danymi testu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-239">In this section, a *Seed* method is written to populate it with test data.</span></span>

<span data-ttu-id="45bb4-240">W *danych* folderu, Utwórz nowy plik klasy o nazwie *DbInitializer.cs* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="45bb4-240">In the *Data* folder, create a new class file named *DbInitializer.cs* and add the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="45bb4-241">Kod sprawdza, czy wszystkie studentów w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-241">The code checks if there are any students in the DB.</span></span> <span data-ttu-id="45bb4-242">Jeśli w bazie danych nie nie studentów, bazy danych jest obsługiwany z danych testowych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-242">If there are no students in the DB, the DB is seeded with test data.</span></span> <span data-ttu-id="45bb4-243">Ładuje dane testowe do tablic zamiast `List<T>` kolekcje w celu optymalizacji wydajności.</span><span class="sxs-lookup"><span data-stu-id="45bb4-243">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="45bb4-244">`EnsureCreated` Metoda automatycznie tworzy bazy danych dla kontekst bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-244">The `EnsureCreated` method automatically creates the DB for the DB context.</span></span> <span data-ttu-id="45bb4-245">Jeśli baza danych istnieje, `EnsureCreated` zwraca bez modyfikowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-245">If the DB exists, `EnsureCreated` returns without modifying the DB.</span></span>

<span data-ttu-id="45bb4-246">W *Program.cs*, zmodyfikuj `Main` metody wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="45bb4-246">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="45bb4-247">Pobierz wystąpienia kontekstu DB z kontenera iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="45bb4-247">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="45bb4-248">Wywołaj metodę inicjatora, przekazanie jej w kontekście.</span><span class="sxs-lookup"><span data-stu-id="45bb4-248">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="45bb4-249">Po zakończeniu metody inicjatora, należy dysponować kontekstu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-249">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="45bb4-250">Poniższy kod przedstawia zaktualizowanego *Program.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-250">The following code shows the updated *Program.cs* file.</span></span>

[!code-csharp[Main](intro/samples/cu/ProgramOriginal.cs?name=snippet)]

<span data-ttu-id="45bb4-251">Podczas pierwszego uruchomienia aplikacji bazy danych jest utworzony i rozpoczęta z danych testowych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-251">The first time the app is run, the DB is created and seeded with test data.</span></span> <span data-ttu-id="45bb4-252">Po zaktualizowaniu modelu danych:</span><span class="sxs-lookup"><span data-stu-id="45bb4-252">When the data model is updated:</span></span>
* <span data-ttu-id="45bb4-253">Usuń bazę danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-253">Delete the DB.</span></span>
* <span data-ttu-id="45bb4-254">Metoda inicjatora aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-254">Update the seed method.</span></span>
* <span data-ttu-id="45bb4-255">Uruchom aplikację i utworzeniu nowego wprowadzonych bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-255">Run the app and a new seeded DB is created.</span></span> 

<span data-ttu-id="45bb4-256">W kolejnych samouczkach bazy danych jest aktualizowany, gdy dane modelu zmiany, bez usunięcia i ponownego utworzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-256">In later tutorials, the DB is updated when the data model changes, without deleting and re-creating the DB.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling"></a><span data-ttu-id="45bb4-257">Dodawanie szkieletu narzędzi</span><span class="sxs-lookup"><span data-stu-id="45bb4-257">Add scaffold tooling</span></span>

<span data-ttu-id="45bb4-258">W tej sekcji konsoli Menedżera pakietów (PMC) służy do dodawania pakietu generowania kodu sieci web programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45bb4-258">In this section, the Package Manager Console (PMC) is used to add the Visual Studio web code generation package.</span></span> <span data-ttu-id="45bb4-259">Ten pakiet jest wymagana do uruchamiania aparatu szkieletów.</span><span class="sxs-lookup"><span data-stu-id="45bb4-259">This package is required to run the scaffolding engine.</span></span>

<span data-ttu-id="45bb4-260">Z **narzędzia** menu, wybierz opcję **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="45bb4-260">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="45bb4-261">W konsoli Menedżera pakietów (PMC) wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="45bb4-261">In the Package Manager Console (PMC), enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Utils
```

<span data-ttu-id="45bb4-262">Poprzednie polecenie dodaje pakietów NuGet do pliku *.csproj:</span><span class="sxs-lookup"><span data-stu-id="45bb4-262">The previous command adds the NuGet packages to the *.csproj file:</span></span>

[!code-csharp[Main](intro/samples/cu/ContosoUniversity1_csproj.txt?highlight=7-8)]

<a name="scaffold"></a>
## <a name="scaffold-the-model"></a><span data-ttu-id="45bb4-263">Tworzenie szkieletu modelu</span><span class="sxs-lookup"><span data-stu-id="45bb4-263">Scaffold the model</span></span>

* <span data-ttu-id="45bb4-264">Otwórz okno polecenia w katalogu projektu (katalog, który zawiera *Program.cs*, *Startup.cs*, i *.csproj* plików).</span><span class="sxs-lookup"><span data-stu-id="45bb4-264">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="45bb4-265">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="45bb4-265">Run the following commands:</span></span>


 ```console
dotnet restore
dotnet aspnet-codegenerator razorpage -m Student -dc SchoolContext -udl -outDir Pages\Students --referenceScriptLibraries
 ```
 
<span data-ttu-id="45bb4-266">Jeśli generowany jest następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="45bb4-266">If the following error is generated:</span></span>

```text
Unhandled Exception: System.IO.FileNotFoundException: 
Could not load file or assembly 
'Microsoft.VisualStudio.Web.CodeGeneration.Utils, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=adb9793829ddae60'.
The system cannot find the file specified.
```

<span data-ttu-id="45bb4-267">Ponownie uruchom polecenie i zostaw komentarz w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="45bb4-267">Run the command again and leave a comment at the bottom of the page.</span></span>

<span data-ttu-id="45bb4-268">Jeśli zostanie wyświetlony błąd:</span><span class="sxs-lookup"><span data-stu-id="45bb4-268">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="45bb4-269">Otwórz okno polecenia w katalogu projektu (katalog, który zawiera *Program.cs*, *Startup.cs*, i *.csproj* plików).</span><span class="sxs-lookup"><span data-stu-id="45bb4-269">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>


<span data-ttu-id="45bb4-270">Skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="45bb4-270">Build the project.</span></span> <span data-ttu-id="45bb4-271">Kompilacja generuje błędy podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="45bb4-271">The build generates errors like the following:</span></span>

 `1>Pages\Students\Index.cshtml.cs(26,38,26,45): error CS1061: 'SchoolContext' does not contain a definition for 'Student'`

 <span data-ttu-id="45bb4-272">Globalnie zmienić `_context.Student` do `_context.Students` (to znaczy dodania "s" do `Student`).</span><span class="sxs-lookup"><span data-stu-id="45bb4-272">Globally change `_context.Student` to `_context.Students` (that is, add an "s" to `Student`).</span></span> <span data-ttu-id="45bb4-273">7 wystąpienia są odnaleźć i zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="45bb4-273">7 occurrences are found and updated.</span></span> <span data-ttu-id="45bb4-274">Mamy nadzieję naprawić [tej usterki](https://github.com/aspnet/Scaffolding/issues/633) w następnej wersji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-274">We hope to fix [this bug](https://github.com/aspnet/Scaffolding/issues/633) in the next release.</span></span>

[!INCLUDE[model4tbl](../../includes/RP/model4tbl.md)]

 <a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="45bb4-275">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="45bb4-275">Test the app</span></span>

<span data-ttu-id="45bb4-276">Uruchom aplikację i wybierz **studentów** łącza.</span><span class="sxs-lookup"><span data-stu-id="45bb4-276">Run the app and select the **Students** link.</span></span> <span data-ttu-id="45bb4-277">W zależności od szerokości przeglądarki **studentów** łącza wyświetlany w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="45bb4-277">Depending on the browser width, the **Students** link appears at the top of the page.</span></span> <span data-ttu-id="45bb4-278">Jeśli **studentów** łącze nie jest widoczne, kliknij ikonę nawigacji w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-278">If the **Students** link is not visible, click the navigation icon in the upper right corner.</span></span>

![Strona główna contoso University wąskie](intro/_static/home-page-narrow.png)

<span data-ttu-id="45bb4-280">Test **Utwórz**, **Edytuj**, i **szczegóły** łącza.</span><span class="sxs-lookup"><span data-stu-id="45bb4-280">Test the **Create**, **Edit**, and **Details** links.</span></span>

## <a name="view-the-db"></a><span data-ttu-id="45bb4-281">Widok bazy danych</span><span class="sxs-lookup"><span data-stu-id="45bb4-281">View the DB</span></span>

<span data-ttu-id="45bb4-282">Po uruchomieniu aplikacji `DbInitializer.Initialize` wywołania `EnsureCreated`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-282">When the app is started, `DbInitializer.Initialize` calls `EnsureCreated`.</span></span> <span data-ttu-id="45bb4-283">`EnsureCreated`wykrywa, czy istnieje bazę danych i tworzy jeden, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="45bb4-283">`EnsureCreated` detects if the DB exists, and creates one if necessary.</span></span> <span data-ttu-id="45bb4-284">Jeśli w bazie danych, nie nie studentów `Initialize` studentów dodaje metody.</span><span class="sxs-lookup"><span data-stu-id="45bb4-284">If there are no Students in the DB, the `Initialize` method adds students.</span></span>

<span data-ttu-id="45bb4-285">Otwórz **Eksplorator obiektów SQL Server** (SSOX) z **widoku** menu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45bb4-285">Open **SQL Server Object Explorer** (SSOX) from the **View** menu in Visual Studio.</span></span>
<span data-ttu-id="45bb4-286">W SSOX, kliknij przycisk **(localdb) \MSSQLLocalDB > baz danych > ContosoUniversity1**.</span><span class="sxs-lookup"><span data-stu-id="45bb4-286">In SSOX, click **(localdb)\MSSQLLocalDB > Databases > ContosoUniversity1**.</span></span>

<span data-ttu-id="45bb4-287">Rozwiń węzeł **tabel** węzła.</span><span class="sxs-lookup"><span data-stu-id="45bb4-287">Expand the **Tables** node.</span></span>

<span data-ttu-id="45bb4-288">Kliknij prawym przyciskiem myszy **uczniowie** tabeli, a następnie kliknij przycisk **danych widoku** kolumn utworzona i wiersze wstawione do tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-288">Right-click the **Student** table and click **View Data** to see the columns created and the rows inserted into the table.</span></span>

<span data-ttu-id="45bb4-289">*.Mdf* i *ldf* pliki bazy danych znajdują się w *C:\Users\\ <yourusername>*  folderu.</span><span class="sxs-lookup"><span data-stu-id="45bb4-289">The *.mdf* and *.ldf* DB files are in the *C:\Users\\<yourusername>* folder.</span></span>

<span data-ttu-id="45bb4-290">`EnsureCreated`jest wywoływana po uruchomieniu aplikacji, dzięki czemu następującego przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="45bb4-290">`EnsureCreated` is called on app start, which allows the following work flow:</span></span>

* <span data-ttu-id="45bb4-291">Usuń bazę danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-291">Delete the DB.</span></span>
* <span data-ttu-id="45bb4-292">Zmień schemat bazy danych (na przykład dodać `EmailAddress` pól).</span><span class="sxs-lookup"><span data-stu-id="45bb4-292">Change the DB schema (for example, add an `EmailAddress` field).</span></span>
* <span data-ttu-id="45bb4-293">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="45bb4-293">Run the app.</span></span>

<span data-ttu-id="45bb4-294">`EnsureCreated`Tworzy baza danych o`EmailAddress` kolumny.</span><span class="sxs-lookup"><span data-stu-id="45bb4-294">`EnsureCreated` creates a DB with the`EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="45bb4-295">Konwencje</span><span class="sxs-lookup"><span data-stu-id="45bb4-295">Conventions</span></span>

<span data-ttu-id="45bb4-296">Ilość kodu napisanego w kolejności EF podstawowych utworzyć pełną bazy danych jest minimalny, z powodu użycia konwencje lub założenia, które wprowadza EF Core.</span><span class="sxs-lookup"><span data-stu-id="45bb4-296">The amount of code written in order for EF Core to create a complete DB is minimal because of the use of conventions, or assumptions that EF Core makes.</span></span>

* <span data-ttu-id="45bb4-297">Nazwy `DbSet` właściwości są używane jako nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-297">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="45bb4-298">Dla jednostek nie odwołuje się `DbSet` właściwość klasy jednostka nazw są używane jako nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="45bb4-298">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="45bb4-299">Nazwy właściwości jednostki są używane dla nazw kolumn.</span><span class="sxs-lookup"><span data-stu-id="45bb4-299">Entity property names are used for column names.</span></span>

* <span data-ttu-id="45bb4-300">Właściwości jednostki, które są nazywane Identyfikatora lub classnameID są rozpoznawane jako właściwości klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="45bb4-300">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="45bb4-301">Właściwość jest interpretowana jako właściwości klucza obcego, jeśli jest o nazwie  *<navigation property name> <primary key property name>*  (na przykład `StudentID` dla `Student` właściwość nawigacji, ponieważ `Student` jest klucza podstawowego jednostki `ID`).</span><span class="sxs-lookup"><span data-stu-id="45bb4-301">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="45bb4-302">Właściwości klucza obcego może mieć nazwę  *<primary key property name>*  (na przykład `EnrollmentID` ponieważ `Enrollment` klucza podstawowego jednostki jest `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="45bb4-302">Foreign key properties can be named *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="45bb4-303">Konwencjonalne zachowanie można przesłonić.</span><span class="sxs-lookup"><span data-stu-id="45bb4-303">Conventional behavior can be overridden.</span></span> <span data-ttu-id="45bb4-304">Na przykład nazwy tabeli można jawnie określić, jak pokazano wcześniej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-304">For example, the table names can be explicitly specified, as shown earlier in this tutorial.</span></span> <span data-ttu-id="45bb4-305">Nazwy kolumn można ustawić jawnie.</span><span class="sxs-lookup"><span data-stu-id="45bb4-305">The column names can be explicitly set.</span></span> <span data-ttu-id="45bb4-306">Klucze podstawowe i klucze obce można ustawić jawnie.</span><span class="sxs-lookup"><span data-stu-id="45bb4-306">Primary keys and foreign keys can be explicitly set.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="45bb4-307">Kod asynchroniczny</span><span class="sxs-lookup"><span data-stu-id="45bb4-307">Asynchronous code</span></span>

<span data-ttu-id="45bb4-308">Programowanie asynchroniczne jest to domyślny tryb dla platformy ASP.NET Core i EF Core.</span><span class="sxs-lookup"><span data-stu-id="45bb4-308">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="45bb4-309">Serwer sieci web ma ograniczoną liczbę dostępnych wątków, a w sytuacjach wysokie obciążenie wszystkich dostępnych wątków może być używana.</span><span class="sxs-lookup"><span data-stu-id="45bb4-309">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="45bb4-310">W takim przypadku serwer nie może przetworzyć nowe żądania aż wątki są zwalniane.</span><span class="sxs-lookup"><span data-stu-id="45bb4-310">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="45bb4-311">Z kodem synchroniczne wiele wątków może powiązany, gdy nie są faktycznie wykonują pracę, ponieważ ich oczekiwania operacji We/Wy zakończyć.</span><span class="sxs-lookup"><span data-stu-id="45bb4-311">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="45bb4-312">Asynchroniczne kodu podczas procesu jest oczekiwania operacji We/Wy zakończyć, jego wątku zostanie zwolniona dla serwera na potrzeby przetwarzania innych żądań.</span><span class="sxs-lookup"><span data-stu-id="45bb4-312">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="45bb4-313">W związku z tym kod asynchroniczny umożliwia bardziej efektywne wykorzystanie zasobów serwera, a serwer jest skonfigurowany do obsługi ruchu więcej bez opóźnień.</span><span class="sxs-lookup"><span data-stu-id="45bb4-313">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="45bb4-314">Asynchroniczne kodu wprowadzenie niewielkiej liczby dodatkowych czynności w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="45bb4-314">Asynchronous code does introduce a small amount of overhead at run time.</span></span> <span data-ttu-id="45bb4-315">W sytuacjach niski ruchu trafień wydajności jest niewielka, podczas w sytuacjach dużego natężenia ruchu sieciowego, potencjalne zwiększenie wydajności jest znacząca.</span><span class="sxs-lookup"><span data-stu-id="45bb4-315">For low traffic situations, the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="45bb4-316">W poniższym kodzie `async` — słowo kluczowe, `Task<T>` zwrócić wartość, `await` — słowo kluczowe, i `ToListAsync` metoda powoduje, że kod asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="45bb4-316">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="45bb4-317">`async` — Słowo kluczowe informuje kompilator, aby:</span><span class="sxs-lookup"><span data-stu-id="45bb4-317">The `async` keyword tells the compiler to:</span></span>

  * <span data-ttu-id="45bb4-318">Generuj wywołania zwrotne dla części treści metody.</span><span class="sxs-lookup"><span data-stu-id="45bb4-318">Generate callbacks for parts of the method body.</span></span>
  * <span data-ttu-id="45bb4-319">Automatyczne tworzenie [zadań](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) obiekt, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="45bb4-319">Automatically create the [Task](https://docs.microsoft.com/dotnet/api/system.threading.tasks.task?view=netframework-4.7) object that is returned.</span></span> <span data-ttu-id="45bb4-320">Aby uzyskać więcej informacji, zobacz [typu zwracanego zadań](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span><span class="sxs-lookup"><span data-stu-id="45bb4-320">For more information, see [Task Return Type](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/async/async-return-types#BKMK_TaskReturnType).</span></span>

* <span data-ttu-id="45bb4-321">Typ zwracany niejawne `Task` reprezentuje pracy w toku.</span><span class="sxs-lookup"><span data-stu-id="45bb4-321">The implicit return type `Task` represents ongoing work.</span></span>

* <span data-ttu-id="45bb4-322">`await` — Słowo kluczowe powoduje, że kompilator podzielić na dwie części metodę.</span><span class="sxs-lookup"><span data-stu-id="45bb4-322">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="45bb4-323">Pierwsza część kończy operację, który jest uruchamiany asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="45bb4-323">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="45bb4-324">Druga część są umieszczane w metodę wywołania zwrotnego, która jest wywoływana po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="45bb4-324">The second part is put into a callback method that is called when the operation completes.</span></span>

* <span data-ttu-id="45bb4-325">`ToListAsync`jest to wersja asynchroniczna elementu `ToList` — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="45bb4-325">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="45bb4-326">Należy pamiętać o podczas pisania kodu asynchroniczne EF Core używa w kilku kwestiach:</span><span class="sxs-lookup"><span data-stu-id="45bb4-326">Some things to be aware of when writing asynchronous code that uses EF Core:</span></span>

* <span data-ttu-id="45bb4-327">Tylko te instrukcje, które powodują zapytań i poleceń do wysłania do bazy danych są wykonywane asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="45bb4-327">Only statements that cause queries or commands to be sent to the DB are executed asynchronously.</span></span> <span data-ttu-id="45bb4-328">Zawierającej, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, i `SaveChangesAsync`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-328">That includes, `ToListAsync`, `SingleOrDefaultAsync`, `FirstOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="45bb4-329">Nie zawiera instrukcji, które można zmienić `IQueryable`, takich jak `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span><span class="sxs-lookup"><span data-stu-id="45bb4-329">It does not include statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="45bb4-330">Kontekst EF Core nie jest bezwątkowy bezpieczne: nie należy próbować wykonać kilka operacji wykonywane równolegle.</span><span class="sxs-lookup"><span data-stu-id="45bb4-330">An EF Core context is not threaded safe: don't try to do multiple operations in parallel.</span></span> 

* <span data-ttu-id="45bb4-331">Można wykorzystać zalety wydajności async kodu, sprawdź, czy pakiety bibliotekę (takie jak w przypadku stronicowania) używają async Jeśli wywołują metody EF podstawowych, które wysyłanie zapytań do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="45bb4-331">To take advantage of the performance benefits of async code, verify that library packages (such as for paging) use async if they call EF Core methods that send queries to the DB.</span></span>

<span data-ttu-id="45bb4-332">Aby uzyskać więcej informacji na temat programowania asynchronicznego w programie .NET, zobacz [omówienie Async](https://docs.microsoft.com/dotnet/articles/standard/async).</span><span class="sxs-lookup"><span data-stu-id="45bb4-332">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

<span data-ttu-id="45bb4-333">W następnym samouczku basic CRUD (tworzenia, odczytu, aktualizowanie i usuwanie) operacje są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="45bb4-333">In the next tutorial, basic CRUD (create, read, update, delete) operations are examined.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="45bb4-334">Next</span><span class="sxs-lookup"><span data-stu-id="45bb4-334">Next</span></span>](xref:data/ef-rp/crud)