> متن اولیه درخواست تحلیل، برای سابقه. دستور شروع فعلی در [START.md](../../START.md) و [تصمیمات جاری](../decisions/USER_DECISIONS.md) ثبت شده و محدودیت توقف تاریخی را در نشست شروع توسعه تعیین تکلیف می‌کند.

# HOMEVLOG STUDIO
# Critical Product Review, Architecture Assessment & Implementation Planning

تو مسئول بررسی فنی، محصولی و اقتصادی پروژه HomeVlog Studio هستی.

در این مأموریت همزمان نقش‌های زیر را بر عهده بگیر:

- Principal Product Manager
- Principal Software Architect
- Staff Windows Desktop Engineer
- Senior Media Processing Engineer
- AI/ML Systems Architect
- UI/UX Product Design Lead
- QA & Release Engineer
- Technical Cost Optimization Consultant

هدف این است که قبل از شروع توسعه، مطمئن شویم بهترین،
ساده‌ترین، کم‌هزینه‌ترین و سریع‌ترین مسیر را انتخاب کرده‌ایم.

مهم:
وظیفه تو تأیید ایده‌های موجود نیست.
باید آنها را منتقدانه بررسی کنی و در صورت وجود
راهکار بهتر، معماری یا حتی مفهوم محصول را تغییر بدهی.


==================================================
1. PROJECT CONTEXT
==================================================

نام موقت محصول:

HomeVlog Studio

این محصول فعلاً برای استفاده شخصی یک زوج طراحی می‌شود.

حمیدرضا و ریحانه تولید محتوای ویدیویی انجام می‌دهند.

موضوعات محتوایی:

- بازسازی خانه
- ولاگ کاپلی
- موتورسواری
- ASMR
- زندگی روزمره
- آشپزی
- تولید محتوای اینستاگرام
- YouTube Shorts
- ویدیوهای بلند YouTube

تجهیزات:

Camera:
GoPro HERO10 / HERO11 Black

PC:
Intel Core i5 14th Gen
NVIDIA RTX 4060
32GB DDR5 RAM

Storage:
1TB Samsung SSD
1TB MSI SSD
1TB External HDD

Operating System:
Windows

کاربر اصلی توسعه‌دهنده نرم‌افزار است و از Codex CLI
برای توسعه پروژه استفاده می‌کند.

محدودیت‌های اصلی:

1. زمان توسعه محدود است.
2. مصرف توکن Codex باید بهینه باشد.
3. هزینه سرویس‌های ابری باید حداقل باشد.
4. استفاده از ابزارهای متن‌باز اولویت دارد.
5. برنامه باید واقعاً کاربردی باشد.
6. رابط کاربری باید مدرن، سریع و ساده باشد.
7. پردازش محلی تا جای ممکن بر پردازش ابری ترجیح دارد.
8. هدف ساخت رقیب DaVinci یا CapCut نیست.


==================================================
2. SOURCE OF TRUTH
==================================================

طرح کامل محصول در Notion مستند شده است.

ابتدا تمام صفحات و زیرصفحات پروژه را مطالعه کن:

HomeVlog Studio:

https://app.notion.com/p/4019ef2b1617819e8e32df9f92a751af

زیرصفحات اصلی:

01 - Product Requirements & UX

02 - Architecture, Storage & AI

03 - Development Roadmap & QA

04 - Content Production, Publishing & Analytics

05 - Technical Review & Open Decisions

در صورت وجود Notion MCP از آن استفاده کن.

اگر دسترسی مستقیم وجود ندارد:
- ابتدا ابزارهای اتصال موجود را بررسی کن.
- ادعای مطالعه اسناد بدون دسترسی واقعی نکن.
- از من بخواه محتوای اسناد را در اختیار تو بگذارم.

تمام تصمیمات قبلی فقط پیشنهاد اولیه هستند،
نه تصمیمات قطعی معماری.


==================================================
3. WORKSPACE RULES
==================================================

Codex CLI در پوشه پروژه اجرا شده است.

همان Current Working Directory را
به‌عنوان Workspace اصلی در نظر بگیر.

ابتدا بررسی کن:

- مسیر فعلی
- فایل‌ها و ساختار موجود
- وضعیت Git در صورت وجود
- پروژه یا کدهای قبلی
- اسناد و تنظیمات موجود

هیچ‌چیز را بدون بررسی overwrite نکن.

اگر پروژه هنوز ایجاد نشده، این موضوع را ثبت کن.

