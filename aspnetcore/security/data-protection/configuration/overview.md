---
title: Konfigurowanie ochrony danych w podstawowej platformy ASP.NET
author: rick-anderson
description: Informacje o sposobie konfigurowania ochrony danych w ASP.NET Core.
keywords: Platformy ASP.NET Core, ochrony danych, konfiguracji
ms.author: riande
manager: wpickett
ms.date: 07/17/2017
ms.topic: article
ms.assetid: 0e4881a3-a94d-4e35-9c1c-f025d65dcff0
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 4713c2bed04af784e74586daa10ec847262a1345
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
# <a name="configuring-data-protection-in-aspnet-core"></a><span data-ttu-id="e5d76-104">Konfigurowanie ochrony danych w podstawowej platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e5d76-104">Configuring Data Protection in ASP.NET Core</span></span>

<span data-ttu-id="e5d76-105">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e5d76-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e5d76-106">Po zainicjowaniu systemu ochrony danych dotyczy [ustawienia domyślne](xref:security/data-protection/configuration/default-settings) oparte na środowisku operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="e5d76-106">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) based on the operational environment.</span></span> <span data-ttu-id="e5d76-107">Te ustawienia są zazwyczaj odpowiednie dla aplikacji działających na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e5d76-107">These settings are generally appropriate for apps running on a single machine.</span></span> <span data-ttu-id="e5d76-108">Istnieją przypadki, w którym deweloper może być konieczne może zmienić ustawienia domyślne, ponieważ ich aplikacji zostanie rozmieszczona na wielu komputerach lub wymaganiami dotyczącymi zgodności.</span><span class="sxs-lookup"><span data-stu-id="e5d76-108">There are cases where a developer may want to change the default settings, perhaps because their app is spread across multiple machines or for compliance reasons.</span></span> <span data-ttu-id="e5d76-109">W tych sytuacjach systemu ochrony danych oferuje interfejs API konfiguracji zaawansowanych.</span><span class="sxs-lookup"><span data-stu-id="e5d76-109">For these scenarios, the Data Protection system offers a rich configuration API.</span></span>

