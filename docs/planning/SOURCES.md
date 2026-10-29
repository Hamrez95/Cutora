> **سابقه بررسی اولیه، نه وضعیت اجرای فعلی.** نام فعلی محصول Cutora است. برای ادامه و رفع تعارض با Gateهای قدیمی، [START](../../START.md)، [تصمیمات جاری](../decisions/USER_DECISIONS.md) و [گردش‌کار رسانه](../specs/MEDIA_WORKFLOWS.md) مقدم‌اند.

# دفتر منابع و شواهد

تاریخ بسته: ۲۸ اکتبر ۲۰۲۶، Asia/Tehran. تحقیق این نشست از ۲۷ تا ۲۸ اکتبر انجام شد. قیمت و API snapshot هستند و پیش از فعال‌سازی باید دوباره بررسی شوند. لینک منبع کنار ادعای اصلی هر سند هم قرار دارد؛ این فایل جای ارجاع محلی را نمی‌گیرد.

## منابع داخلی و وضعیت Workspace

در بسته تحویل ریپو، [نسخه آفلاین شش صفحه Notion](../reference/notion/README.md) نیز ذخیره شده است. برای نیاز فعلی و دستور شروع، تصمیمات جاری و START مقدم‌اند؛ صفحات مرجع اولیه بازنویسی نشده‌اند.

