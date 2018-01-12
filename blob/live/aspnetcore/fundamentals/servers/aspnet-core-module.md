---
title: "Moduł platformy ASP.NET Core"
author: tdykstra
description: "Wprowadza platformy ASP.NET Core modułu (ANCM), moduł usług IIS, który umożliwia Kestrel serwera sieci web usług IIS lub usług IIS Express jest używany jako serwer zwrotnego serwera proxy."
keywords: "Moduł Core platformy ASP.NET Core usług IIS, usługi IIS Express,ASP.NET, UseIISIntegration"
ms.author: tdykstra
manager: wpickett
ms.date: 08/03/2017
ms.topic: article
ms.assetid: 4661af33-34c5-4d71-93a0-8c7632f43580
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/servers/aspnet-core-module
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5eef9405c0c3d219755d7cffa5d45c3df45ddb5c
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2018
---
# <a name="introduction-to-aspnet-core-module"></a><span data-ttu-id="083ef-104">Wprowadzenie do platformy ASP.NET Core modułu</span><span class="sxs-lookup"><span data-stu-id="083ef-104">Introduction to ASP.NET Core Module</span></span>

<span data-ttu-id="083ef-105">Przez [Dykstra Tomasz](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), i [Roaming Krzysztof](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="083ef-105">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span> 

<span data-ttu-id="083ef-106">Program ASP.NET Core modułu (ANCM) umożliwia uruchamianie platformy ASP.NET Core aplikacje za usług IIS, przy użyciu usług IIS dla co to jest dobrze sobie radzi (zabezpieczeń, możliwości zarządzania i wiele więcej) i [Kestrel](kestrel.md) dla co to jest dobrze sobie radzi (co naprawdę fast) i pobierania korzyści z obu tych technologii jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="083ef-106">ASP.NET Core Module (ANCM) lets you run ASP.NET Core applications behind IIS, using IIS for what it's good at (security, manageability, and lots more) and using [Kestrel](kestrel.md) for what it's good at (being really fast), and getting the benefits from both technologies at once.</span></span> <span data-ttu-id="083ef-107">**ANCM działa tylko w przypadku Kestrel; nie jest zgodna z WebListener (w ASP.NET Core 1.x) lub sterownik HTTP.sys (w 2.x).**</span><span class="sxs-lookup"><span data-stu-id="083ef-107">**ANCM works only with Kestrel; it isn't compatible with WebListener (in ASP.NET Core 1.x) or HTTP.sys (in 2.x).**</span></span> 

<span data-ttu-id="083ef-108">Obsługiwane wersje systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="083ef-108">Supported Windows versions:</span></span>

* <span data-ttu-id="083ef-109">Windows 7 i Windows Server 2008 R2 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="083ef-109">Windows 7 and Windows Server 2008 R2 and later</span></span>

<span data-ttu-id="083ef-110">[Wyświetlić lub pobrać przykładowy kod](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample) ([sposobu pobierania](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="083ef-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-aspnet-core-module-does"></a><span data-ttu-id="083ef-111">Jak działa moduł platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="083ef-111">What ASP.NET Core Module does</span></span>

<span data-ttu-id="083ef-112">ANCM jest macierzysty moduł usług IIS, który przechwytuje do potoku usług IIS i przekierowuje ruch z zapleczem aplikacji platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="083ef-112">ANCM is a native IIS module that hooks into the IIS pipeline and redirects traffic to the backend ASP.NET Core application.</span></span> <span data-ttu-id="083ef-113">Większość innych modułów, takich jak uwierzytelnianie systemu windows, nadal otrzymywać możliwość uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="083ef-113">Most other modules, such as windows authentication, still get a chance to run.</span></span> <span data-ttu-id="083ef-114">Podczas obsługi został wybrany do żądania i mapowanie obsługi jest zdefiniowany w aplikacji ANCM tylko przejmuje kontrolę *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="083ef-114">ANCM only takes control when a handler is selected for the request, and handler mapping is defined in the application *web.config* file.</span></span>

<span data-ttu-id="083ef-115">Ponieważ aplikacje platformy ASP.NET Core w procesie oddzielić od proces roboczy usług IIS, ANCM także przetwarzać zarządzania.</span><span class="sxs-lookup"><span data-stu-id="083ef-115">Because ASP.NET Core applications run in a process separate from the IIS worker process, ANCM also does process management.</span></span> <span data-ttu-id="083ef-116">ANCM uruchamia proces dla aplikacji platformy ASP.NET Core podczas pierwszego żądania jest dostępna i ponownie go uruchamia uległa awarii.</span><span class="sxs-lookup"><span data-stu-id="083ef-116">ANCM starts the process for the ASP.NET Core application when the first request comes in and restarts it when it crashes.</span></span> <span data-ttu-id="083ef-117">Jest to zasadniczo takie samo zachowanie jako klasycznych aplikacji programu ASP.NET uruchomienia procesu w usługach IIS i są zarządzane przez usługę WAS (Windows Activation Service).</span><span class="sxs-lookup"><span data-stu-id="083ef-117">This is essentially the same behavior as classic ASP.NET applications that run in-process in IIS and are managed by WAS (Windows Activation Service).</span></span>

<span data-ttu-id="083ef-118">Oto diagramie przedstawiono relację między aplikacjami usług IIS, ANCM i ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="083ef-118">Here's a diagram that illustrates the relationship between IIS, ANCM, and ASP.NET Core applications.</span></span>

![Moduł platformy ASP.NET Core](aspnet-core-module/_static/ancm.png)

<span data-ttu-id="083ef-120">Żądania pochodzą sieci Web i trafień sterownik Http.Sys trybu jądra, który kieruje je do usług IIS na głównej portu (80) lub portu protokołu SSL (port 443).</span><span class="sxs-lookup"><span data-stu-id="083ef-120">Requests come in from the Web and hit the kernel mode Http.Sys driver which routes them into IIS on the primary port (80) or SSL port (443).</span></span> <span data-ttu-id="083ef-121">ANCM przekazuje żądanie do aplikacji platformy ASP.NET Core na port protokołu HTTP skonfigurowany dla aplikacji, która nie jest port 80/443.</span><span class="sxs-lookup"><span data-stu-id="083ef-121">ANCM forwards the requests to the ASP.NET Core application on the HTTP port configured for the application, which is not port 80/443.</span></span>

<span data-ttu-id="083ef-122">Kestrel nasłuchuje ruchu przychodzącego z ANCM.</span><span class="sxs-lookup"><span data-stu-id="083ef-122">Kestrel listens for traffic coming from ANCM.</span></span>  <span data-ttu-id="083ef-123">ANCM Określa port, za pomocą zmiennej środowiskowej podczas uruchamiania i [UseIISIntegration](#call-useiisintegration) metody konfiguruje serwer do nasłuchiwania `http://localhost:{port}`.</span><span class="sxs-lookup"><span data-stu-id="083ef-123">ANCM specifies the port via environment variable at startup, and the [UseIISIntegration](#call-useiisintegration) method configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="083ef-124">Istnieją dodatkowe kontrole do odrzucania żądań nie z ANCM.</span><span class="sxs-lookup"><span data-stu-id="083ef-124">There are additional checks to reject requests not from ANCM.</span></span> <span data-ttu-id="083ef-125">(ANCM nie obsługuje przekazywanie protokołu HTTPS, więc żądania są przekazywane za pośrednictwem protokołu HTTP, nawet jeśli odebranych przez usługi IIS przy użyciu protokołu HTTPS.)</span><span class="sxs-lookup"><span data-stu-id="083ef-125">(ANCM does not support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.)</span></span>

<span data-ttu-id="083ef-126">Kestrel przejmuje żądań z ANCM i umieszcza je w potoku oprogramowania pośredniczącego platformy ASP.NET Core, który następnie je obsługuje i przekazuje je na jako `HttpContext` wystąpienia logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="083ef-126">Kestrel picks up requests from ANCM and pushes them into the ASP.NET Core middleware pipeline, which then handles them and passes them on as `HttpContext` instances to application logic.</span></span> <span data-ttu-id="083ef-127">Odpowiedzi aplikacji są następnie przekazywane z powrotem do usług IIS, które umieszcza je z powrotem do klienta HTTP, który zainicjował żądania.</span><span class="sxs-lookup"><span data-stu-id="083ef-127">The application's responses are then passed back to IIS, which pushes them back out to the HTTP client that initiated the requests.</span></span>

<span data-ttu-id="083ef-128">ANCM ma kilka innych funkcji, jak również:</span><span class="sxs-lookup"><span data-stu-id="083ef-128">ANCM has a few other functions as well:</span></span>

* <span data-ttu-id="083ef-129">Ustawia zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="083ef-129">Sets environment variables.</span></span>
* <span data-ttu-id="083ef-130">Dzienniki `stdout` dane wyjściowe do pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="083ef-130">Logs `stdout` output to file storage.</span></span>
* <span data-ttu-id="083ef-131">Przekazuje tokeny uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="083ef-131">Forwards Windows authentication tokens.</span></span>

## <a name="how-to-use-ancm-in-aspnet-core-apps"></a><span data-ttu-id="083ef-132">Jak używać ANCM w aplikacji platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="083ef-132">How to use ANCM in ASP.NET Core apps</span></span>

<span data-ttu-id="083ef-133">Ta sekcja zawiera omówienie procesu konfigurowania aplikacji platformy ASP.NET Core i serwera usług IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-133">This section provides an overview of the process for setting up an IIS server and ASP.NET Core application.</span></span> <span data-ttu-id="083ef-134">Aby uzyskać szczegółowe instrukcje, zobacz [hosta w systemie Windows z programem IIS](xref:host-and-deploy/iis/index).</span><span class="sxs-lookup"><span data-stu-id="083ef-134">For detailed instructions, see [Host on Windows with IIS](xref:host-and-deploy/iis/index).</span></span>

### <a name="install-ancm"></a><span data-ttu-id="083ef-135">Zainstaluj ANCM</span><span class="sxs-lookup"><span data-stu-id="083ef-135">Install ANCM</span></span>


<span data-ttu-id="083ef-136">Moduł platformy ASP.NET Core musi być zainstalowany w usługach IIS na serwerach i w usługach IIS Express na maszynach w rozwoju.</span><span class="sxs-lookup"><span data-stu-id="083ef-136">The ASP.NET Core Module has to be installed in IIS on your servers and in IIS Express on your development machines.</span></span> <span data-ttu-id="083ef-137">W przypadku serwerów ANCM znajduje się w [pakietu .NET Core systemu Windows serwer obsługujący](https://aka.ms/dotnetcore-2-windowshosting).</span><span class="sxs-lookup"><span data-stu-id="083ef-137">For servers, ANCM is included in the [.NET Core Windows Server Hosting bundle](https://aka.ms/dotnetcore-2-windowshosting).</span></span> <span data-ttu-id="083ef-138">Programowanie maszyn Visual Studio automatycznie instaluje ANCM w usługach IIS Express i w usługach IIS, jeśli jest już zainstalowany na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="083ef-138">For development machines, Visual Studio automatically installs ANCM in IIS Express, and in IIS if it is already installed on the machine.</span></span>

### <a name="install-the-iisintegration-nuget-package"></a><span data-ttu-id="083ef-139">Zainstaluj pakiet IISIntegration NuGet</span><span class="sxs-lookup"><span data-stu-id="083ef-139">Install the IISIntegration NuGet package</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="083ef-140">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="083ef-140">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="083ef-141">[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) pakietu znajduje się w metapackages platformy ASP.NET Core ([Microsoft.AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore/) i [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) ).</span><span class="sxs-lookup"><span data-stu-id="083ef-141">The [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package is included in the ASP.NET Core metapackages ([Microsoft.AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore/) and [Microsoft.AspNetCore.All](xref:fundamentals/metapackage)).</span></span> <span data-ttu-id="083ef-142">Jeśli nie używasz jednego z metapackages, zainstaluj `Microsoft.AspNetCore.Server.IISIntegration` oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="083ef-142">If you don't use one of the metapackages, install `Microsoft.AspNetCore.Server.IISIntegration` separately.</span></span> <span data-ttu-id="083ef-143">`IISIntegration` Pakiet jest pakiet współdziałanie odczytujący zmiennych środowiskowych emitowane przez ANCM do skonfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="083ef-143">The `IISIntegration` package is an interoperability pack that reads environment variables broadcast by ANCM to set up your app.</span></span> <span data-ttu-id="083ef-144">Zmienne środowiskowe, podaj informacje o konfiguracji, takie jak port do nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="083ef-144">The environment variables provide configuration information, such as the port to listen on.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="083ef-145">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="083ef-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="083ef-146">W aplikacji, należy zainstalować [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/).</span><span class="sxs-lookup"><span data-stu-id="083ef-146">In your application, install [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/).</span></span> <span data-ttu-id="083ef-147">`IISIntegration` Pakiet jest pakiet współdziałanie odczytujący zmiennych środowiskowych emitowane przez ANCM do skonfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="083ef-147">The `IISIntegration` package  is an interoperability pack that reads environment variables broadcast by ANCM to set up your app.</span></span> <span data-ttu-id="083ef-148">Zmienne środowiskowe, podaj informacje o konfiguracji, takie jak port do nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="083ef-148">The environment variables provide configuration information, such as the port to listen on.</span></span> 

---

### <a name="call-useiisintegration"></a><span data-ttu-id="083ef-149">Wywołanie UseIISIntegration</span><span class="sxs-lookup"><span data-stu-id="083ef-149">Call UseIISIntegration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="083ef-150">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="083ef-150">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="083ef-151">`UseIISIntegration` — Metoda rozszerzenia na [ `WebHostBuilder` ](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) jest wywoływana automatycznie po uruchomieniu z programu IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-151">The `UseIISIntegration` extension method on [`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder) is called automatically when you run with IIS.</span></span>

<span data-ttu-id="083ef-152">Jeśli nie są przy użyciu jednej z platformy ASP.NET Core metapackages i nie zostały zainstalowane `Microsoft.AspNetCore.Server.IISIntegration` pakietów, Pobierz błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="083ef-152">If you aren't using one of the ASP.NET Core metapackages and haven't installed the  `Microsoft.AspNetCore.Server.IISIntegration` package, you get a runtime error.</span></span> <span data-ttu-id="083ef-153">Jeśli należy wywołać `UseIISIntegration` jawnie, Pobierz błąd w czasie kompilacji Jeśli pakiet nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="083ef-153">If you call `UseIISIntegration` explicitly, you get a compile time error if the package isn't installed.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="083ef-154">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="083ef-154">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="083ef-155">W aplikacji `Main` metody, wywołaj `UseIISIntegration` — metoda rozszerzenia na [ `WebHostBuilder` ](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="083ef-155">In your application's `Main` method, call the `UseIISIntegration` extension method on [`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> 

[!code-csharp[](aspnet-core-module/sample/Program.cs?name=snippet_Main&highlight=12)]

---

<span data-ttu-id="083ef-156">`UseIISIntegration` Metoda szuka zmiennych środowiskowych, które ustawia ANCM i nie ops, jeśli nie można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="083ef-156">The `UseIISIntegration` method looks for environment variables that ANCM sets, and it no-ops if they aren't found.</span></span> <span data-ttu-id="083ef-157">To zachowanie ułatwia scenariuszy, takich jak tworzenie i testowanie na macOS lub Linux i wdrażanie na serwer z uruchomionymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-157">This behavior facilitates scenarios like developing and testing on macOS or Linux and deploying to a server that runs IIS.</span></span> <span data-ttu-id="083ef-158">Podczas uruchamiania na macOS lub Linux, Kestrel działa jako serwer sieci web; Jednak gdy aplikacja jest wdrażana w środowisku usług IIS, automatycznie używa ANCM i usług IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-158">While running on macOS or Linux, Kestrel acts as the web server; but when the app is deployed to the IIS environment, it automatically uses ANCM and IIS.</span></span>

### <a name="ancm-port-binding-overrides-other-port-bindings"></a><span data-ttu-id="083ef-159">Powiązanie portu ANCM przesłania pozostałych powiązaniach portu</span><span class="sxs-lookup"><span data-stu-id="083ef-159">ANCM port binding overrides other port bindings</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="083ef-160">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="083ef-160">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="083ef-161">ANCM generuje portów dynamicznych do przypisania do procesu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="083ef-161">ANCM generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="083ef-162">`UseIISIntegration` Metoda przejmuje ten port dynamiczny i konfiguruje Kestrel do nasłuchiwania `http://locahost:{dynamicPort}/`.</span><span class="sxs-lookup"><span data-stu-id="083ef-162">The `UseIISIntegration` method picks up this dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="083ef-163">Przesłania inne konfiguracje adresu URL, takie jak wywołania `UseUrls` lub [API nasłuchiwania na Kestrel](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span><span class="sxs-lookup"><span data-stu-id="083ef-163">This overrides other URL configurations, such as calls to `UseUrls` or [Kestrel's Listen API](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span> <span data-ttu-id="083ef-164">W związku z tym nie należy wywołać `UseUrls` lub jego Kestrel `Listen` interfejsu API, korzystając z ANCM.</span><span class="sxs-lookup"><span data-stu-id="083ef-164">Therefore, you don't need to call `UseUrls` or Kestrel's `Listen` API when you use ANCM.</span></span> <span data-ttu-id="083ef-165">Jeśli zostanie wywołana `UseUrls` lub `Listen`, Kestrel nasłuchuje na porcie określić podczas uruchamiania aplikacji bez usług IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-165">If you do call `UseUrls` or `Listen`, Kestrel listens on the port you specify when you run the app without IIS.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="083ef-166">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="083ef-166">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="083ef-167">ANCM generuje portów dynamicznych do przypisania do procesu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="083ef-167">ANCM generates a dynamic port to assign to the back-end process.</span></span> <span data-ttu-id="083ef-168">`UseIISIntegration` Metoda przejmuje ten port dynamiczny i konfiguruje Kestrel do nasłuchiwania `http://locahost:{dynamicPort}/`.</span><span class="sxs-lookup"><span data-stu-id="083ef-168">The `UseIISIntegration` method picks up this dynamic port and configures Kestrel to listen on `http://locahost:{dynamicPort}/`.</span></span> <span data-ttu-id="083ef-169">Przesłania inne konfiguracje adresu URL, takie jak wywołania `UseUrls`.</span><span class="sxs-lookup"><span data-stu-id="083ef-169">This overrides other URL configurations, such as calls to `UseUrls`.</span></span> <span data-ttu-id="083ef-170">W związku z tym nie należy wywołać `UseUrls` korzystając ANCM.</span><span class="sxs-lookup"><span data-stu-id="083ef-170">Therefore, you don't need to call `UseUrls` when you use ANCM.</span></span> <span data-ttu-id="083ef-171">Jeśli zostanie wywołana `UseUrls`, Kestrel nasłuchuje na porcie określić podczas uruchamiania aplikacji bez usług IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-171">If you do call `UseUrls`, Kestrel listens on the port you specify when you run the app without IIS.</span></span>

<span data-ttu-id="083ef-172">W ASP.NET Core 1.0, jeśli wywołujesz `UseUrls`, wywołać ją **przed** należy wywołać `UseIISIntegration` tak, aby port skonfigurowany ANCM nie zostać zastąpione.</span><span class="sxs-lookup"><span data-stu-id="083ef-172">In ASP.NET Core 1.0, if you call `UseUrls`, call it **before** you call `UseIISIntegration` so that the ANCM-configured port doesn't get overwritten.</span></span> <span data-ttu-id="083ef-173">To zamówienie wywołania nie jest wymagane w ASP.NET Core 1.1, ponieważ ustawienie ANCM zastępuje `UseUrls`.</span><span class="sxs-lookup"><span data-stu-id="083ef-173">This calling order isn't required in ASP.NET Core 1.1, because the ANCM setting overrides `UseUrls`.</span></span>

---

### <a name="configure-ancm-options-in-webconfig"></a><span data-ttu-id="083ef-174">Skonfiguruj opcje ANCM w pliku Web.config</span><span class="sxs-lookup"><span data-stu-id="083ef-174">Configure ANCM options in Web.config</span></span>

<span data-ttu-id="083ef-175">Konfiguracja modułu platformy ASP.NET Core są przechowywane w *web.config* pliku, który znajduje się w folderze głównym.</span><span class="sxs-lookup"><span data-stu-id="083ef-175">Configuration for the ASP.NET Core Module is stored in the *web.config* file that is located in the application's root folder.</span></span> <span data-ttu-id="083ef-176">Ustawienia w tym pliku punktu do uruchamiania polecenia i argumentów, które uruchomiona aplikacja platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="083ef-176">Settings in this file point to the startup command and arguments that start your ASP.NET Core app.</span></span> <span data-ttu-id="083ef-177">Dla przykładu *web.config* wskazówki na temat opcji konfiguracji i kod zobacz [odwołania do platformy ASP.NET Core modułu konfiguracji](xref:host-and-deploy/aspnet-core-module).</span><span class="sxs-lookup"><span data-stu-id="083ef-177">For sample *web.config* code and guidance on configuration options, see [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module).</span></span>

### <a name="run-with-iis-express-in-development"></a><span data-ttu-id="083ef-178">Uruchom z programem IIS Express do rozwoju</span><span class="sxs-lookup"><span data-stu-id="083ef-178">Run with IIS Express in development</span></span>

<span data-ttu-id="083ef-179">Usługi IIS Express można uruchomić programu Visual Studio przy użyciu domyślnego profilu zdefiniowany za pomocą szablonów ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="083ef-179">IIS Express can be launched by Visual Studio using the default profile defined by the ASP.NET Core templates.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="083ef-180">Konfiguracja serwera proxy używa protokołu HTTP i token parowania</span><span class="sxs-lookup"><span data-stu-id="083ef-180">Proxy configuration uses HTTP protocol and a pairing token</span></span>

<span data-ttu-id="083ef-181">Serwer proxy między ANCM i Kestrel używa protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="083ef-181">The proxy created between the ANCM and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="083ef-182">Przy użyciu protokołu HTTP jest optymalizacji wydajności których ruch między ANCM i Kestrel odbywa się na adres sprzężenia zwrotnego wylogowuje interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="083ef-182">Using HTTP is a performance optimization where the traffic between the ANCM and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="083ef-183">Nie istnieje ryzyko z podsłuchiwaniu ruch między ANCM i Kestrel z lokalizacji wylogowuje na serwerze.</span><span class="sxs-lookup"><span data-stu-id="083ef-183">There's no risk of eavesdropping the traffic between the ANCM and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="083ef-184">Token parowania służy do zagwarantowania, że żądań odebranych przez Kestrel były przekazywane przez serwer proxy przez usługi IIS i nie pochodzą z innego źródła.</span><span class="sxs-lookup"><span data-stu-id="083ef-184">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="083ef-185">Token parowania zostanie utworzona i ustawiona w zmiennej środowiskowej (`ASPNETCORE_TOKEN`) przez ANCM.</span><span class="sxs-lookup"><span data-stu-id="083ef-185">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the ANCM.</span></span> <span data-ttu-id="083ef-186">Token parowania zostanie również ustawiona w nagłówku (`MSAspNetCoreToken`) na każde żądanie przekazywane przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="083ef-186">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="083ef-187">Oprogramowanie pośredniczące IIS sprawdzanie żądań odbierze upewnij się, że parowania wartość tokenu nagłówka odpowiada wartości zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="083ef-187">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="083ef-188">Jeśli wartości tokenów są niezgodne, żądanie jest rejestrowane i odrzucone.</span><span class="sxs-lookup"><span data-stu-id="083ef-188">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="083ef-189">Parowania zmiennej środowiskowej tokenu i komunikacji między ANCM i Kestrel nie są dostępne z lokalizacji wylogowuje na serwerze.</span><span class="sxs-lookup"><span data-stu-id="083ef-189">The pairing token environment variable and the traffic between the ANCM and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="083ef-190">Bez wiedzy o parowania wartość tokenu, osoba atakująca nie może przesłać żądania, które pomijają wyboru w oprogramowaniu pośredniczącym usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="083ef-190">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="next-steps"></a><span data-ttu-id="083ef-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="083ef-191">Next steps</span></span>

<span data-ttu-id="083ef-192">Aby uzyskać więcej informacji, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="083ef-192">For more information, see the following resources:</span></span>

* [<span data-ttu-id="083ef-193">Przykładowa aplikacja dla tego artykułu</span><span class="sxs-lookup"><span data-stu-id="083ef-193">Sample app for this article</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample)
* [<span data-ttu-id="083ef-194">Kod źródłowy platformy ASP.NET Core modułu</span><span class="sxs-lookup"><span data-stu-id="083ef-194">ASP.NET Core Module source code</span></span>](https://github.com/aspnet/AspNetCoreModule)
* [<span data-ttu-id="083ef-195">Odwołania do konfiguracji modułu platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="083ef-195">ASP.NET Core Module Configuration Reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="083ef-196">Hosting w systemie Windows z usługami IIS</span><span class="sxs-lookup"><span data-stu-id="083ef-196">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)