در این مرحله اجازه پیاده‌سازی محصول را نداری.

فقط بررسی، تحلیل، طراحی معماری و مستندسازی
مجاز است.

بعد از نهایی شدن تصمیمات و تأیید صریح من،
اجازه شروع توسعه خواهی داشت.


==================================================
4. FIRST TASK — BUILD VS BUY VS INTEGRATE
==================================================

اول بررسی کن آیا اصلاً لازم است
HomeVlog Studio را بسازیم؟

محصولات و ابزارهای موجود را بررسی کن:

- CapCut Desktop
- DaVinci Resolve
- FFmpeg
- Insta360 Studio
- GoPro Quik
- Buffer
- Metricool
- ابزارهای مدیریت و آرشیو ویدیو
- ابزارهای AI Video Editing
- ابزارهای Auto Subtitle
- ابزارهای AI Highlight Detection

و هر ابزار جدید و مناسبی که پیدا می‌کنی.

برای هر نیاز مشخص کن:

A. استفاده از محصول آماده

B. توسعه قابلیت اختصاصی

C. اتصال چند ابزار موجود

کدام بهتر است؟

به‌خصوص بررسی کن آیا می‌توانیم
با ساخت یک لایه Automation ساده،
بیشتر نیازها را پوشش دهیم؟

هدف جلوگیری از توسعه امکاناتی است که
همین حالا راهکار آماده و مناسب دارند.


==================================================
5. CRITICAL USER EXPERIENCE
==================================================

مهم‌ترین خواسته کاربر:

وصل کردن GoPro به کامپیوتر
و انجام حداکثر کارها با حداقل دخالت انسانی.

Desired Workflow:

Connect Camera
    ↓
Automatic Detection
    ↓
Safe Import
    ↓
Duplicate Detection
    ↓
Automatic Organization
    ↓
Verified Backup
    ↓
Media Analysis
    ↓
Smart Library
    ↓
Quick Edit
    ↓
Persian Subtitles
    ↓
Multiple Export Formats
    ↓
Content Library
    ↓
AI Caption Generation
    ↓
Scheduling
    ↓
Publishing
    ↓
Analytics

این Workflow را از نظر فنی بررسی کن.

برای هر مرحله مشخص کن:

- چه میزان Automation ممکن است؟
- چه مقدار دخالت انسانی لازم است؟
- چه ابزارهایی وجود دارند؟
- هزینه پیاده‌سازی چیست؟
- چه محدودیت‌هایی دارد؟
- آیا واقعاً ارزش توسعه دارد؟

به‌خصوص امکان اتصال مستقیم GoPro
از طریق USB/MTP را بررسی کن.

اگر روش قابل‌اعتمادتری مثل SD Card Reader
وجود دارد، آن را پیشنهاد بده.

مهم:
هیچ فایل اصلی بدون تأیید کاربر پاک نشود.


==================================================
6. SMART MEDIA LIBRARY
==================================================

هدف این است که کاربر مجبور نباشد
صدها ویدیو را تک‌تک بررسی کند.

امکانات پیشنهادی:

- Auto Import
- Duplicate Detection
- Automatic Folder Organization
- Date-Based Grouping
- Event Detection
- Video Thumbnails
- Video Preview
- Auto Tagging
- Scene Detection
- Speech Transcription
- Searchable Video Library
- Backup Management
- Storage Optimization

بررسی کن کدام امکانات را می‌توانیم
کاملاً لوکال و بدون API پیاده کنیم.

همچنین بررسی کن کدام قابلیت‌ها
واقعاً به AI احتیاج دارند.


==================================================
7. AI VIDEO EDITING
==================================================

یکی از اهداف اصلی:

کاربر چندین ویدیو وارد می‌کند.

برنامه بتواند با کمک AI:

- محتوای ویدیوها را تحلیل کند.
- لحظه‌های مهم را پیشنهاد دهد.
- صحنه‌های مناسب را انتخاب کند.
- یک Storyline پیشنهاد دهد.
- یک Rough Cut تولید کند.

مثلاً:

Input:
30 raw GoPro videos

Output A:
30-second Instagram Reel

Output B:
45-second ASMR Reel

Output C:
60-second Storytelling Video

Output D:
Long-form YouTube Draft

راهکارهای زیر را مقایسه کن:

1. FFmpeg + Rule-Based Editing

2. Local AI Models

3. OpenAI API

4. Gemini Video Understanding

