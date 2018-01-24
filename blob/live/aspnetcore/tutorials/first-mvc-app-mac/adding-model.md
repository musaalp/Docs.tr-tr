---
title: "Model bir ASP.NET Core MVC uygulamasına ekleme"
author: rick-anderson
description: "Bir model için basit bir ASP.NET Core uygulama ekleyin."
ms.author: riande
manager: wpickett
ms.devlang: csharp
ms.date: 09/22/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: .net-core
uid: tutorials/first-mvc-app-mac/adding-model
ms.openlocfilehash: 3a7db5e435fe72150feb1e0ec905b6f6adc16f2c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2018
---
[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model1.md)]

* <span data-ttu-id="d86ff-103">Sağ *modelleri* klasörünü ve ardından **Ekle** > **yeni dosya**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-103">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span> 
* <span data-ttu-id="d86ff-104">İçinde **yeni dosya** iletişim:</span><span class="sxs-lookup"><span data-stu-id="d86ff-104">In the **New File** dialog:</span></span>

  * <span data-ttu-id="d86ff-105">Seçin **genel** sol bölmede.</span><span class="sxs-lookup"><span data-stu-id="d86ff-105">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="d86ff-106">Seçin **boş sınıfı** center sorun içinde.</span><span class="sxs-lookup"><span data-stu-id="d86ff-106">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="d86ff-107">Sınıf adını **film** seçip **yeni**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-107">Name the class **Movie** and select **New**.</span></span>

<span data-ttu-id="d86ff-108">Aşağıdaki özellikleri ekleyin `Movie` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="d86ff-108">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieNoEF.cs?name=snippet_1)]

<span data-ttu-id="d86ff-109">`ID` Alan veritabanı için birincil anahtarı gerekli.</span><span class="sxs-lookup"><span data-stu-id="d86ff-109">The `ID` field is required by the database for the primary key.</span></span>

<span data-ttu-id="d86ff-110">Herhangi bir hata yoksa doğrulamak için projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d86ff-110">Build the project to verify you don't have any errors.</span></span> <span data-ttu-id="d86ff-111">Artık elinizde bir **M**odeldeki, **M**VC uygulama.</span><span class="sxs-lookup"><span data-stu-id="d86ff-111">You now have a **M**odel in your **M**VC app.</span></span>

## <a name="prepare-the-project-for-scaffolding"></a><span data-ttu-id="d86ff-112">Proje için askılamayı hazırlama</span><span class="sxs-lookup"><span data-stu-id="d86ff-112">Prepare the project for scaffolding</span></span>

- <span data-ttu-id="d86ff-113">Proje dosyasını sağ tıklatın ve ardından **Araçlar > Düzenle dosya**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-113">Right click on the project file, and then select **Tools > Edit File**.</span></span>

  ![Yukarıdaki adımı görünümü](adding-model/_static/1.png)

- <span data-ttu-id="d86ff-115">Aşağıdaki vurgulanmış şekilde NuGet paketlerini eklemek *MvcMovie.csproj* dosyası:</span><span class="sxs-lookup"><span data-stu-id="d86ff-115">Add the following highlighted NuGet packages to the *MvcMovie.csproj* file:</span></span>
             
  [!code-csharp[Main](../first-mvc-app-xplat/start-mvc/sample/MvcMovie/MvcMovie.csproj?highlight=7,10)]

- <span data-ttu-id="d86ff-116">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d86ff-116">Save the file.</span></span>

- <span data-ttu-id="d86ff-117">Oluşturma bir *Models/MvcMovieContext.cs* dosya ve aşağıdakileri ekleyin `MvcMovieContext` sınıfı:[!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span><span class="sxs-lookup"><span data-stu-id="d86ff-117">Create a *Models/MvcMovieContext.cs* file and add the following `MvcMovieContext` class:  [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Models/MvcMovieContext.cs)]</span></span>
   
