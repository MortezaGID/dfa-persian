<div dir="rtl">

# Web APIs

قبل از اینکه شروع به ساختن وب api خودمان کنیم مهم است که مرور کنیم صفحات وب واقعا چگونه کار می کنند.

گذشته از همه اینها یک "وب api" به معنای واقعی کلمه در بالای معماری حال حاضر شبکه جهانی وب قرار می گیرد و از مجموعه ای از فناوری ها از جمله HTTP، TCP/IP و غیره استفاده می کند.

در این فصل اصطلاحات اساسی وب API را بررسی خواهیم کرد: <span dir="ltr">endpoints, resources, HTTP
verbs</span>, کدهای وضعیت HTTP و REST. حتی اگر با این موارد از قبل آشنایی دارید توصیه می کنم که این فصل را به طور کامل بخوانید.


### شبکه جهانی وب

اینترنت سیستمی از شبکه های کامپیوتری به هم پیوسته است که حداقل از دهه 1960 وجود داشته است. به هر حال استفاده اولیه از اینترنت محدود به تعداد کمی از شبکه‌های مجزا، عمدتاً دولتی، نظامی یا علمی بود که اطلاعات را به صورت الکترونیکی رد و بدل می‌کردند.

در دهه <a href="https://en.wikipedia.org/wiki/Internet">1980</a>، بسیاری از مؤسسات تحقیقاتی و دانشگاه ها از اینترنت برای به اشتراک گذاری داده ها استفاده می کردند.

در اروپا، بزرگترین گره(Node) اینترنتی در CERN (سازمان اروپایی تحقیقات هسته ای) در ژنو سوئیس که بزرگترین آزمایشگاه فیزیک ذرات جهان را اداره میکند قرار داشت. این آزمایش‌ها مقادیر عظیمی از داده‌ها را تولید می‌کنند که باید از راه دور با دانشمندان در سراسر جهان به اشتراک گذاشته می شدند.

در مقایسه با امروز، استفاده کلی از اینترنت در دهه 1980 بسیار ناچیز بود.اکثر مردم به آن دسترسی نداشتند یا حتی دلیل اهمیت آن را درک نمی کردند. تعداد کمی از گره‌های اینترنتی تمام ترافیک را تأمین می‌کردند و رایانه‌هایی که از آن استفاده می‌کردند، عمدتاً در همان شبکه‌های کوچک بودند.

همه اینها در سال 1989 زمانی که یک دانشمند محقق در سرن، (Tim Berners-Lee) HTTP را اختراع کرد، تغییر کرد و شبکه جهانی وب مدرن را آغاز کرد. نگرش او این بود که سیستم <a href="https://en.wikipedia.org/wiki/Hypertext">hypertext</a> موجود، که در آن متن نمایش داده شده بر روی صفحه کامپیوتر حاوی پیوند (هایپرلینک) به اسناد دیگر است، می تواند به اینترنت منتقل شود.

اختراع او، <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol">پروتکل انتقال هایپرتکست</a> (HTTP)، اولین راه استاندارد و جهانی برای به اشتراک گذاری اسناد از طریق اینترنت بود. این پروتکل این موارد را در قالب صفحات وب ارائه می دهد: اسناد گسسته با URL پیوندها و منابعی مثل عکس ها صوت و ویدیو.

امروزه، زمانی که بیشتر مردم به «اینترنت» فکر می‌کنند، در واقع به شبکه جهانی وب فکر می‌کنند، که در حال حاضر راه اصلی برقراری ارتباط آنلاین میلیاردها نفر و رایانه است.


### URLs

یک url (تعیین کننده محل منابع) آدرس یک منبع بر روی شبکه اینترنت می باشد. برای مثال صفحه اصلی گوگل در https://www.google.com می باشد.

وقتی که می خواهید به صفحه اصلی گوگل بروید شما url کامل آن را در مرورگر تایپ می کنید. 
مرورگر شما از طریق اینترنت یک درخواست می فرستد و یک سرور  به درخواست شما برای نمایش دیتاهای موردنیاز صفحه اصلی Google در مرورگر شما پاسخ می دهد(به زودی آنچه واقعا اتفاق می افتد را پوشش خواهیم داد).

این الگوی درخواست و پاسخ اساس همه ارتباطات وب است. یک کلاینت (معمولاً یک مرورگر اما می تواند یک برنامه یا هر دستگاه متصل به اینترنت باشد) اطلاعاتی را درخواست می کند و سرور پاسخ می دهد.

