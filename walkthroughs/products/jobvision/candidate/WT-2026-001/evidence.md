---
walkthrough_id: WT-2026-001
status: draft
product_group: jobvision
product: candidate
candidate_areas:
  - Job Search
recorded_at: 2026-08-06T13:11:12Z
updated_at: 2026-08-08T06:38:13Z
source:
  type: browser-agent
  reference: واکتروی مستقیم محیط Production با مرورگر داخلی Codex؛ اجرای اولیه read-only و ادامه با مجوز کاربر برای تغییر داده‌های همین حساب
reviewed_by: []
reviewed_at:
---

# بسته شواهد واکترو

## زمینه

- Goal: کشف فرصت‌های شغلی از صفحه اصلی و محدودکردن نتایج با جستجو، شهر، گروه شغلی، فیلترها و مرتب‌سازی؛ سپس پوشش شکاف‌های همین محدوده شامل فیلترهای پیشرفته، صفحه‌بندی، ذخیره جستجو، تاریخچه، ریسپانسیو و تعامل صفحه‌کلید.
- Actor: کارجو
- Role: Candidate
- Authentication state: واردشده؛ این وضعیت از آیتم‌های ناوبری احراز هویت‌شده و سطوح شخصی‌سازی‌شده قابل مشاهده است.
- Account, plan, or configuration: نوع پلن و تنظیمات دقیق نامشخص است؛ هیچ شناسه حساب یا مقدار شخصی در این بسته ثبت نشده است.
- Permissions: دسترسی عادی Candidate مشاهده شد؛ مدل دقیق permission نامشخص است.
- Environment: Production
- Starting point: صفحه اصلی JobVision و صفحه `/jobs`
- Permitted actions: ورود عبارت تست غیرحساس، انتخاب و حذف فیلترها، مرتب‌سازی، ناوبری و refresh؛ در ادامه و با مجوز صریح کاربر، ذخیره یک جستجوی تستی، فعال/غیرفعال‌کردن اعلان آن و پاک‌کردن تاریخچه جستجو نیز انجام شد.
- Forbidden actions: پرداخت، تغییر permission، حل CAPTCHA، افشای داده حساس یا اقدامی خارج از محدوده این واکترو.
- Stop conditions: پرداخت، CAPTCHA، داده حساس یا اقدامی که به تصمیم محصولی خارج از محدوده Job Search نیاز داشته باشد.

## پوشش

### پوشش‌داده‌شده

- نقطه ورود جستجوی صفحه اصلی
- ورود keyword و رفتن به نتایج
- انتخاب پیشنهاد شهر و اعمال آن
- انتخاب گروه شغلی و اعمال آن
- فهرست کامل کنترل‌های فیلتر در صفحه نتایج
- فیلترهای دورکاری و نوع همکاری
- ترکیب فیلترها و حذف مستقل آن‌ها
- مدل گزینه‌های زمان انتشار، حقوق، سابقه کاری، سطح ارشدیت، مزایا، صنعت، کارآموزی، استخدام معلولین و امریه سربازی
- اعمال نمونه‌ای از فیلترهای تک‌انتخابی و چندانتخابی و ثبت URL و تعداد نتایج
- سه حالت مرتب‌سازی شامل مرتبط‌ترین، جدیدترین و بیشترین حقوق
- ماندگاری state مبتنی بر URL پس از refresh و در یک تب تازه
- صفحه‌بندی، Back/Forward و بازگشت از Job Details
- empty state
- ذخیره جستجو، فعال و غیرفعال‌کردن اعلان، صفحه مدیریت جستجوهای ذخیره‌شده و وضعیت کانال ایمیل
- پاک‌کردن همه جستجوهای اخیر
- نمای باریک/موبایل برای جستجو و پنل فیلترها
- ارسال keyword با کلید Enter و بررسی رفتار Tab در فیلد keyword
- بازآزمایی دو باگ مشکوک قبلی

### روایت‌شده ولی نمایش‌داده‌نشده

- موردی وجود ندارد. همه موارد این بسته از مشاهده مستقیم مرورگر به‌دست آمده‌اند.

### پوشش‌داده‌نشده

