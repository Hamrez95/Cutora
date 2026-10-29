> **سابقه بررسی اولیه، نه وضعیت اجرای فعلی.** نام فعلی محصول Cutora است. برای ادامه و رفع تعارض با Gateهای قدیمی، [START](../../START.md)، [تصمیمات جاری](../decisions/USER_DECISIONS.md) و [گردش‌کار رسانه](../specs/MEDIA_WORKFLOWS.md) مقدم‌اند.

# معماری انتشار و مدیریت محتوای آماده

## توصیه نهایی

در MVP فایل نهایی، کاور و متن آماده شود و کاربر آن‌ها را در رابط رسمی **Buffer یا YouTube Studio** بارگذاری کند. scheduler و dashboard تازه نسازیم. برای Instagram نیز ابزار رسمی/سرویس مجاز، نه شبیه‌سازی login و ذخیره password. اتصال اختصاصی بعد از اثبات اتلاف وقت در کار دستی بررسی شود.

پوشه Ready می‌تواند ویدئوی تدوین‌شده در DaVinci یا هر برنامه دیگر را بپذیرد. وضعیت داخلی اولیه `draft / ready / externally_scheduled / published / failed / unknown` است؛ ثبت دستی وضعیت را از پاسخ معتبر API تفکیک کنیم. «زمان‌بندی محلی» با «پذیرش‌شده در سرویس خارجی» یکی نیست.

## گزینه‌های موجود و هزینه

| گزینه | اطلاعات رسمی بررسی‌شده | انتخاب برای این پروژه |
|---|---|---|
| Buffer Free | تا ۳ کانال، ۱۰ پست در صف هر کانال، یک کاربر، یک API key و ۳۰۰۰ درخواست ماهانه | مناسب شروع Instagram + YouTube؛ ۲۰ ویدئو را یکجا در یک صف Free نمی‌توان پذیرفته فرض کرد |
| Buffer Essentials | برای کانال‌های نخست، ماهانه ۶ دلار/کانال؛ پرداخت سالانه ۶۰ دلار/کانال | تنها در صورت پرشدن صف/نیاز واقعی؛ دو کانال ماهانه ۱۲ دلار یا سالانه ۱۲۰ دلار |
| Buffer Team | چند کاربر و approval پیشرفته در پلن Team | اگر دو نفر باید مستقل حساب سرویس داشته باشند، Free معادل دو عضو نیست |
| Metricool Free | یک برند، سقف ۲۰ پست ماهانه و ۳۰ روز تاریخچه analytics؛ محدودیت پلتفرم | جایگزین برای استفاده کم‌حجم، نه API رایگان عمومی |
| Metricool API | در Advanced/Custom؛ MCP در همه پلن‌ها طبق راهنمای جدید | API و MCP را یک قابلیت/مجوز فرض نکنیم؛ برای استفاده شخصی هزینه adapter توجیه نشده |
| مستقیم Meta/YouTube | دسترسی API رسمی، همراه OAuth و محدودیت حساب/سهمیه | بدون هزینه اشتراک scheduler ممکن است، اما هزینه مهندسی و نگهداری بیشتر |