| منبع | وضعیت دسترسی و استفاده |
|---|---|
| [متن مأموریت اولیه](../reference/ORIGINAL_BRIEF.md) | کامل خوانده شد؛ Gate آن تاریخی است و اختیار فعلی در تصمیمات جدید آمده |
| [HomeVlog: صفحه اصلی](https://app.notion.com/p/4019ef2b1617819e8e32df9f92a751af) | با Notion MCP خوانده شد؛ پنج زیرصفحه لینک شده؛ آخرین ویرایش گزارش‌شده ۲۲ اکتبر |
| [01 نیازمندی و UX](https://app.notion.com/p/4019ef2b16178172a57bf49ef56dfc35) | کامل در خروجی fetch؛ جریان، صفحات و پذیرش اولیه |
| [02 معماری، فایل و AI](https://app.notion.com/p/4019ef2b1617813089e0ebb5a997abbd) | پیشنهاد PySide6، قرارداد ایمنی، مدل داده و integrationها |
| [03 نقشه راه و QA](https://app.notion.com/p/4019ef2b161781ffb260d66189686ba5) | فازها و ریسک‌ها؛ توکن‌های اولیه صریحاً غیرمستند |
| [04 چرخه محتوا و انتشار](https://app.notion.com/p/4019ef2b1617811888bec81fad415479) | Ready Library، سبک‌های محتوا، تأیید انسانی |
| [05 بازبینی و تصمیمات باز](https://app.notion.com/p/4019ef2b1617819c94f1d891113eaeae) | مسئله‌های باز، تفکیک ایده از عملکرد |
| پیام‌های تازه کاربر | اولویت UI زیبا/موشن/نصب؛ تدوین در DaVinci؛ بررسی آپشن Codex control |
| گزارش محلی manifest و inventory انتقال قبلی | در سیستم مبدأ بررسی شد؛ ۵۷ فایل و ۹٬۵۶۰٬۳۱۳٬۳۶۶ بایت؛ نه اثبات بکاپ دوم. خود inventory واقعی رسانه برای حفظ حریم خصوصی در این ریپو قرار نگرفته است |
| بررسی shell این نشست | مسیر، Git، فایل‌های markdown/config موجود، AGENTS در پروژه/والدها، OS و فضای آزاد بررسی شد؛ کد محصول پیدا نشد |

خروجی‌های fetch، محتوای صفحه‌ها را بدون علامت truncation/unknown block در پاسخ دریافتی نمایش دادند. در پنج صفحه فرزند، child-page دیگری دیده نشد. ادعای دسترسی به صفحه پنهان، attachment یا discussion بازیابی‌نشده نداریم. منبع مرجع برای تعارض زمانی: درخواست تازه کاربر بر طرح ۲۲ اکتبر مقدم است.

## ابزارهای تدوین و کتابخانه

| منبع رسمی/اولیه | چه چیزی را پشتیبانی می‌کند؟ | حد اطمینان |
|---|---|---|
| [DaVinci Resolve](https://www.blackmagicdesign.com/products/davinciresolve) | محصول، نسخه Free/Studio و حوزه تدوین | صفحه باز شد؛ کارکرد روی PC ما آزمون نشد |
| [توقف Quik دسکتاپ](https://gopro.com/en/bt/news/gopro-sunsetting-quik-desktop-app) | توقف مسیر desktop و عدم عرضه Windows وعده‌داده‌شده | اعلام رسمی ۷ نوامبر ۲۰۲۴؛ سرویس فعلی نصب نشد |
| [راهنمای HERO10](https://gopro.com/content/dam/help/hero10-black/manuals/HERO10Black_UM_ENG_REVB.pdf) | انتقال با کارت‌خوان | منبع رسمی؛ firmware فعلی کاربر ارزیابی نشد |
| [LRV/THM](https://community.gopro.com/s/article/What-are-thm-and-lrv-files?language=en_US) | ماهیت فایل‌های کمکی | توضیح رسمی GoPro |
| [CapCut Auto Caption](https://www.capcut.com/help/how-to-recognise-subtitles) | وجود workflow و وابستگی به نسخه/منطقه | فارسی و قیمت در حساب کاربر قطعی نشده |
| [Shotcut Download](https://www.shotcut.org/download/) | ابزار آزاد و دریافت رسمی Windows | نصب/مقایسه عملی انجام نشد |
| [Insta360 import](https://onlinemanual.insta360.com/studio/en-us/operation-guide/file-management/creative-import) | فرمت‌های قابل ورود و workflow | پشتیبانی ویژه GoPro از پذیرش MP4 نتیجه نشده |
| [digiKam video](https://docs.digikam.org/fr/supported_materials/movie_formats.html) | metadata، thumbnail، preview و نبود تدوینگر فیلم | راهنمای رسمی بازیابی‌شده به زبان فرانسه با متن انگلیسی مرتبط |
| [LosslessCut](https://github.com/mifi/lossless-cut) و [محدودیت‌ها](https://github.com/mifi/lossless-cut/blob/master/docs/troubleshooting.md) | ابزار آماده و محدودیت keyframe | مخزن خود سازنده؛ آزمون روی GoPro فعلی نشده |
| [Subtitle Edit ASR](https://github.com/SubtitleEdit/subtitleedit/blob/main/docs/features/speech-to-text.md) | موتورهای آماده و workflow تبدیل گفتار | مخزن اصلی؛ سرعت فارسی ادعا نشده |

## معماری، رسانه و AI

| منبع | شواهد استفاده‌شده / محدودیت |
|---|---|
| [Electron process model](https://www.electronjs.org/docs/latest/tutorial/process-model) | Chromium/Node و جداسازی main/renderer/utility |
| [Electron security](https://www.electronjs.org/docs/latest/tutorial/security) | IPC، isolation، sandbox و پرهیز از remote code |
| [Electron native modules](https://www.electronjs.org/docs/latest/tutorial/using-native-node-modules) | ABI و rebuild؛ پایداری بسته ما هنوز آزموده نشده |
| [better-sqlite3](https://github.com/WiseLibs/better-sqlite3) | SQLite binding و مجوز مخزن؛ نسخه نهایی pin نشده |
| [electron-builder Windows](https://www.electron.build/win/) | مقصد ابزار packaging بررسی شد ولی متن صفحه در ابزار بازیابی نشد؛ جزئیات installer این گزارش **طرح پیشنهادی** است، نه build تأییدشده |
| [Tauri prerequisite](https://v2.tauri.app/start/prerequisites/) و [sidecar](https://v2.tauri.app/develop/sidecar/) | WebView2، ابزار build و بسته‌بندی binary خارجی |
| [Qt Multimedia](https://doc.qt.io/qt-6/qtmultimedia-index.html) | قابلیت پخش و backend/تفاوت platform؛ جایگزین ردشده |
| [Flutter video_player](https://docs.flutter.dev/cookbook/plugins/play-video) | محدودیت پشتیبانی رسمی Windows؛ همه pluginهای جامعه بررسی نشده‌اند |
| [WPD operations](https://learn.microsoft.com/en-us/windows/win32/wpd_sdk/operating-on-device-content) | عملیات محتوا/انتقال در Windows؛ سازگاری HERO10 نیازمند Spike |
| [FFmpeg legal](https://www.ffmpeg.org/legal.html) | نتیجه جست‌وجوی رسمی درباره LGPL/GPL؛ fetch مستقیم timeout داد؛ audit build هنوز انجام نشده |
| [فیلتر subtitles](https://ffmpeg.org/doxygen/trunk/vf__subtitles_8c_source.html) | استفاده libass در implementation رسمی |
| [whisper.cpp](https://github.com/ggml-org/whisper.cpp/blob/master/README.md) | backendهای CPU/CUDA/Vulkan و اجرای محلی |
| [faster-whisper](https://github.com/SYSTRAN/faster-whisper) | benchmark با سخت‌افزار/مدل اعلام‌شده و وابستگی‌های GPU؛ نه benchmark فارسی RTX 4060 |
| [OpenAI pricing](https://developers.openai.com/api/docs/pricing) | قیمت STT همان روز؛ صفحه رسمی باز شد؛ قابلیت timestamp هر مدل نیازمند بررسی انتخاب نهایی |
| [Gemini video](https://ai.google.dev/gemini-api/docs/video-understanding) و [pricing](https://ai.google.dev/gemini-api/docs/pricing) | دریافت ویدئو و محاسبه هزینه نمونه؛ اجرای حساب/region انجام نشده |
| [OpenAI supported countries](https://developers.openai.com/api/docs/supported-countries) و [Gemini available regions](https://ai.google.dev/gemini-api/docs/available-regions) | فهرست رسمی بررسی شد و ایران در آن نبود؛ درباره کشور واقعی کاربر از timezone نتیجه‌گیری نشده |
| [OTIO adapters](https://github.com/AcademySoftwareFoundation/OpenTimelineIO/blob/main/docs/tutorials/adapters.md) و [FCP7 adapter](https://github.com/OpenTimelineIO/otio-fcp-adapter) | adapterها و محدودیت قابلیت؛ سازگاری واقعی Resolve آزمایش نشده |

## انتشار

| منبع | نتیجه قابل اتکا |
|---|---|
| [Buffer pricing](https://buffer.com/pricing) | سهمیه و پلن‌ها در تاریخ بررسی |
| [Buffer feature table](https://support.buffer.com/article/595-features-available-on-each-buffer-plan) | هزینه ماهانه/سالانه و تعداد کاربران/API |
| [Buffer queue limits](https://support.buffer.com/en-us/articles/how-many-posts-can-i-schedule-in-advance-Kmy2IEecqm) | صف هم‌زمان، نه سقف ماهانه |
| [Buffer authentication](https://developers.buffer.com/guides/authentication.html) | API key و OAuth PKCE، دامنه key |
| [Buffer video example](https://developers.buffer.com/examples/create-video-post.html) | ساخت video post/queue از URL |
| [Buffer hosting](https://developers.buffer.com/guides/hosting-media.html) | نبود upload endpoint در API و الزام URL عمومی پایدار |
| [Buffer API reference](https://developers.buffer.com/reference.html) | schema فعلی؛ همه analytics/featureها برای حساب کاربر اثبات نشده |
| [Metricool plans/API](https://help.metricool.com/plans-add-ons-and-api-access-explained-xux1u) | تفاوت API پلن بالاتر با MCP همه پلن‌ها |
| [Metricool Free details](https://help.metricool.com/main-differences-between-free-and-paid-plans-bl0v9) | ۲۰ پست/ماه و شمارش هر شبکه؛ اختلاف واژه schedule/publish در صفحات دیگر ثبت شد |
| [Meta Instagram collection](https://www.postman.com/meta/instagram/documentation/6yqw8pt/instagram-api?entity=request-23987686-3fe78620-2258-44b6-893f-42d76c7200d7) | نتیجه جست‌وجوی مجموعه رسمی Meta شامل permissions و مثال Reel؛ fetch نمای کلی Postman متن پویا را کامل نشان نداد |
| صفحات مستقیم Meta developers | برای login/content-publishing/insights در این ابزار در دسترس نبودند؛ جزئیات review/insights/version باز ماندند |
| [YouTube insert](https://developers.google.com/youtube/data/reference/rest/v3/videos/insert) | upload و OAuth و سهمیه فعلی |
| [YouTube video status](https://developers.google.com/youtube/data/reference/rest/v3/videos) | publishAt و privacy؛ رفتار unverified فعلی |
| [YouTube quota](https://developers.google.com/youtube/data/guides/quota_and_compliance_audits) | متن به‌روزشده ۱۵ اکتبر ۲۰۲۶؛ تفاوت با راهنماهای قدیمی |
| [YouTube Analytics](https://developers.google.com/youtube/analytics/reference/) | OAuth و دامنه گزارش‌ها، نه وعده همه metrics برای همه حساب‌ها |

## کنترل Resolve

| منبع | نتیجه / حد تعمیم |
|---|---|
| [پاسخ مدیر محصول Blackmagic](https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=205175) | محدودیت Free و external scripting در بحث ۲۰۲۴؛ شاهد تاریخی مستقیم |
| [تأیید Studio](https://forum.blackmagicdesign.com/viewtopic.php?f=21&t=204977) | تأیید تاریخی از تیم Blackmagic؛ الزام آزمون نسخه فعلی حفظ شد |
| [Resolve 21 New Features](https://documents.blackmagicdesign.com/SupportNotes/DaVinci_Resolve_21_New_Features_Guide.pdf) | قابلیت‌های UI متن/موشن/word timing؛ وجود API و کیفیت فارسی از آن نتیجه نشده |
| مسیرهای معمول نصب روی سیستم فعلی | نصب/پردازش Resolve پیدا نشد؛ نصب در جای دیگر رد نشده؛ API محلی خوانده نشد |
| مهارت Computer Use محیط | دستورالعمل موجود خوانده شد؛ فعال‌سازی runtime و کنترل UI انجام نشد |

## چه چیزی منبع بیرونی نیست؟

امتیازهای انتخاب فناوری، برآورد ساعت، reserve ریسک، اهداف UX/کیفیت، ترتیب roadmap و توصیه build/hybrid، قضاوت مهندسی این بررسی‌اند. آن‌ها را به شرکت سازنده، benchmark یا مقاله نسبت ندهیم. هزینه‌های نمونه، محاسبه از نرخ رسمی با فرض صریح‌اند و quote تجاری نیستند.