- ارسال درخواست برای یک Job Post؛ این رفتار به محدوده برنامه‌ریزی‌شده `WT-2026-002` تعلق دارد.
- موفقیت حذف یک جستجوی ذخیره‌شده؛ کنترل حذف در این اجرا واکنش قابل مشاهده‌ای نداشت و رکورد تستی باقی ماند.
- تحویل واقعی اعلان از طریق ایمیل، پیامک یا بله، زمان‌بندی آن، deduplication و رفتار در نبود مقصد معتبر
- تعویض موفق کانال سراسری اعلان از ایمیل به پیامک
- پاک‌کردن یک مورد منفرد از جستجوهای اخیر؛ فقط «پاک کردن همه» دیده و اجرا شد.
- همه ترکیب‌های ممکن فیلترها، سقف تعداد انتخاب‌ها و تقدم/تأخر کامل آن‌ها
- رفتار unauthenticated و سایر نوع‌های حساب یا پلن Candidate
- screen reader کامل و آزمون جامع صفحه‌کلید خارج از رفتار Enter و Tab در فیلد keyword
- breakpointها و دستگاه‌های بیشتر از یک نمای باریک و یک نمای دسکتاپ
- خطای شبکه، retry، timeout و حالت offline

### نامشخص یا مسدود

- اینکه نتایج ظاهراً نامرتبط در مرتب‌سازی «جدیدترین» broad match عمدی، match روی توضیحات/شرکت یا خطای ranking است.
- اثر عنوان موقتاً قدیمی یا عمومی صفحه بر analytics و accessibility.
- علت واکنش‌ندادن کنترل حذف جستجوی ذخیره‌شده.
- علت باقی‌ماندن فوکوس روی keyword پس از چند بار Tab و اینکه آیا در همه مرورگرها تکرار می‌شود.
- الزامات دقیق authentication و permission برای پیشنهادهای شخصی و اعلان‌های ذخیره جستجو.

## شواهد

### E-001 — صفحه اصلی یک ورودی چندبخشی برای جستجوی شغل ارائه می‌کند

- Type: observed
- Timestamp: 2026-08-06T13:11:12Z
- Scope: صفحه اصلی Production؛ session واردشده Candidate
- Conditions: نمای دسکتاپ پیش‌فرض مرورگر
- Confidence: high
- Claim: کارجو می‌تواند عنوان شغلی یا شرکت را وارد کند، گروه شغلی و شهر را انتخاب کند و با «جستجو در مشاغل» جریان را آغاز کند.
- Remaining uncertainty: اجباری یا اختیاری‌بودن فیلدها و رفتار unauthenticated آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-002 — ارسال keyword یک صفحه نتایج محدودشده به همان keyword می‌سازد

- Type: observed
- Timestamp: 2026-08-06T13:11:48Z
- Scope: keyword «طراح محصول»؛ Production
- Conditions: متن شهر وارد شده بود ولی هیچ پیشنهاد شهری انتخاب نشده بود.
- Confidence: high
- Claim: ارسال «طراح محصول» به URL مبتنی بر keyword رفت، keyword را در فیلد نگه داشت، heading مرتبط نشان داد و مرتب‌سازی را به‌صورت پیش‌فرض روی «مرتبط‌ترین» قرار داد.
- Remaining uncertainty: قواعد matching، stemming، synonym، تطبیق نام شرکت و ranking نامشخص‌اند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-003 — متن شهر فقط پس از انتخاب پیشنهاد و submit اعمال می‌شود

- Type: observed
- Timestamp: 2026-08-06T13:11:36Z–2026-08-06T13:12:32Z
- Scope: جستجوی شهر «تهران» همراه keyword «طراح محصول»؛ Production
- Conditions: بار اول فقط «تهران» تایپ شد؛ بار دوم پیشنهاد «تمامی شهرهای تهران» انتخاب شد.
- Confidence: high
- Claim: تایپ متن شهر به‌تنهایی جستجوی submitشده را محدود نکرد. پس از انتخاب «تمامی شهرهای تهران» و submit، شهر در URL و heading آمد و تعداد قابل مشاهده از 740 به 526 تغییر کرد.
- Remaining uncertainty: انتخاب یک شهر در برابر کل استان، انتخاب چند شهر و انتخاب فقط با صفحه‌کلید آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-004 — صفحه نتایج مجموعه گسترده‌ای از فیلترها و کنترل‌های مرتب‌سازی دارد

