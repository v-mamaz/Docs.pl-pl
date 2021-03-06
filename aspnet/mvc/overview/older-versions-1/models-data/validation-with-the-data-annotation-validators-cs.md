---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: Weryfikacja przy użyciu modułów weryfikacji adnotacji danych (C#) | Dokumentacja firmy Microsoft
author: microsoft
description: Korzystaj z integratora modelu adnotacji danych do wykonywania sprawdzania poprawności w aplikacji ASP.NET MVC. Dowiedz się, jak używać różnych typów weryfikacji...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 203e49e67d8a9c6eb9dbf605a8d7d860737de073
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/16/2018
ms.locfileid: "41754864"
---
<a name="validation-with-the-data-annotation-validators-c"></a>Weryfikacja przy użyciu modułów weryfikacji adnotacji danych (C#)
====================
przez [firmy Microsoft](https://github.com/microsoft)

> Korzystaj z integratora modelu adnotacji danych do wykonywania sprawdzania poprawności w aplikacji ASP.NET MVC. Dowiedz się, jak używać różnych typów atrybutów modułu sprawdzania poprawności i pracować z nimi w programie Microsoft Entity Framework.


W tym samouczku dowiesz się, jak używać modułów weryfikacji adnotacji danych do przeprowadzania weryfikacji w aplikacji ASP.NET MVC. Zaletą używania modułów weryfikacji adnotacji danych jest, czy umożliwiają one do wykonywania sprawdzania poprawności, po prostu dodając jeden lub więcej atrybutów — na przykład wymagane lub atrybut StringLength — do właściwości klasy.

Zanim będzie można użyć modułów weryfikacji adnotacji danych, należy pobrać integratora modelu adnotacji danych. Próbka integratora modelu adnotacji danych można pobrać z witryny CodePlex, po kliknięciu [tutaj](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).


Jest ważne dowiedzieć się, że integratora modelu adnotacji danych nie jest oficjalną częścią platformę Microsoft ASP.NET MVC. Mimo że integratora modelu adnotacji danych został utworzony przez zespół programu Microsoft ASP.NET MVC, Microsoft nie oferuje oficjalne pomocy technicznej dla integratora modelu adnotacji danych opisano i używanych w tym samouczku.


## <a name="using-the-data-annotation-model-binder"></a>Za pomocą integratora modelu adnotacji danych

Aby użyć integratora modelu adnotacji danych w aplikacji ASP.NET MVC, należy najpierw dodać odwołanie do zestawu Microsoft.Web.Mvc.DataAnnotations.dll i zestawu System.ComponentModel.DataAnnotations.dll. Wybierz opcję menu **projektu, Dodaj odwołanie**. Następnie kliknij przycisk **Przeglądaj** kartę, a następnie przejdź do lokalizacji, w której pobrano (i rozpakowanej) przykładowe integratora modelu adnotacji danych (zobacz **rys.1**).

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**Rysunek 1**: Dodawanie odwołania do integratora modelu adnotacji danych ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](validation-with-the-data-annotation-validators-cs/_static/image3.png))

Wybierz zestaw Microsoft.Web.Mvc.DataAnnotations.dll i zestawu System.ComponentModel.DataAnnotations.dll, a następnie kliknij przycisk **OK** przycisku.


Nie można użyć zestawu System.ComponentModel.DataAnnotations.dll dołączone do programu .NET Framework z dodatkiem Service Pack 1 za pomocą integratora modelu adnotacji danych. Należy użyć wersji zestawu System.ComponentModel.DataAnnotations.dll dołączone do pobierania próbki integratora modelu adnotacji danych.


Na koniec należy zarejestrować DataAnnotations integratora modelu w pliku Global.asax. Dodaj następujący wiersz kodu do aplikacji\_Start() obsługi zdarzeń, aby aplikacja\_metody Start() wygląda następująco:

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

Ten wiersz kodu rejestruje ataAnnotationsModelBinder jako domyślnego integratora modelu dla całej aplikacji ASP.NET MVC.

## <a name="using-the-data-annotation-validator-attributes"></a>Przy użyciu atrybutów weryfikacji adnotacji danych

Gdy używasz integratora modelu adnotacji danych, używasz modułu sprawdzania poprawności atrybutów do wykonywania sprawdzania poprawności. Przestrzeń nazw System.ComponentModel.DataAnnotations zawiera następujące atrybuty weryfikacji:

- Zakres — umożliwia weryfikuje, czy wartość właściwości należące do określonego zakresu wartości.
- Wyrażenia regularnego — można sprawdzić, czy wartość właściwości odpowiada wzorcowi określonemu wyrażeniu regularnemu.
- Wymagane — można oznaczać właściwości zgodnie z potrzebami.
- StringLength — umożliwia określenie maksymalnej długości dla właściwości ciągu.
- Sprawdzanie poprawności — klasa bazowa dla wszystkich atrybutów modułu sprawdzania poprawności.

> [!NOTE] 
> 
> Jeśli Twoje potrzeby sprawdzania poprawności nie są spełnione przez żaden standardowych modułów weryfikacji następnie zawsze istnieje możliwość tworzenia atrybutu niestandardowego modułu weryfikacji przez dziedziczenie nowy atrybut weryfikacji z atrybutu podstawowego sprawdzania poprawności.


Klasa produktu w **ofercie 1** ilustruje sposób użycia tych atrybutów modułu sprawdzania poprawności. Nazwa, opis i cena jednostkowa właściwości są oznaczone jako wymagane. Nazwa właściwości musi mieć długość ciągu, która jest mniejsza niż 10 znaków. Na koniec właściwość UnitPrice musi być zgodna z wzorcem wyrażenia regularnego, który reprezentuje kwotę w walucie.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**Wyświetlanie listy 1**: Models\Product.cs

Klasa produktu ilustruje sposób użycia jednego dodatkowego atrybutu: atrybut DisplayName. Atrybut DisplayName służy do modyfikowania nazwę właściwości, gdy właściwość jest wyświetlana w komunikacie o błędzie. Zamiast wyświetlać komunikat o błędzie "wymagane jest pole Cenyjednostkowej" można wyświetlić komunikat o błędzie "wymagane jest pole ceny".

> [!NOTE] 
> 
> Aby dostosować komunikat o błędzie wyświetlany przez moduł weryfikacji niestandardowy komunikat o błędzie można przypisać do właściwości komunikat o błędzie weryfikacji następująco: `<Required(ErrorMessage:="This field needs a value!")>`


Można użyć klasy produktu w **ofercie 1** za pomocą akcji kontrolera Create() w **ofercie 2**. Ta akcja kontrolera zostanie ponownie Utwórz widok podczas stanu modelu zawiera błędy.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**Wyświetlanie listy 2**: Controllers\ProductController.vb

Na koniec możesz utworzyć widok w **ofercie 3** , kliknij prawym przyciskiem myszy działanie Create() i wybierając opcję menu **Dodaj widok**. Utwórz widok silnie typizowaną klasą produktu jako klasy modelu. Wybierz **Utwórz** z listy rozwijanej zawartości widoku (zobacz **na rysunku 2**).

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**Rysunek 2**: Dodawanie widoku Create

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**Wyświetlanie listy 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> Usuń pole identyfikatora formularza tworzenia generowane przez **Dodaj widok** opcji menu. Ponieważ pole identyfikatora odnosi się do kolumny tożsamości, nie chcesz zezwalać użytkownikom na wprowadzanie wartości dla tego pola.


Jeśli prześlesz formularz dla tworzenia produktu i nie należy wprowadzać wartości dla wymaganych pól, a następnie komunikaty o błędach weryfikacji w **rysunek 3** są wyświetlane.

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**Rysunek 3**: Brak wymaganych pól

Jeśli wprowadzasz kwotę w walucie nieprawidłowy, a następnie komunikat o błędzie w **rysunek 4** jest wyświetlana.

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**Rysunek 4**: kwotę w walucie nieprawidłowy

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Przy użyciu modułów weryfikacji adnotacji danych za pomocą programu Entity Framework

Jeśli używasz Microsoft Entity Framework do generowania klasach modeli danych nie można zastosować atrybuty weryfikacji bezpośrednio do swojej klasy. Ponieważ Entity Framework Designer generuje klasy modelu, wszelkie zmiany wprowadzone do klasy modelu zostanie zastąpiony podczas następnego wprowadzisz zmiany w projektancie.

Jeśli chcesz użyć moduły weryfikacji przy użyciu klas wygenerowanych przez program Entity Framework następnie należy utworzyć meta klasy danych. Moduły weryfikacji dotyczą meta klasy danych zamiast stosowania moduły weryfikacji do rzeczywistego klasy.

Załóżmy, że utworzono klasę filmu używający narzędzia Entity Framework (zobacz **rysunek 5**). Wyobraź sobie, ponadto chcesz wprowadzić tytuł filmu i dyrektor ds. właściwości wymaganych właściwości. W takim przypadku można utworzyć klasy częściowe i meta klasy danych w **listę 4**.

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**Rysunek 5**: klasa filmu generowane przez program Entity Framework

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**Wyświetlanie listy 4**: Models\Movie.cs

Plik w **listę 4** zawiera dwie klasy o nazwie MovieMetaData i filmów. Klasa film jest klasy częściowej. Odnosi się do klasy częściowej generowane przez program Entity Framework, który jest zawarty w pliku DataModel.Designer.vb.

.NET framework nie obsługuje obecnie częściowe właściwości. W związku z tym, nie ma możliwości dotyczą atrybutów weryfikacji właściwości klasy filmu zdefiniowane w pliku DataModel.Designer.vb przez zastosowanie atrybutów weryfikacji właściwości klasy filmu zdefiniowane w pliku w **listę 4**.

Należy zauważyć, że klasy częściowej film zostanie nadany atrybut MetadataType, który wskazuje na klasy MovieMetaData. Klasa MovieMetaData zawiera właściwości serwera proxy dla właściwości klasy filmu.

Atrybuty modułu sprawdzania poprawności są stosowane do właściwości klasy MovieMetaData. Właściwości tytułu, Dyrektor ds. i DateReleased są oznaczone jako wymagane właściwości. Dyrektor ds. właściwość musi być przypisany jest ciąg zawierający mniej niż 5 znaków. Na koniec atrybut DisplayName jest stosowany do właściwości DateReleased, aby wyświetlić komunikat o błędzie, takie jak "pole daty wydania jest wymagane." zamiast błędu "DateReleased pole jest wymagane."

> [!NOTE] 
> 
> Należy zauważyć, że właściwości serwera proxy w klasie MovieMetaData nie ma potrzeby reprezentują te same typy jako odpowiednie właściwości w klasie filmu. Na przykład właściwość Dyrektor jest właściwością ciągu w klasie film i właściwości obiektu w klasie MovieMetaData.


Na stronie **rysunek 6** ilustruje komunikatów o błędach zwracanych podczas wprowadzania nieprawidłowe wartości dla właściwości filmu.

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**Rysunek 6**: przy użyciu modułów weryfikacji za pomocą programu Entity Framework ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](validation-with-the-data-annotation-validators-cs/_static/image14.png))

## <a name="summary"></a>Podsumowanie

W tym samouczku przedstawiono sposób korzystać z zalet integratora modelu adnotacji danych do wykonywania sprawdzania poprawności w aplikacji ASP.NET MVC. Pokazaliśmy ci, jak używać różnych typów atrybutów StringLength i modułu sprawdzania poprawności atrybutów, takich jak jest to wymagane. Przedstawiono również sposób użycia tych atrybutów podczas pracy z usługą Microsoft Entity Framework.

> [!div class="step-by-step"]
> [Poprzednie](validating-with-a-service-layer-cs.md)
> [dalej](creating-model-classes-with-the-entity-framework-vb.md)
