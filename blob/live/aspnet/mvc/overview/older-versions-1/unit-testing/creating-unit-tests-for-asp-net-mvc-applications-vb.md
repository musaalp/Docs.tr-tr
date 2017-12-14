---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: "ASP.NET MVC uygulamaları (VB) için birim testleri oluşturma | Microsoft Docs"
author: StephenWalther
description: "Denetleyici eylemleri için birim testleri oluşturmayı öğrenin. Bu öğreticide, bir denetleyici eylemi bir parti döndürüp döndürmediğini test etme Stephen Walther gösteren..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: d92ee0c26787e5c482e8695001d8809d3ee9ee30
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a><span data-ttu-id="fc276-104">ASP.NET MVC uygulamaları (VB) için birim testleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc276-104">Creating Unit Tests for ASP.NET MVC Applications (VB)</span></span>
====================
<span data-ttu-id="fc276-105">tarafından [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="fc276-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="fc276-106">PDF indirin</span><span class="sxs-lookup"><span data-stu-id="fc276-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> <span data-ttu-id="fc276-107">Denetleyici eylemleri için birim testleri oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fc276-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="fc276-108">Bu öğreticide, bir denetleyici eylemi belirli bir görünüm verir, belirli bir veri kümesi döndürür veya farklı türde bir eylem sonucunu döndürür olup olmadığını test etme Stephen Walther gösterir.</span><span class="sxs-lookup"><span data-stu-id="fc276-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="fc276-109">Bu öğreticinin amacı nasıl, denetleyicileri için birim testleri, ASP.NET MVC uygulamaları yazabilir göstermektir.</span><span class="sxs-lookup"><span data-stu-id="fc276-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="fc276-110">Biz, üç farklı türde birim testleri oluşturmak nasıl ele almaktadır.</span><span class="sxs-lookup"><span data-stu-id="fc276-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="fc276-111">Bir denetleyici eylemi tarafından döndürülen görünümü test etme, görünümü bir denetleyici eylemi tarafından döndürülen verileri test etme ve ikinci bir denetleyici eylemi yönlendiren bir denetleyici eylemi olup olmadığını test etme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fc276-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="fc276-112">Test denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc276-112">Creating the Controller under Test</span></span>

<span data-ttu-id="fc276-113">Test düşündüğünüz denetleyicisi oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="fc276-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="fc276-114">Adlı denetleyicisi `ProductController`, listeleme 1'de yer alır.</span><span class="sxs-lookup"><span data-stu-id="fc276-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="fc276-115">**Kod 1 –`ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-115">**Listing 1 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

<span data-ttu-id="fc276-116">`ProductController` Adlı iki eylem yöntemleri içeren `Index()` ve `Details()`.</span><span class="sxs-lookup"><span data-stu-id="fc276-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="fc276-117">Her iki eylem yöntemleri bir görünümü döndürün.</span><span class="sxs-lookup"><span data-stu-id="fc276-117">Both action methods return a view.</span></span> <span data-ttu-id="fc276-118">Dikkat `Details()` Eylem Kimliği adlı bir parametre kabul eder</span><span class="sxs-lookup"><span data-stu-id="fc276-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="fc276-119">Bir denetleyici tarafından döndürülen görünümü test etme</span><span class="sxs-lookup"><span data-stu-id="fc276-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="fc276-120">Test etmek istiyoruz düşünün desteklemediğini `ProductController` sağ görünümdeki döndürür.</span><span class="sxs-lookup"><span data-stu-id="fc276-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="fc276-121">Emin olmak istiyoruz olduğunda `ProductController.Details()` eylem çağrıldığında, ayrıntı görünümü döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fc276-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="fc276-122">2. listeleme test sınıfı tarafından döndürülen görünümü test etme için birim testi içerir `ProductController.Details()` eylem.</span><span class="sxs-lookup"><span data-stu-id="fc276-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="fc276-123">**Kod 2 –`ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-123">**Listing 2 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

<span data-ttu-id="fc276-124">Adlı bir test yöntemi listeleme 2 sınıfında içerir `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="fc276-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="fc276-125">Bu yöntem üç satır kod içerir.</span><span class="sxs-lookup"><span data-stu-id="fc276-125">This method contains three lines of code.</span></span> <span data-ttu-id="fc276-126">Kod ilk satırını yeni bir örneğini oluşturur `ProductController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fc276-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="fc276-127">İkinci satır kod denetleyicinin çağırır `Details()` eylem yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="fc276-128">Son olarak, son satırının desteklemediğini görünümü tarafından döndürülen kodu denetimleri `Details()` Ayrıntılar görünümü bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="fc276-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="fc276-129">`ViewResult.ViewName` Özelliği, denetleyici tarafından döndürülen görünümün adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fc276-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="fc276-130">Bu özellik test etme hakkında bir büyük uyarı.</span><span class="sxs-lookup"><span data-stu-id="fc276-130">One big warning about testing this property.</span></span> <span data-ttu-id="fc276-131">Bir denetleyici görünüm döndürebilir iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="fc276-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="fc276-132">Bir denetleyici açıkça şuna benzer bir görünüm döndürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fc276-132">A controller can explicitly return a view like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

<span data-ttu-id="fc276-133">Alternatif olarak, görünümün adını şöyle denetleyici eylemini addan:</span><span class="sxs-lookup"><span data-stu-id="fc276-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

<span data-ttu-id="fc276-134">Bu denetleyici eylemi de adlı bir görünüm verir `Details`.</span><span class="sxs-lookup"><span data-stu-id="fc276-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="fc276-135">Ancak, görünümün adını eylem adından algılanır.</span><span class="sxs-lookup"><span data-stu-id="fc276-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="fc276-136">Görünüm adı test etmek isterseniz, açıkça Görünüm adı denetleyici eylemden döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="fc276-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="fc276-137">Her iki tuş bileşimini girerek birim testi listeleme 2'de çalıştırabilirsiniz **Ctrl-R, A** veya tıklatarak **Çözümdeki tüm Testleri Çalıştır** (bkz: Şekil 1) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fc276-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="fc276-138">Test başarılı olursa, Şekil 2 Test Sonuçları penceresinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fc276-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


<span data-ttu-id="fc276-139">[![Çözümde tüm Testleri Çalıştır](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fc276-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span></span>

<span data-ttu-id="fc276-140">**Şekil 01**: Çözümdeki tüm testleri çalıştır ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fc276-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))</span></span>


<span data-ttu-id="fc276-141">[![Başarılı!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="fc276-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span></span>

<span data-ttu-id="fc276-142">**Şekil 02**: başarılı!</span><span class="sxs-lookup"><span data-stu-id="fc276-142">**Figure 02**: Success!</span></span> <span data-ttu-id="fc276-143">([Tam boyutlu görüntüyü görüntülemek için tıklatın](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="fc276-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="fc276-144">Bir denetleyici tarafından döndürülen görünüm verileri test etme</span><span class="sxs-lookup"><span data-stu-id="fc276-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="fc276-145">MVC denetleyicisi veri olarak adlandırılan bir şey kullanarak bir görünümüne geçirir  *`View Data`* .</span><span class="sxs-lookup"><span data-stu-id="fc276-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="fc276-146">Örneğin, çağırdığınızda, belirli bir ürünü ayrıntılarını görüntülemek istediğiniz düşünün `ProductController Details()` eylem.</span><span class="sxs-lookup"><span data-stu-id="fc276-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="fc276-147">Bu durumda, bir örneğini oluşturabilirsiniz bir `Product` sınıfı (modelinizde tanımlı) ve örneğine geçirin `Details` yararlanarak Görünüm `View Data`.</span><span class="sxs-lookup"><span data-stu-id="fc276-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="fc276-148">Değiştirilen `ProductController` listeleme 3'te güncelleştirilmiş içeren `Details()` bir ürün döndüren eylem.</span><span class="sxs-lookup"><span data-stu-id="fc276-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="fc276-149">**Kod 3 –`ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-149">**Listing 3 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

<span data-ttu-id="fc276-150">İlk olarak, `Details()` eylemi yeni bir örneğini oluşturur `Product` dizüstü bilgisayar temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="fc276-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="fc276-151">Sonraki, örneği `Product` sınıfı için ikinci parametre olarak geçirilir `View()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="fc276-152">Birim testleri yazma beklenen verileri olup olmadığını sınamak için Görünüm veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fc276-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="fc276-153">Dizüstü bilgisayar temsil eden bir ürün çağırdığınızda döndürülen olup olmadığına bakılmaksızın Birim listeleme 4 testlerindeki test `ProductController Details()` eylem yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="fc276-154">**4 listeleme –`ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-154">**Listing 4 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

<span data-ttu-id="fc276-155">Listeleme 4'te `TestDetailsView()` yöntemi çağırma tarafından döndürülen görünüm verilerini testleri `Details()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="fc276-156">`ViewData` Üzerinde bir özellik olarak sunulan `ViewResult` çağırarak döndürülen `Details()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="fc276-157">`ViewData.Model` Özelliği, görünüme iletilen ürün içerir.</span><span class="sxs-lookup"><span data-stu-id="fc276-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="fc276-158">Test yalnızca görünüm verilerde bulunan ürün dizüstü bilgisayar adına sahip olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="fc276-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="fc276-159">Bir denetleyici tarafından döndürülen eylem sonucu test etme</span><span class="sxs-lookup"><span data-stu-id="fc276-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="fc276-160">Daha karmaşık bir denetleyici eylemi denetleyicisi eyleme geçirilen parametreler, eylem sonuçlarını değerlere bağlı olarak farklı türlerde döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="fc276-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="fc276-161">Bir denetleyici eylemi çeşitli türleri dahil olmak üzere eylem sonuçlarını döndürebilir bir `ViewResult`, `RedirectToRouteResult`, veya `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="fc276-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="fc276-162">Örneğin, değiştirilmiş `Details()` listeleme 5 eylemde döndürür `Details` geçerli bir ürün kimliği için eylem geçirdiğinizde görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="fc276-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="fc276-163">Bir geçersiz ürün kimliği--değeri olan bir kimliği 1--sonra yönlendirilirsiniz daha az geçirirseniz `Index()` eylem.</span><span class="sxs-lookup"><span data-stu-id="fc276-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="fc276-164">**5 listeleme –`ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-164">**Listing 5 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

<span data-ttu-id="fc276-165">Davranışını sınayabilirsiniz `Details()` listeleme 6'daki birim testi eylemiyle.</span><span class="sxs-lookup"><span data-stu-id="fc276-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="fc276-166">Listeleme 6'daki birim testi için yönlendirilir doğrular `Index` görüntülemek için bir kimlik değeri -1 ile geçirildiğinde `Details()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fc276-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="fc276-167">**6 listeleme –`ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="fc276-167">**Listing 6 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

<span data-ttu-id="fc276-168">Çağırdığınızda `RedirectToAction()` denetleyici eylemi bir denetleyici eylem yöntemine döndürür bir `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="fc276-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="fc276-169">Test denetimleri olup olmadığını `RedirectToRouteResult` kullanıcı adlı bir denetleyici eylemi yönlendirir `Index`.</span><span class="sxs-lookup"><span data-stu-id="fc276-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="fc276-170">Özet</span><span class="sxs-lookup"><span data-stu-id="fc276-170">Summary</span></span>

<span data-ttu-id="fc276-171">Bu öğreticide, MVC denetleyici eylemleri için birim testleri oluşturmak nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="fc276-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="fc276-172">İlk olarak, sağ görünümdeki bir denetleyici eylemi tarafından döndürülen olup olmadığını doğrulamak nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="fc276-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="fc276-173">Nasıl kullanılacağı hakkında bilgi edindiniz `ViewResult.ViewName` özelliği bir görünümün adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fc276-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="fc276-174">Ardından, içeriği test nasıl incelenmesi `View Data`.</span><span class="sxs-lookup"><span data-stu-id="fc276-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="fc276-175">Doğru ürün içinde döndürüldü olup olmadığını denetlemek öğrendiniz `View Data` bir denetleyici eylemi çağrıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="fc276-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="fc276-176">Son olarak, eylem sonuçlarını farklı türde bir denetleyici eylemin getirdiği olup olmadığını nasıl sınayabilirsiniz açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fc276-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="fc276-177">Bir denetleyici döndürüp döndürmediğini test etme hakkında bilgi edindiniz bir `ViewResult` veya `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="fc276-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="fc276-178">Önceki</span><span class="sxs-lookup"><span data-stu-id="fc276-178">Previous</span></span>](creating-unit-tests-for-asp-net-mvc-applications-cs.md)