از آنجایی که ارتباطات وب از طریق HTTP انجام می شود، اینها بیشتر به عنوان درخواست های HTTP و پاسخ های HTTP شناخته می شوند.

در یک URL داده شده نیز چندین مؤلفه مجزا وجود دارد. برای مثال صفحه اصلی گوگل را که در https://www.google.com واقع شده است در نظر بگیرید. قسمت اول یا همان https به نوع درخواست استفاده شده اشاره دارد.

این بخش به مرورگر وب می گوید که چگونه به منابع موجود در أدرس دسترسی داشته باشد.

برای یک وب‌سایت، این معمولاً http یا https است، اما همچنین می‌تواند برای فایل‌ها ftp، برای ایمیل smtp و غیره باشد. 
بخش بعدی، www.google.com، نام میزبان(host) یا نام واقعی سایت است. هر URL حاوی یک نوع درخواست و یک میزبان(هاست) است.

بسیاری از صفحات وب همچنین شامل یک مسیر اختیاری هستند. اگر به صفحه اصلی پایتون در https://www.python.org بروید و روی پیوند صفحه «about» کلیک کنید، به https://www.python.org/about/ هدایت خواهید شد. /about/ یک بخش از آدرس صفحه است.

به طور خلاصه، هر URL مانند https://python.org/about/ دارای سه بخش نهانی است:

- یک شمای کلی(نوع درخواست) - https
- نام میزبان - www.python.org
- و یک مسیر (اختیاری) - /about/


### مجموعه پروتکل اینترنت

هنگامی که URL یک منبع را می دانیم، مجموعه کاملی از فناوری های دیگر باید به درستی (با هم) کار کنند تا کلاینت را به سرور متصل کرده و یک صفحه وب واقعی را بارگیری کند. این به طور گسترده به عنوان <a href="https://en.wikipedia.org/wiki/Internet_protocol_suite">مجموعه پروتکل اینترنت</a> نامیده می شود و کتاب های کاملی وجود دارد که فقط برای این موضوع نوشته شده است. با این حال، برای اهداف خود، می‌توانیم به اصول کلی پایبند باشیم.

هنگامی که کاربر https://www.google.com را در مرورگر وب خود تایپ می کند و دکمه اینتر را می زند، چندین اتفاق می افتد.ابتدا مرورگر باید سرور مورد نظر را در جایی در اینترنت پیدا کند.
از یک سرویس نام دامنه (DNS) برای ترجمه نام دامنه "google.com" به آدرس IP استفاده می کند، که یک دنباله منحصر به فرد از اعداد است که هر دستگاه متصل را نشان می دهد.
اینترنت از نام های دامنه استفاده می کند زیرا به خاطر سپردن نام دامنه برای انسان آسان تر است
مانند «google.com» تا یک <a href="https://en.wikipedia.org/wiki/IP_address">آدرس IP</a> مانند «172.217.164.68».

پس از اینکه مرورگر آدرس IP یک دامنه معین را داشت، به راهی برای ایجاد یک ارتباط ثابت با سرور مورد نظر نیاز دارد.این از طریق پروتکل کنترل انتقال (TCP) اتفاق می افتد.
که مطمئن، مرتب شده و عاری از خطا انتقال بایت ها را بین دو برنامه ارائه می دهد.

برای ایجاد یک اتصال TCP بین دو کامپیوتر، یک "handshake" سه مسیره بین کلاینت و سرور رخ می دهد:

- کلاینت یک SYN(یک نوع پیام) می فرستد و درخواست برقراری اتصال می کند
- سرور با تایید درخواست و ارسال یک پارامتر اتصال با یک SYN-ACK پاسخ می دهد
- کلاینت یک ACK(نشان‌دهنده‌ی دریافت پیام SYN) را برای تایید اتصال به سرور ارسال می کند

هنگامی که اتصال TCP برقرار شد، دو کامپیوتر می توانند از طریق HTTP ارتباط برقرار کنند.


### HTTP Verbs

هر صفحه وب شامل یک آدرس (URL) و همچنین لیستی از اقدامات مورد تایید به نام HTTP verbs است. تاکنون عمدتاً در مورد دریافت یک صفحه وب صحبت کرده ایم، اما امکان ایجاد، ویرایش و حذف محتوا نیز وجود دارد.