5. Existing AI Editing Tools

6. Hybrid Architecture

بررسی کن آیا واقعاً لازم است
خودمان یک Timeline Editor توسعه دهیم؟

یا بهتر است یک Edit Decision List بسازیم
و تدوین نهایی را به ابزارهای موجود بسپاریم؟

اگر راهکار دوم سریع‌تر و قابل‌اعتمادتر است،
همان را پیشنهاد بده.

همچنین امکان Export به DaVinci
از طریق XML/EDL را بررسی کن.

بدون آزمایش سازگاری، آن را قطعی فرض نکن.


==================================================
8. PERSIAN SUBTITLES
==================================================

بررسی کن بهترین روش ساخت
زیرنویس خودکار فارسی چیست.

گزینه‌ها:

- whisper.cpp
- faster-whisper
- OpenAI Speech-to-Text
- سایر راهکارهای معتبر

نیازها:

- پشتیبانی از فارسی محاوره‌ای
- Timestamp Accuracy
- Subtitle Editing
- SRT Export
- Burned-in Captions
- RTL Rendering
- Caption Templates
- Subtitle Styling

پردازش محلی روی RTX 4060
باید بررسی و در صورت امکان Benchmark شود.

تجربه کاربر باید ساده باشد:

Generate Subtitles
    ↓
Review Text
    ↓
Choose Style
    ↓
Apply


==================================================
9. MULTI-PLATFORM EXPORT
==================================================

برنامه باید بتواند با کمترین دخالت،
چند خروجی از یک پروژه تولید کند.

Instagram Reels:
9:16

YouTube Shorts:
9:16

Instagram Feed:
4:5

YouTube Video:
16:9

قابلیت‌ها:

- Export Presets
- Auto Reframe
- Crop Preview
- Subtitle Safe Zones
- Batch Rendering
- Hardware Acceleration
- Background Rendering
- Render Queue

بررسی کن چه قسمت‌هایی با FFmpeg
به‌سادگی قابل پیاده‌سازی هستند.

توجه کن که تبدیل نسبت تصویر نباید
باعث حذف اتفاق مهم یا سوژه شود.


==================================================
10. SOCIAL MEDIA MANAGEMENT
==================================================

یکی دیگر از قابلیت‌های موردنظر:

مدیریت محتوای آماده برای انتشار.

سناریو:

کاربر 10 تا 20 ویدیوی آماده دارد.

می‌خواهد:

- ویدیوها را در یک Library نگهداری کند.
- برای هر ویدیو عنوان انتخاب کند.
- با AI چند کپشن حرفه‌ای بسازد.
- هشتگ پیشنهاد بگیرد.
- Cover انتخاب کند.
- تاریخ انتشار تعیین کند.
- پلتفرم انتشار را انتخاب کند.
- وضعیت پست‌ها را مشاهده کند.
- محتوای منتشرشده را تحلیل کند.

بررسی کن:

Buffer API
Instagram Graph API
YouTube Data API
Metricool

کدام روش برای ما بهتر است؟

مخصوصاً بررسی کن:

- آیا انتشار خودکار واقعاً پشتیبانی می‌شود؟
- آیا به حساب Professional نیاز داریم؟
- چه OAuth Permissionهایی لازم است؟
- هزینه سرویس چیست؟
- محدودیت پلن رایگان چیست؟
- آیا ویدیو باید جایی Host شود؟
- اگر کامپیوتر خاموش باشد چه اتفاقی می‌افتد؟
- چه نوع محتوایی قابل انتشار است؟
- آیا آمار بازدید و تعامل از API قابل دریافت است؟

اطلاعات را از مستندات رسمی و به‌روز تأیید کن.

از APIهای غیررسمی و روش‌هایی که
ممکن است امنیت حساب Instagram را
به خطر بیندازند استفاده نکن.

اگر اتصال مستقیم به Buffer
پیچیدگی غیرضروری ایجاد می‌کند،
راهکار ساده‌تر پیشنهاد بده.


==================================================
11. ARCHITECTURE REVIEW
==================================================

معماری اولیه پیشنهادی:

Frontend:
Python + PySide6

Backend / Processing:
Python

Media Engine:
FFmpeg

Database:
SQLite

AI:
Optional Providers

Windows Packaging:
PyInstaller + Inno Setup

اما این معماری هنوز نهایی نشده.

آن را با گزینه‌های زیر مقایسه کن:

- Flutter Desktop
- Tauri + React
- Electron
- PySide6

