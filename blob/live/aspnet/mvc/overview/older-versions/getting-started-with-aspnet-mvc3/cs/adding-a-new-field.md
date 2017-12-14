---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: Dodanie nowego pola filmu modelu i tabeli (C#) | Dokumentacja firmy Microsoft
author: Rick-Anderson
description: "Ten samouczek pokazuje podstawowe informacje dotyczące tworzenia aplikacji sieci Web programu ASP.NET MVC przy użyciu Microsoft Visual Web Developer 2010 Express Service Pack 1, która jest..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: c10f3be30a92a605c34fa1c56fa3691389374beb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="94a17-103">Dodanie nowego pola filmu modelu i tabeli (C#)</span><span class="sxs-lookup"><span data-stu-id="94a17-103">Adding a New Field to the Movie Model and Table (C#)</span></span>
====================
<span data-ttu-id="94a17-104">Przez [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="94a17-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="94a17-105">Dostępna jest zaktualizowana wersja tego samouczka [tutaj](../../../getting-started/introduction/getting-started.md) używającej platformy ASP.NET MVC 5 i Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="94a17-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="94a17-106">Jest bardziej bezpieczne, łatwiej wykonać i pokazuje więcej funkcji.</span><span class="sxs-lookup"><span data-stu-id="94a17-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="94a17-107">Ten samouczek pokazuje podstawowe informacje dotyczące tworzenia aplikacji sieci Web programu ASP.NET MVC przy użyciu Microsoft Visual Web Developer 2010 Express Service Pack 1, która jest bezpłatna wersja programu Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94a17-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="94a17-108">Przed rozpoczęciem upewnij się, że po zainstalowaniu wymagania wstępne wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="94a17-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="94a17-109">Można zainstalować wszystkie z nich, klikając poniższe łącze: [Instalatora platformy sieci Web](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="94a17-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="94a17-110">Alternatywnie można zainstalować oddzielnie wymagania wstępne, korzystając z następujących linków:</span><span class="sxs-lookup"><span data-stu-id="94a17-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="94a17-111">Visual Studio Web Developer Express z dodatkiem SP1 wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94a17-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="94a17-112">Aktualizacji narzędzi programu ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="94a17-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="94a17-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(środowisko uruchomieniowe + narzędzia pomocy technicznej)</span><span class="sxs-lookup"><span data-stu-id="94a17-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="94a17-114">Jeśli używasz programu Visual Studio 2010, zamiast Visual Web Developer 2010, zainstaluj wymagania wstępne, klikając poniższe łącze: [wymagania wstępne programu Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="94a17-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="94a17-115">Projekt Visual Web Developer z kodu źródłowego C# jest dostępna powiązany z tym tematem.</span><span class="sxs-lookup"><span data-stu-id="94a17-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="94a17-116">[Pobierz wersję języka C#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="94a17-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="94a17-117">Jeśli wolisz Visual Basic, przełącz się do [wersji Visual Basic](../vb/intro-to-aspnet-mvc-3.md) tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="94a17-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="94a17-118">W tej sekcji możesz wprowadzić kilka zmian dla klasy modelu i Dowiedz się, jak można zaktualizować schemat bazy danych, aby dopasować zmiany modelu.</span><span class="sxs-lookup"><span data-stu-id="94a17-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="94a17-119">Dodawanie właściwości klasyfikacji do modelu film</span><span class="sxs-lookup"><span data-stu-id="94a17-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="94a17-120">Rozpocznij od dodania nowej `Rating` właściwości do istniejącej `Movie` klasy.</span><span class="sxs-lookup"><span data-stu-id="94a17-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="94a17-121">Otwórz *Movie.cs* plik i dodać `Rating` właściwości podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="94a17-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="94a17-122">Pełną `Movie` klasy teraz wygląda podobnie do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="94a17-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="94a17-123">Ponowne skompilowanie aplikacji przy użyciu **debugowania** &gt; **kompilacji filmu** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="94a17-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="94a17-124">Teraz, gdy użytkownik zaktualizował `Model` klasy, należy również zaktualizować *\Views\Movies\Index.cshtml* i *\Views\Movies\Create.cshtml* wyświetlania szablonów w celu zapewnienia obsługi nowych `Rating`właściwości.</span><span class="sxs-lookup"><span data-stu-id="94a17-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="94a17-125">Otwórz *\Views\Movies\Index.cshtml* plik i dodać `<th>Rating</th>` tuż po nagłówek kolumny **cen** kolumny.</span><span class="sxs-lookup"><span data-stu-id="94a17-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="94a17-126">Następnie dodaj `<td>` kolumny zbliża się koniec szablon do renderowania `@item.Rating` wartość.</span><span class="sxs-lookup"><span data-stu-id="94a17-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="94a17-127">Poniżej znajduje się jakie zaktualizowane *Index.cshtml* Wyświetl szablon wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="94a17-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="94a17-128">Następnie otwórz folder *\Views\Movies\Create.cshtml* i Dodaj następujący kod pod koniec formularza.</span><span class="sxs-lookup"><span data-stu-id="94a17-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="94a17-129">Renderuje pola tekstowego, tak aby po utworzeniu nowego movie, można określić klasyfikację.</span><span class="sxs-lookup"><span data-stu-id="94a17-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="94a17-130">Zarządzanie modelu i różnice schematu bazy danych</span><span class="sxs-lookup"><span data-stu-id="94a17-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="94a17-131">Użytkownik zaktualizował teraz kodu aplikacji do obsługi nowej `Rating` właściwości.</span><span class="sxs-lookup"><span data-stu-id="94a17-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="94a17-132">Teraz uruchom aplikację i przejdź do */Movies* adresu URL.</span><span class="sxs-lookup"><span data-stu-id="94a17-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="94a17-133">Po wykonaniu tej czynności, zostanie wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="94a17-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="94a17-134">Ten błąd jest wyświetlane, ponieważ zaktualizowanego `Movie` klasy modelu w aplikacji teraz różni się od schematu `Movie` tabeli istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="94a17-135">(Brak nie `Rating` kolumny w tabeli bazy danych.)</span><span class="sxs-lookup"><span data-stu-id="94a17-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="94a17-136">Domyślnie korzystając z programu Entity Framework Code First automatycznie utworzyć bazę danych, tak jak wcześniej w tym samouczku Code First dodaje tabeli do bazy danych, aby sprawdzić, czy schemat bazy danych jest zsynchronizowana z klasy modelu, który został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="94a17-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="94a17-137">Jeśli nie są zsynchronizowane, Entity Framework zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="94a17-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="94a17-138">Ułatwia to śledzenie problemów w czasie opracowywania, znajdującego się w przeciwnym razie tylko (przez zasłoniętej błędy) w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="94a17-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="94a17-139">Funkcja sprawdzania synchronizacji jest, co powoduje, że ma być wyświetlany komunikat o błędzie, który został wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="94a17-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="94a17-140">Istnieją dwa podejścia do rozwiązania problemu:</span><span class="sxs-lookup"><span data-stu-id="94a17-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="94a17-141">Ma automatycznie porzucenia i ponownego utworzenia bazy danych na podstawie nowego schematu klasy modelu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="94a17-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="94a17-142">Ta metoda jest bardzo wygodny w trakcie rozwoju active w testowej bazy danych, ponieważ pozwala szybko razem sformułować schematu modelu i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="94a17-143">Wadą interfejsu, jest jednak, że utracić istniejące dane w bazie danych — dlatego możesz *nie* chcesz użyć tej metody w produkcyjnej bazie danych!</span><span class="sxs-lookup"><span data-stu-id="94a17-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="94a17-144">Jawnie modyfikować schemat z istniejącej bazy danych, tak aby był zgodny z klasy modelu.</span><span class="sxs-lookup"><span data-stu-id="94a17-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="94a17-145">Zaletą tej metody jest, aby zachować dane.</span><span class="sxs-lookup"><span data-stu-id="94a17-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="94a17-146">Można to zrobić to ręcznie lub przez tworzenie bazy danych należy zmienić skryptu.</span><span class="sxs-lookup"><span data-stu-id="94a17-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="94a17-147">W tym samouczku, użyjemy pierwszego podejścia — będziesz mieć Entity Framework Code First automatycznie ponownie utworzyć bazę danych, w dowolnym momencie zmiany modelu.</span><span class="sxs-lookup"><span data-stu-id="94a17-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="94a17-148">Automatyczne ponowne tworzenie bazy danych na zmiany modelu</span><span class="sxs-lookup"><span data-stu-id="94a17-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="94a17-149">Teraz należy zaktualizować aplikacji, tak aby Code First automatycznie porzuca i ponownie utworzy bazę danych, w dowolnym momencie zmienić modelu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94a17-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94a17-150">**Ostrzeżenie** należy włączyć takie podejście automatycznie porzucenie i ponowne utworzenie bazy danych tylko wtedy, gdy używasz deweloperskich lub testowania bazy danych i *nigdy nie* na produkcyjną bazę danych, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="94a17-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="94a17-151">Używanie go na serwerze produkcyjnym może prowadzić do utraty danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-151">Using it on a production server can lead to data loss.</span></span>


<span data-ttu-id="94a17-152">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *modele* folderu, wybierz opcję **Dodaj**, a następnie wybierz **klasy**.</span><span class="sxs-lookup"><span data-stu-id="94a17-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="94a17-153">Nazwa klasy "MovieInitializer".</span><span class="sxs-lookup"><span data-stu-id="94a17-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="94a17-154">Aktualizacja `MovieInitializer` klasa może zawierać następujący kod:</span><span class="sxs-lookup"><span data-stu-id="94a17-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="94a17-155">`MovieInitializer` Klasa określa, czy porzucić i automatycznie ponownie utworzyć klasy modelu kiedykolwiek zmiany bazy danych używanej przez model.</span><span class="sxs-lookup"><span data-stu-id="94a17-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="94a17-156">Kod zawiera `Seed` metodę, aby określić, niektóre dane domyślne automatyczne dodawanie do bazy danych dowolnej czasu utworzony (lub odtwarzaniu).</span><span class="sxs-lookup"><span data-stu-id="94a17-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="94a17-157">Zapewnia to wygodny sposób na wypełnianie bazy danych z przykładowymi danymi, bez konieczności ręcznie wypełnić je po każdym wprowadzeniu zmiany modelu.</span><span class="sxs-lookup"><span data-stu-id="94a17-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="94a17-158">Teraz, gdy zdefiniowano `MovieInitializer` klasy, należy połączenie go z się tak, że w każdym uruchomieniu aplikacji sprawdza czy klasy modelu różnią się od schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="94a17-159">W takim przypadku można uruchomić inicjatora ponownie utworzyć bazę danych do zgodny z modelem, a następnie wypełnij bazy danych z przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="94a17-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="94a17-160">Otwórz *Global.asax* plik, który znajduje się w katalogu głównym `MvcMovies` projektu:</span><span class="sxs-lookup"><span data-stu-id="94a17-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="94a17-161">*Global.asax* plik zawiera klasę, która definiuje całej aplikacji dla projektu i zawiera `Application_Start` obsługi zdarzeń, który jest uruchamiany po pierwszym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94a17-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="94a17-162">Dodajmy dwie instrukcje using do początku pliku.</span><span class="sxs-lookup"><span data-stu-id="94a17-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="94a17-163">Pierwszy odwołuje się do przestrzeni nazw programu Entity Framework, a drugi odwołuje się do przestrzeni nazw gdzie naszych `MovieInitializer` życie klasy:</span><span class="sxs-lookup"><span data-stu-id="94a17-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="94a17-164">Następnie znajdź `Application_Start` — metoda i dodaj wywołanie do `Database.SetInitializer` na początku metody, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="94a17-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="94a17-165">`Database.SetInitializer` Instrukcji dodaną wskazuje, że bazy danych używane przez `MovieDBContext` wystąpienia powinien zostać automatycznie usunięta i utworzona ponownie, jeśli schemat i bazy danych nie są zgodne.</span><span class="sxs-lookup"><span data-stu-id="94a17-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="94a17-166">I jak widać, zostanie również wypełnić bazę danych przykładowych danych, które jest określone w `MovieInitializer` klasy.</span><span class="sxs-lookup"><span data-stu-id="94a17-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="94a17-167">Zamknij *Global.asax* pliku.</span><span class="sxs-lookup"><span data-stu-id="94a17-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="94a17-168">Ponownie uruchom aplikację i przejdź do */Movies* adresu URL.</span><span class="sxs-lookup"><span data-stu-id="94a17-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="94a17-169">Podczas uruchamiania aplikacji, wykryje, że struktura modelu nie jest już zgodny schemat bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="94a17-170">Automatycznie ponownie utworzy bazę danych do dopasowania nową strukturę modelu i wypełnienie bazy danych o przykładowe filmy:</span><span class="sxs-lookup"><span data-stu-id="94a17-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="94a17-172">Kliknij przycisk **Utwórz nowy** łącze, aby dodać nowy filmu.</span><span class="sxs-lookup"><span data-stu-id="94a17-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="94a17-173">Należy pamiętać, że można dodać ocenę.</span><span class="sxs-lookup"><span data-stu-id="94a17-173">Note that you can add a rating.</span></span>

<span data-ttu-id="94a17-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="94a17-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="94a17-175">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="94a17-175">Click **Create**.</span></span> <span data-ttu-id="94a17-176">Nowe film, w tym ocenę, teraz wyświetlone w filmy wyświetlania:</span><span class="sxs-lookup"><span data-stu-id="94a17-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="94a17-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="94a17-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="94a17-178">W tej sekcji przedstawiono sposób modyfikowania modelu obiektów i zachować synchronizację ze zmianami bazy danych.</span><span class="sxs-lookup"><span data-stu-id="94a17-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="94a17-179">Przedstawiono również sposób wypełnienia nowo utworzonej bazy danych z przykładowymi danymi, więc można wypróbować scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="94a17-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="94a17-180">Następnie Oto jak można dodać bardziej rozbudowane logikę weryfikacji dla klasy modelu i włączyć niektóre reguły biznesowe są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="94a17-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="94a17-181">[Poprzednie](examining-the-edit-methods-and-edit-view.md)
[dalej](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="94a17-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>