- Type: observed
- Timestamp: 2026-08-06T13:11:48Z
- Scope: صفحه نتایج keyword؛ Production؛ session واردشده Candidate
- Conditions: keyword «طراح محصول»
- Confidence: high
- Claim: صفحه نتایج فیلترهای زمان انتشار، دورکاری، نوع همکاری، کارآموزی، حقوق، سابقه کاری، سطح ارشدیت، مزایا، صنعت، استخدام معلولین و امریه سربازی را همراه مرتب‌سازی جدیدترین، مرتبط‌ترین و بیشترین حقوق و کنترل اعلان جستجوی ذخیره‌شده ارائه کرد.
- Remaining uncertainty: همه permutationهای فیلترها آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-005 — دورکاری یک فیلتر فوری و قابل حذف است

- Type: observed
- Timestamp: 2026-08-06T13:12:45Z–2026-08-06T13:13:08Z
- Scope: keyword «طراح محصول»، تمامی شهرهای تهران؛ Production
- Conditions: فیلتر دیگری در نتایج انتخاب نشده بود.
- Confidence: high
- Claim: انتخاب «دورکاری» بلافاصله segment دورکاری را به URL افزود، heading را تغییر داد، تعداد قابل مشاهده را از 526 به 62 رساند و یک فیلتر فعال نشان داد. حذف آن URL، heading و تعداد قبلی را برگرداند.
- Remaining uncertainty: تک‌تک Job Postهای برگشتی از نظر پشتیبانی واقعی دورکاری audit نشدند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-006 — نوع همکاری سه گزینه تک‌انتخابی دارد

- Type: observed
- Timestamp: 2026-08-06T13:13:46Z–2026-08-06T13:14:34Z
- Scope: keyword «طراح محصول»، تمامی شهرهای تهران؛ Production
- Conditions: فیلتر نوع همکاری باز بود.
- Confidence: high
- Claim: فیلتر نوع همکاری سه radio برای تمام‌وقت، پاره‌وقت و قراردادی/پروژه‌ای نشان داد. انتخاب پاره‌وقت بلافاصله segment مربوط را به URL افزود، heading را تغییر داد، تعداد را به 41 رساند و یک فیلتر فعال نشان داد.
- Remaining uncertainty: جابه‌جایی مستقیم میان هر سه گزینه آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-007 — دورکاری و پاره‌وقت با هم ترکیب و مستقل حذف می‌شوند

- Type: observed
- Timestamp: 2026-08-06T13:14:47Z–2026-08-06T13:15:52Z
- Scope: keyword «طراح محصول»، تمامی شهرهای تهران؛ Production
- Conditions: پاره‌وقت پیش از دورکاری انتخاب شد.
- Confidence: high
- Claim: افزودن دورکاری به پاره‌وقت یک URL ترکیبی، heading شامل هر دو شرط، تعداد 25 و شمارنده دو فیلتر فعال ساخت. حذف دورکاری پاره‌وقت را حفظ کرد و کنترل × روی chip پاره‌وقت فیلتر باقی‌مانده را حذف کرد.
- Remaining uncertainty: همه ترکیب‌ها و محدودیت حداکثر انتخاب آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-008 — مرتب‌سازی در URL ثبت و پس از refresh بازیابی می‌شود

- Type: observed
- Timestamp: 2026-08-06T13:13:23Z، 2026-08-06T13:17:27Z و 2026-08-08T06:37:56Z
- Scope: نتایج keyword و نتایج عمومی؛ Production
- Conditions: مرتب‌سازی میان مرتبط‌ترین، جدیدترین و بیشترین حقوق تغییر کرد.
- Confidence: high
- Claim: «جدیدترین» مقدار `sort` را از 1 به 0 تغییر داد و «بیشترین حقوق» URL با `sort=2` ساخت. پس از refresh، keyword و مرتب‌سازی جدیدترین از URL بازیابی شدند.
- Remaining uncertainty: پایداری دقیق ترتیب بین دو بار بارگذاری با داده زنده آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-009 — ویرایش شهر و گروه شغلی تا submit جستجو staged می‌ماند

