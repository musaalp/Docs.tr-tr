---
title: "Belirli bir düzen - ASP.NET Core yetkilendirmek"
author: rick-anderson
description: "Bu makalede, birden çok kimlik doğrulama yöntemleri ile çalışırken, belirli bir düzeni kimliğine sınırlamak açıklanmaktadır."
keywords: "ASP.NET Core, kimlik, kimlik doğrulama şeması"
ms.author: riande
manager: wpickett
ms.date: 10/12/2017
ms.topic: article
ms.assetid: d3d6ca1b-b4b5-4bf7-898e-dcd90ec1bf8c
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/limitingidentitybyscheme
ms.openlocfilehash: 8c9d068b88263d0c06b11a6b87416fb02885c475
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/10/2017
---
# <a name="authorize-with-a-specific-scheme"></a><span data-ttu-id="53fb9-104">Belirli bir düzeniyle yetkilendirmek</span><span class="sxs-lookup"><span data-stu-id="53fb9-104">Authorize with a specific scheme</span></span>

<span data-ttu-id="53fb9-105">Tek sayfa uygulamaları (SPAs) gibi bazı senaryolarda birden çok kimlik doğrulama yöntemlerini kullanmayı yaygındır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-105">In some scenarios, such as Single Page Applications (SPAs), it's common to use multiple authentication methods.</span></span> <span data-ttu-id="53fb9-106">Örneğin, uygulama oturum açma tanımlama bilgisi tabanlı kimlik doğrulaması ve JWT taşıyıcı kimlik doğrulaması için JavaScript istekleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-106">For example, the app may use cookie-based authentication to log in and JWT bearer authentication for JavaScript requests.</span></span> <span data-ttu-id="53fb9-107">Bazı durumlarda, uygulama bir kimlik doğrulama işleyicisi birden çok örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-107">In some cases, the app may have multiple instances of an authentication handler.</span></span> <span data-ttu-id="53fb9-108">Örneğin, iki tanımlama bilgisi işleyicileri burada temel bir kimlik içeriyor ve bir oluşturulduğunda bir multi-Factor authentication (MFA) tetiklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="53fb9-108">For example, two cookie handlers where one contains a basic identity and one is created when a multi-factor authentication (MFA) has been triggered.</span></span> <span data-ttu-id="53fb9-109">Kullanıcıya ek güvenlik gerektiren bir işlem istediğinden MFA tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-109">MFA may be triggered because the user requested an operation that requires extra security.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="53fb9-110">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="53fb9-111">Kimlik doğrulama hizmeti kimlik doğrulama işlemi sırasında yapılandırıldığında, bir kimlik doğrulama düzeni olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-111">An authentication scheme is named when the authentication service is configured during authentication.</span></span> <span data-ttu-id="53fb9-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="53fb9-112">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication()
        .AddCookie(options => {
            options.LoginPath = "/Account/Unauthorized/";
            options.AccessDeniedPath = "/Account/Forbidden/";
        })
        .AddJwtBearer(options => {
            options.Audience = "http://localhost:5001/";
            options.Authority = "http://localhost:5000/";
        });
```

<span data-ttu-id="53fb9-113">Önceki kod, iki kimlik doğrulama işleyicisi eklenmiştir: tanımlama bilgileri, diğeri taşıyıcı için için.</span><span class="sxs-lookup"><span data-stu-id="53fb9-113">In the preceding code, two authentication handlers have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="53fb9-114">Varsayılan düzeni belirtme sonuçlanıyor `HttpContext.User` kimliğe ayarlanan özelliği.</span><span class="sxs-lookup"><span data-stu-id="53fb9-114">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="53fb9-115">Bu davranışı isterseniz, bu değil parametresiz biçiminde çağırarak devre dışı `AddAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="53fb9-115">If that behavior isn't desired, disable it by invoking the parameterless form of `AddAuthentication`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="53fb9-116">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-116">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="53fb9-117">Kimlik doğrulama sırasında kimlik doğrulama middlewares yapılandırıldığında kimlik doğrulama şemasını adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-117">Authentication schemes are named when authentication middlewares are configured during authentication.</span></span> <span data-ttu-id="53fb9-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="53fb9-118">For example:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // Code omitted for brevity

    app.UseCookieAuthentication(new CookieAuthenticationOptions()
    {
        AuthenticationScheme = "Cookie",
        LoginPath = "/Account/Unauthorized/",
        AccessDeniedPath = "/Account/Forbidden/",
        AutomaticAuthenticate = false
    });
    
    app.UseJwtBearerAuthentication(new JwtBearerOptions()
    {
        AuthenticationScheme = "Bearer",
        AutomaticAuthenticate = false,
        Audience = "http://localhost:5001/",
        Authority = "http://localhost:5000/",
        RequireHttpsMetadata = false
    });
