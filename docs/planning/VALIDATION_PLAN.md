> **سابقه بررسی اولیه، نه وضعیت اجرای فعلی.** نام فعلی محصول Cutora است. برای ادامه و رفع تعارض با Gateهای قدیمی، [START](../../START.md)، [تصمیمات جاری](../decisions/USER_DECISIONS.md) و [گردش‌کار رسانه](../specs/MEDIA_WORKFLOWS.md) مقدم‌اند.

# برنامه اعتبارسنجی و آزمون

وضعیت: همه آزمون‌های محصول **برنامه‌ریزی‌شده و اجرا‌نشده** هستند. بررسی حاضر فقط خواندن منابع، محیط و سازگاری مستندات بوده است. انتقال قبلی شاهد موردی کپی است، نه اجرای suite محصول.

## مجموعه داده و ابزار سنجش

با اجازه بعدی، از کپی fixture استفاده شود؛ source اصلی read-only بماند. مجموعه پایه ۲۰ فایل شامل MP4 H.264/HEVC، چند chapter، بدون audio، عکس، فایل خراب عمدی، نام یکسان/محتوای متفاوت، نام فارسی/انگلیسی و فایل بیش از ۴GiB. برای عملکرد، حداقل ۳۰–۶۰ دقیقه خام واقعی با bitrateهای ثبت‌شده و manifest مرجع لازم است؛ نمونه فعلی ۱۸ MP4 الزاماً همه این حالات را پوشش نمی‌دهد.

دو محیط: PC هدف RTX 4060/32GB و دستگاه کم‌توان واقعی. ثبت version ویندوز/driver/Electron/FFmpeg/Resolve، profile و وضعیت برق/دیسک. VM برای installer مفید است ولی نتیجه GPU/پخش VM جای دستگاه واقعی نیست.

## Gateهای مستقل

| Gate | سناریو | انتظار قابل بررسی | شاهد ذخیره‌شده |
|---|---|---|---|
| G0 ارزش | سه جلسه با workflow آماده | baseline زمان انسان، مشکلات پرتکرار و اولویت واقعی | فرم زمان‌سنجی و تصمیم build/stop |
| G1 نصب/رسانه | EXE روی سیستم بدون Node/Python | برنامه باز، SQLite قابل نوشتن، FFprobe و proxy قابل اجرا | log نسخه‌ها، نصب/حذف/نصب مجدد |
| G2 ایمنی ورود | قطع کابل/kill process در read، verify، rename و DB commit | source ثابت، partial سالم معرفی نشود، resume نشست بدون duplicate | manifest پیش/پس، hash و recovery report |
| G3 dedupe | سه بار ورود، نام/سایز یکسان با hash متفاوت | فایل تازه حفظ، یک محتوای تکراری با occurrenceهای متعدد | شمار Asset/Occurrence و مسیرها |
| G4 بکاپ | هارد غایب، پر، read-only، corruption | وضعیت دقیق، retry محدود و restore مستقل | checksum مقصد/restore و زمان |
| G5 مرور | چندصد/هزار metadata + رسانه نماینده | grid پاسخ‌گو، preview بدون UI freeze | latency، RAM و queue trace |
| G6 مسیر تدوین | پنج کلیپ منتخب → Resolve → سه خروجی | ۳۰ثانیه تقریبی، بدون کشیدگی، کادر مناسب و صوت sync | پروژه و MP4 QC شده |
| G7 نصب دستگاه دوم | انتقال library و project package | relink مشخص، فایل‌ها online؛ secrets نیازمند ورود مجدد | گزارش restore/relink و export دوم |
| A0 زیرنویس | مجموعه فارسی چندسبکی | سرعت/کیفیت/timestamp و اصلاح انسانی سنجیده | جدول موتور/مدل و transcript مرجع |
| A1 RTL | فارسی/انگلیسی/عدد/نیم‌فاصله در SRT و burn-in | ترتیب درست و glyph کامل در فایل نهایی | تصویر نمونه از خروجی واقعی |
| R0–R3 Resolve agent | طبق RESOLVE_ASSISTANT | قابلیت edition، عملیات قطعی و صرفه‌جویی واقعی | capability matrix، plan و diff پروژه |
| S0 نشر آینده | submit موفق، timeout، revoke، PC خاموش | unknown و reconciliation؛ بدون duplicate یا ادعای غلط | remote ID و گزارش سرویس |

