# 🛠️ 02 | معماری فنی، فایل‌ها و هوش مصنوعی

> نسخه مرجع طرح اولیه، برای مطالعه آفلاین. دستور اجرایی جاری در [START.md](../../../START.md) و [تصمیمات جاری](../../decisions/USER_DECISIONS.md) است. STOP و پیشنهادهای این صفحه سابقه‌اند و اختیار توسعه فعلی را تغییر نمی‌دهند.

منبع: [صفحه اصلی Notion](https://app.notion.com/p/4019ef2b1617813089e0ebb5a997abbd?pvs=204). انتقال به ریپو: ۲۹ اکتبر ۲۰۲۶. آخرین ویرایش گزارش‌شده منبع: 2026-10-22T14:26:01.679Z.

## پیشنهاد اولیه معماری، نه تصمیم قطعی

- UI: Python + PySide6/Qt برای نسخه Windows و سرعت رسیدن به برنامه نصب‌شونده. Sol باید در مقایسه با Flutter Desktop و Tauri + React نیز تصمیم بدهد.
- هسته: Python services + SQLite برای پروژه‌ها، ایندکس رسانه و صف کارهای پایدار.
- Video: FFprobe/FFmpeg برای بررسی رسانه، thumbnail، crop، transcoding، proxy و رندر؛ GPU RTX 4060 با NVENC در صورت سازگاری، CPU fallback.
- Preview: پخش بهینه فایل‌های GoPro (اغلب HEVC/4K/5.3K)، proxy در صورت نیاز و waveform.
- Offline STT: whisper.cpp یا faster-whisper بعد از benchmark فارسی؛ transcript segment با زمان دقیق، correction editor و SRT/burn-in.
- Scene Detection: PySceneDetect و keyframe extraction فقط در صورت بهبود واقعی سرعت کار.
- AI Adapter: اختیاری، قابل تعویض بین سرویس‌ها و قابل خاموش‌کردن؛ OpenAI API برای روایت، کپشن و Edit Decision List؛ Gemini video understanding به عنوان جایگزین قابل تحقیق. **قیمت/قابلیت دقیق مدل‌ها هنوز تأیید نشده‌اند.**
- Publishing Adapter: Buffer/Meta/YouTube فقط پس از بررسی مستندات واقعی و مجوز OAuth.

## مسیر دقیق وارد کردن فایل (Data Safety)

1. شناسایی اتصال USB/MTP یا کارت SD. ممکن است GoPro USB به صورت فایل‌سیستم معمولی ظاهر نشود؛ کارت‌خوان SD fallback جدی است.
2. enumerate فایل‌ها، خواندن metadata، تشخیص تکراری بر اساس شناسه/سایز/هش و فهرست manifest.
3. بررسی فضای آزاد؛ کپی به فایل موقت روی SSD، flush و راستی‌آزمایی checksum، rename امن و ثبت transaction.
4. بکاپ مستقل روی هارد اکسترنال (اگر متصل بود) همراه با verification؛ اگر نبود وضعیت backup\_pending و امکان sync بعدی.
5. indexing پس‌زمینه: thumbnail، proxy، waveform، تاریخ، برچسب ابتدایی، transcription در صف کم‌اولویت.
6. هر مرحله resumable، idempotent و دارای log؛ **هیچ پاک‌کردن خودکار فایل اصلی روی دوربین یا SSD** انجام نشود.
نکته: دو کپی روی یک دیسک بکاپ مستقل محسوب نمی‌شود. هارد اکسترنال ۱TB نیمه‌پر ممکن است برای آرشیو طولانی کافی نباشد؛ monitor فضای آزاد ضروری است.

## مدل داده پیشنهادی

- Asset: id، source device/path، file fingerprint/hash، captured\_at، codec/dimensions/duration، archive path، proxy path، tags، integrity state.
- ImportSession: دستگاه، manifest، progress، dedupe، failures، resume.
- BackupRecord: asset، destination، checksum/verified\_at، pending/complete/error.
- Event/Collection: عنوان رویداد، بازه زمانی، موضوع/اتاق/نوع، asset references، manual overrides.
- TranscriptSegment: asset id، start/end، text، model version، manually corrected.
- EditProject: source assets، timeline/clip in-out، crop per platform، subtitle track، نسخه ویرایش.
- RenderJob: preset، output path، status، error، start/finish.
- PostDraft/PublishJob: output، caption، channel، approval state، schedule، remote ID، error/retry.
- InsightSnapshot: post ID، metrics available، read timestamp، origin API.

## AI تدوین سریع — چهارچوب واقعی

- داده‌هایی که محلی استخراج می‌شوند: metadata + transcript + keyframes منتخب + scene boundaries.
- AI اختیاری: پیشنهاد ۲ یا ۳ نسخه Edit Plan JSON با انتخاب Asset ID و timestamps؛ storyboard و دلیل انتخاب هر صحنه.
- validation برنامه: timecodeها داخل duration، عدم ارجاع به فایل ناموجود، رعایت زمان نهایی و خروجی‌ها.
- کاربر preview و تأیید کند؛ FFmpeg رندر را انجام می‌دهد. انتخاب سکانس خوب تضمین نمی‌شود و با نمونه‌های واقعی آزمایش لازم است.
- حالت ASMR: حذف مکث/نویزگیری تهاجمی پیش‌فرض خاموش؛ حفظ صداهای اصلی هدف است.

## نصب ویندوزی و نگهداری

- build پیشنهادی PyInstaller و نصب‌کننده Inno Setup برای Setup.exe، شورتکات، uninstaller، migration دیتابیس و log؛ در حال حاضر **فایل اجرایی ساخته نشده**.
- اندازه نصب مدل‌ها و FFmpeg، به‌روزرسانی، خطاهای HEVC، تغییر حرف درایو، قطع USB، cache و آزادسازی فضا را باید در Spike تست کرد.
- اسرار در Windows Credential Manager/DPAPI؛ config متنی یا repo محل API token نیست. اینترنت و ارسال ویدئو/متن برای AI باید opt-in باشد.
- بررسی license کتابخانه‌ها، FFmpeg/codec، مدل ASR و حقوق نشر الزامی است.

## انتخاب ابزارهای موجود

CapCut Desktop یا DaVinci برای تدوین حرفه‌ای حفظ شوند. انتقال edit plan به نرم‌افزار تدوین از طریق EDL/XML فقط در صورت اثبات سازگاری؛ پیش‌فرض MVP خروجی MP4 سالم است.

## مهم‌ترین ریسک‌های فنی

اتصال MTP GoPro، codec و seek سنگین، زیرنویس فارسی راست‌به‌چپ، خرابی ناقص فایل و بکاپ، crop اشتباه، مصرف فضای SSD، crash jobs و انتشار تکراری در retry.