```

<span data-ttu-id="53fb9-119">Önceki kod, iki kimlik doğrulama middlewares eklenmiştir: tanımlama bilgileri, diğeri taşıyıcı için için.</span><span class="sxs-lookup"><span data-stu-id="53fb9-119">In the preceding code, two authentication middlewares have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="53fb9-120">Varsayılan düzeni belirtme sonuçlanıyor `HttpContext.User` kimliğe ayarlanan özelliği.</span><span class="sxs-lookup"><span data-stu-id="53fb9-120">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="53fb9-121">Bu davranışı isterseniz, bu değil ayarlayarak devre dışı `AuthenticationOptions.AutomaticAuthenticate` özelliğine `false`.</span><span class="sxs-lookup"><span data-stu-id="53fb9-121">If that behavior isn't desired, disable it by setting the `AuthenticationOptions.AutomaticAuthenticate` property to `false`.</span></span>

---

## <a name="selecting-the-scheme-with-the-authorize-attribute"></a><span data-ttu-id="53fb9-122">Authorize özniteliği düzeniyle seçme</span><span class="sxs-lookup"><span data-stu-id="53fb9-122">Selecting the scheme with the Authorize attribute</span></span>

<span data-ttu-id="53fb9-123">Yetkilendirme noktasında kullanılacak işleyici uygulamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-123">At the point of authorization, the app indicates the handler to be used.</span></span> <span data-ttu-id="53fb9-124">Uygulama ile yetkilendirmek için kimlik doğrulama şemasını virgülle ayrılmış bir listesini geçirerek işleyici seçin `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="53fb9-124">Select the handler with which the app will authorize by passing a comma-delimited list of authentication schemes to `[Authorize]`.</span></span> <span data-ttu-id="53fb9-125">`[Authorize]` Özniteliği, kimlik doğrulama düzeni veya varsayılan bir yapılandırılmış bağımsız olarak kullanılacak düzenleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-125">The `[Authorize]` attribute specifies the authentication scheme or schemes to use regardless of whether a default is configured.</span></span> <span data-ttu-id="53fb9-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="53fb9-126">For example:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="53fb9-127">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-127">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="53fb9-128">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-128">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

---

<span data-ttu-id="53fb9-129">Önceki örnekte tanımlama bilgisi ve taşıyıcı işleyicileri çalıştırın ve oluşturma ve geçerli kullanıcı için bir kimlik ekleme fırsatına sahip.</span><span class="sxs-lookup"><span data-stu-id="53fb9-129">In the preceding example, both the cookie and bearer handlers run and have a chance to create and append an identity for the current user.</span></span> <span data-ttu-id="53fb9-130">Yalnızca tek bir düzen belirterek, karşılık gelen işleyici çalışır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-130">By specifying a single scheme only, the corresponding handler runs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="53fb9-131">ASP.NET 2.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="53fb9-132">ASP.NET 1.x çekirdek</span><span class="sxs-lookup"><span data-stu-id="53fb9-132">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

---

<span data-ttu-id="53fb9-133">Önceki kodda yalnızca işleyici "Bearer" şema ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-133">In the preceding code, only the handler with the "Bearer" scheme runs.</span></span> <span data-ttu-id="53fb9-134">Tanımlama bilgisi tabanlı kimlikleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="53fb9-134">Any cookie-based identities are ignored.</span></span>

## <a name="selecting-the-scheme-with-policies"></a><span data-ttu-id="53fb9-135">İlkeleri düzeniyle seçme</span><span class="sxs-lookup"><span data-stu-id="53fb9-135">Selecting the scheme with policies</span></span>

<span data-ttu-id="53fb9-136">İstenen düzenleri belirtmek istiyorsanız [İlkesi](xref:security/authorization/policies), ayarlayabileceğiniz `AuthenticationSchemes` ilkeniz eklerken koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="53fb9-136">If you prefer to specify the desired schemes in [policy](xref:security/authorization/policies), you can set the `AuthenticationSchemes` collection when adding your policy:</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("Over18", policy =>
    {
        policy.AuthenticationSchemes.Add(JwtBearerDefaults.AuthenticationScheme);
        policy.RequireAuthenticatedUser();
        policy.Requirements.Add(new MinimumAgeRequirement());
    });
});
```

<span data-ttu-id="53fb9-137">Önceki örnekte, "Over18" ilke "Bearer" işleyicisi tarafından oluşturulan kimlik karşı yalnızca çalışır.</span><span class="sxs-lookup"><span data-stu-id="53fb9-137">In the preceding example, the "Over18" policy only runs against the identity created by the "Bearer" handler.</span></span> <span data-ttu-id="53fb9-138">İlke ayarı kullanın `[Authorize]` özniteliğin `Policy` özelliği:</span><span class="sxs-lookup"><span data-stu-id="53fb9-138">Use the policy by setting the `[Authorize]` attribute's `Policy` property:</span></span>

```csharp
[Authorize(Policy = "Over18")]
public class RegistrationController : Controller
```