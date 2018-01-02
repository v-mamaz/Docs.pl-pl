---
title: Metapackage Microsoft.AspNetCore.All dla platformy ASP.NET Core 2.x i nowsze
author: Rick-Anderson
description: "Microsoft.AspNetCore.All metapackage obejmuje wszystkie obsługiwane pakiety Entity Framework Core i ASP.NET Core, wraz z ich zależności."
keywords: ASP.NET Core,NuGet,package,Microsoft.AspNetCore.All,metapackage
ms.author: riande
manager: wpickett
ms.date: 09/20/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/metapackage
ms.openlocfilehash: ff25d80be907994f7ac3d64a8ffa39ae53278ba6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
#<a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-2x"></a>Metapackage Microsoft.AspNetCore.All dla platformy ASP.NET Core 2.x

Ta funkcja wymaga platformy ASP.NET Core 2.x docelowy .NET Core 2.x.

[Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage dla platformy ASP.NET Core obejmuje:

* Wszystkie obsługiwane pakiety przez zespół platformy ASP.NET Core.
* Wszystkie obsługiwane pakiety przez Entity Framework Core. 
* Zależności wewnętrzne i firm 3rd używane przez Entity Framework Core i ASP.NET Core. 

Wszystkie funkcje platformy ASP.NET Core 2.x i Entity Framework Core 2.x znajdują się w `Microsoft.AspNetCore.All` pakietu. Tego pakietu używać domyślnych szablonów projektu.

Numer wersji `Microsoft.AspNetCore.All` metapackage reprezentuje wersji platformy ASP.NET Core i wersji programu Entity Framework Core (zgodne z wersją .NET Core).

Aplikacje używające `Microsoft.AspNetCore.All` metapackage automatycznie korzystać z [.NET Core środowiska uruchomieniowego magazynu](https://docs.microsoft.com/dotnet/core/deploying/runtime-store). Magazyn środowiska uruchomieniowego zawiera wszystkie zasoby środowiska uruchomieniowego potrzebne do uruchomienia aplikacji 2.x platformy ASP.NET Core. Jeśli używasz `Microsoft.AspNetCore.All` metapackage, **nie** zasobów, z którym związane są odwołania pakietów platformy ASP.NET Core NuGet zostały wdrożone za pomocą aplikacji &mdash; magazynie środowiska uruchomieniowego .NET Core zawiera te zasoby. Zasoby w magazynie środowiska uruchomieniowego są wstępnie skompilowana zwiększające czasu uruchomienia aplikacji.

Proces przycinanie pakietu służy do usuwania pakietów, które nie są używane. Przycięte pakiety są wyłączone w danych wyjściowych opublikowanej aplikacji.

Następujące *.csproj* pliku odwołań `Microsoft.AspNetCore.All` metapackage dla platformy ASP.NET Core:

[!code-xml[Main](..\mvc\views\view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=9)]