# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="52239-101">ASP.NET Core yanıt önbelleğe alma örneği</span><span class="sxs-lookup"><span data-stu-id="52239-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="52239-102">Bu örnek ASP.NET Core kullanımını göstermektedir [yanıt önbelleğe alma Ara](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span><span class="sxs-lookup"><span data-stu-id="52239-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="52239-103">Uygulama, dizin sayfasıyla yanıt dahil olmak üzere bir `Cache-Control` önbelleğe alma davranışını yapılandırmak için üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="52239-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="52239-104">Uygulama ayrıca ayarlar `Vary` yanıt eksikse hizmet önbelleğini yapılandırmak için üstbilgi `Accept-Encoding` sonraki istekleri üstbilgisinin eşleşir, özgün istekteki veriye.</span><span class="sxs-lookup"><span data-stu-id="52239-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="52239-105">Örnek çalıştırırken, dizin sayfası depolandığında ve 10 saniye için önbelleğe önbelleğinden sunulur.</span><span class="sxs-lookup"><span data-stu-id="52239-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>