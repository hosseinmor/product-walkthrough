---
walkthrough_id: WT-2026-002
status: reviewed
product_group: JobVision
product: Candidate
candidate_areas:
  - Application Management (primary candidate area)
  - Resume Management
  - Job Details & Evaluation
recorded_at: 2026-08-09
source:
  type: browser-agent
  reference: واکتروی مستقیم Production در Chrome متصل به نشست واردشده؛ timestampها نسبت به شروع session مرورگر هستند و هیچ تصویر یا داده شخصی در repository ذخیره نشده است.
reviewed_by:
  - Product Owner (confirmed in Codex)
reviewed_at: 2026-08-09
---

# بسته شواهد واکترو

## زمینه

- Goal: کشف معیارهای قابل مشاهدهٔ «کامل بودن رزومه» و بررسی کامل flow متفاوت Application Submission برای Candidate با رزومه ناقص.
- Actor: مالک حساب کارجویی
- Role: Candidate / jobseeker
- Authentication state: واردشده
- Account, plan, or configuration: حساب واقعی Production با رزومه فارسی ۱۰۰٪ و وضعیت «تکمیل شده» در شروع؛ entitlement یا پلن بررسی نشد.
- Permissions: Candidate؛ Owner صریحاً یک تغییر حداقلی و قابل‌بازگشت در رزومه و شروع Apply را مجاز کرد.
- Environment: Production (`https://jobvision.ir`)
- Starting point: هوم‌پیج
- Browser context: Chrome متصل به نشست کاربر، desktop
- Expected level of coverage: مسیر اصلی gate رزومه ناقص، close/retry، wizard تکمیل و مسیر جایگزین upload؛ بدون ایجاد Application واقعی برای کارفرمای Production.
- Permitted actions: تغییر موقت و برگشت‌پذیر انتخاب‌های completeness، بازکردن یک آگهی فعال، شروع Apply، حرکت در wizard بدون ثبت نهایی و بازگرداندن رزومه.
- Forbidden actions: کلیک نهایی «ارسال رزومه» پس از فعال‌شدن، upload فایل شخصی، پیام، خرید، حذف داده، تغییر نامرتبط حساب و ذخیرهٔ داده شخصی در evidence.
- Privacy: اطلاعات هویتی و تماس در رابط دیده شد اما عمداً در این package بازتولید نشده است.

## پوشش

### پوشش‌داده‌شده

- ورود از هوم‌پیج به «رزومه من».
- baseline رزومه فارسی تکمیل‌شده و رابطهٔ آن با بخش‌های اختیاری.
- تست کنترل‌شدهٔ تصمیم زبان خارجی و تصمیم تحصیلات دانشگاهی.
- تبدیل رزومه از ۱۰۰٪ تکمیل‌شده به ۶۵٪ ناقص با برداشتن تصمیم تحصیلات.
- ورود به یک آگهی فعال و شروع Apply از CTA «ارسال رزومه».
- modal gate رزومه ناقص، close و retry.
- مسیر recovery چهارمرحله‌ای تکمیل رزومه در context همان صفحه مشاغل.
- مرحله‌های اطلاعات اولیه، تحصیلات، سوابق شغلی و مهارت‌ها.
- validation مرحله مهارت‌ها و فعال‌شدن CTA نهایی پس از بازگرداندن تصمیم زبان.
- مسیر جایگزین «بارگذاری رزومه شخصی» هنگام خروج از wizard.
- بازگرداندن رزومه به ۱۰۰٪ تکمیل‌شده و تأیید ساخته‌نشدن Application.

### روایت‌شده ولی نمایش‌داده‌نشده

- Owner پیش از تست بیان کرد که کامل‌بودن رزومه برای ارسال درخواست الزامی است؛ این قاعده در context آزموده‌شده با gate مشاهده‌شده پشتیبانی شد، اما نباید بدون آزمون به همهٔ حساب‌ها، آگهی‌ها یا مسیرهای upload تعمیم داده شود.

### پوشش‌داده‌نشده

- کلیک نهایی «ارسال رزومه» بعد از کامل‌شدن wizard و ایجاد Application واقعی.
- upload و ارسال رزومه شخصی.
- همهٔ معیارها و وزن‌های completeness؛ فقط تصمیم تحصیلات و تصمیم زبان آزموده شد.
- validation فیلدهای خالی اطلاعات اولیه یا رکوردهای تحصیلی و شغلی.
- state رزومه کاملاً خالی یا حساب تازه.
- duplicate application، آگهی بسته یا منقضی، network failure و retry سمت سرور.
- mobile، keyboard، screen reader و accessibility.
- رفتار Employer و نوع representation یا snapshot رزومه در Application.

