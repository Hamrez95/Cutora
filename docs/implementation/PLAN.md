# برنامه اجرای نسخه شخصی Cutora

مرجع اختیار: [START](../../START.md) و [تصمیمات جاری](../decisions/USER_DECISIONS.md). قرارداد رسانه: [MEDIA_WORKFLOWS](../specs/MEDIA_WORKFLOWS.md). این برنامه شامل قابلیت‌های جدید مدیریت هارد است؛ تخمین MVP کوچک‌تر در گزارش اولیه، تعهد زمانی این دامنه نیست.

## شیوه اجرا

پس از دستور شروع کاربر روی کیس، از اولین milestone ناتمام ادامه بده. بعد از Gate موفق، به milestone بعدی برو و برای ادامه عادی دوباره مجوز یکسان نخواه. اگر Gate شکست خورد، اول علت را اصلاح یا fallback واقعی/دامنه پشتیبانی را ثبت کن؛ featureهای جذاب تازه را روی زیرساخت نامعتبر اضافه نکن.

UI، هسته و آزمون باید در هر برش وصل باشند. هر قابلیت با داده واقعی یا fixture معنی‌دار کار کند؛ دکمه نمایشی یا progress ساختگی به‌عنوان Done ثبت نشود. مدل AI، API و انتشار عمومی پیش‌نیاز هسته نیستند.

## M0 — شناخت کیس و اثبات مسیر بیلد

کارها: inspect repo/hardware/OS/space/SDK، انتخاب نسخه‌های سازگار، scaffold کوچک، مرزبندی main/preload/renderer/worker، DB native، FFmpeg/FFprobe و installer آزمایشی. baseline زمانی انتقال و preview روی نمونه مجاز. پیدا کردن edition/version Resolve اگر نصب است؛ USB probe در صورت اتصال واقعی.

پذیرش: نصب و اجرای برنامه آزمایشی بدون Node/Python توسعه، query/نوشتن DB در worker و probe/preview یک فایل؛ IPC اعتبارسنجی‌شده. نسخه و license binary ثبت شود. کارت/GPU/Resolve غایب، تست سخت‌افزار مربوط را pending می‌کند، نه اینکه با نتیجه ساختگی پاس شود.

پایان: ADR نسخه‌ها و تصمیم USB/کارت‌خوان، هزینه/زمان اندازه‌گیری‌شده و اصلاح تخمین ادامه. timebox اولیه یک Spike محدود است، نه مجوز توقف همیشگی پس از موفقیت.

## M1 — ورود امن و شناسه رسانه

UI source انتخاب‌شده، scan report، preflight فضا، import queue، temporary، hash readback، journal و DB reconciliation. discovery همراه‌ها/انواع ناشناخته و dedupe کامل. default read-only و job cancellation.

پذیرش: MW-01، MW-02، MW-03، MW-13، MW-14، MW-18؛ log و manifest با fixture. فایل‌های دارای collision حفظ شوند. MW-20 در job plan پایه پوشش داده شود.

## M2 — replica، بکاپ و restore

نقش storage، هویت دیسک، availability جدا از integrity، pending/verified/error، copy/verify مستقل، catalog backup سازگار و restore به مسیر تازه. dual partition یک backup مستقل نیست.

پذیرش: MW-04، MW-05، MW-10 و رفتار source غایب. حداقل یک restore واقعی از فایل و metadata به مسیر جدید؛ صرف وجود backup record کافی نیست.

## M3 — کتابخانه و دسته‌بندی کاربردی

ورود/گروه تاریخ، رویداد و topic مجازی، اصلاح/merge/split/undo، منتخب، فیلتر ترکیبی، thumbnail، preview/proxy لازم، grid مجازی و feedback واقعی. افزودن آرشیو قدیمی به صورت index-only یا copy-managed؛ منبع قدیمی بی‌اجازه دست‌کاری نشود.

پذیرش: MW-06، MW-09، MW-12، MW-15، MW-19. metadata/thumbnail در حالت offline قابل مرور؛ date تخمینی و topic پیشنهادی صریح باشند. رابط فارسی با DPI و keyboard مناسب.

## M4 — هارد ↔ SSD و قابل حمل بودن Library