- <span data-ttu-id="d86ff-118">Açık *haline* dosya ve iki kullanımları ekleyin:[!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span><span class="sxs-lookup"><span data-stu-id="d86ff-118">Open the *Startup.cs* file and add two usings:  [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet1&highlight=1,2)]</span></span>

- <span data-ttu-id="d86ff-119">Veritabanı bağlamı Ekle *haline* dosyası:</span><span class="sxs-lookup"><span data-stu-id="d86ff-119">Add the database context to the *Startup.cs* file:</span></span>

   [!code-csharp[Main](../../tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-7)]

  <span data-ttu-id="d86ff-120">Bu, hangi modeli sınıfları veri modelinde bulunan Entity Framework bildirir.</span><span class="sxs-lookup"><span data-stu-id="d86ff-120">This tells Entity Framework which model classes are included in the data model.</span></span> <span data-ttu-id="d86ff-121">Bir tanımladığınız *varlık kümesini* veritabanında bir filmi tablo olarak temsil edilir film nesnelerin.</span><span class="sxs-lookup"><span data-stu-id="d86ff-121">You're defining one *entity set* of Movie objects, which will be represented in the database as a Movie table.</span></span>

- <span data-ttu-id="d86ff-122">Bir hata doğrulamak için projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d86ff-122">Build the project to verify there are no errors.</span></span>

## <a name="scaffold-the-moviecontroller"></a><span data-ttu-id="d86ff-123">İskele MovieController</span><span class="sxs-lookup"><span data-stu-id="d86ff-123">Scaffold the MovieController</span></span>

<span data-ttu-id="d86ff-124">Proje klasöründe bir terminal penceresi açın ve aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d86ff-124">Open a terminal window in the project folder and run the following commands:</span></span>

