---
title: Arama ekleme
author: rick-anderson
description: "Basit ASP.NET Core MVC uygulaması için arama eklemeyi gösterir"
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: aaa00a9eedda73a2c66da30b5ace3b5b5a7760b2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2018
---
[!INCLUDE[adding-model](../../includes/mvc-intro/search1.md)]

<span data-ttu-id="ecadd-103">Hızlı bir şekilde adlandırabilirsiniz `searchString` parametresi `id` ile **yeniden adlandırma** komutu.</span><span class="sxs-lookup"><span data-stu-id="ecadd-103">You can quickly rename the `searchString` parameter to `id` with the **rename** command.</span></span> <span data-ttu-id="ecadd-104">Sağ tıklayın `searchString` **> yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="ecadd-104">Right click on `searchString` **> Rename**.</span></span>

![Bağlam menüsü](search/_static/rename.png)

<span data-ttu-id="ecadd-106">Yeniden Adlandır hedefleri vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="ecadd-106">The rename targets are highlighted.</span></span>

![Dizin ActionResult yöntemi vurgulanmış değişkeni gösteren kod Düzenleyicisi](search/_static/rename2.png)

<span data-ttu-id="ecadd-108">Parametre değiştirme `id` ve tüm oluşumlarını `searchString` değiştirmek `id`.</span><span class="sxs-lookup"><span data-stu-id="ecadd-108">Change the parameter to `id` and all occurrences of `searchString` change to `id`.</span></span>

![Kod Düzenleyicisi değişkeni gösteren kimliğine değiştirildi](search/_static/rename3.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search2.md)]

<span data-ttu-id="ecadd-110">IntelliSense bize işaretleme güncelleştirme nasıl yardımcı olduğunu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ecadd-110">Notice how intelliSense helps us update the markup.</span></span>

![Form öğesi için öznitelikler listesinde seçili yöntemiyle IntelliSense bağlamsal menüsü](search/_static/int_m.png)

![IntelliSense bağlamsal menüsüyle yöntemi öznitelik değerleri listesinde seçili](search/_static/int_get.png)

<span data-ttu-id="ecadd-113">Ayırt edici yazı tipini fark `<form>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="ecadd-113">Notice the distinctive font in the `<form>` tag.</span></span> <span data-ttu-id="ecadd-114">Etiket tarafından desteklenen farklı yazı gösterir [etiket Yardımcıları](../../mvc/views/tag-helpers/intro.md).</span><span class="sxs-lookup"><span data-stu-id="ecadd-114">That distinctive font indicates the tag is supported by [Tag Helpers](../../mvc/views/tag-helpers/intro.md).</span></span>

![Form etiketi mor metin ile](search/_static/th_font.png)

[!INCLUDE[adding-model](../../includes/mvc-intro/search3.md)]

>[!div class="step-by-step"]
<span data-ttu-id="ecadd-116">[Önceki](controller-methods-views.md)
[sonraki](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="ecadd-116">[Previous](controller-methods-views.md)
[Next](new-field.md)</span></span>  