سه جریان واقعی UI: «برای تدوین آماده کن»، «روی هارد آرشیو کن»، «بازیابی کن». transfer preview، فضای peak، replica reuse، archive package، library relocation، relink و عدم cleanup خودکار. drive-letter change و rerun idempotence.

پذیرش: MW-07، MW-08، MW-11، MW-20 و ادامه MW-09/15. خروجی مورد انتظار، فایل‌های سالم در مقصد و references قابل بازیابی است؛ انیمیشن انتقال کافی نیست. تا replica کافی و اجازه روشن، old original حفظ شود.

این milestone بخشی از هسته نسخه شخصی است و نباید به‌عنوان «بهبود آینده» حذف شود؛ درخواست تازه کاربر همین گردش‌کار را برجسته کرده است.

## M5 — handoff و خروجی واقعی با DaVinci

مجموعه منتخب، مسیرهای ثابت، online original/working copy، selection manifest و بازکردن/تحویل به Resolve. اگر API هنوز موجود نیست، import دستی روشن و قابل استفاده داشته باشد. نمونه پنج‌کلیپی به draft حدود ۳۰ ثانیه و خروجی نسبت‌های مختلف با کادر بازبینی‌شده برسد.

پذیرش: MW-16 و خروجی قابل پخش واقعی، اصل ثابت، صوت sync و preview crop صحیح. پس از جابه‌جایی آرشیو، mapping/relink آزمایش شود. هیچ XML/EDL تا آزمون round-trip «سازگار» نامیده نشود.

## M6 — آپشن دستیار Resolve، در دامنه قابل اثبات

مرجع: [RESOLVE_ASSISTANT](../planning/RESOLVE_ASSISTANT.md). capability probe، README رسمی محلی، نسخه/edition، plan ساخت‌یافته و adapter allowlist. ترتیب: اتصال read-only، پروژه کپی، montage قطعی، سپس قالب عنوان و SRT فارسی در صورت پوشش واقعی. اجرای control با UI فقط با ابزار فعال و محدودیت مشخص؛ نه ادعای دسترسی عمومی از CLI.

پذیرش: R0/R1 و برای قابلیت‌های موجود R2/R3. Core می‌تواند با handoff دستی آماده شود، ولی `Resolve Assistant Ready` فقط با شواهد مختص خودش. اگر خرید Studio/کلید پولی لازم است، خرید نکن؛ حالت unavailable/partial و راه جایگزین را تحویل بده. قابلیت غیرفعال نباید مانع کار با Library شود.

فراتر از توان رایگان/محلی موجود، اسکوپ را پنهانی گسترش نده. «موشن دلخواه و تدوین کامل هر پروژه» هدف تست‌نشده و خارج وعده نسخه اول است.

## M7 — مقاوم‌سازی، نصب و تحویل

Regression معیارهای MW، crash/recovery و تست‌های release در VALIDATION_PLAN؛ test binary packaged، DPI/RTL/کاهش حرکت، کمبود فضا و CPU fallback. بررسی license/notices، خروجی build، راهنمای نصب/backup/restore/انتقال بین کیس و لپ‌تاپ و uninstall بدون حذف رسانه.

پذیرش: installer واقعی، نسخه دقیق تست‌شده و شواهد media workflow. اگر دستگاه دوم در دسترس نیست، آن تست Not Run باقی بماند و ادعای «روی هر سیستم تست شده» نشود. وضعیت `Core Release Ready` فقط به دامنه Windows/سخت‌افزار آزموده‌شده تعلق دارد.

## شواهد و ادامه

در هر milestone: tests passed/failed/not-run، نسخه‌ها، پذیرش‌های MW، commit، زمان فعال، blocker واقعی و اقدام بعدی در STATUS ثبت شود. گزارش واقعی حاوی private path یا نام فایل شخصی، خارج Git نگه‌داری و در گزارش عمومی خلاصه شود.

بعد از تحویل هسته، فقط به خاطر وجود P1/P2 در سند قدیمی کار بی‌پایان روی social/LLM شروع نکن. آمادگی نسخه شخصی با تکمیل تمام ایده‌های محصول متفاوت است؛ گزارش صریح هسته و گزینه Resolve و backlog باقی‌مانده پایان معتبر است.
