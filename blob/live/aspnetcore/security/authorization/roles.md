---
title: "Rol tabanlı yetkilendirme"
author: rick-anderson
description: "Bu belge Authorize özniteliğine rolleri geçirerek ASP.NET Core denetleyici ve eylem erişimi kısıtlamak nasıl gösterir."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/roles
ms.openlocfilehash: 18964464fea76c91d716202d89ee3a3eb36c3078
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2018
---
# <a name="role-based-authorization"></a><span data-ttu-id="fabf7-103">Rol tabanlı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="fabf7-103">Role based Authorization</span></span>

<a name="security-authorization-role-based"></a>

<span data-ttu-id="fabf7-104">Kimlikteki oluşturduğunuzda bir veya daha fazla role ait.</span><span class="sxs-lookup"><span data-stu-id="fabf7-104">When an identity is created it may belong to one or more roles.</span></span> <span data-ttu-id="fabf7-105">Örneğin, Scott yalnızca kullanıcı rolüne ait olabilir adımında Tracy yönetici ve kullanıcı role ait.</span><span class="sxs-lookup"><span data-stu-id="fabf7-105">For example, Tracy may belong to the Administrator and User roles whilst Scott may only belong to the User role.</span></span> <span data-ttu-id="fabf7-106">Bu roller nasıl oluşturulduğunu ve yönetilen Yetkilendirme işlemi yedekleme deposunda bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fabf7-106">How these roles are created and managed depends on the backing store of the authorization process.</span></span> <span data-ttu-id="fabf7-107">Rolleri geliştiriciye açığa [IsInRole](https://docs.microsoft.com/dotnet/api/system.security.principal.genericprincipal.isinrole) yöntemi [ClaimsPrincipal](https://docs.microsoft.com/dotnet/api/system.security.claims.claimsprincipal) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fabf7-107">Roles are exposed to the developer through the [IsInRole](https://docs.microsoft.com/dotnet/api/system.security.principal.genericprincipal.isinrole) method on the [ClaimsPrincipal](https://docs.microsoft.com/dotnet/api/system.security.claims.claimsprincipal) class.</span></span>

## <a name="adding-role-checks"></a><span data-ttu-id="fabf7-108">Rol denetimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fabf7-108">Adding role checks</span></span>

<span data-ttu-id="fabf7-109">Rol tabanlı yetkilendirme denetimleri bildirim temelli&mdash;Geliştirici bunları kendi kodundaki bir denetleyici veya eylemin bir denetleyici içinde karşı istenen kaynağa erişmek için geçerli kullanıcının bir üyesi olması gereken roller belirtme katıştırır.</span><span class="sxs-lookup"><span data-stu-id="fabf7-109">Role-based authorization checks are declarative&mdash;the developer embeds them within their code, against a controller or an action within a controller, specifying roles which the current user must be a member of to access the requested resource.</span></span>

<span data-ttu-id="fabf7-110">Örneğin, aşağıdaki kod üzerinde herhangi bir eylem erişimi sınırlar `AdministrationController` kullanıcılara bir üyesi olan `Administrator` rol:</span><span class="sxs-lookup"><span data-stu-id="fabf7-110">For example, the following code limits access to any actions on the `AdministrationController` to users who are a member of the `Administrator` role:</span></span>

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

<span data-ttu-id="fabf7-111">Birden çok rol bir virgülle ayrılmış liste olarak belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fabf7-111">You can specify multiple roles as a comma separated list:</span></span>

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

<span data-ttu-id="fabf7-112">Bu denetleyici yalnızca üyeleri olan kullanıcılar tarafından erişilebilir olan, `HRManager` rol veya `Finance` rol.</span><span class="sxs-lookup"><span data-stu-id="fabf7-112">This controller would be only accessible by users who are members of the `HRManager` role or the `Finance` role.</span></span>

<span data-ttu-id="fabf7-113">Birden çok öznitelik uygularsanız erişen bir kullanıcı belirtilen tüm rollerinin bir üyesi olması gerekir; Aşağıdaki örnek bir kullanıcı hem de bir üyesi olmasını gerektirir `PowerUser` ve `ControlPanelUser` rol.</span><span class="sxs-lookup"><span data-stu-id="fabf7-113">If you apply multiple attributes then an accessing user must be a member of all the roles specified; the following sample requires that a user must be a member of both the `PowerUser` and `ControlPanelUser` role.</span></span>

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

<span data-ttu-id="fabf7-114">Eylem düzeyinde ek rol yetkilendirme öznitelikleri uygulayarak erişimi daha da sınırlandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fabf7-114">You can further limit access by applying additional role authorization attributes at the action level:</span></span>

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

<span data-ttu-id="fabf7-115">Önceki kod parçacığını üyelerinde `Administrator` rol veya `PowerUser` rol denetleyicisi erişebilir ve `SetTime` eylem, ancak yalnızca üyeleri `Administrator` rol erişebilir `ShutDown` eylem.</span><span class="sxs-lookup"><span data-stu-id="fabf7-115">In the previous code snippet members of the `Administrator` role or the `PowerUser` role can access the controller and the `SetTime` action, but only members of the `Administrator` role can access the `ShutDown` action.</span></span>

<span data-ttu-id="fabf7-116">Ayrıca, denetleyicisi kilit ancak ayrı Eylemler anonim ve kimliği doğrulanmamış erişim izin.</span><span class="sxs-lookup"><span data-stu-id="fabf7-116">You can also lock down a controller but allow anonymous, unauthenticated access to individual actions.</span></span>

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a><span data-ttu-id="fabf7-117">İlke tabanlı rol denetimleri</span><span class="sxs-lookup"><span data-stu-id="fabf7-117">Policy based role checks</span></span>

<span data-ttu-id="fabf7-118">Rol gereksinimlerini de burada bir geliştirici başlangıçta bir ilke yetkilendirme hizmet yapılandırmasının bir parçası kaydeder yeni ilke sözdizimi kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="fabf7-118">Role requirements can also be expressed using the new Policy syntax, where a developer registers a policy at startup as part of the Authorization service configuration.</span></span> <span data-ttu-id="fabf7-119">Bu normalde oluşuyor `ConfigureServices()` içinde *haline* dosya.</span><span class="sxs-lookup"><span data-stu-id="fabf7-119">This normally occurs in `ConfigureServices()` in your *Startup.cs* file.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole", policy => policy.RequireRole("Administrator"));
    });
}
```

<span data-ttu-id="fabf7-120">İlkeleri kullanarak uygulanır `Policy` özellikte `AuthorizeAttribute` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="fabf7-120">Policies are applied using the `Policy` property on the `AuthorizeAttribute` attribute:</span></span>

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

<span data-ttu-id="fabf7-121">Birden çok izin verilen rol bir gereksinim olarak belirtmek istediğiniz sonra için parametre olarak belirtebilirsiniz `RequireRole` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fabf7-121">If you want to specify multiple allowed roles in a requirement then you can specify them as parameters to the `RequireRole` method:</span></span>

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

<span data-ttu-id="fabf7-122">Bu örnek ait kullanıcılar yetkilendirir `Administrator`, `PowerUser` veya `BackupAdministrator` rolleri.</span><span class="sxs-lookup"><span data-stu-id="fabf7-122">This example authorizes users who belong to the `Administrator`, `PowerUser` or `BackupAdministrator` roles.</span></span>