- Type: observed
- Timestamp: 2026-08-06T13:16:56Z–2026-08-06T13:17:07Z و 2026-08-06T13:18:53Z–2026-08-06T13:19:25Z
- Scope: کنترل‌های جستجوی صفحه نتایج؛ Production
- Conditions: نتایج keyword از قبل فعال بود.
- Confidence: high
- Claim: پاک‌کردن شهر یا انتخاب/پاک‌کردن گروه شغلی ابتدا فقط کنترل متناظر را تغییر داد؛ URL و نتایج تا submit «جستجو در مشاغل» تغییر نکردند.
- Remaining uncertainty: رفتار کامل انتخاب شهر فقط با صفحه‌کلید آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-010 — انتخاب‌گر گروه شغلی قابل جستجو است و category را در URL اعمال می‌کند

- Type: observed
- Timestamp: 2026-08-06T13:18:44Z–2026-08-06T13:19:04Z
- Scope: کنترل گروه شغلی صفحه نتایج؛ Production
- Conditions: keyword بدون نتیجه از قبل فعال بود.
- Confidence: high
- Claim: بازکردن کنترل گروه شغلی یک فیلد جستجو و فهرست بلند گزینه‌ها نشان داد. انتخاب «طراحی رابط و تجربه کاربری (UI/UX)» و submit، category مربوط به UI/UX را به URL افزود.
- Remaining uncertainty: multi-select، ترتیب گزینه‌ها و zero-match درون picker آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-011 — جستجوی بدون نتیجه راهنمای بازیابی ارائه می‌کند

- Type: observed
- Timestamp: 2026-08-06T13:17:45Z و 2026-08-08T06:36:35Z
- Scope: keyword عمدی بدون match؛ Production
- Conditions: keyword `xyzqwalkthrough1405`
- Confidence: high
- Claim: وقتی هیچ Job Postی match نشد، صفحه اعلام کرد فرصتی پیدا نشده و پیشنهاد بررسی املاء، امتحان keyword دیگر یا حذف فیلترها را نشان داد. submit با کلید Enter نیز همین URL و empty state را ساخت.
- Remaining uncertainty: خطای موقت سرور و حالت partial-result آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-012 — focus روی keyword کمک جستجوهای ذخیره‌شده و اخیر را نشان می‌دهد

- Type: observed
- Timestamp: 2026-08-06T13:18:08Z و 2026-08-08T06:25:56Z
- Scope: صفحه نتایج؛ session واردشده Candidate
- Conditions: فیلد keyword focus گرفت.
- Confidence: high
- Claim: در دسکتاپ، focus روی keyword بخش جستجوهای ذخیره‌شده با ورودی «ویرایش»، بخش جستجوهای اخیر و کنترل «پاک کردن همه» را نشان داد.
- Remaining uncertainty: مدت نگه‌داری، سقف history، deduplication و مالکیت دقیق داده‌ها نامشخص‌اند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-013 — فیلترهای پیشرفته ترکیبی از مدل تک‌انتخابی، چندانتخابی و toggle هستند

- Type: observed
- Timestamp: 2026-08-08T06:17:00Z–2026-08-08T06:18:00Z
- Scope: `/jobs`؛ Production؛ دسکتاپ
- Conditions: فیلترها یکی‌یکی باز شدند.
- Confidence: high
- Claim: زمان انتشار چهار radio برای 3 روز، 1 هفته، 15 روز و 1 ماه اخیر دارد؛ حقوق 10 بازه از زیر 10 تا بالای 300 میلیون تومان دارد؛ سابقه کاری 6 بازه از بدون سابقه تا بالاتر از 12 سال دارد؛ سطح ارشدیت 7 گزینه از کارگر تا مدیرعامل دارد. مزایا و صنعت checkbox چندانتخابی‌اند و فهرست مزایا 25 گزینه قابل مشاهده داشت. کارآموزی، استخدام معلولین و امریه سربازی toggle هستند.
- Remaining uncertainty: تغییرات آینده taxonomy و ترتیب گزینه‌ها با داده/config زنده نامشخص است.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-014 — نمونه‌های تک‌انتخابی بلافاصله URL و نتایج را تغییر می‌دهند

