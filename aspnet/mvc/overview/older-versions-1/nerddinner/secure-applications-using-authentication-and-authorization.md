---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: "Güvenli kimlik doğrulama ve yetkilendirme kullanarak uygulamaları | Microsoft Docs"
author: microsoft
description: "Adım 9 kullanıcılar kaydetmeniz gerekir böylece NerdDinner uygulamamız güvenli hale getirmek için yetkilendirme ve kimlik doğrulaması ekleme gösterir ve oturum açma oluşturmak için siteye..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: a23b2cf4d1728624698c0db49c25ea7efd3af67d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
<a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="db0fa-103">Güvenli kimlik doğrulama ve yetkilendirme kullanarak uygulamaları</span><span class="sxs-lookup"><span data-stu-id="db0fa-103">Secure Applications Using Authentication and Authorization</span></span>
====================
<span data-ttu-id="db0fa-104">tarafından [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="db0fa-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="db0fa-105">PDF indirin</span><span class="sxs-lookup"><span data-stu-id="db0fa-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="db0fa-106">9. adım bir ücretsiz budur ["NerdDinner" uygulaması Öğreticisi](introducing-the-nerddinner-tutorial.md) , yetenekte küçük bir yapı ancak tamamlandı, ASP.NET MVC 1 kullanarak web uygulamasına nasıl aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="db0fa-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="db0fa-107">Adım 9 kullanıcılar kaydetmeniz gerekir böylece NerdDinner uygulamamız güvenli hale getirmek için yetkilendirme ve kimlik doğrulaması ekleme gösterir ve yeni azalma ve yalnızca bir Yemeği barındırma kullanıcı oluşturmak için siteye oturum açma düzenleyebilir, daha sonra.</span><span class="sxs-lookup"><span data-stu-id="db0fa-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="db0fa-108">ASP.NET MVC 3 kullanıyorsanız, izlemeniz önerilir [MVC 3 ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik deposu](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticileri.</span><span class="sxs-lookup"><span data-stu-id="db0fa-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="db0fa-109">NerdDinner 9. adım: Kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="db0fa-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="db0fa-110">Şu anda uygulama herkes verir bizim NerdDinner oluşturma ve tüm Yemeği ayrıntılarını düzenleme yeteneğini sitesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="db0fa-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="db0fa-111">Kullanıcıların kaydetmeniz gerekir böylece bu değiştirelim ve yeni azalma oluşturmak ve böylece kimin bir Yemeği barındırma kullanıcı onu daha sonra düzenleyebilirsiniz bir kısıtlama eklemek için site oturum açın.</span><span class="sxs-lookup"><span data-stu-id="db0fa-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="db0fa-112">Bu ayarı etkinleştirmek için kimlik doğrulama ve yetkilendirme uygulamamız güvenli hale getirmek için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="db0fa-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="db0fa-113">Anlama kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="db0fa-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="db0fa-114">*Kimlik doğrulama* tanımlamak ve bir uygulamaya erişmeyi istemci kimliğini doğrulama işlemidir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="db0fa-115">Daha fazla basitçe, "bir Web sitesini ziyaret ettiğinizde olan son kullanıcı" tanımlama hakkında öyledir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="db0fa-116">ASP.NET tarayıcı kullanıcıların kimliklerini doğrulamak için birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="db0fa-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="db0fa-117">Internet web uygulamaları için kullanılan en yaygın kimlik doğrulama yaklaşımını "Forms kimlik doğrulaması" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="db0fa-118">Form kimlik doğrulaması, bir HTML oturum açma formu, uygulama içinde yazar ve ardından bir son kullanıcı bir veritabanı veya başka bir parola kimlik bilgisi deposunda karşı gönderen kullanıcı adı/parola doğrulamak bir geliştirici sağlar.</span><span class="sxs-lookup"><span data-stu-id="db0fa-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="db0fa-119">Kullanıcı adı/parola bileşimi doğru ise, geliştirici sonra gelecekteki istekler genelinde kullanıcıyı tanımlamak için şifrelenmiş bir HTTP tanımlama vermek için ASP.NET sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="db0fa-120">Form kimlik doğrulaması ile NerdDinner uygulamamızı kullanarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="db0fa-121">*Yetkilendirme* kimliği doğrulanmış bir kullanıcı belirli bir URL/kaynağa erişmek için veya bazı eylemleri gerçekleştirmek için izni olup olmadığını belirleme işlemidir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="db0fa-122">Örneğin, NerdDinner uygulamamız içinde biz yalnızca oturum açan kullanıcılar erişebilir yetkilendirmek istersiniz */azalma/oluşturma* URL ve yeni azalma oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db0fa-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="db0fa-123">Biz de böylece yalnızca bir Yemeği barındırma kullanıcının – düzenlemek ve diğer tüm kullanıcılara düzenleme erişimi reddetme yetkilendirme mantığı eklemek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="db0fa-124">Form kimlik doğrulaması ve AccountController</span><span class="sxs-lookup"><span data-stu-id="db0fa-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="db0fa-125">Yeni ASP.NET MVC uygulamaları oluştururken ASP.NET MVC için varsayılan Visual Studio Proje şablonu otomatik olarak form kimlik doğrulamasını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="db0fa-126">Bir site içinde güvenlik tümleştirmek gerçekten kolay hale getirir projeye – önceden oluşturulmuş hesap oturum açma sayfası uygulama da otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="db0fa-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="db0fa-127">Ona erişen kullanıcı kimliği doğrulanmamış olduğunda varsayılan Site.master ana sayfa "Oturum Aç" bağlantı sağ üst tarafında sitenin görüntüler:</span><span class="sxs-lookup"><span data-stu-id="db0fa-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="db0fa-128">"Oturum Aç" bağlantısını tıklatarak geçen bir kullanıcıya */Account/oturum açma* URL'si:</span><span class="sxs-lookup"><span data-stu-id="db0fa-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="db0fa-129">Kayıtlı olmayabilirsiniz ziyaretçileri yapabilirsiniz onlara sürer "Register" bağlantıyı – tıklatarak */Account/Register* URL ve izin vermeniz hesabı ayrıntılarını girin:</span><span class="sxs-lookup"><span data-stu-id="db0fa-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="db0fa-130">"Register" düğmesini tıklatarak ASP.NET üyelik sistemi içinde yeni bir kullanıcı oluşturun ve forms kimlik doğrulaması kullanarak site üzerine kullanıcı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="db0fa-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="db0fa-131">Bir kullanıcı oturum açmış olduğunda, bir "Hoş Geldiniz [username]!" çıktısını almak için sayfanın sağ üst Site.master değiştirir</span><span class="sxs-lookup"><span data-stu-id="db0fa-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="db0fa-132">ileti ve işler bir "günlük birinde yerine" bir "Oturumu Kapat" bağlayın.</span><span class="sxs-lookup"><span data-stu-id="db0fa-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="db0fa-133">"Oturumu Kapat" bağlantısını tıklatarak kullanıcı kaydeder:</span><span class="sxs-lookup"><span data-stu-id="db0fa-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="db0fa-134">Yukarıdaki oturum açma, oturum kapatma ve kayıt işlevi proje oluşturduğunuzda, Projemizin için Visual Studio tarafından eklenen AccountController sınıfı içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="db0fa-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="db0fa-135">AccountController ilişkin kullanıcı Arabirimi \Views\Account dizininde görünüm şablonları kullanılarak uygulanır:</span><span class="sxs-lookup"><span data-stu-id="db0fa-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="db0fa-136">AccountController sınıf ASP.NET formları kimlik doğrulamasını sistem şifreli kimlik doğrulaması tanımlama bilgileri ve depolamak ve kullanıcı adları/parolaları doğrulamak için ASP.NET üyelik API'si vermek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="db0fa-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="db0fa-137">ASP.NET üyelik API genişletilebilir ve kullanılacak bir parola kimlik bilgisi deposunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="db0fa-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="db0fa-138">ASP.NET, kullanıcı adı/parola Active Directory veya bir SQL veritabanı içinde depolama yerleşik üyelik sağlayıcısı uygulamaları ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="db0fa-139">Proje kökündeki "web.config" dosyasını açarak ve aramakta NerdDinner uygulamamızı kullanması gereken hangi üyelik sağlayıcısı yapılandırabilmeniz için &lt;üyelik&gt; içindeki bölümü.</span><span class="sxs-lookup"><span data-stu-id="db0fa-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="db0fa-140">Proje oluşturduğunuzda eklenen varsayılan web.config SQL üyelik sağlayıcısı kaydeder ve "ApplicationServices" adlı bir bağlantı dizesi kullanmak için yapılandırır veritabanı konumu belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="db0fa-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="db0fa-141">Varsayılan "ApplicationServices" bağlantı dizesini (içinde belirtilen &lt;connectionStrings&gt; web.config dosyasının) SQL Express kullanmak üzere yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="db0fa-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="db0fa-142">"ASPNETDB. adlı SQL Express bir veritabanına işaret eder MDF"uygulamanın altında" uygulama\_Data "dizini.</span><span class="sxs-lookup"><span data-stu-id="db0fa-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="db0fa-143">Bu veritabanı üyelik API'si uygulama içerisinden ilk defa yoksa, ASP.NET otomatik olarak veritabanını oluşturmak ve uygun üyelik veritabanı şeması içindeki sağlayın:</span><span class="sxs-lookup"><span data-stu-id="db0fa-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="db0fa-144">Biz isteyen bir tam SQL Server örneğini kullanın (veya uzak bir veritabanına bağlanmak için) SQL Express kullanmak yerine, tüm yapılacaklar ihtiyacımız ise "ApplicationServices" bağlantı dizesi web.config dosyasında güncelleştirmek ve emin olmak için uygun üyelik şeması konumundaki işaret veritabanına eklendi.</span><span class="sxs-lookup"><span data-stu-id="db0fa-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="db0fa-145">Çalıştırabilirsiniz "aspnet\_regsql.exe" bir üyelik ve bir ASP.NET uygulama hizmetleri için uygun şema eklemek için \Windows\Microsoft.NET\Framework\v2.0.50727\ dizininde yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="db0fa-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="db0fa-146">Azalma/oluşturma [Authorize] filtresini kullanarak URL yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="db0fa-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="db0fa-147">Güvenli kimlik doğrulaması ve hesap yönetim uygulaması NerdDinner uygulama için etkinleştirmek için herhangi bir kod yazmak zorunda alamadık.</span><span class="sxs-lookup"><span data-stu-id="db0fa-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="db0fa-148">Kullanıcılar yeni hesapları bizim uygulama ve sitenin oturum açma/oturum kapatma ile kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="db0fa-149">Şimdi biz yetkilendirme mantığı uygulamaya ekleyin ve bunlar görebileceği ve neleri site içinde yapamayacağı denetlemek için ziyaretçileri kullanıcı adı ve kimlik doğrulama durumu kullanın.</span><span class="sxs-lookup"><span data-stu-id="db0fa-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="db0fa-150">Bizim DinnersController sınıfı "Oluştur" eylem yöntemlerinin yetkilendirme mantığı ekleyerek başlayalım.</span><span class="sxs-lookup"><span data-stu-id="db0fa-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="db0fa-151">Biz, özellikle gerektirecektir erişen kullanıcılar */azalma/oluşturma* URL oturum,.</span><span class="sxs-lookup"><span data-stu-id="db0fa-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="db0fa-152">Bunlar oturum açmadıysanız, oturum açma böylece biz bunları oturum açma sayfasına yeniden yönlendir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="db0fa-153">Bu mantık uygulanması oldukça kolaydır.</span><span class="sxs-lookup"><span data-stu-id="db0fa-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="db0fa-154">Tüm yapılacaklar ihtiyacımız olan bizim oluşturma eylem yöntemleri [Authorize] filtresi öznitelik eklemek için şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="db0fa-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="db0fa-155">ASP.NET MVC "için eylem yöntemleri bildirimli olarak uygulanabilir yeniden kullanılabilir mantığını uygulamak için kullanılan eylem filtrelerini" oluşturabilme destekler.</span><span class="sxs-lookup"><span data-stu-id="db0fa-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="db0fa-156">[Authorize] filtre ASP.NET MVC tarafından sağlanan yerleşik eylem filtreleri biridir ve yetkilendirme kuralları eylem yöntemleri ve denetleyici sınıfları bildirimli olarak uygulamak bir geliştirici sağlar.</span><span class="sxs-lookup"><span data-stu-id="db0fa-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="db0fa-157">Herhangi bir parametre (like yukarıda) olmadan uygulandığında [Authorize] filtre eylem yöntemi isteği yapan kullanıcı içinde – oturum açmış olmanız gerekir ve yoksa onu otomatik olarak tarayıcı oturum açma URL'sine yönlendirir zorlar.</span><span class="sxs-lookup"><span data-stu-id="db0fa-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="db0fa-158">İlk olarak istenen URL bir sorgu dizesi bağımsız değişken olarak geçirilen bu yeniden yönlendirme yaparken (örneğin: / Account/oturum açma? ReturnUrl = % 2fDinners % 2fCreate).</span><span class="sxs-lookup"><span data-stu-id="db0fa-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="db0fa-159">Bunlar oturum sonra AccountController kullanıcıyı başta istenen URL'ye sonra yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="db0fa-160">[Authorize] filtre isteğe bağlı olarak kullanıcı hem de ve izin verilen kullanıcıların veya izin verilen güvenlik rolünün bir üyesi listesini içinde kaydedildiğini istemek için kullanılan bir "Kullanıcılar" veya "Rol" özelliği belirtmek için özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="db0fa-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="db0fa-161">Örneğin, aşağıdaki kodu yalnızca iki belirli kullanıcılar, "scottgu" ve "billg" azalma/Oluştur URL'ye erişmek sağlar:</span><span class="sxs-lookup"><span data-stu-id="db0fa-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="db0fa-162">Kod içinde belirli bir kullanıcı adları katıştırma ancak oldukça beklemediğiniz sürdürülebilir olma eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="db0fa-163">Daha iyi bir yaklaşım üst düzey "rol" tanımlamaktır, kod karşı denetler ve ardından bir veritabanı veya active directory sistemi (koddan dışarıdan depolanması gerçek kullanıcı eşleme listesi etkinleştirme) kullanarak rolü halinde kullanıcıları eşlemek için.</span><span class="sxs-lookup"><span data-stu-id="db0fa-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="db0fa-164">ASP.NET, yerleşik rol yönetimi API bu kullanıcı/rol eşleme gerçekleştirmek yardımcı olabilir (olanları SQL ve Active Directory dahil) rol sağlayıcıları yerleşik bir kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="db0fa-165">Ardından yalnızca kullanıcıların belirli "Yönetici" rolü içindeki azalma/Oluştur URL erişmesine izin vermek üzere kod güncelleştiriyoruz:</span><span class="sxs-lookup"><span data-stu-id="db0fa-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="db0fa-166">Oluştururken User.Identity.Name özelliğini kullanarak azalma</span><span class="sxs-lookup"><span data-stu-id="db0fa-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="db0fa-167">Biz denetleyici temel sınıfını kullanıma sunulan User.Identity.Name özelliğini kullanarak bir isteğin geçerli oturum açma kullanıcı adını alabilir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="db0fa-168">Önceki biz bizim Create() eylem yöntemini HTTP POST sürümü uygulandığında biz sabit kodlanmış bir statik dizeye Yemeği "HostedBy" özelliği vardı.</span><span class="sxs-lookup"><span data-stu-id="db0fa-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="db0fa-169">Biz şimdi bunun yerine User.Identity.Name özelliği kullanmak için bu kodu güncelleştir yanı sıra bir RSVP Yemeği oluşturma ana bilgisayar için otomatik olarak Ekle:</span><span class="sxs-lookup"><span data-stu-id="db0fa-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="db0fa-170">Create() yöntemi [Authorize] özniteliği ekledik olduğundan, ASP.NET MVC azalma/Oluştur URL'yi ziyaret eden kullanıcı sitesinde oturum açtıysa, eylem yönteminin yalnızca yürütüldüğünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="db0fa-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="db0fa-171">Bu nedenle, User.Identity.Name özellik değeri her zaman geçerli bir kullanıcı adı içerir.</span><span class="sxs-lookup"><span data-stu-id="db0fa-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="db0fa-172">Düzenlerken User.Identity.Name özelliğini kullanarak azalma</span><span class="sxs-lookup"><span data-stu-id="db0fa-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="db0fa-173">Artık kullanıcıları sınırlar ve böylece yalnızca bunlar kendilerini barındıran azalma özelliklerini düzenleyebilirsiniz bazı yetkilendirme mantığı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="db0fa-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="db0fa-174">Bu konuda yardımcı olmak için önce bir "IsHostedBy(username)" yardımcı yöntemi (içinde daha önce oluşturduğumuz Dinner.cs parçalı sınıf) bizim Yemeği nesnesine ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="db0fa-175">True veya false sağlanan kullanıcı Yemeği HostedBy özelliği eşleşen ve bunları büyük küçük harf duyarlı dize karşılaştırması gerçekleştirmek için gerekli mantığı yalıtır bağlı olarak bu yardımcı yöntemini döndürür:</span><span class="sxs-lookup"><span data-stu-id="db0fa-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="db0fa-176">Ardından bir [Authorize] özniteliği Edit() eylem yöntemlerini bizim DinnersController sınıfı içinde ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="db0fa-177">Bu kullanıcılar isteğine oturum açmanız gerekir, sağlayacak bir */Dinners/düzenleme / [kimlik]* URL.</span><span class="sxs-lookup"><span data-stu-id="db0fa-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="db0fa-178">Kodu daha sonra oturum açan kullanıcının Yemeği konak eşleşip eşleşmediğini doğrulamak için Dinner.IsHostedBy(username) yardımcı yöntemini kullanan bizim düzenleme yöntemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="db0fa-179">Kullanıcı konak değilse, biz "InvalidOwner" görüntülemek ve istek sonlandırmak.</span><span class="sxs-lookup"><span data-stu-id="db0fa-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="db0fa-180">Bunu yapmak için kod aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="db0fa-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="db0fa-181">Biz sonra \Views\Dinners dizinde sağ tıklayın ve Add - seçin&gt;görüntülemek yeni bir "InvalidOwner" görünümü oluşturmak için menü komutu.</span><span class="sxs-lookup"><span data-stu-id="db0fa-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="db0fa-182">Biz ile dolduracaksınız aşağıdaki hata iletisi:</span><span class="sxs-lookup"><span data-stu-id="db0fa-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="db0fa-183">Ve şimdi kullanıcının sahip olmadığınız bir Yemeği Düzenle girişiminde bulunduğunda, bunlar bir hata iletisi alırsınız:</span><span class="sxs-lookup"><span data-stu-id="db0fa-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="db0fa-184">Azalma de silmek ve yalnızca bir Yemeği ana onu silebilirsiniz olun izni kilitlemek için bizim denetleyicisi içinde biz Delete() eylem yöntemleri için aynı adımları yineleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0fa-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="db0fa-185">Gösterme/gizleme düzenleme ve silme bağlantılar</span><span class="sxs-lookup"><span data-stu-id="db0fa-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="db0fa-186">Biz, düzenleme ve silme eylem yöntemine bizim DinnersController sınıfının bizim ayrıntıları URL'den bağlıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="db0fa-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="db0fa-187">Şu anda biz ayrıntıları URL ziyaretçiye Yemeği ana olup bakılmaksızın düzenleme ve silme eylem bağlantıları gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="db0fa-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="db0fa-188">Böylece bağlantıları ziyaret kullanıcı Yemeği sahibi ise yalnızca görüntülenir bu değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="db0fa-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="db0fa-189">Bizim DinnersController içinde Details() eylem yöntemi Yemeği nesnesini alır ve bunu bizim görünüm şablonu model nesnesi olarak geçirir:</span><span class="sxs-lookup"><span data-stu-id="db0fa-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="db0fa-190">Biz koşullu Göster/Düzenle ve Sil bağlantıları yardımcı yöntemi gibi aşağıda Dinner.IsHostedBy() kullanarak Gizle için bizim görünüm şablonu güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db0fa-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="db0fa-191">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="db0fa-191">Next Steps</span></span>

<span data-ttu-id="db0fa-192">Şimdi nasıl RSVP AJAX kullanarak azalma için kimliği doğrulanmış kullanıcılara etkinleştirme sırasında bakalım.</span><span class="sxs-lookup"><span data-stu-id="db0fa-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="db0fa-193">[Önceki](implement-efficient-data-paging.md)
[sonraki](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="db0fa-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>