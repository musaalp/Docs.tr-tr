---
title: "Bir MVC uygulamasına bir görünümü ekleme"
author: Rick-Anderson
description: "Bir MVC uygulamasına bir görünümü ekleme"
ms.author: riande
manager: wpickett
ms.date: 09/1721/2017
ms.topic: article
ms.technology: dotnet-mvc
ms.prod: .net-framework
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 52f15784f16d355791360021f045cf4f3c467897
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/19/2017
---
<a name="adding-a-view"></a><span data-ttu-id="f7e7b-103">Bir görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="f7e7b-103">Adding a View</span></span>
====================
<span data-ttu-id="f7e7b-104">Tarafından [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f7e7b-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="f7e7b-105">Bu bölümde değiştirme oluşturacağız `HelloWorldController` sınıfı şablon dosyalarını düzgün bir şekilde kapsülleyen bir istemci HTML yanıtlarını oluşturma işlemine görünümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="f7e7b-106">Görünüm şablonu kullanarak bir dosyaya oluşturacaksınız [Razor görüntüleme altyapısı](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="f7e7b-107">Razor tabanlı görünümü şablonları bir *.cshtml* dosya uzantısı ve C# kullanarak çıktısını HTML oluşturmak için zarif bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="f7e7b-108">Razor karakter ve bir görünüm şablon yazarken gereken tuş vuruşları sayısını en aza indirir ve iş akışı kodlama hızlı, sıvı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="f7e7b-109">Şu anda `Index` yöntemi controller sınıfında sabit kodlanmış olduğunu belirten bir ileti ile bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="f7e7b-110">Değişiklik `Index` döndürülecek yöntemi bir `View` nesnesi, aşağıdaki kodda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f7e7b-110">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="f7e7b-111">`Index` Yukarıdaki yöntemi tarayıcıya bir HTML yanıtı oluşturmak için bir görünüm şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="f7e7b-112">Denetleyici yöntemlerine (olarak da bilinen [eylem yöntemleri](http://rachelappel.com/asp.net-mvc-actionresults-explained)), gibi `Index` yukarıdaki genellikle döndürme bir [ActionResult](https://msdn.microsoft.com/en-us/library/system.web.mvc.actionresult.aspx) (veya türetilmiş bir sınıf [ActionResult](https://msdn.microsoft.com/en-us/library/system.web.mvc.actionresult.aspx)), olmayan ilkel türler, string ister.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/en-us/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/en-us/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="f7e7b-113">Sağ tıklayın *Views\HelloWorld* klasörü ve tıklatın **Ekle**, ardından **MVC 5 (düzeni Razor) olan görünüm sayfası**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with (Layout Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="f7e7b-114">İçinde **öğesi için ad belirtmek** iletişim kutusunda, girin *dizin*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="f7e7b-115">İçinde **düzen sayfası seçin** iletişim kutusunda, varsayılanı kabul  **\_Layout.cshtml** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="f7e7b-116">Yukarıdaki iletişim *görünümler/paylaşılan* klasörü, sol bölmede seçilidir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="f7e7b-117">Başka bir klasöre özel yerleşim dosya'i seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="f7e7b-118">Biz Düzen dosyası hakkında daha sonra öğreticide konuşun</span><span class="sxs-lookup"><span data-stu-id="f7e7b-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="f7e7b-119">*MvcMovie\Views\HelloWorld\Index.cshtml* dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="f7e7b-120">Aşağıdaki vurgulanmış biçimlendirmeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="f7e7b-121">Sağ tıklayın *Index.cshtml* dosya ve seçin **tarayıcıda görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="f7e7b-123">Ayrıca sağ tıklayabilir, *Index.cshtml* dosya ve seçin **sayfa denetçisi görünümünde.**</span><span class="sxs-lookup"><span data-stu-id="f7e7b-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="f7e7b-124">Bkz: [sayfa denetçisi öğretici](../../views/using-page-inspector-in-aspnet-mvc.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="f7e7b-125">Alternatif olarak, uygulamayı çalıştırın ve Gözat `HelloWorld` denetleyici (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="f7e7b-126">`Index` Denetleyicinizi yönteminde kadar iş yapmak olmadı; yalnızca bir deyim çalışan `return View()`, hangi belirtilen tarayıcı yanıta işlemek için yöntemi bir görünüm şablon dosyası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="f7e7b-127">Kullanılacak görünüm şablonu dosyasının adı açıkça belirtmediğiniz olduğundan, ASP.NET MVC kullanarak varsayılan *Index.cshtml* görünüm dosyasında *\Views\HelloWorld* klasör.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="f7e7b-128">Aşağıdaki görüntü dizesini gösterir &quot;bizim görünüm şablondan Hello!&quot; görünümünde sabit kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="f7e7b-129">Oldukça iyi görünür.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-129">Looks pretty good.</span></span> <span data-ttu-id="f7e7b-130">Ancak, tarayıcının başlık çubuğunda gösterdiğine dikkat edin &quot;Index - My ASP.NET Uy "ve"Uygulama adı"büyük bağlantı sayfanın üst kısmında diyor</span><span class="sxs-lookup"><span data-stu-id="f7e7b-130">However, notice that the browser's title bar shows &quot;Index - My ASP.NET Appli" and the big link on the top of the page says "Application name."</span></span> <span data-ttu-id="f7e7b-131">Tarayıcı pencerenizi nasıl küçük yaptığınız bağlı olarak üç çubukları görmek için üst sağ tıklatın gerekebilir için **giriş**, **hakkında**, **kişi**, **Kaydetmek** ve **oturum** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="f7e7b-132">Görünümleri ve Düzen sayfaları değiştirme</span><span class="sxs-lookup"><span data-stu-id="f7e7b-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="f7e7b-133">İlk olarak, değiştirmek istediğiniz &quot;uygulama adı&quot; sayfanın üst kısmındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="f7e7b-134">Metnin her sayfaya yaygındır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-134">That text is common to every page.</span></span> <span data-ttu-id="f7e7b-135">Uygulamadaki her sayfada görünse bile projesinde, yalnızca tek bir yerde gerçekten uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="f7e7b-136">Git */görünümler/paylaşılan* klasöründe **Çözüm Gezgini** açarak  *\_Layout.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="f7e7b-137">Bu dosya adında bir *düzen sayfası* ve paylaşılan klasörde diğer tüm sayfalar kullanın.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="f7e7b-139">Düzen şablonları, tek bir yerde, sitenizin HTML kapsayıcı düzeni belirtin ve sitenizin birden çok sayfada üzerinden uygulanan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="f7e7b-140">Bul `@RenderBody()` satır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="f7e7b-141">`RenderBody`olan burada tüm görünüm özgü sayfaları, bir yer tutucu oluşturmak Göster, &quot;Sarmalanan&quot; düzeni sayfasında.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="f7e7b-142">Örneğin, **hakkında** bağlantı *Views\Home\About.cshtml* görünümü içinde işlenir `RenderBody` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="f7e7b-143">Title öğesi içeriğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-143">Change the contents of the title element.</span></span> <span data-ttu-id="f7e7b-144">Değişiklik [ActionLink](https://msdn.microsoft.com/en-us/library/dd504972(v=vs.108).aspx) Düzen şablonu içinde &quot;uygulama adı&quot; için &quot;MVC film&quot; ve denetleyicisinden `Home` için `Movies`.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-144">Change the [ActionLink](https://msdn.microsoft.com/en-us/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="f7e7b-145">Tam yerleşimi dosya aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f7e7b-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="f7e7b-146">Uygulama ve şimdi yazacaktır bildirimi çalıştırmak &quot;MVC film &quot;.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="f7e7b-147">Tıklatın **hakkında** bağlantı ve bakın nasıl bu sayfada görüntülenir &quot;MVC film&quot;, çok.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="f7e7b-148">Düzen şablonda değişiklik kez bulduk ve sahip sitesindeki tüm sayfalara yansıtacak yeni başlığı.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="f7e7b-149">Ne zaman önce oluşturduğumuz *Views\HelloWorld\Index.cshtml* dosya, aşağıdaki kod içeriyor:</span><span class="sxs-lookup"><span data-stu-id="f7e7b-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="f7e7b-150">Yukarıdaki Razor kod açıkça düzen sayfası ayarlıyor.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="f7e7b-151">İncelemek *görünümleri\\_ViewStart.cshtml* dosyası tam aynı Razor biçimlendirme içeriyor.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="f7e7b-152"> *[Görünümleri\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)*  dosyası tüm görünümleri kullanacağı ortak yerleşim tanımlar, out veya bu koddan kaldırma bu nedenle yorum yapabileceği *Views\HelloWorld\ Index.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="f7e7b-153">Kullanabileceğiniz `Layout` farklı bir görünümü ayarlayın veya ayarlamak özellik `null` herhangi bir düzen dosyası kullanılacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="f7e7b-154">Şimdi, dizin görünümünün başlığı değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="f7e7b-155">Açık *MvcMovie\Views\HelloWorld\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="f7e7b-156">Bir değişiklik yapmak için iki yerde vardır: ilk olarak, metin görünür tarayıcının başlık ve ardından ikincil üstbilgisinde ( `<h2>` öğesi).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="f7e7b-157">Hangi bölümünün uygulamanın hangi bit kod değişiklikleri görebilmeleri biraz farklı yapmanız.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="f7e7b-158">HTML Başlığı görüntülemek için ayarlar yukarıdaki kodu belirtmek için bir `Title` özelliği `ViewBag` nesne (olduğu içinde *Index.cshtml* şablonu görüntüle).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="f7e7b-159">Dikkat Düzen şablonunu ( *görünümler/paylaşılan\\_Layout.cshtml* ) bu değeri kullanır `<title>` öğesi bir parçası olarak `<head>` bölümünde daha önce değiştirilmiş HTML.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="f7e7b-160">Bu kullanarak `ViewBag` yaklaşımı, kolayca iletebilir diğer parametreleri şablonu görüntüleme ve düzeni dosyanız arasında.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="f7e7b-161">Uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-161">Run the application.</span></span> <span data-ttu-id="f7e7b-162">Tarayıcı başlığı, birincil başlık ve ikincil başlıklar değişmiş dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="f7e7b-163">(Değişiklikleri tarayıcıda görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="f7e7b-164">Yüklenecek sunucudan yanıt zorlamak için tarayıcınızda CTRL + F5'e basın.) Tarayıcı başlığı ile oluşturulan `ViewBag.Title` biz kümesinde *Index.cshtml* görüntülemek şablonu ve ek &quot;-film uygulaması&quot; düzeni dosyasına eklendi.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="f7e7b-165">Ayrıca dikkat edin nasıl içerik *Index.cshtml* görünüm şablonu birleştirilmiş ile  *\_Layout.cshtml* şablonu görüntüleme ve tek bir HTML yanıtını tarayıcıya gönderildi.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="f7e7b-166">Düzen şablonları, uygulamanızdaki sayfaların tümünü uygulamak değişiklik gerçekten kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="f7e7b-167">Bizim az biti &quot;veri&quot; (Bu durumda &quot;bizim görünüm şablondan Hello!&quot; ileti) sabit kodlanmış, ancak olduğu.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="f7e7b-168">MVC uygulaması bir &quot;V&quot; (Görünüm) ve aldığınız bir &quot;C&quot; (denetleyicisi), ancak hiçbir &quot;M&quot; (henüz model).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="f7e7b-169">Kısa bir süre içinde biz nasıl adım geçireceğiz bir veritabanı oluşturun ve model verileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-169">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="f7e7b-170">Denetleyici geçirme verileri görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="f7e7b-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="f7e7b-171">Bir veritabanına gidin ve modelleri hakkında konuşun önce ancak şimdi ilk bilgi denetleyicisinden bir görünüme geçirme hakkında konuşun.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="f7e7b-172">Denetleyici sınıfları, gelen bir URL isteğine yanıt olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="f7e7b-173">Denetleyici gelen tarayıcı işleyen kodu istekleri, bir veritabanından veri alır ve sonuçta ne tür bir tarayıcıya göndermek için yanıt verirse yazma burada sınıfıdır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="f7e7b-174">Görünüm şablonları daha sonra bir denetleyicisinden oluşturur ve tarayıcıya bir HTML yanıtını biçimlendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="f7e7b-175">Denetleyicileri sırada tarayıcı yanıta işlemek bir şablonu görüntüleme için hangi veri veya nesneler gerekli sağlamak için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="f7e7b-176">En iyi yöntem: **şablonu görüntüleme hiçbir zaman iş mantığı gerçekleştirmek veya bir veritabanı ile doğrudan etkileşim**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="f7e7b-177">Bunun yerine, şablonu görüntüleme için denetleyici tarafından sağlanan verileri ile çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="f7e7b-178">Bu koruma &quot;sorunları ayrılması&quot; tutan kodunuzu temiz, test edilebilir ve daha korunabilir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="f7e7b-179">Şu anda `Welcome` eylem yönteminde `HelloWorldController` sınıfını alır bir `name` ve `numTimes` parametresi ve çıkışları doğrudan tarayıcıya değerleri.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="f7e7b-180">Bu yanıt dize olarak işleme denetleyiciniz yerine bir görünüm şablonu kullanmayı denetleyicisi değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="f7e7b-181">Şablonu görüntüleme yanıtı oluşturmak için uygun veri bitleri denetleyicisinden görünüme iletmek gerektiği anlamına gelir dinamik bir yanıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="f7e7b-182">Bu şablonu görüntüleme gereksinimlerinize dinamik veri (parametre) put denetleyicisi sağlayarak yapmak bir `ViewBag` şablonu görüntüle daha sonra erişebilirsiniz nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="f7e7b-183">Geri dönüp *HelloWorldController.cs* dosya ve değişiklik `Welcome` ekleme yöntemi bir `Message` ve `NumTimes` değeri `ViewBag` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="f7e7b-184">`ViewBag`istediğiniz ona koyabilirsiniz yani dinamik bir nesne değil; `ViewBag` nesnesi içindeki put kadar tanımlı hiçbir özellik sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="f7e7b-185">[ASP.NET MVC model bağlama sistem](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) adlandırılmış parametreleri otomatik olarak eşlenir (`name` ve `numTimes`) Sorgu dizesinden yönteminizi parametrelere adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="f7e7b-186">Tam *HelloWorldController.cs* dosya şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="f7e7b-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="f7e7b-187">Şimdi `ViewBag` nesnesi görünümüne otomatik olarak geçirilen verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="f7e7b-188">Ardından, bir Hoş Geldiniz görünüm şablonu gerekiyor!</span><span class="sxs-lookup"><span data-stu-id="f7e7b-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="f7e7b-189">İçinde **yapı** menüsünde, select **yapı çözümü** (veya Ctrl + Shift + B) proje derlenmiş emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="f7e7b-190">Sağ tıklayın *Views\HelloWorld* klasörü ve tıklatın **Ekle**, ardından **MVC 5 Düzen (Razor) olan görünüm sayfası**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="f7e7b-191">İçinde **öğesi için ad belirtmek** iletişim kutusunda, girin *Hoş Geldiniz*ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="f7e7b-192">İçinde **düzen sayfası seçin** iletişim kutusunda, varsayılanı kabul  **\_Layout.cshtml** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="f7e7b-193">*MvcMovie\Views\HelloWorld\Welcome.cshtml* dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="f7e7b-194">Biçimlendirme Değiştir *Welcome.cshtml* dosya.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="f7e7b-195">Bildiren bir döngü oluşturacaksınız &quot;Hello&quot; sayıda kullanıcı onu gerektiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="f7e7b-196">Tam *Welcome.cshtml* dosya aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="f7e7b-197">Uygulamayı çalıştırın ve aşağıdaki URL'ye gidin:</span><span class="sxs-lookup"><span data-stu-id="f7e7b-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="f7e7b-198">Şimdi veri URL'den alınır ve denetleyici kullanmaya geçirilen [model Bağlayıcısı](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7e7b-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="f7e7b-199">Verileri denetleyicisi paketleri bir `ViewBag` nesnesini ve nesne görünümüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="f7e7b-200">Görünümü sonra verileri HTML olarak kullanıcıya görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="f7e7b-201">Yukarıdaki örnekte, kullandık bir `ViewBag` denetleyicisinden bir görünüme veri iletmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="f7e7b-202">Öğreticide daha sonra bir denetleyicisinden bir görünüme veri iletmek için bir görünüm modeli kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="f7e7b-203">Veri geçirme görünüm modeli yaklaşım görünüm paketi genellikle çok tercih edilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="f7e7b-204">Blog girişine bakın [dinamik V kesin türü belirtilmiş görünümleri](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="f7e7b-205">Bir tür iyi, bir &quot;M&quot; modeli, ancak veritabanı türü değil.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="f7e7b-206">Ne biz öğrendiğinize ve film bir veritabanı oluşturmak atalım.</span><span class="sxs-lookup"><span data-stu-id="f7e7b-206">Let's take what we've learned and create a database of movies.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f7e7b-207">[Önceki](adding-a-controller.md)
[sonraki](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="f7e7b-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>