وبسایت فیسبوک را درنظر بگیرید.

بعد از لاگین شما می توانید پست های تایملاینتان را بخوانید یک پست جدید ایجاد کنید یا پست های موجودتان را ویرایش یا حذف کنید. این چهار عمل (خواندن - ساختن - ویرایش کردن - حذف کردن) به صورت عامیانه به عنوان اعمال CRUD شناخته می شوند و اکثر کارهایی که به صورت آنلاین انجام می شود را نمایش می دهد.

پروتکل HTTP حاوی تعدادی <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_method">متود درخواست</a> است که می توان از آنها در هنگام درخواست اطلاعات از یک سرور استفاده کرد. چهار عمل رایج برای عملکرد CRUD. چهار عمل POST، GET، PUT و DELETE هستند.

<div dir="ltr">

```
CRUD                            HTTP Verbs
----
Create  <-------------------->  POST
Read    <-------------------->  GET
Update  <-------------------->  PUT
Delete  <-------------------->  DELETE
```

</div>

برای ایجاد محتوا از POST، برای خواندن محتوا از GET، برای به روز رسانی آن PUT و برای حذف آن از DELETE استفاده می کنند.

### Endpoints

یک وب سایت از صفحات وب با HTML، CSS، تصاویر، جاوا اسکریپت و موارد دیگر تشکیل شده است. اما یک وب API به جای آن اندپوینت دارد که urlهایی  با فهرستی از اعمال موجود (HTTP VERBS) هستند که داده‌ها را نشان می‌دهند (معمولاً در <a href="https://json.org/">JSON</a> که رایج‌ترین قالب داده این روزها و پیش‌فرض برای django-rest-framework است).

برای مثال، می‌توانیم اندپوینت API زیر را برای یک وب‌سایت جدید به نام mysite در نظر بگیریم:

<div dir="ltr">

```
https://www.mysite.com/api/users      # GET returns all users
https://www.mysite.com/api/users/<id> # GET returns a single user
```

</div>

در اولین اندپوینت /api/users، یک درخواست GET  لیستی از تمام کاربران موجود را برمی گرداند. این نوع اندپوینت که چندین دیتا را برمی گرداند به عنوان یک مجموعه (کالکشن) شناخته می شود.

اندپوینت دوم /api/users/id یک کاربر واحد را نشان می دهد. یک درخواست GET اطلاعات مربوط به یک کاربر را برمی گرداند.

اگر متود POST را به اندپوینت اول اضافه کنیم، می‌توانیم یک کاربر جدید ایجاد کنیم، در حالی که افزودن متود DELETE به اندپوینت دوم به ما امکان حذف یک کاربر را می‌دهد.

در طول این کتاب با اندپوینت های API بیشتر آشنا خواهیم شد، اما در نهایت ایجاد یک API مستلزم ساخت یک سری اندپوینت است: URL هایی با HTTP verbs مرتبط.

یک صفحه وب از HTML، CSS، تصاویر و موارد دیگر تشکیل شده است. اما اندپوینت تنها راهی برای دسترسی به داده ها از طریق  HTTP verbs موجود است.

### HTTP

قبلاً در این فصل در مورد HTTP صحبت کرده‌ایم، اما در اینجا توضیح خواهیم داد که در واقع HTTP چیست و چگونه کار می‌کند.

پروتکل HTTP یک پروتکل درخواست-پاسخ بین دو کامپیوتر است که در آن یک اتصال TCP وجود دارد. رایانه ای که درخواست ها را می فرستد به عنوان کلاینت شناخته می شود در حالی که رایانه پاسخ دهنده به عنوان سرور شناخته می شود. به طور معمول یک کلاینت یک مرورگر وب است اما می تواند یک برنامه iOS یا هر دستگاه متصل به اینترنت باشد. سرور نامی مناسب برای هر رایانه ای است که برای کار از طریق اینترنت بهینه شده است. تنها چیزی که برای تبدیل یک لپ‌تاپ به سرور نیاز داریم یک نرم‌افزار مخصوص و اتصال دائمی به اینترنت است.

هر پیام HTTP از یک خط وضعیت(status)، سرصفحه درخواست(header) و داده های بدنه(body) که اختیاری می باشد تشکیل شده است. به عنوان مثال، در اینجا یک نمونه پیام HTTP است که ممکن است یک مرورگر برای درخواست به صفحه اصلی Google https://www.google.com ارسال کند.
 
