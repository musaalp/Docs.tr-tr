---
title: ASP.NET Core uygulaması oluşturulan sayfaları güncelleştirme
author: rick-anderson
description: ASP.NET Core uygulaması oluşturulan sayfaları güncelleştirme hakkında bilgi edinin.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/da1
ms.openlocfilehash: f47a68840a6307b69bc92a7b157037d91dce5422
ms.sourcegitcommit: f5d403004f3550e8c46585fdbb16c49e75f495f3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/20/2018
ms.locfileid: "49477221"
---
# <a name="update-the-generated-pages-in-an-aspnet-core-app"></a>ASP.NET Core uygulaması oluşturulan sayfaları güncelleştirme

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

Film uygulaması için iyi bir başlangıç sahibiz ancak sunu ideal değildir. Saat (12:00: 00'da aşağıdaki görüntüde) görmesini istemediğiniz ve **ReleaseDate** olmalıdır **yayın tarihi** (iki kelimeye).

![Film verileri gösteren Chrome'da açık film uygulaması](sql/_static/m55.png)

## <a name="update-the-generated-code"></a>Oluşturulan kodu güncelleştirme

Açık *Models/Movie.cs* dosya ve aşağıdaki kodda gösterilen vurgulanan satırları ekleyin:

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieDate.cs?name=snippet_1&highlight=10-11)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie21/Models/MovieDate.cs?name=snippet_1&highlight=10-11,15)]

::: moniker-end

Kırmızı dalgalı çizgi üzerinde sağ tıklayın > **hızlı Eylemler ve yeniden düzenlemeler**.

  ![Bağlamsal menüyü gösterir ** > Hızlı Eylemler ve yeniden düzenlemeler **.](da1/qa.png)

Seçin `using System.ComponentModel.DataAnnotations;`

  ![listenin en üstünde System.ComponentModel.DataAnnotations kullanma](da1/da.png)

  Visual Studio ekler `using System.ComponentModel.DataAnnotations;`.

[!INCLUDE [model1](~/includes/RP/da2.md)]

> [!div class="step-by-step"]
> [Önceki: SQL Server LocalDB ile çalışma](xref:tutorials/razor-pages/sql)
> [sonraki: arama Ekle](xref:tutorials/razor-pages/search)