معیارهای تصمیم‌گیری:

1. Development Speed
2. Codex Efficiency
3. Runtime Performance
4. Memory Usage
5. Video Playback
6. Windows Integration
7. UI/UX Quality
8. Maintainability
9. Installer Size
10. Long-Term Extensibility

فقط یک معماری نهایی پیشنهاد بده.

همچنین توضیح بده چرا سایر گزینه‌ها
در شرایط فعلی مناسب‌تر نیستند.

از معماری پیچیده و Microserviceهای
غیرضروری خودداری کن.


==================================================
12. UI/UX REQUIREMENTS
==================================================

طراحی باید:

- Modern Desktop First
- Dark Theme
- Clean & Minimal
- Fast
- Intuitive
- Persian RTL
- Professional Typography
- Responsive Layout
- Clear Loading/Error/Empty States

باشد.

کاربر نباید برای یک عملیات ساده
بین چندین صفحه جابه‌جا شود.

از الگوهای خوب رابط کاربری نرم‌افزارهای:

- DaVinci Resolve
- CapCut
- Frame.io
- Adobe Lightroom
- Modern Media Asset Managers

الهام بگیر.

اما UI آنها را کپی نکن.

قبل از تصمیم نهایی معماری،
صفحات اصلی محصول را مشخص کن.

اگر قابلیت‌ها بیش از حد پیچیده شده‌اند،
آنها را ساده‌تر کن.

هدف زیبایی همراه با کارایی است،
نه صرفاً یک داشبورد زیبا.


==================================================
13. DEVELOPMENT COST & TOKEN OPTIMIZATION
==================================================

بسیار مهم:

کاربر می‌خواهد از Codex استفاده کند،
اما منابع و توکن نامحدود ندارد.

برای هر فاز تخمین بده:

- Complexity
- Estimated Development Time
- Technical Risks
- Dependencies
- Validation Requirements
- Approximate Token Consumption
- External API Costs

تخمین‌ها باید دارای بازه و
سطح اطمینان باشند.

عددسازی نکن.

قبلاً تخمین‌هایی برای مصرف توکن داده شده،
اما نباید آنها را بدون بررسی مبنا قرار دهی.

پیشنهادهای کاهش هزینه ارائه کن.

مثلاً:

- Reusing Existing Libraries
- Avoiding Custom Editors
- Local-First Processing
- Small Independent Modules
- Automated Tests
- Limited API Calls
- Reusable Components
- Clear Acceptance Criteria

هر قابلیت باید ارزش توسعه داشته باشد.


==================================================
14. MVP DEFINITION
==================================================

یک MVP کوچک ولی واقعاً کاربردی تعریف کن.

هدف MVP:

کاربر GoPro یا کارت حافظه را وصل کند،
فایل‌ها وارد شوند،
آرشیو و بکاپ انجام شود،
چند کلیپ انتخاب کند،
یک ویدیو بسازد
و خروجی قابل انتشار بگیرد.

اگر قابلیت دیگری برای این تجربه ضروری است،
آن را اضافه کن.

اگر ضروری نیست، حذف یا به فاز بعد منتقل کن.

برای هر قابلیت:

P0 - Must Have
P1 - Should Have
P2 - Nice to Have

مشخص کن.

MVP نباید به پروژه‌ای چندماهه
و بی‌پایان تبدیل شود.


==================================================
15. RISK ASSESSMENT
==================================================

ریسک‌های زیر را بررسی کن:

- Video Data Loss
- Backup Failure
- Storage Capacity
- GoPro Connectivity
- HEVC Compatibility
- GPU Acceleration
- Persian Subtitle Accuracy
- AI Hallucinations
- Video Processing Performance
- Instagram API Limitations
- Social Account Security
- API Pricing
- Software Licensing
- Windows Installer Problems
- Maintenance Cost
- Scope Creep

برای هرکدام:

Severity
Probability
Mitigation

تعریف کن.

همچنین مشخص کن کدام موارد
قبل از توسعه نیازمند Proof of Concept هستند.


==================================================
16. REQUIRED DELIVERABLES
==================================================

در پایان بررسی، خروجی‌های زیر را آماده کن:

01. Executive Summary

02. Critical Product Review

03. Build vs Buy vs Integrate Matrix

04. Recommended Product Scope

05. Final Architecture Proposal

06. Technology Decision Records

07. MVP Definition

08. Prioritized Product Backlog