<div dir="ltr">

```
GET / HTTP/1.1
Host: google.com
Accept_Language: en-US
```

</div>

خط اول به عنوان خط درخواست شناخته می شود و متود پروتکل HTTP که استفاده شده را مشخص می کند (GET) (/) نشان دهنده مسیر و (HTTP/1.1) ورژن HTTP که در حال استفاده است را مشخص می کند.

دو خطی که در ادامه آمده سربرگ(header) HTTP می باشد: هاست همان نام دامنه و accept_Language هم همان زبان مورد استفاده است که در این مورد انگلیسی می باشد. به طور کل سربرگ های (<a href="https://en.wikipedia.org/wiki/List_of_HTTP_header_fields">header</a>) HTTP دردسترس زیادی وجود دارد.

پیام‌های HTTP همچنین دارای بخش سوم اختیاری هستند که به عنوان بدنه شناخته می‌شود. با این حال ما فقط یک پیام بدنه با پاسخ های HTTP حاوی داده می بینیم.

برای سادگی، اجازه دهید فرض کنیم که صفحه اصلی گوگل فقط حاوی یک صفحه html به صورت "Hello, World!" است.

پاسخ پیام HTTP از یک سرور Google ممکن است به این صورت باشد.

<div dir="ltr">

```
HTTP/1.1 200 OK
Date: Mon, 03 Aug 2020 23:26:07 GMT
Server: gws
Accept-Ranges: bytes
Content-Length: 13
Content-Type: text/html; charset=UTF-8

Hello, world!
```

</div>

خط اول خط پاسخ است و مشخص می کند که ما از HTTP/1.1 استفاده می کنیم. کد وضعیت 200 OK نشان‌دهنده موفقیت‌آمیز بودن درخواست مشتری است (به زودی در مورد کدهای وضعیت بیشتر توضیح خواهیم داد).

بنابراین هر پیام HTTP درخواست یا پاسخ (request, response)، فرمت زیر را دارد:

<div dir="ltr">

```
Response/request line
Headers...

(optional) Body
```

</div>

اکثر صفحات وب حاوی منابع متعددی هستند که به چندین چرخه درخواست/پاسخ HTTP نیاز دارند.
اگر یک صفحه وب دارای HTML، یک فایل CSS و یک تصویر باشد، قبل از اینکه صفحه وب کامل در مرورگر نمایش داده شود، سه بار درخواست و پاسخ جداگانه بین کلاینت و سرور لازم است.

### Status Codes

هنگامی که مرورگر وب شما یک درخواست HTTP را در یک URL فرستاد، هیچ تضمینی وجود ندارد که همه چیز واقعاً کار کند! بنابراین یک لیست طولانی از <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes">کدهای وضعیت HTTP</a> همراه هر پاسخ HTTP وجود دارد.

می توانید نوع کلی کد وضعیت را بر اساس سیستم زیر تشخیص دهید:

- کدهای 2xx  موفقیت - درخواست توسط کلاینت دریافت، درک و پذیرفته شد

- کدهای 3xx ریدایرکت - درخواست url منتقل شده است

- کدهای 4xx ارور کلاینت - خطایی وجود دارد، معمولاً نوع درخواست URL به صورت نادرست توسط کلاینت فرستاده شده است.

- کدهای 5xx ارور سرور- سرور نمیتواند درخواست کلاینت را به درستی پاسخ دهد.

نیازی به حفظ تمام کدهای وضعیت موجود نیست. با تمرین با رایج ترین موارد مانند 200 (OK)، 201 (ایجاد شده)، 301 (به طور دائم منتقل شده)، 404 (یافت نشد) و 500 (خطای سرور) آشنا خواهید شد.

نکته مهمی که باید به خاطر بسپارید این است که، به طور کلی، تنها چهار نتیجه کلی برای هر درخواست HTTP وجود دارد: انجام شد (2xx)، به نحوی هدایت شد (3xx)، خطای کلاینت (4xx)، یا سرور یک خطا ایجاد کرده است (5xx).

این کدهای وضعیت به طور خودکار در خط درخواست/پاسخ در بالای هر پیام HTTP قرار می گیرند.


### Statelessness(عدم وابستگی)