- Type: observed
- Timestamp: 2026-08-08T06:20:19Z–2026-08-08T06:22:11Z
- Scope: نتایج عمومی `/jobs`؛ Production؛ دسکتاپ
- Conditions: هر نمونه از state بدون فیلتر آغاز شد.
- Confidence: high
- Claim: «3 روز اخیر» URL با `searchTimeRange=1` و 3,900 نتیجه ساخت؛ حقوق «بین 40 تا 60 میلیون تومان» URL با `salary=6` و 16,588 نتیجه ساخت؛ سابقه «کمتر از 2 سال» URL با `workExperiences=1` و 24,671 نتیجه ساخت؛ سطح «کارشناس» URL با `seniorityLevels=97` و 24,135 نتیجه ساخت. تعدادها snapshot داده زنده همان لحظه‌اند.
- Remaining uncertainty: mapping همه option IDها و ثبات تعداد نتایج در طول زمان آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-015 — مزایا و صنعت تا «مشاهده نتایج» staged می‌مانند و چند مقدار را در URL تکرار می‌کنند

- Type: observed
- Timestamp: 2026-08-08T06:22:56Z–2026-08-08T06:23:34Z
- Scope: نتایج عمومی `/jobs`؛ Production؛ دسکتاپ
- Conditions: دو گزینه در هر فیلتر انتخاب شد.
- Confidence: high
- Claim: انتخاب «سرویس رفت و برگشت» و «وام» URL را تا کلیک «مشاهده نتایج» تغییر نداد؛ پس از آن URL شامل دو `jobBenefits` و تعداد 17,252 شد. انتخاب «حسابرسی» و «بانکداری» نیز تا همان دکمه staged ماند و سپس URL شامل دو `industries` و تعداد 481 شد. UI پس از اعمال، برای هر فیلتر عبارت «2 مورد» نشان داد.
- Remaining uncertainty: منطق AND/OR دقیق درون هر فیلتر و میان فیلترها از count به‌تنهایی قطعی نیست.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-016 — صفحه‌بندی، history مرورگر، Job Details و URL اشتراک‌پذیر state فیلتر را حفظ می‌کنند

- Type: observed
- Timestamp: 2026-08-08T06:23:53Z–2026-08-08T06:25:01Z
- Scope: دو صنعت «حسابرسی» و «بانکداری»؛ Production؛ دسکتاپ
- Conditions: 481 نتیجه و حداقل سه صفحه قابل مشاهده بود.
- Confidence: high
- Claim: انتخاب صفحه 2 مقدار `page=2` را به URL افزود. Back صفحه 1 و Forward صفحه 2 را با همان دو صنعت و همان count بازگرداند. بازکردن نخستین Job Post و سپس Back نیز صفحه 2 فیلترشده را بازیابی کرد. بازکردن همان URL در تب تازه دو صنعت، صفحه 2 و count را بازسازی کرد.
- Remaining uncertainty: scroll position و رفتار روی همه نوع deep link آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-017 — toggle اعلان یک جستجو را ذخیره می‌کند و خاموش‌کردن اعلان رکورد را حذف نمی‌کند

- Type: observed
- Timestamp: 2026-08-08T06:25:41Z–2026-08-08T06:29:30Z
- Scope: جستجوی دو صنعت «حسابرسی» و «بانکداری»؛ حساب واردشده Production
- Conditions: پیش از آزمون دو جستجوی ذخیره‌شده در حساب وجود داشت.
- Confidence: high
- Claim: روشن‌کردن toggle «ذخیره جستجو و دریافت آگهی‌های جدید در ایمیل یا پیامک» پیام موفقیت و حالت فعال نشان داد و شمار جستجوهای ذخیره‌شده را از 2 به 3 رساند. رکورد جدید با عنوان «حسابرسی»، خلاصه «حسابرسی بانکداری»، تاریخ امروز و toggle روشن در `/saved-searches` دیده شد. خاموش‌کردن اعلان checkbox رکورد را خاموش کرد ولی آن را از فهرست حذف نکرد.
- Remaining uncertainty: زمان تحویل، مقصد دقیق، ارتباط با بله و رفتار در نبود email/phone معتبر آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-018 — مدیریت جستجوهای ذخیره‌شده اعلان هر مورد و یک تنظیم سراسری کانال دارد