<span data-ttu-id="e5d76-110">Brak metody rozszerzenia [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) zwracającą [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span><span class="sxs-lookup"><span data-stu-id="e5d76-110">There's an extension method [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) that returns an [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span></span> <span data-ttu-id="e5d76-111">`IDataProtectionBuilder`udostępnia metody rozszerzenia, czy użytkownik może łańcuch można skonfigurować ochrony danych opcje.</span><span class="sxs-lookup"><span data-stu-id="e5d76-111">`IDataProtectionBuilder` exposes extension methods that you can chain together to configure Data Protection options.</span></span>

## <a name="persistkeystofilesystem"></a><span data-ttu-id="e5d76-112">PersistKeysToFileSystem</span><span class="sxs-lookup"><span data-stu-id="e5d76-112">PersistKeysToFileSystem</span></span>

<span data-ttu-id="e5d76-113">Do przechowywania kluczy w udziale UNC, a nie na *LOCALAPPDATA %* domyślna lokalizacja, skonfigurować system z [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span><span class="sxs-lookup"><span data-stu-id="e5d76-113">To store keys on a UNC share instead of at the *%LOCALAPPDATA%* default location, configure the system with [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> <span data-ttu-id="e5d76-114">Zmiana lokalizacji klucza trwałości, system nie będzie automatycznie szyfruje klucze magazynowane, ponieważ nie wiadomo, czy DPAPI to mechanizm szyfrowania odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="e5d76-114">If you change the key persistence location, the system no longer automatically encrypts keys at rest, since it doesn't know whether DPAPI is an appropriate encryption mechanism.</span></span>

## <a name="protectkeyswith"></a><span data-ttu-id="e5d76-115">ProtectKeysWith\*</span><span class="sxs-lookup"><span data-stu-id="e5d76-115">ProtectKeysWith\*</span></span>

<span data-ttu-id="e5d76-116">Możesz skonfigurować system do ochrony kluczy magazynowane wywołując jedną z [ProtectKeysWith\* ](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) interfejsy API konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-116">You can configure the system to protect keys at rest by calling any of the [ProtectKeysWith\*](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) configuration APIs.</span></span> <span data-ttu-id="e5d76-117">W poniższym przykładzie, który klucze są przechowywane w udziale UNC i szyfruje te klucze przechowywane przy użyciu określonego certyfikatu X.509 należy wziąć pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="e5d76-117">Consider the example below, which stores keys on a UNC share and encrypts those keys at rest with a specific X.509 certificate:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

<span data-ttu-id="e5d76-118">Zobacz [klucza szyfrowania w Rest](xref:security/data-protection/implementation/key-encryption-at-rest) więcej przykładów oraz Omówienie mechanizmów wbudowane szyfrowanie klucza.</span><span class="sxs-lookup"><span data-stu-id="e5d76-118">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more examples and discussion on the built-in key encryption mechanisms.</span></span>

## <a name="setdefaultkeylifetime"></a><span data-ttu-id="e5d76-119">SetDefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="e5d76-119">SetDefaultKeyLifetime</span></span>

<span data-ttu-id="e5d76-120">Aby skonfigurować system do użycia zamiast domyślnego okresu istnienia klucza 14 dni 90 dni, użyj [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span><span class="sxs-lookup"><span data-stu-id="e5d76-120">To configure the system to use a key lifetime of 14 days instead of the default 90 days, use [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a><span data-ttu-id="e5d76-121">SetApplicationName</span><span class="sxs-lookup"><span data-stu-id="e5d76-121">SetApplicationName</span></span>

<span data-ttu-id="e5d76-122">Domyślnie systemu ochrony danych izoluje aplikacje od siebie, nawet jeśli ich współużytkowania tego samego repozytorium klucza fizycznych.</span><span class="sxs-lookup"><span data-stu-id="e5d76-122">By default, the Data Protection system isolates apps from one another, even if they're sharing the same physical key repository.</span></span> <span data-ttu-id="e5d76-123">Zapobiega to opis ładunków chronionych drugiej strony aplikacje.</span><span class="sxs-lookup"><span data-stu-id="e5d76-123">This prevents the apps from understanding each other's protected payloads.</span></span> <span data-ttu-id="e5d76-124">Aby udostępnić chronionych ładunków między dwiema aplikacjami, należy użyć [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) z taką samą wartość dla każdej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e5d76-124">To share protected payloads between two apps, use [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) with the same value for each app:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a><span data-ttu-id="e5d76-125">DisableAutomaticKeyGeneration</span><span class="sxs-lookup"><span data-stu-id="e5d76-125">DisableAutomaticKeyGeneration</span></span>

<span data-ttu-id="e5d76-126">Scenariusz, w którym nie ma automatycznie wycofanie kluczy (Tworzenie nowych kluczy) zgodnie z ich podejścia wygaśnięcia aplikacji może być.</span><span class="sxs-lookup"><span data-stu-id="e5d76-126">You may have a scenario where you don't want an app to automatically roll keys (create new keys) as they approach expiration.</span></span> <span data-ttu-id="e5d76-127">Przykładem może być w relacji podstawowe i pomocnicze, gdy tylko głównej aplikacji jest odpowiedzialny za zarządzanie kluczami problemy i dodatkowej aplikacji po prostu ma widoku tylko do odczytu pierścienia klucz aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-127">One example of this might be apps set up in a primary/secondary relationship, where only the primary app is responsible for key management concerns and secondary apps simply have a read-only view of the key ring.</span></span> <span data-ttu-id="e5d76-128">Dodatkowej aplikacji można skonfigurować, aby traktować pierścień klucz jako tylko do odczytu przez skonfigurowanie systemu z [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span><span class="sxs-lookup"><span data-stu-id="e5d76-128">The secondary apps can be configured to treat the key ring as read-only by configuring the system with [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a><span data-ttu-id="e5d76-129">Na poziomie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5d76-129">Per-application isolation</span></span>

<span data-ttu-id="e5d76-130">Gdy systemu ochrony danych jest obsługiwane przez hosta platformy ASP.NET Core, go automatycznie izoluje aplikacje od siebie, nawet jeśli te aplikacje działają w ramach tego samego konta procesu roboczego i korzystają z tej samej materiał klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="e5d76-130">When the Data Protection system is provided by an ASP.NET Core host, it automatically isolates apps from one another, even if those apps are running under the same worker process account and are using the same master keying material.</span></span> <span data-ttu-id="e5d76-131">Przypomina trochę modyfikator IsolateApps z elementu System.Web w  **\<machineKey >** elementu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-131">This is somewhat similar to the IsolateApps modifier from System.Web's **\<machineKey>** element.</span></span>

<span data-ttu-id="e5d76-132">Mechanizm izolacji polega na uwzględnieniu każdej aplikacji na komputerze lokalnym jako unikatowy dzierżawy, w związku z tym [interfejsu IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) ścieżką do katalogu głównego dla danej aplikacji obejmują automatycznie Identyfikatora aplikacji jako dyskryminatora.</span><span class="sxs-lookup"><span data-stu-id="e5d76-132">The isolation mechanism works by considering each app on the local machine as a unique tenant, thus the [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) rooted for any given app automatically includes the app ID as a discriminator.</span></span> <span data-ttu-id="e5d76-133">Unikatowy identyfikator aplikacji jest dostarczany z jednej z dwóch miejscach:</span><span class="sxs-lookup"><span data-stu-id="e5d76-133">The app's unique ID comes from one of two places:</span></span>

1. <span data-ttu-id="e5d76-134">Jeśli aplikacja jest obsługiwana w usługach IIS, unikatowy identyfikator jest ścieżki konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-134">If the app is hosted in IIS, the unique identifier is the app's configuration path.</span></span> <span data-ttu-id="e5d76-135">Jeśli aplikacja jest wdrażana w środowisku farmy sieci web, ta wartość powinna być stała, przy założeniu, że w środowiskach usług IIS są skonfigurowane podobnie na wszystkich komputerach w farmie sieci web.</span><span class="sxs-lookup"><span data-stu-id="e5d76-135">If an app is deployed in a web farm environment, this value should be stable assuming that the IIS environments are configured similarly across all machines in the web farm.</span></span>

2. <span data-ttu-id="e5d76-136">Jeśli aplikacja nie jest obsługiwana przez serwer IIS, unikatowy identyfikator jest ścieżkę fizyczną aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-136">If the app isn't hosted in IIS, the unique identifier is the physical path of the app.</span></span>

<span data-ttu-id="e5d76-137">Unikatowy identyfikator jest przeznaczona na przetrwanie resetuje &mdash; poszczególnych aplikacji i komputera samego w sobie.</span><span class="sxs-lookup"><span data-stu-id="e5d76-137">The unique identifier is designed to survive resets &mdash; both of the individual app and of the machine itself.</span></span>

<span data-ttu-id="e5d76-138">Ten mechanizm izolacji przyjęto założenie, aplikacje nie są złośliwe.</span><span class="sxs-lookup"><span data-stu-id="e5d76-138">This isolation mechanism assumes that the apps are not malicious.</span></span> <span data-ttu-id="e5d76-139">Złośliwe aplikacji zawsze może wpłynąć na inną aplikację do uruchamiania tego samego konta procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="e5d76-139">A malicious app can always impact any other app running under the same worker process account.</span></span> <span data-ttu-id="e5d76-140">W udostępnionym środowisku macierzystym których aplikacje są wzajemnie niezaufanych dostawca hostingu powinna przyjmować kroki w celu zapewnienia systemu operacyjnego poziom izolacji między aplikacjami, w tym oddzielanie repozytoria klucza podstawowego w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="e5d76-140">In a shared hosting environment where apps are mutually untrusted, the hosting provider should take steps to ensure OS-level isolation between apps, including separating the apps' underlying key repositories.</span></span>

<span data-ttu-id="e5d76-141">Jeśli system ochrony danych nie został podany przez hosta platformy ASP.NET Core (na przykład, jeśli go za pomocą wystąpienia `DataProtectionProvider` specyficzne typu) izolacji aplikacji jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="e5d76-141">If the Data Protection system isn't provided by an ASP.NET Core host (for example, if you instantiate it via the `DataProtectionProvider` concrete type) app isolation is disabled by default.</span></span> <span data-ttu-id="e5d76-142">Wyłączenie izolacji aplikacji, wszystkie aplikacje obsługiwana przez tego samego materiału klucza można udostępniać ładunków tak długo, jak zapewniają odpowiednią [celów](xref:security/data-protection/consumer-apis/purpose-strings).</span><span class="sxs-lookup"><span data-stu-id="e5d76-142">When app isolation is disabled, all apps backed by the same keying material can share payloads as long as they provide the appropriate [purposes](xref:security/data-protection/consumer-apis/purpose-strings).</span></span> <span data-ttu-id="e5d76-143">Zapewnienie izolacji aplikacji, w tym środowisku, należy wywołać [SetApplicationName](#setapplicationname) metody konfiguracji obiektu i Podaj unikatową nazwę dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-143">To provide app isolation in this environment, call the [SetApplicationName](#setapplicationname) method on the configuration object and provide a unique name for each app.</span></span>

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a><span data-ttu-id="e5d76-144">Zmiana algorytmów z UseCryptographicAlgorithms</span><span class="sxs-lookup"><span data-stu-id="e5d76-144">Changing algorithms with UseCryptographicAlgorithms</span></span>

<span data-ttu-id="e5d76-145">Stos ochrony danych pozwala na zmianę domyślnego algorytmu, używany przez nowo wygenerować kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5d76-145">The Data Protection stack allows you to change the default algorithm used by newly-generated keys.</span></span> <span data-ttu-id="e5d76-146">Najprostszym sposobem, w tym celu na wywołanie jest [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) zwrotne konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e5d76-146">The simplest way to do this is to call [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) from the configuration callback:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e5d76-147">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-147">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptorConfiguration()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e5d76-148">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptionSettings()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

---

<span data-ttu-id="e5d76-149">Wartość domyślna algorytm szyfrowania to AES-256-CBC, a domyślna ValidationAlgorithm jest HMACSHA256.</span><span class="sxs-lookup"><span data-stu-id="e5d76-149">The default EncryptionAlgorithm is AES-256-CBC, and the default ValidationAlgorithm is HMACSHA256.</span></span> <span data-ttu-id="e5d76-150">Można ustawić domyślną zasadę przez administratora systemu za pośrednictwem [komputera zasad](xref:security/data-protection/configuration/machine-wide-policy), ale jawnym wywołaniem `UseCryptographicAlgorithms` zastępują zasady domyślne.</span><span class="sxs-lookup"><span data-stu-id="e5d76-150">The default policy can be set by a system administrator via a [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy), but an explicit call to `UseCryptographicAlgorithms` overrides the default policy.</span></span>

<span data-ttu-id="e5d76-151">Wywoływanie `UseCryptographicAlgorithms` służy do określania wybranego algorytmu ze wstępnie zdefiniowanej listy wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="e5d76-151">Calling `UseCryptographicAlgorithms` allows you to specify the desired algorithm from a predefined built-in list.</span></span> <span data-ttu-id="e5d76-152">Nie musisz martwić się o Implementacja algorytmu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-152">You don't need to worry about the implementation of the algorithm.</span></span> <span data-ttu-id="e5d76-153">W powyższym scenariuszu systemu ochrony danych próbuje użyć implementacji CNG AES, jeśli uruchomiony w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e5d76-153">In the scenario above, the Data Protection system attempts to use the CNG implementation of AES if running on Windows.</span></span> <span data-ttu-id="e5d76-154">W przeciwnym razie go powraca do zarządzanej [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) klasy.</span><span class="sxs-lookup"><span data-stu-id="e5d76-154">Otherwise, it falls back to the managed [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) class.</span></span>

<span data-ttu-id="e5d76-155">Można ręcznie określić implementację za pośrednictwem wywołania [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span><span class="sxs-lookup"><span data-stu-id="e5d76-155">You can manually specify an implementation via a call to [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span></span>

> [!TIP]
> <span data-ttu-id="e5d76-156">Zmiana algorytmów nie ma wpływu na istniejące klucze w kręgu klucza.</span><span class="sxs-lookup"><span data-stu-id="e5d76-156">Changing algorithms doesn't affect existing keys in the key ring.</span></span> <span data-ttu-id="e5d76-157">Wpływa tylko na nowo wygenerować kluczy.</span><span class="sxs-lookup"><span data-stu-id="e5d76-157">It only affects newly-generated keys.</span></span>

### <a name="specifying-custom-managed-algorithms"></a><span data-ttu-id="e5d76-158">Określanie niestandardowych algorytmów zarządzanych</span><span class="sxs-lookup"><span data-stu-id="e5d76-158">Specifying custom managed algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e5d76-159">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-159">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="e5d76-160">Aby określić niestandardowy zarządzany algorytmów, tworzyć [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) wystąpienia, który wskazuje typy wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="e5d76-160">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptorConfiguration()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e5d76-161">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-161">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="e5d76-162">Aby określić niestandardowy zarządzany algorytmów, tworzyć [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) wystąpienia, który wskazuje typy wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="e5d76-162">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptionSettings()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

---

<span data-ttu-id="e5d76-163">Zazwyczaj \*typ właściwości musi wskazywać na konkretnych, tworzone jako wystąpienia (za pośrednictwem publicznego ctor bez parametrów) implementacje [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) i [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), ale przypadki specjalne systemu niektórych wartości, takich jak `typeof(Aes)` dla wygody.</span><span class="sxs-lookup"><span data-stu-id="e5d76-163">Generally the \*Type properties must point to concrete, instantiable (via a public parameterless ctor) implementations of [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) and [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), though the system special-cases some values like `typeof(Aes)` for convenience.</span></span>

> [!NOTE]
> <span data-ttu-id="e5d76-164">`SymmetricAlgorithm` Musi mieć klucz o długości > = 128 bitów — blok o rozmiarze > = 64-bitowy, i musi obsługiwać szyfrowania w trybie CBC z dopełnienie PKCS #7.</span><span class="sxs-lookup"><span data-stu-id="e5d76-164">The `SymmetricAlgorithm` must have a key length of >= 128 bits, a block size of >= 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="e5d76-165">`KeyedHashAlgorithm` Musi mieć rozmiar szyfrowanego > = 128 bitów i musi obsługiwać klucze o długości równej długości szyfrowanego algorytmem wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-165">The `KeyedHashAlgorithm` must have a digest size of >= 128 bits, and it must support keys of length equal to the hash algorithm's digest length.</span></span> <span data-ttu-id="e5d76-166">`KeyedHashAlgorithm` Nie jest ściśle musi być HMAC.</span><span class="sxs-lookup"><span data-stu-id="e5d76-166">The `KeyedHashAlgorithm` isn't strictly required to be HMAC.</span></span>
> <span data-ttu-id="e5d76-167">SymmetricAlgorithm musi mieć klucz o długości ≥ 128 bitów i blok o rozmiarze ≥ 64-bitowy, a musi obsługiwać szyfrowania w trybie CBC z dopełnienie PKCS #7.</span><span class="sxs-lookup"><span data-stu-id="e5d76-167">The SymmetricAlgorithm must have a key length of ≥ 128 bits and a block size of ≥ 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="e5d76-168">KeyedHashAlgorithm musi mieć rozmiar szyfrowanego > = 128 bitów i musi obsługiwać klucze o długości równej długości szyfrowanego algorytmem wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-168">The KeyedHashAlgorithm must have a digest size of >= 128 bits, and it must support keys of length equal to the hash algorithm's digest length.</span></span> <span data-ttu-id="e5d76-169">KeyedHashAlgorithm nie jest ściśle musi być HMAC.</span><span class="sxs-lookup"><span data-stu-id="e5d76-169">The KeyedHashAlgorithm is not strictly required to be HMAC.</span></span>

### <a name="specifying-custom-windows-cng-algorithms"></a><span data-ttu-id="e5d76-170">Określanie niestandardowych algorytmów CNG systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e5d76-170">Specifying custom Windows CNG algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e5d76-171">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-171">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="e5d76-172">Aby określić niestandardowy algorytm CNG systemu Windows przy użyciu szyfrowania w trybie CBC przy weryfikacji HMAC, Utwórz [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) wystąpienia, który zawiera informacje algorytmicznego:</span><span class="sxs-lookup"><span data-stu-id="e5d76-172">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e5d76-173">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-173">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="e5d76-174">Aby określić niestandardowy algorytm CNG systemu Windows przy użyciu szyfrowania w trybie CBC przy weryfikacji HMAC, Utwórz [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) wystąpienia, który zawiera informacje algorytmicznego:</span><span class="sxs-lookup"><span data-stu-id="e5d76-174">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

---

> [!NOTE]
> <span data-ttu-id="e5d76-175">Algorytm szyfrowania symetrycznego bloku musi mieć klucz o długości > = 128 bitów — blok o rozmiarze > = 64-bitowy, i musi obsługiwać szyfrowania w trybie CBC z dopełnienie PKCS #7.</span><span class="sxs-lookup"><span data-stu-id="e5d76-175">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of >= 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="e5d76-176">Algorytm wyznaczania wartości skrótu musi mieć rozmiar szyfrowanego > = 128 bitów i musi obsługiwać otwierany z BCRYPT\_ALG\_obsługi\_HMAC\_flagi flagi.</span><span class="sxs-lookup"><span data-stu-id="e5d76-176">The hash algorithm must have a digest size of >= 128 bits and must support being opened with the BCRYPT\_ALG\_HANDLE\_HMAC\_FLAG flag.</span></span> <span data-ttu-id="e5d76-177">\*Dostawcy właściwości można ustawić wartości null do używania domyślnego dostawcę dla określonego algorytmu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-177">The \*Provider properties can be set to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="e5d76-178">Zobacz [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-178">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e5d76-179">Program ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-179">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="e5d76-180">Aby określić niestandardowy algorytm CNG systemu Windows przy użyciu szyfrowania tryb Galois liczników ze sprawdzaniem poprawności, Utwórz [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) wystąpienia, który zawiera informacje algorytmicznego:</span><span class="sxs-lookup"><span data-stu-id="e5d76-180">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e5d76-181">Program ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="e5d76-181">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="e5d76-182">Aby określić niestandardowy algorytm CNG systemu Windows przy użyciu szyfrowania tryb Galois liczników ze sprawdzaniem poprawności, Utwórz [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) wystąpienia, który zawiera informacje algorytmicznego:</span><span class="sxs-lookup"><span data-stu-id="e5d76-182">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

---

> [!NOTE]
> <span data-ttu-id="e5d76-183">Algorytm szyfrowania symetrycznego bloku musi mieć klucz o długości > = 128 bitów — blok o rozmiarze dokładnie 128 bitów i musi obsługiwać usługi GCM szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="e5d76-183">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of exactly 128 bits, and it must support GCM encryption.</span></span> <span data-ttu-id="e5d76-184">Można ustawić [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) właściwości na wartość null, aby użyć domyślnego dostawcy dla określonego algorytmu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-184">You can set the [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) property to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="e5d76-185">Zobacz [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-185">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

### <a name="specifying-other-custom-algorithms"></a><span data-ttu-id="e5d76-186">Określanie inne algorytmy niestandardowych</span><span class="sxs-lookup"><span data-stu-id="e5d76-186">Specifying other custom algorithms</span></span>

<span data-ttu-id="e5d76-187">Chociaż nie są widoczne jako najwyższej jakości interfejsu API, system ochrony danych jest rozszerzalny, aby umożliwić Określanie niemal każdego rodzaju algorytmu.</span><span class="sxs-lookup"><span data-stu-id="e5d76-187">Though not exposed as a first-class API, the Data Protection system is extensible enough to allow specifying almost any kind of algorithm.</span></span> <span data-ttu-id="e5d76-188">Na przykład jest to możliwe, aby zachować wszystkich kluczy zawartych w sprzętowego modułu zabezpieczeń (HSM) i do implementacji niestandardowych rdzenia procedury szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="e5d76-188">For example, it's possible to keep all keys contained within a Hardware Security Module (HSM) and to provide a custom implementation of the core encryption and decryption routines.</span></span> <span data-ttu-id="e5d76-189">Zobacz [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) w [podstawowe rozszerzalności kryptografii](xref:security/data-protection/extensibility/core-crypto) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e5d76-189">See [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) in [Core cryptography extensibility](xref:security/data-protection/extensibility/core-crypto) for more information.</span></span>

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a><span data-ttu-id="e5d76-190">Utrwalanie klucze odnośnie do hostowania w kontenerze Docker</span><span class="sxs-lookup"><span data-stu-id="e5d76-190">Persisting keys when hosting in a Docker container</span></span>

<span data-ttu-id="e5d76-191">Odnośnie do hostowania w [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) kontenera kluczy należy utrzymywać albo:</span><span class="sxs-lookup"><span data-stu-id="e5d76-191">When hosting in a [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) container, keys should be maintained in either:</span></span>

* <span data-ttu-id="e5d76-192">Folder, który jest Docker woluminu, który będzie się powtarzać, poza okres istnienia kontenera, takich jak udostępnionego woluminu lub wolumin zainstalowany w hoście.</span><span class="sxs-lookup"><span data-stu-id="e5d76-192">A folder that's a Docker volume that persists beyond the container's lifetime, such as a shared volume or a host-mounted volume.</span></span>
* <span data-ttu-id="e5d76-193">Zewnętrznego dostawcy, takich jak [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) lub [Redis](https://redis.io/).</span><span class="sxs-lookup"><span data-stu-id="e5d76-193">An external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span>

## <a name="see-also"></a><span data-ttu-id="e5d76-194">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e5d76-194">See also</span></span>

* [<span data-ttu-id="e5d76-195">Scenariusze pamiętać z systemem innym niż Podpisane</span><span class="sxs-lookup"><span data-stu-id="e5d76-195">Non DI Aware Scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)
* [<span data-ttu-id="e5d76-196">Międzynarodowe zasad komputera</span><span class="sxs-lookup"><span data-stu-id="e5d76-196">Machine Wide Policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)