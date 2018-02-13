# <a name="working-with-sqlite-in-and-razor-pages"></a>İçinde SQLite ve Razor sayfaları ile çalışma

Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)

`MovieContext` Nesnesini işleme veritabanına bağlanırken ve eşleme görevi `Movie` veritabanı kayıtlarını nesnelere. Veritabanı bağlamı kayıtlı [bağımlılık ekleme](xref:fundamentals/dependency-injection) kapsayıcısında `ConfigureServices` yönteminde *haline* dosyası:

[!code-csharp[Main](code/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a>SQLite

[SQLite](https://www.sqlite.org/) Web sitesi durumları:

> SQLite kendi içinde bulunan, yüksek güvenilirlik, katıştırılmış, tam özellikli, ortak etki alanı, bir SQL veritabanı altyapısı ' dir. SQLite dünyanın en fazla kullanılan veritabanı altyapısıdır.

Çok sayıda üçüncü taraf araçları indirebilirsiniz vardır yönetmek ve bir SQLite veritabanı görüntülemek için. Aşağıdaki görüntü arasındadır [SQLite DB tarayıcı](http://sqlitebrowser.org/). Sık kullanılan bir SQLite aracı varsa, bu konuda şeyleri üzerinde bir yorum bırakın.

![SQLite gösteren film db DB tarayıcısı](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a>Çekirdek veritabanı

Adlı yeni bir sınıf oluşturun `SeedData` içinde *modelleri* klasör. Oluşturulan kod aşağıdakiyle değiştirin:

[!code-csharp[Main](code\Models\SeedData.cs)]

Olup olmadığını herhangi filmler DB'de, çekirdek Başlatıcı döndürür.

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a>Çekirdek Başlatıcısı ekleme

Çekirdek Başlatıcısı ekleme `Main` yönteminde *Program.cs* dosyası:

[!code-csharp[Main](../../tutorials/razor-pages\razor-pages-start\sample\RazorPagesMovie\Program.cs)]

### <a name="test-the-app"></a>Uygulamayı test etme

(Seed yöntemi çalışacak şekilde) DB tüm kayıtları silin. Durdurun ve veritabanını oluşturmak için uygulamayı başlatın.

Uygulama hazırlığı yapmış veriler gösterir.