### نامشخص یا مسدود

- آیا upload رزومه شخصی بدون تکمیل رزومه جاب‌ویژنی مستقیماً Application می‌سازد یا مرحله تأیید دیگری دارد.
- آیا CTA نهایی wizard هم‌زمان تغییرات رزومه و Application را ذخیره می‌کند.
- آیا معیارهای completeness برای همهٔ حساب‌ها و آگهی‌ها یکسان‌اند.
- آیا Application یک snapshot از رزومه می‌گیرد یا به رزومه جاری اشاره می‌کند.

## شواهد

### E-001 — baseline رزومه فارسی می‌تواند ۱۰۰٪ تکمیل‌شده باشد در حالی که بخش‌های اختیاری خالی‌اند

- Type: accepted
- Timestamp: T+00:35
- Scope: Candidate واردشده، Resume Management در Production.
- Conditions: رزومه موجود حساب در شروع سناریو.
- Confidence: high
- Claim: صفحه رزومه فارسی را ۱۰۰٪ و «تکمیل شده» نشان داد، در حالی که بخش‌های «معرفی صوتی» و «بارگذاری رزومه شخصی» صفر درصد بودند؛ بنابراین این دو بخش برای completeness فارسی در این حساب الزامی نیستند.
- Remaining uncertainty: سایر بخش‌های اختیاری و ruleهای حساب‌های دیگر آزموده نشدند.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-002 — برداشتن تصمیم «زبان خارجی ندارم» به‌تنهایی completeness کلی را فوراً تغییر نداد

- Type: accepted
- Timestamp: T+02:08
- Scope: بخش زبان‌ها در همان رزومه Production.
- Conditions: checkbox «مهارت زبان خارجی ندارم» از حالت checked خارج شد و ۲٫۲ ثانیه برای به‌روزرسانی صبر شد.
- Confidence: medium
- Claim: پس از برداشتن تصمیم زبان، کارت زبان‌ها همچنان ۱۰۰٪ و وضعیت کلی رزومه فارسی همچنان تکمیل‌شده باقی ماند.
- Remaining uncertainty: امکان تأخیر بیشتر، cache یا محاسبهٔ متفاوت در Application wizard وجود دارد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-003 — تصمیم تحصیلات دانشگاهی یک معیار مؤثر completeness در این حساب است

- Type: accepted
- Timestamp: T+04:09–T+04:35
- Scope: بخش سوابق تحصیلی و نشانگر کلی رزومه فارسی.
- Conditions: checkbox «تحصیلات دانشگاهی ندارم» از حالت checked خارج شد؛ هیچ رکورد تحصیلی جایگزین ثبت نشد.
- Confidence: high
- Claim: برداشتن تصمیم تحصیلات، وضعیت «تکمیل شده» را حذف و completeness رزومه فارسی را از ۱۰۰٪ به ۶۵٪ کاهش داد.
- Remaining uncertainty: وزن دقیق سایر گزینه‌ها و اینکه ۳۵ واحد کاهش در همهٔ حساب‌ها ثابت است معلوم نیست.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-004 — Apply با رزومه ۶۵٪ به gate رزومه ناقص منتهی می‌شود

- Type: accepted
- Timestamp: T+05:10–T+05:37
- Scope: یک آگهی فعال Production با CTA «ارسال رزومه».
- Conditions: Candidate واردشده؛ رزومه فارسی ۶۵٪ به‌علت تصمیم تحصیلات حل‌نشده.
- Confidence: high
- Claim: کلیک «ارسال رزومه» Application ایجاد نکرد و modal «رزومه شما تکمیل نیست!» را با ۶۵٪ تکمیل‌شده نشان داد. modal مسیر ادامه یا ارسال ندارد و فقط بستن یا «تکمیل رزومه جاب‌ویژن» را ارائه می‌کند.
- Remaining uncertainty: رفتار برای درصدهای دیگر یا آگهی‌های دارای سؤال‌های screening آزموده نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-005 — بستن gate و تلاش مجدد state را دور نمی‌زند