## آزمون فنی جزئی

- state machine job و invariantهای فایل/DB: هیچ `verified` بدون hash، هیچ `backed_up` بدون replica معتبر، هیچ تغییر خام در عملیات مشتق.
- قطع پس از rename پیش از commit و برعکس، startup reconciliation و retry idempotent.
- volume جدید با همان drive letter، دو partition از یک دیسک، مسیر long/فارسی، symlink و archive زیر source؛ جلوگیری از recursion و پاکسازی خارج cache.
- فضای ناکافی حین عملیات؛ app هم‌زمان دو instance؛ cancellation در مرحله حساس و باقی‌نماندن lock.
- DB migration شکست‌خورده با rollback، backup/restore WAL و بازسازی catalog از manifest.
- IPC با asset ID نامعتبر، path traversal، metadata/script مخرب و response مدل حاوی فرمان؛ همه باید داده بی‌اثر بمانند.
- رندر: CFR/VFR و نرخ‌های کسری، rotation، audio 44.1/48kHz، clip بدون audio، A/V sync، خطای encoder و خروجی نیمه‌کاره. فایل موفق صرفاً با exit code اثبات نشود؛ probe و decode/QC لازم است.

## عملکرد و UX

هدف‌های پیشنهادی برای سنجش، نه نتایج: بازخورد کلیک فوری، عدم block رابط در hash/render، نمایش progress بر اساس بایت/مرحله، preview به کمک proxy. برای زمان import یا render، ابتدا baseline روی سخت‌افزار واقعی بگیریم؛ «زیر یک دقیقه» بدون طول/codec منبع هدف معتبر نیست.

تست دستی با هر دو نفر: واردکردن بدون توضیح توسعه‌دهنده، فهم تفاوت pending و verified، پیدا کردن سه شات، تحویل به Resolve و ثبت خروجی. خطا باید راه اصلاح داشته باشد. empty state، loading قابل لغو، مشکل دوربین، هارد غایب و source offline هرکدام متن مشخص و یک اقدام بعدی داشته باشند.

موشن در حالت عادی و reduced motion، DPI ۱۰۰/۱۵۰/۲۰۰٪، فونت فارسی، focus keyboard و پنجره کم‌ارتفاع بررسی شود. انیمیشن نباید ترتیب داده را عوض کند یا وضعیت موفقیت کاذب بسازد.

## آزمون تبادل DaVinci

قبل از اعلام XML/EDL: پنج کلیپ با نرخ‌های ۲۵ و ۲۹٫۹۷ و ۵۹٫۹۴، start timecode غیرصفر، trim غیر-keyframe، یک rotation، audio و نام فارسی. import در نسخه/edition دقیق Resolve و مقایسه تعداد، ترتیب، frame in/out و relink. font، subtitle، Fusion، speed ramp و افکت‌ها جدا آزمون شوند؛ موفقیت basic cuts اثبات حفظ افکت نیست. فایل `.otio` یا XML را صرف وجود adapter «سازگار با داوینچی» معرفی نکنیم.

برای UI control، تغییر focus، modal، DPI و قطع session آزمون شود. agent باید از موقعیت نامعلوم متوقف شود. پروژه اصلی و فایل خام با checksum/نسخه پیش از کار کنترل شوند. هیچ نمونه‌ای با timeline تولیدشده ولی بررسی‌نشده Done نیست.

## Done و گزارش انتشار

هر milestone: scope دقیق، نسخه build، نمونه‌ها، فرمان/روش آزمون، نتایج واقعی، شکست‌ها، زمان و مصرف، قابلیت‌های خارج دامنه و راه rollback. اثبات نصب EXE، restore و یک فایل نهایی واقعی لازم است. تستی که اجرا نشده، skipped/pending ثبت شود؛ به‌عنوان pass گزارش نشود.

این مرحله فقط اسناد Markdown را ایجاد و ارجاع‌های داخلی/پوشش آن‌ها را بررسی می‌کند؛ اجرای benchmark، نصب dependency، ساخت EXE و Tech Spike به تأیید بعدی نیاز دارد.
