> **سابقه بررسی اولیه، نه وضعیت اجرای فعلی.** نام فعلی محصول Cutora است. برای ادامه و رفع تعارض با Gateهای قدیمی، [START](../../START.md)، [تصمیمات جاری](../decisions/USER_DECISIONS.md) و [گردش‌کار رسانه](../specs/MEDIA_WORKFLOWS.md) مقدم‌اند.

# دفتر ریسک

سطح احتمال، ارزیابی کیفی پیش از آزمایش است؛ آمار واقعی وقوع نداریم. شدت «بحرانی» یعنی امکان از دست‌دادن رسانه یا امنیت حساب؛ «زیاد» یعنی شکست مسیر اصلی؛ «متوسط» یعنی هزینه یا اصلاح قابل توجه.

| ID | ریسک | شدت | احتمال برآوردی | کاهش ریسک / مسئول طراحی | آزمون پیش از توسعه گسترده |
|---|---|---|---|---|---|
| R01 | حذف/overwrite خام | بحرانی | متوسط | importer read-only، بدون delete در P0، مقصد یکتا، journal | قطع/تصادم نام/درخواست AI مخرب |
| R02 | بکاپ ناقص با برچسب موفق | بحرانی | متوسط | Replica state، readback، تشخیص دیسک فیزیکی، restore | هارد غایب و corruption عمدی روی fixture |
| R03 | پرشدن فضای SSD/HDD | زیاد | زیاد روی سیستم فعلی | preflight هر volume، cache محدود، عدم auto-delete اصل | فضای ناکافی قبل/میانه copy و render |
| R04 | قطع یا قفل MTP | زیاد | متوسط تا زیاد | کارت‌خوان مسیر اصلی؛ WPD adapter جدا | Spike اتصال/قطع/وصل و source identity |
| R05 | duplicate اشتباه یا از دست‌دادن chapter | زیاد | متوسط | SHA-256 کل، نام اصلی، mapping chapter غیرتخریبی | نام/سایز یکسان، محتوای متفاوت، chapterهای متوالی |
| R06 | HEVC/5.3K روی Free یا سیستم کم‌توان | زیاد | متوسط | proxy استاندارد، original محفوظ، CPU fallback | فایل واقعی روی Resolve Free و هر دستگاه هدف |
| R07 | NVENC/decoder ناموجود یا driver نامناسب | متوسط | متوسط | capability probe، fallback، خطای واضح | GPU خاموش/driver متفاوت؛ کیفیت و sync |
| R08 | ASR فارسی ضعیف یا متن خیالی در سکوت | زیاد | زیاد در محیط پرنویز | VAD قابل تنظیم، بازبینی متن، نگه‌داری اصل transcript | benchmark چندسبکی با مرجع انسانی |
| R09 | شکست RTL/اعداد/نام‌ها در زیرنویس | زیاد | متوسط | UTF-8، فونت دارای مجوز، rendering واقعی | Resolve و libass روی نمونه فارسی-انگلیسی |
| R10 | hallucination در EditPlan و داستان | زیاد | زیاد | schema، asset allowlist، زمان معتبر، عدم اجرای فرمان از پاسخ | ورودی نامعتبر و قضاوت انسانی داستان |
| R11 | حذف سوژه در crop | زیاد | زیاد با center crop | preview هر شات، pad/manual reframe | دو نفر، ابزار دست، موتور و حرکات سریع |
| R12 | کار سنگین UI را قفل کند | زیاد | متوسط | worker، queue، virtualized grid، proxy | واردکردن هم‌زمان با مرور و کنترل responsiveness |
| R13 | محدودیت API/پلن نشر | زیاد برای feature نشر | زیاد در طول زمان | آماده‌سازی خروجی مستقل؛ استفاده UI سرویس | تست حساب و قالب محتوا در Gate نشر |
| R14 | سرقت token یا credential | بحرانی | متوسط | DPAPI/credential store، renderer بی‌دسترسی، log redaction | revoke، token expiry، XSS/IPC مسیر مخرب |
| R15 | نشر دوباره پس از timeout | زیاد | متوسط | remote ID، reconciliation، حالت unknown؛ بدون retry کور | قطع پس از ارسال و پیش از دریافت پاسخ |
| R16 | قیمت/دسترسی منطقه‌ای API | متوسط | زیاد | cloud خاموش، سقف بودجه، بررسی entitlement واقعی | کنترل مستندات و دسترسی پیش از هر فعال‌سازی |
| R17 | مجوز FFmpeg/فونت/مدل و موسیقی | زیاد در توزیع | متوسط | inventory دقیق build و license، فقط assets مجاز | release review، نه ادعای «متن‌باز پس بدون شرط» |
| R18 | installer و ABI SQLite | زیاد | متوسط | از اولین Spike نصب واقعی، pin و rebuild روی Windows | دستگاه تمیز بدون Node/Python/Build Tools |
| R19 | تغییر نسخه Electron/Resolve | زیاد | متوسط | نسخه تست‌شده، capability matrix، تست regressions محدود | ارتقای آزمایشی قبل از به‌روزرسانی کاربر |
| R20 | scope creep و فرسودگی | زیاد | زیاد | Gate، سقف زمان، هر بار یک vertical slice، no custom NLE | بازنگری هر milestone در برابر زمان صرفه‌جویی |
| R21 | Codex کلیک نادرست در Resolve | زیاد | زیاد بدون API | API/plan نخست، UI کمکی، پروژه کپی، checkpoint | تغییر DPI، پنجره modal، گم‌شدن focus |
| R22 | external scripting در Free در دسترس نباشد | زیاد برای agent | متوسط تا زیاد | داخل برنامه یا handoff دستی؛ خرید Studio تصمیم جدا | Gate R0 روی edition/version نصب‌شده |
| R23 | موشن و زیرنویس API پوشش کامل نداشته باشد | زیاد | زیاد برای کار دلخواه | template allowlist، fallback UI/دستی | Gate قالب Fusion و track زیرنویس فارسی |
| R24 | انتقال پروژه به سیستم دیگر ناقص باشد | زیاد | متوسط | manifest نسبی، relink، fonts/templates/assets همراه | بازکردن پروژه و رندر روی دستگاه دوم |
| R25 | DB سالم ولی رسانه مفقود / بالعکس | زیاد | متوسط | reconcile journal، reconstruct از manifest، صحت مستقل | crash در هر مرز commit/rename و restore catalog |
| R26 | زمان‌بندی محلی با PC خاموش اجرا نشود | زیاد | قطعی اگر فقط محلی باشد | تحویل و تأیید صف خارجی؛ timezone صریح | خاموش‌کردن PC پس از پذیرش سرویس |

مالک همه ریسک‌ها در این مرحله توسعه‌دهنده اصلی است؛ واگذاری فرضی به تیم QA یا DevOps وجود ندارد. امتیاز شدت/احتمال در پایان هر Spike با شاهد به‌روز شود. R01/R02/R18 پیش‌شرط MVP و R21/R22/R23 پیش‌شرط دستیار تدوین هستند.

## محدودیت مشاهده فعلی

ورود و حذف قبلی دوربین در یک نشست موفق شد؛ سناریوهای crash، دستگاه دوم، بکاپ مستقل، HEVC decode و زمان رندر آنجا آزموده نشد. نتیجه آن نشست مجوز عبور از Gateهای این دفتر نیست. هیچ ریسک این جدول صرفاً با نوشتن مستند «بسته‌شده» نیست.