منابع: [Buffer pricing](https://buffer.com/pricing)، [جدول پلن‌ها و هزینه ماهانه](https://support.buffer.com/article/595-features-available-on-each-buffer-plan)، [حد صف Buffer](https://support.buffer.com/en-us/articles/how-many-posts-can-i-schedule-in-advance-Kmy2IEecqm)، [پلن و API Metricool](https://help.metricool.com/plans-add-ons-and-api-access-explained-xux1u)، [شیوه شمارش Metricool](https://help.metricool.com/main-differences-between-free-and-paid-plans-bl0v9).

محدودیت Buffer صف هم‌زمان است، نه ۱۰ پست در ماه. در Metricool پست‌های انتشار‌یافته در هر شبکه جدا حساب می‌شوند؛ ۱۰ محتوا در دو شبکه می‌تواند سقف ۲۰ را مصرف کند. بعضی صفحات Metricool «scheduled» و بعضی «published» می‌نویسند؛ پیش از وعده عملی، شمارنده حساب واقعی کنترل شود. یک کاربر Free را با اشتراک رمز بین دو نفر حل نکنیم؛ بازبینی محتوا می‌تواند بیرون سرویس باشد و مالک حساب منتشر کند.

قیمت‌ها snapshot تحقیق‌اند، مالیات، کشور پرداخت و تغییر پلن در آن‌ها لحاظ نشده. هیچ اشتراک خریداری یا حسابی متصل نشده است.

## Buffer: API واقعاً موجود است، اما مسیر ساده‌تر داریم

API فعلی GraphQL در `api.buffer.com` است و برای حساب شخصی API key با Bearer token دارد. مستندات OAuth نیز authorization code با PKCE و public client برای desktop را توضیح می‌دهد. key شخصی scope محدود به یک سازمان ندارد؛ بنابراین فقط در main/credential store نگه‌داری شود. [احراز هویت رسمی](https://developers.buffer.com/guides/authentication.html)

ایجاد video post و افزودن به queue در نمونه رسمی وجود دارد. اما **API، endpoint آپلود فایل ندارد**: باید URL مستقیم عمومی و پایدار بدهیم و URL تا زمان انتشار قابل دسترس بماند. لینک loginدار یا signed URL با انقضای زودرس مناسب نیست. این نیاز برای UI خود Buffer الزام یکسانی ایجاد نمی‌کند؛ بارگذاری دستی در خود سرویس، راه ساده‌تر شروع است. [نمونه video post](https://developers.buffer.com/examples/create-video-post.html)، [الزام میزبانی رسانه](https://developers.buffer.com/guides/hosting-media.html)

در نتیجه adapter «ارسال فایل محلی به Buffer» فقط یک HTTP call نیست؛ hosting، دسترسی عمومی، cleanup پس از انتشار، حجم آپلود و امنیت محتوای خانوادگی هم دارد. اگر بعداً لازم شد، فقط خروجی تأییدشده upload شود؛ هیچ raw یا URL خصوصی بدون اجازه عمومی نشود. hosting مستقل از انتخاب Electron است و در P0 وجود ندارد.

پشتیبانی post/reel/story و فیلدهای خاص باید از capabilities کانال و پاسخ همان حساب خوانده شود؛ از وجود فیلد در schema نتیجه نگیریم همه کانال‌ها و پلن‌ها آن را دارند. [مرجع API](https://developers.buffer.com/reference.html)، [توضیح دامنه API فعلی](https://support.buffer.com/en-us/articles/what-is-buffers-api-GtIYIQilz5). دسترسی همه metrics تحلیلی موردنظر از API در این بررسی اثبات نشده؛ از داشبورد آماده استفاده شود.

## Instagram مستقیم

مجموعه رسمی Meta در Postman، حساب‌های Professional شامل Business/Creator و انتشار محتوا را توضیح می‌دهد؛ Stories در مسیر مستندشده فقط Business است. دو مسیر login را مخلوط نکنیم:

| مسیر | مجوزهای اولیه مرتبط در مجموعه رسمی | ملاحظه |
|---|---|---|
| Instagram Login | `instagram_business_basic` و `instagram_business_content_publish` | مسیر مخصوص حساب حرفه‌ای؛ نام مجوزهای کوتاه قدیمی مبنا نباشد |
| Facebook Login | `pages_show_list`، `pages_read_engagement`، `instagram_basic`، `instagram_content_publish` | صفحه مرتبط و mapping حساب در این مسیر لازم است |

برای Reel در نمونه رسمی، URL عمومی ویدئو → media container → بررسی آماده‌شدن → media_publish است. ایجاد container به معنی انتشار نیست. [مجموعه رسمی Meta و نمونه Reels](https://www.postman.com/meta/instagram/documentation/6yqw8pt/instagram-api?entity=request-23987686-3fe78620-2258-44b6-893f-42d76c7200d7)

صفحات مستقیم developers.facebook.com در ابزار تحقیق باز نشدند؛ شاهد جایگزین، مجموعه خود Meta بود. نیاز دقیق Advanced Access/App Review، مجوز insights، محدودیت روزانه و جزئیات video spec برای نسخه API منتخب و حساب واقعی هنوز Gate باز هستند. از منابع غیررسمی برای قطعی‌کردن آن‌ها استفاده نشده است. قابلیت بررسی‌شده برای API ریلز را به همه موسیقی‌های ترند، stickerها و ابزارهای داخل Instagram تعمیم ندهیم.

نبود scheduler مستقل در این طرح یعنی برنامه desktop باید در زمان انتشار مستقیم روشن و متصل باشد. برای تضمین انتشار با PC خاموش، سرویس خارجی باید رسانه و job را پذیرفته باشد یا worker همیشه‌روشن رسمی طراحی شود؛ دومی به hosting و عملیات اضافه نیاز دارد و پیشنهاد فعلی نیست.

## YouTube مستقیم

آپلود فایل مستقیم از دستگاه با OAuth scope حداقلی `youtube.upload` امکان‌پذیر است؛ برای این upload به URL عمومی فایل نیاز نداریم. زمان‌بندی از `status.publishAt` با وضعیت private و شرایط ویدئوی منتشرنشده استفاده می‌کند. پس از اتمام upload/processing و پذیرش زمان‌بندی، PC لازم نیست روشن بماند. تاریخ گذشته ممکن است انتشار فوری ایجاد کند؛ preview تاریخ/منطقه زمانی لازم است. [videos.insert](https://developers.google.com/youtube/data/reference/rest/v3/videos/insert)، [publishAt](https://developers.google.com/youtube/data/reference/rest/v3/videos)

راهنمای فعلی سهمیه، به‌روزشده ۱۵ اکتبر ۲۰۲۶، ۱۰۰ فراخوانی videos.insert در روز و ۱۰۰ search.list و ۱۰هزار واحد برای سایر endpointها را شرح می‌دهد؛ جدول videos.insert هزینه ۱ واحد از bucket آپلود را نشان می‌دهد. همچنین مرجع فعلی تصریح می‌کند آپلود از پروژه API تأییدنشده دیگر به‌طور کلی محدود به private نیست؛ توصیه‌های قدیمیِ ۱۶۰۰ واحد یا private اجباری مبنای این گزارش نیستند. تنظیم واقعی quota/account پیش از adapter بازخوانی شود. [سهمیه رسمی فعلی](https://developers.google.com/youtube/data/guides/quota_and_compliance_audits)

آمار پایه در video statistics، و گزارش عمیق‌تر با YouTube Analytics و scope `yt-analytics.readonly` قابل بررسی است؛ retention و شاخص‌های دیگر به نوع گزارش/مالکیت وابسته‌اند. [مرجع Analytics](https://developers.google.com/youtube/analytics/reference/). استفاده از آپلود آماده YouTube Studio برای نیاز دو نفره همچنان ساده‌تر از ساخت OAuth client است.

## قرارداد انتشار آینده

۱. یک خروجی immutable با hash، metadata تأییدشده، cover، کپشن، حقوق موسیقی، پلتفرم و timezone انتخاب شود.
۲. تأیید انسانی به همان revision تعلق داشته باشد؛ تغییر فایل/کپشن approval را باطل کند.
۳. submit فقط پس از preflight اتصال، مجوز و schema. external ID و receipt پایدار ثبت شوند.
۴. timeout پس از ارسال = `unknown`؛ ابتدا وضعیت خارجی reconcile، سپس تصمیم retry. نبود idempotency رسمی با key داخلی به‌تنهایی exactly-once نمی‌سازد.
۵. `scheduled` تنها بعد از تأیید سرویس؛ `published` فقط با remote status معتبر. خطاهای token/account/permission قابل اقدام باشند.
۶. زمان UTC همراه timezone اصلی و نمایش Asia/Tehran ثبت شود؛ اختلاف ساعت میزبان منبع حقیقت نباشد.

برای analytics، snapshot با platform، تاریخ دریافت، تعریف metric و window ثبت شود. views، reach، impressions و watch time معادل نیستند. مقایسه چند ASMR با چند ولاگ، دلیل علّی رشد محسوب نمی‌شود. در P0 این تحلیل به ابزار آماده سپرده می‌شود.