09. Development Roadmap

10. Technical Risk Register

11. AI Integration Strategy

12. Storage & Backup Strategy

13. Media Processing Pipeline

14. Social Publishing Architecture

15. Estimated Development Effort

16. Token Optimization Strategy

17. Validation & Testing Plan

18. Unresolved Decisions

19. Questions Requiring My Approval

20. Recommended Next Actions

تمام گزارش‌ها را به فارسی روان بنویس،
اما نام ابزارها و اصطلاحات تخصصی
را در صورت نیاز انگلیسی نگه دار.

مطالب تکراری و توضیحات غیرضروری ننویس.

اولویت با گزارش دقیق و اجرایی است.


==================================================
17. DOCUMENTATION
==================================================

خروجی بررسی را در Workspace فعلی
داخل پوشه زیر ثبت کن:

docs/planning/

با فایل‌های Markdown منظم.

حداقل:

PRODUCT_REVIEW.md
ARCHITECTURE_DECISIONS.md
MVP_SCOPE.md
ROADMAP.md
RISK_REGISTER.md
OPEN_DECISIONS.md

در صورت نیاز فایل‌های دیگر اضافه کن،
اما مستندات تکراری تولید نکن.

در صورت وجود Git:

- وضعیت قبلی را حفظ کن.
- تغییرات نامرتبط را دست نزن.
- هیچ Branch موجودی را حذف نکن.
- هیچ تغییر کدی انجام نده.

مستندات باید برای ادامه کار Codex
در جلسات بعدی قابل استفاده باشند.


==================================================
18. APPROVAL GATE — VERY IMPORTANT
==================================================

بعد از پایان بررسی:

STOP.

هیچ کد Production ننویس.
هیچ Dependency غیرضروری نصب نکن.
هیچ پروژه بزرگی Scaffold نکن.
هیچ API پولی فعال نکن.
هیچ سرویس ابری راه‌اندازی نکن.

ابتدا نتایج را به من ارائه کن.

باید دقیقاً مشخص باشد:

- چه چیزهایی بسازیم؟
- چه چیزهایی نسازیم؟
- چه چیزهایی را به ابزارهای موجود بسپاریم؟
- معماری نهایی چیست؟
- زمان و هزینه تقریبی چقدر است؟
- MVP دقیقاً چه قابلیت‌هایی دارد؟
- اولین اقدام اجرایی چیست؟

سپس منتظر تأیید صریح من بمان.

فقط بعد از تأیید:

1. تصمیمات تأییدشده را ثبت کن.
2. Taskهای فنی را نهایی کن.
3. Workspace را آماده کن.
4. Git و ساختار پروژه را تنظیم کن.
5. Tech Spike ضروری را انجام بده.
6. نتیجه را تست و گزارش کن.
7. اگر Gate موفق بود، توسعه MVP را شروع کن.

در مرحله پیاده‌سازی:

- Small Iterations
- Test-Driven Validation
- Clean Architecture
- Minimal Dependencies
- Real Working Features
- No Fake Implementations
- No Demo-Only Completion

را رعایت کن.

هر فاز باید قابل اجرا و تست باشد.

قبل از رفتن به فاز بعدی،
Acceptance Criteria فاز فعلی را بررسی کن.

پس از هر Milestone موفق،
گزارش تغییرات، تست‌ها و موارد باقی‌مانده را ثبت کن.

هیچ قابلیت تست‌نشده‌ای را Done اعلام نکن.


==================================================
19. START NOW
==================================================

اکنون فقط فاز نقد و بررسی را اجرا کن.

ابتدا:

1. Workspace را بررسی کن.
2. اسناد Notion را بخوان.
3. امکانات محصولات موجود را بررسی کن.
4. APIهای مهم را با منابع رسمی تأیید کن.
5. معماری‌های جایگزین را ارزیابی کن.
6. MVP پیشنهادی را مشخص کن.
7. مستندات را ایجاد کن.
8. تصمیمات مهم را به من گزارش بده.

برای نقد و بررسی از استدلال فنی عمیق استفاده کن.

در صورت نیاز تحقیق کن،
اما از جست‌وجوهای تکراری و بی‌هدف پرهیز کن.

هدف نهایی:

ساخت بهترین راهکار ممکن
با کمترین زمان توسعه،
کمترین مصرف توکن،
کمترین هزینه عملیاتی،
و بالاترین ارزش واقعی برای کاربر.

Do not start implementation before explicit approval.