```
dotnet restore
dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries 
```
<span data-ttu-id="d86ff-125">Hata alırsanız `No executable found matching command "dotnet-aspnet-codegenerator", verify`:</span><span class="sxs-lookup"><span data-stu-id="d86ff-125">If you get the error `No executable found matching command "dotnet-aspnet-codegenerator", verify`:</span></span>

 * <span data-ttu-id="d86ff-126">Proje dizininde var.</span><span class="sxs-lookup"><span data-stu-id="d86ff-126">You are in the project directory.</span></span> <span data-ttu-id="d86ff-127">Proje dizinine sahip *Program.cs*, *haline* ve *.csproj* dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d86ff-127">The project directory has the *Program.cs*, *Startup.cs* and *.csproj* files.</span></span>
 * <span data-ttu-id="d86ff-128">Dotnet sürüm 1.1 veya daha üstü olduğunda.</span><span class="sxs-lookup"><span data-stu-id="d86ff-128">Your dotnet version is 1.1 or higher.</span></span> <span data-ttu-id="d86ff-129">Çalıştırma `dotnet` sürümü almak için.</span><span class="sxs-lookup"><span data-stu-id="d86ff-129">Run `dotnet` to get the version.</span></span>
 * <span data-ttu-id="d86ff-130">Eklediğiniz `<DotNetCliToolReference>` öğesine [MvcMovie.csproj dosya](#prepare-the-project-for-scaffolding).</span><span class="sxs-lookup"><span data-stu-id="d86ff-130">You have added the `<DotNetCliToolReference>` element to the [MvcMovie.csproj file](#prepare-the-project-for-scaffolding).</span></span>
 
<!--
> [!NOTE]
> If you get an error when the scaffolding command runs, see [issue 444 in the scaffolding repository](https://github.com/aspnet/scaffolding/issues/444) for a workaround.
-->

<span data-ttu-id="d86ff-131">Yapı iskelesi altyapısı aşağıdaki oluşturur:</span><span class="sxs-lookup"><span data-stu-id="d86ff-131">The scaffolding engine creates the following:</span></span>

* <span data-ttu-id="d86ff-132">Film denetleyicisi (*Controllers/MoviesController.cs*)</span><span class="sxs-lookup"><span data-stu-id="d86ff-132">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="d86ff-133">Razor Görünüm Oluştur, Sil, ayrıntıları, düzenleme ve dizin sayfalar için dosyaları (*görünümler/filmler/\*.cshtml*)</span><span class="sxs-lookup"><span data-stu-id="d86ff-133">Razor view files for Create, Delete, Details, Edit and Index pages (*Views/Movies/\*.cshtml*)</span></span>

<span data-ttu-id="d86ff-134">Otomatik olarak oluşturulmasını [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemleri ve görünümler olarak bilinir *iskele*.</span><span class="sxs-lookup"><span data-stu-id="d86ff-134">The automatic creation of [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span> <span data-ttu-id="d86ff-135">En kısa sürede bir filmi veritabanı yönetmenizi sağlayan bir tam olarak işlevsel bir web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d86ff-135">You'll soon have a fully functional web application that lets you manage a movie database.</span></span>

### <a name="add-the-files-to-visual-studio"></a><span data-ttu-id="d86ff-136">Visual Studio için dosyaları Ekle</span><span class="sxs-lookup"><span data-stu-id="d86ff-136">Add the files to Visual Studio</span></span>

* <span data-ttu-id="d86ff-137">Ekleme *MovieController.cs* Visual Studio projesi dosyasına:</span><span class="sxs-lookup"><span data-stu-id="d86ff-137">Add the *MovieController.cs* file to the Visual Studio project:</span></span>

  * <span data-ttu-id="d86ff-138">Sağ tıklayın *denetleyicileri* klasörü ve select **Ekle > dosyaları Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-138">Right-click on the *Controllers* folder and select **Add > Add Files**.</span></span>
  * <span data-ttu-id="d86ff-139">Seçin *MovieController.cs* dosya.</span><span class="sxs-lookup"><span data-stu-id="d86ff-139">Select the *MovieController.cs* file.</span></span>

* <span data-ttu-id="d86ff-140">Ekleme *filmler* klasör ve görünümler:</span><span class="sxs-lookup"><span data-stu-id="d86ff-140">Add the *Movies* folder and views:</span></span>

  * <span data-ttu-id="d86ff-141">Sağ tıklayın *görünümleri* klasörü ve select **Ekle > varolan klasörü Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-141">Right-click on the *Views* folder and select **Add > Add Existing Folder**.</span></span>
  * <span data-ttu-id="d86ff-142">Gidin *görünümleri* klasöründe seçin *Views\Movies*ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-142">Navigate to the *Views* folder, select *Views\Movies*, and then select **Open**.</span></span>
  * <span data-ttu-id="d86ff-143">İçinde **film eklenecek dosyaları seçin** iletişim kutusunda **dahil tüm**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d86ff-143">In the **Select files to add from Movies** dialog, select **Include All**, and then **OK**.</span></span>

[!INCLUDE[adding-model 2x](../../includes/mvc-intro/adding-model2xp.md)]

[!INCLUDE[adding-model](../../includes/mvc-intro/adding-model3.md)]

<span data-ttu-id="d86ff-144">Bir veritabanı ve görüntüleme, düzenleme, güncelleştirme ve verileri silmek için sayfaları artık sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="d86ff-144">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="d86ff-145">Sonraki öğreticide biz veritabanı ile çalışması.</span><span class="sxs-lookup"><span data-stu-id="d86ff-145">In the next tutorial, we'll work with the database.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d86ff-146">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d86ff-146">Additional resources</span></span>

* [<span data-ttu-id="d86ff-147">Etiket Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="d86ff-147">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="d86ff-148">Genelleştirme ve yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="d86ff-148">Globalization and localization</span></span>](xref:fundamentals/localization)

>[!div class="step-by-step"]
<span data-ttu-id="d86ff-149">[Önceki bir görünümü ekleme](adding-view.md)
[sonraki SQL ile çalışma](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="d86ff-149">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  