- Type: accepted
- Timestamp: T+05:58
- Scope: همان آگهی و همان state رزومه ناقص.
- Conditions: modal بسته و CTA «ارسال رزومه» دوباره انتخاب شد.
- Confidence: high
- Claim: بستن modal کاربر را به صفحه آگهی برگرداند و تلاش مجدد همان gate ۶۵٪ را دوباره باز کرد؛ هیچ مسیر bypass مشاهده نشد.
- Remaining uncertainty: persistence پس از refresh یا session دیگر آزموده نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-006 — recovery در همان صفحه یک wizard چهارمرحله‌ای باز می‌کند

- Type: accepted
- Timestamp: T+06:12–T+08:34
- Scope: action «تکمیل رزومه جاب‌ویژن» از modal gate.
- Conditions: Candidate واردشده در صفحه مشاغل؛ رزومه ناقص.
- Confidence: high
- Claim: action تکمیل رزومه به route `/my-cv` ناوبری نکرد و یک wizard در context همان صفحه باز کرد. wizard شامل ۱) اطلاعات اولیه، ۲) سوابق تحصیلی، ۳) سوابق شغلی و ۴) مهارت‌ها بود و داده‌های موجود حساب را prefill کرد.
- Remaining uncertainty: آیا ترتیب یا تعداد مرحله‌ها با missing fieldهای دیگر تغییر می‌کند.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-007 — مرحله تحصیلات از یک degree decision به رکورد قابل مرور تبدیل می‌شود

- Type: accepted
- Timestamp: T+07:36–T+08:07
- Scope: مرحله ۲ از ۴ wizard.
- Conditions: وضعیت اصلی حساب «زیر دیپلم» دوباره انتخاب شد.
- Confidence: high
- Claim: مرحله تحصیلات گزینه‌های زیر دیپلم، دیپلم، کاردانی، کارشناسی، کارشناسی ارشد و دکترا را ارائه کرد؛ action «ادامه» تا انتخاب یک گزینه disabled بود. پس از انتخاب وضعیت اصلی، یک رکورد تحصیلی ساخته شد و «مرحله بعد» فعال شد.
- Remaining uncertainty: فیلدها و validationهای موردنیاز برای مقاطع دیگر آزموده نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-008 — مرحله مهارت‌ها یک تصمیم زبان را برای فعال‌شدن ارسال نهایی لازم می‌داند

- Type: accepted
- Timestamp: T+08:34–T+09:24
- Scope: مرحله ۴ از ۴ wizard.
- Conditions: رکورد تحصیلات و سابقه شغلی موجود بودند؛ تصمیم زبان قبلاً برای تست برداشته شده بود.
- Confidence: high
- Claim: مرحله مهارت‌ها سطح زبان انگلیسی یا گزینه «زبان انگلیسی بلد نیستم» را ارائه کرد و CTA نهایی «ارسال رزومه» disabled بود. با بازگرداندن گزینه «زبان انگلیسی بلد نیستم»، CTA نهایی enabled شد.
- Remaining uncertainty: validation نرم‌افزارها و اینکه داشتن حداقل یک نرم‌افزار الزامی است آزموده نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-009 — خروج از wizard مسیر جایگزین رزومه شخصی را پیشنهاد می‌دهد

- Type: accepted
- Timestamp: T+09:52–T+10:09
- Scope: خروج از مرحله ۴ wizard پیش از ارسال نهایی.
- Conditions: CTA نهایی enabled بود ولی کلیک نشد.
- Confidence: high
- Claim: بستن wizard مستقیماً modalها را خاتمه نداد؛ modal «بارگذاری رزومه شخصی» باز شد و اعلام کرد کارجو می‌تواند به‌جای تکمیل رزومه جاب‌ویژنی، فایل رزومه شخصی را برای کارفرما ارسال کند. این modal action انتخاب فایل و مسیر بازگشت به تکمیل رزومه جاب‌ویژنی داشت.
- Remaining uncertainty: فرمت، اندازه، validation، ذخیره و نتیجه Application پس از upload آزموده نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

### E-010 — سناریو بدون Application واقعی پایان یافت و رزومه بازیابی شد

- Type: accepted
- Timestamp: T+10:25–T+11:21
- Scope: Resume Management و همان آگهی Production پس از خروج از flow.
- Conditions: وضعیت اصلی تحصیلات و زبان در wizard بازگردانده شد؛ هیچ CTA نهایی ارسال یا upload اجرا نشد.
- Confidence: high
- Claim: بازگشت به Resume Management هر دو تصمیم اصلی تحصیلات و زبان را checked، رزومه فارسی را ۱۰۰٪ و «تکمیل شده» نشان داد. همان آگهی همچنان CTA «ارسال رزومه» داشت؛ بنابراین در این سناریو Application واقعی ساخته نشد.
- Remaining uncertainty: audit سمت Employer یا Application database انجام نشد.