- Type: observed
- Timestamp: 2026-08-08T06:25:56Z–2026-08-08T06:26:51Z
- Scope: `/saved-searches`؛ حساب واردشده Production
- Conditions: سه رکورد ذخیره‌شده قابل مشاهده بود.
- Confidence: medium
- Claim: هر کارت عنوان، خلاصه فیلتر، toggle ارسال آگهی‌های جدید، زمان ذخیره، «مشاهده نتایج» و کنترل حذف داشت. بخش «تنظیمات» دو گزینه ایمیل و پیامک نشان داد و ایمیل در این حساب فعال بود.
- Remaining uncertainty: کلیک‌های موس و keyboard روی «پیامک» انتخاب فعال ایمیل را تغییر ندادند؛ نامشخص است پیامک غیرفعال، نیازمند پیش‌شرط یا دچار اشکال است.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-019 — «پاک کردن همه» تاریخچه اخیر را بدون confirmation مرئی حذف می‌کند

- Type: observed
- Timestamp: 2026-08-08T06:35:28Z و 2026-08-08T06:37:00Z
- Scope: dropdown کمک keyword؛ حساب واردشده Production؛ دسکتاپ
- Conditions: ابتدا سه رکورد اخیر از واکتروی قبلی و سپس یک keyword تستی جدید وجود داشت.
- Confidence: high
- Claim: کلیک «پاک کردن همه» بدون modal یا confirmation مرئی هر سه رکورد اخیر را حذف کرد؛ کنترل و آیکون‌های history نیز ناپدید شدند. پس از ساخت یک recent search تستی با Enter، همان عمل دوباره آن را پاک کرد.
- Remaining uncertainty: امکان بازیابی یا audit history برای کاربر وجود داشت یا نه، مشاهده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-020 — نمای موبایل جستجو و فیلترها را به سطوح جدا تبدیل می‌کند

- Type: observed
- Timestamp: 2026-08-08T06:30:00Z–2026-08-08T06:31:54Z
- Scope: نمای باریک مرورگر؛ `/jobs`؛ حساب واردشده Production
- Conditions: همان session با layout ریسپانسیو باریک.
- Confidence: high
- Claim: header به لوگو، منوی همبرگری، حساب و اعلان خلاصه شد؛ کنترل‌های سرچ بالای صفحه فشرده شدند؛ لمس keyword یک سطح جدا با جستجوهای ذخیره‌شده و «ویرایش» باز کرد و با وجود وجود recent history در آن زمان، بخش جستجوهای اخیر را نشان نداد. آیکون فیلتر URL داخلی `/jobs/filters/all` و یک صفحه تمام‌ارتفاع با «حذف همه» و «مشاهده نتایج» باز کرد. انتخاب دورکاری URL را تا «مشاهده نتایج» تغییر نداد و سپس به `/jobs/type/remote?page=1&sort=1` با 1,713 نتیجه رفت.
- Remaining uncertainty: landscape، tablet، چند breakpoint دیگر و accessibility کامل آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-021 — Enter جستجو را submit می‌کند اما Tab فوکوس را از keyword خارج نکرد

- Type: observed
- Timestamp: 2026-08-08T06:36:11Z–2026-08-08T06:36:35Z
- Scope: فیلد keyword در دسکتاپ؛ Production
- Conditions: فیلد ابتدا focus داشت.
- Confidence: medium
- Claim: واردکردن `xyzqwalkthrough1405` و فشردن Enter به URL keyword و empty state رفت. در مقابل، هشت بار Tab از کنترل مرورگر و یک بار Tab مستقیم روی locator، `document.activeElement` را همچنان همان input نگه داشتند.
- Remaining uncertainty: رفتار Tab باید در مرورگر مستقل و با screen reader بازآزمایی شود تا محدودیت automation رد شود.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

## باگ‌های مشکوک

### B-001 — عنوان صفحه پس از جستجوی client-side موقتاً با URL و محتوای جدید هماهنگ نبود

- Timestamp: 2026-08-06T13:17:45Z–2026-08-06T13:17:59Z و 2026-08-08T06:36:35Z–2026-08-08T06:36:45Z
- Scope: رفتن از نتایج قبلی یا عمومی به keyword بدون نتیجه
- Observation: URL و محتوای visible به keyword بدون نتیجه تغییر کرد، اما title ابتدا مقدار قبلی/عمومی را نگه داشت. در بازآزمایی دوم title طی حدود 10 ثانیه بدون نیاز قطعی به refresh اصلاح شد.
- Why it may be a bug: title، URL و state visible برای مدتی ناسازگارند و ممکن است بر accessibility، analytics یا درک tab اثر بگذارد.
- Owner note:

### B-002 — مرتب‌سازی «جدیدترین» عنوان‌های ظاهراً نامرتبط را پیش از عنوان matchشده نشان داد

- Timestamp: 2026-08-06T13:13:23Z–2026-08-06T13:13:31Z و 2026-08-08T06:38:13Z
- Scope: keyword «طراح محصول»؛ sort «جدیدترین»
- Observation: در بازآزمایی، نخستین کارت‌های آگهی شامل «مهندس هوش مصنوعی»، «متخصص سئو و مدیریت وب‌سایت» و «کارشناس فروش و توسعه بازار - خانم» بودند و سپس «طراح UI/UX» دیده شد.
- Why it may be a bug: عنوان‌های بالای لیست match آشکاری با keyword ندارند. broad match، match روی توضیح/شرکت یا trade-off رتبه‌بندی ممکن است عمدی باشد و نیازمند تأیید Owner است.
- Owner note:

### B-003 — کنترل حذف جستجوی ذخیره‌شده هیچ اثر قابل مشاهده‌ای نداشت

- Timestamp: 2026-08-08T06:27:00Z–2026-08-08T06:29:30Z
- Scope: نخستین رکورد `/saved-searches` با عنوان «حسابرسی»
- Observation: دکمه حذف enabled و visible بود، اما کلیک عادی، force click، کلیک مختصاتی، Enter و تعامل مستقیم DOM هیچ modal، toast، تغییر count یا حذف رکوردی ایجاد نکردند. خاموش‌کردن اعلان فقط checkbox را خاموش کرد و رکورد همچنان در فهرست سه‌تایی باقی ماند.
- Why it may be a bug: control عمل حذف را القا می‌کند اما هیچ feedback یا تغییر state ارائه نمی‌دهد؛ داده تستی نیز قابل پاک‌سازی نشد.
- Owner note:

### B-004 — Tab ممکن است داخل فیلد keyword گیر کند

- Timestamp: 2026-08-08T06:36:11Z–2026-08-08T06:36:35Z
- Scope: فیلد keyword؛ دسکتاپ؛ in-app Browser
- Observation: پس از focus روی input، هشت Tab متوالی و یک Tab اضافی از مسیر locator، active element را تغییر ندادند؛ Enter همچنان کار کرد.
- Why it may be a bug: کاربر صفحه‌کلید ممکن است نتواند از فیلد عبور کند. برای حذف احتمال محدودیت automation، بازآزمایی مستقل لازم است.
- Owner note:

## شکاف‌های پوشش

- اجرای موفق حذف جستجوی ذخیره‌شده پس از بررسی B-003 و پاک‌سازی رکورد تستی «حسابرسی» که اکنون اعلانش خاموش است.
- اعتبارسنجی تحویل واقعی اعلان، زمان‌بندی، deduplication و تفاوت ایمیل/پیامک/بله با حساب تست مناسب.
- انتقال Apply به `WT-2026-002` و اجرای آن روی آگهی تست/مجاز، بدون مخلوط‌کردن scope Product Areaها.
- مقایسه authenticated و unauthenticated و variationهای حساب.
- آزمون screen reader، keyboard مستقل و چند breakpoint واقعی موبایل/تبلت.
- آزمون خطای شبکه، retry و offline.
- بررسی B-001 و B-002 با analytics/log و B-004 در مرورگر مستقل.

## پیشنهاد ثبت بعدی

- یک recording کوتاه برای بازتولید B-003 و پاک‌سازی رکورد تستی، سپس recording جدا برای تحویل واقعی اعلان‌ها و accessibility صفحه‌کلید/screen reader.

## خلاصه handoff

تکمیل نشده است. package همچنان `draft` است و همه evidence itemها به تصمیم Owner نیاز دارند. Apply عمداً به `WT-2026-002` واگذار شده است. یک جستجوی ذخیره‌شده تستی با عنوان «حسابرسی» و اعلان خاموش به‌دلیل B-003 در حساب باقی مانده و سه رکورد recent search قبلی طبق مجوز کاربر پاک شده‌اند.