آخرین نکته مهم در مورد HTTP این است که یک پروتکل بدون وضعیت است. این بدان معناست که هر درخواست/پاسخ کاملاً مستقل از قبلی است. هیچ حافظه ذخیره شده ای از فعل و انفعالات گذشته وجود ندارد که در علوم کامپیوتر به عنوان وضعیت)(<a href="https://en.wikipedia.org/wiki/State_(computer_science)">state</a>) شناخته می شود.

این ویژگی عدم وابستگی مزایای زیادی برای HTTP به همراه دارد. از آنجایی که همه سیستم‌های ارتباطی الکترونیکی در طول زمان علامت های خود را از دست می‌دهند، اگر پروتکل بدون وضعیت نداشته باشیم،بهتر بگویم اگر یک چرخه درخواست/پاسخ طی نشود، همه چیز دائماً خراب می‌شود. در نتیجه HTTP به عنوان یک پروتکل توزیع شده بسیار انعطاف پذیر شناخته می شود.

اما نکته منفی این است که مدیریت وضعیت(state) واقعاً در برنامه های وب بسیار مهم است.این موضوع وضعیت(state) این است که چگونه یک وب سایت به یاد می آورد که شما وارد سیستم شده اید و چگونه یک سایت فروشگاه اینترنتی سبد خرید شما را مدیریت می کند. این برای نحوه استفاده ما از وب سایت های مدرن است، اما در خود HTTP پشتیبانی نمی شود.

وضعیت ها قبلا روی سرور حفظ می‌شد، اما بیشتر و بیشتر به سمت کلاینت، مرورگر وب، در فریمورک های فرانت اند مدرن مانند React، Angular و Vue منتقل شده است. هنگامی که احراز هویت کاربر را پوشش می‌دهیم، درباره این موضوع بیشتر می‌آموزیم، اما به یاد داشته باشید که HTTP بدون وضعیت است. این باعث می شود برای ارسال مطمئن اطلاعات بین دو رایانه یک نکته مثبت باشد، اما در به خاطر سپردن هر چیزی خارج از هر درخواست/پاسخ فردی، یک ویژگی منفی باشد.


### REST

موضوع <a href="https://en.wikipedia.org/wiki/Representational_state_transfer">Representational State Transfer (REST)</a> ​​یک معماری است که اولین بار در سال 2000 توسط روی فیلدینگ در پایان نامه خود پیشنهاد شد. این رویکردی است که بالای معماری دنیای وب یعنی بالای موضوع پروتکل HTTP قرار می گیرد.

کل کتاب‌ دارای مجموعه پروتکل اینترنت می باشد که در مورد آنچه که API را واقعاً REST می‌کند یا نه نوشته شده است. اما سه ویژگی اصلی وجود دارد که ما در اینجا برای اهداف خود روی آنها تمرکز خواهیم کرد. هر RESTful API:

- مانند HTTP بدون وضعیت(stateless) است

- از CRUD (GET, POST, PUT, DELETE, etc.) پشتیبانی می کند

- داده ها را در قالب JSON یا XML برمی گرداند

هر API RESTful حداقل باید این سه اصل را داشته باشد. این استاندارد مهم است زیرا یک اصول ثابت برای طراحی و استفاده از APIهای وب ارائه می دهد.


### Conclusion(نتیجه‌گیری)

در حالی که فناوری های زیادی در زیربنای اینترنت مدرن وجود دارد، ما به عنوان توسعه دهندگان مجبور نیستیم همه آن را از ابتدا پیاده سازی کنیم. ترکیب زیبای Django و Django REST Framework به درستی اکثر پیچیدگی های مربوط به API های وب را کنترل می کند. با این حال، داشتن حداقل درک کلی از کار کردن این معماری ها با هم مهم است.

در نهایت یک وب API مجموعه ای از اندپوسنت هاست که بخش های خاصی از یک دیتابیس را نمایش می دهد.ما به‌عنوان توسعه‌دهنده، URL‌ها را برای هر اندپوینت کنترل می‌کنیم، که چه داده‌هایی در دسترس است و چه اقداماتی از طریق HTTP verbs امکان‌پذیر است. همانطور که در ادامه کتاب خواهیم دید، با استفاده از هدرهای HTTP، می‌توانیم سطوح مختلف احراز هویت و دسترسی را نیز تنظیم کنیم.

</div>