#### بررسی Owner

- Decision: accepted
- Final claim:
- Owner note:

## باگ‌های مشکوک

### B-001 — کارت تحصیلات ۱۰۰٪ می‌ماند در حالی که completeness کلی ۶۵٪ است

- Timestamp: T+04:09–T+04:35
- Scope: Resume Management، state تصمیم تحصیلات حل‌نشده.
- Observation: پس از برداشتن «تحصیلات دانشگاهی ندارم»، کارت سوابق تحصیلی همچنان ۱۰۰٪ نمایش داده شد ولی completeness فارسی به ۶۵٪ افت کرد و برچسب «تکمیل شده» حذف شد.
- Why it may be a bug: نشانگر per-section با state واقعی section و نشانگر کلی ناسازگار است و می‌تواند کاربر را درباره بخش ناقص گمراه کند.
- Owner note:

### B-002 — معیار زبان در صفحه رزومه و wizard ارسال هم‌راستا دیده نشد

- Timestamp: T+02:08 و T+08:34–T+09:24
- Scope: Resume Management و مرحله ۴ Application completion wizard.
- Observation: برداشتن تصمیم زبان در صفحه رزومه completeness کلی را فوراً تغییر نداد، اما در wizard همان تصمیم باعث disabled ماندن CTA نهایی شد تا سطح زبان یا «بلد نیستم» انتخاب شود.
- Why it may be a bug: دو سطح محصول ظاهراً تعریف متفاوتی از آمادگی رزومه نشان می‌دهند؛ ممکن است rule متفاوت عمدی، cache یا به‌روزرسانی با تأخیر باشد.
- Owner note:

## شکاف‌های پوشش

- ایجاد واقعی Application پس از تکمیل wizard با آگهی تست مجاز.
- رفتار کامل upload رزومه شخصی و اینکه آیا رزومه جاب‌ویژنی ناقص را bypass می‌کند.
- ماتریس همهٔ معیارهای completeness و وزن هر بخش.
- validation فیلدهای اطلاعات اولیه، تحصیلات، سابقه شغلی و نرم‌افزارها.
- failure و recovery سمت API، refresh و session/device دیگر.
- duplicate application و آگهی بسته/منقضی.
- تفاوت رزومه جاری با snapshot یا representation متصل به Application.
- mobile، keyboard، screen reader و accessibility.

## پیشنهاد واکتروی بعدی

- با یک آگهی تست تحت کنترل تیم، CTA نهایی wizard اجرا و ایجاد Application، confirmation، tracking و representation رزومه سمت Employer بررسی شود.
- مسیر upload رزومه شخصی با یک فایل غیرشخصی و مجاز تست شود تا فرمت، validation، persistence و outcome مشخص شود.
- با یک حساب disposable، هر معیار completeness جداگانه تغییر داده شود تا ماتریس required/optional و وزن‌ها مستند شود.
- B-001 و B-002 با Owner و instrumentation/API بررسی شوند.

## Product Areaهای مرتبط

- Primary: JobVision Candidate / Application Management
- Secondary: JobVision Candidate / Resume Management
- Secondary: JobVision Candidate / Job Details & Evaluation
- Shared concepts for later reconciliation only: `shared.application` و `shared.resume`

## پیشنهادهای Product Knowledge

- از این package draft برای تغییر canonical Product Knowledge استفاده نشود.
- پس از review Owner، claimهای پذیرفته‌شده برای Application eligibility، resume-readiness gate، wizard recovery و alternate personal-resume path با Product Areaهای Application Management و Resume Management مقایسه شوند.
- مرحله شروع Apply در Job Details & Evaluation باقی بماند، اما validation و submission flow زیر Application Management مستند شود.
- unknown مربوط به snapshot در `shared.application` و `shared.resume` حفظ شود.

## خلاصه handoff

این بخش فقط پس از review Owner تکمیل می‌شود.

- Package status: reviewd
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: بخش «شکاف‌های پوشش» را ببینید.
- Suggested Product Knowledge scope: Candidate Application Management، Resume Management و مرز شروع Apply در Job Details & Evaluation.

یک package reviewed منبع تأییدشده برای reconciliation است، اما canonical Product Knowledge نیست و نباید بدون مقایسه با branch جاری `product-knowledge/main` مستقیماً در مستندات محصول کپی شود.
