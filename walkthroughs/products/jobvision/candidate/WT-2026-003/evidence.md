---
walkthrough_id: WT-2026-003
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Resume Management (candidate area)
recorded_at: 2026-08-07
updated_at: 2026-08-08T07:20:00Z
source:
  type: browser-agent
  reference: واکتروی مستقیم محیط Production در مرورگر داخلی Codex؛ مشاهدهٔ اولیه read-only و بازبینی مجدد با مجوز کاربر برای اقدام‌های حساب
reviewed_by: []
reviewed_at:
---

# بسته شواهد واکترو

## زمینه

- Goal: بررسی نقطه‌های ورود مدیریت رزومه برای کارجوی واردشده، stateهای قابل مشاهده، پیش‌نمایش کارفرما، شاخص‌های تکمیل و مرز validation بدون ذخیره‌سازی یا تغییر داده.
- Actor: کارجو
- Role: Candidate
- Authentication state: واردشده
- Account, plan, or configuration: حساب Production دارای رزومهٔ تکمیل‌شده؛ پلن اشتراک و entitlementها بررسی نشد.
- Permissions: سطح دسترسی مشاهده‌شدهٔ Candidate؛ دسترسی متقاطع یا Employer آزموده نشد.
- Environment: Production (`https://jobvision.ir`)
- Starting point: صفحه اصلی و سپس `/my-cv`
- Browser context: مرورگر داخلی Codex؛ نمای دسکتاپ.
- Permitted actions: مشاهده، ناوبری، بازکردن form بدون ذخیره، انتخاب preview و بازکردن نتیجهٔ موجود AI. در بازبینی دوم نیز فقط مشاهده انجام شد.
- Forbidden actions: ذخیره یا حذف دادهٔ رزومه، upload/download، ارسال درخواست، خرید، تغییر privacy، شروع ارزیابی AI یا اقدام اثرگذار بر دادهٔ واقعی.
- Privacy: مقادیر شخصی رزومه در رابط دیده شدند اما عمداً در این package ثبت نشده‌اند.

## پوشش

### پوشش‌داده‌شده

- state ورود Candidate و route مدیریت رزومه از header (`/my-cv`).
- state رزومهٔ موجود و navigation بخش‌ها.
- نشانگر تکمیل کلی و per-section، از جمله بخش‌های اختیاری با درصد صفر.
- نمای Candidate/self در برابر employer preview.
- مشاهدهٔ کنترل‌های add، edit و delete بدون اجرای mutation.
- بازکردن form «درباره من» و بررسی فیلدها تا مرز pre-save.
- بازکردن نتیجهٔ موجود ارزیابی AI بدون شروع ارزیابی تازه.
- مشاهدهٔ کنترل download رزومه بدون آغاز download.

### روایت‌شده ولی نمایش‌داده‌نشده

- موردی وجود ندارد.

### پوشش‌داده‌نشده

- ذخیره، حذف یا تغییر هر دادهٔ رزومه.
- upload رزومه شخصی، portfolio، معرفی صوتی یا فایل دیگر.
- download رزومهٔ تولیدشده یا گزارش AI.
- شروع ارزیابی تازهٔ رزومه با AI.
- پیام‌های validation که به پاک‌کردن یا تغییر مقدار موجود نیاز دارند.
- state رزومهٔ خالی، ناقص یا تازه‌ساخته‌شده.
- persistence پس از mutation یا در device/session دیگر.
- دسترسی Employer از حساب واقعی Employer.
- ارسال درخواست یا representation رزومهٔ متصل به Application.
- خرید، ارتقای پلن، تغییر privacy و visibility configuration.

### نامشخص یا مسدود

- مسیر تعاملی دقیق profile menu ریسپانسیو در automation اولیه قابل اتکا نبود؛ مقصد `/my-cv` از ساختار header صفحه اصلی شناخته و مستقیم باز شد.
- اینکه employer preview دقیقاً با همهٔ سطوح Employer یکسان است نامشخص است؛ فقط preview سمت Candidate دیده شد.
- required-field validation بدون تغییر امن مقادیر موجود یا تلاش برای save قابل آزمون نبود.
- formatهای download، variantهای زبانی و permissionهای download آزموده نشد.

## شواهد

### E-001 — Candidate واردشده از context صفحه اصلی به Resume Management می‌رسد

- Type: observed
- Timestamp: 2026-08-07T17:12:53Z–2026-08-07T17:15:00Z
- Scope: JobVision Candidate، حساب واردشده در Production و header ریسپانسیو صفحه اصلی.
- Conditions: session احراز هویت‌شدهٔ Candidate.
- Confidence: high
- Claim: context صفحه اصلی برای Candidate واردشده مقصد «رزومه من» با route `/my-cv` را نشان می‌دهد و بازکردن آن صفحهٔ Resume Management کارجو را نمایش می‌دهد.
- Remaining uncertainty: sequence دقیق کلیک از profile popover ریسپانسیو در automation اولیه قابل اتکا نبود.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Resume Management یک رزومه را در بخش‌های ساختاریافته با state تکمیل سازمان می‌دهد

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z
- Scope: رزومهٔ موجود و تکمیل‌شده در نمای Candidate.
- Conditions: این حساب state کلی تکمیل‌شده نشان داد؛ نباید به رزومه‌های ناقص تعمیم داده شود.
- Confidence: high
- Claim: Resume Management یک پروفایل حرفه‌ای ساختاریافته با نشانگر تکمیل کلی، نشانگرهای تکمیل per-section و navigation میان هویت، تجربه، مهارت، معرف‌ها، افتخارات، اطلاعات تماس، attachment، portfolio و بخش‌های مربوط به assessment ارائه می‌کند.
- Remaining uncertainty: قواعد محاسبهٔ تکمیل و بخش‌های required آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-003 — نمای self کنترل‌های مدیریت رزومه را نشان می‌دهد

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z–2026-08-07T17:15:53Z
- Scope: نمای self از یک رزومهٔ موجود و تکمیل‌شده.
- Conditions: فقط مشاهده؛ هیچ control تغییر‌دهنده‌ای تأیید نشد.
- Confidence: high
- Claim: در نمای پیش‌فرض «خودم»، صفحه کنار محتوای رزومه controlهای add، edit و delete در سطح بخش را نشان می‌دهد.
- Remaining uncertainty: permission، confirmation، validation و persistence پشت این controlها آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-004 — employer preview کنترل‌های مدیریت را حذف و برخی بخش‌ها را محدود می‌کند

- Type: observed
- Timestamp: 2026-08-07T17:15:27Z و مقایسهٔ کنترل‌شدهٔ بعدی
- Scope: preview «کارفرما» در سمت Candidate روی همان رزومهٔ Production.
- Conditions: preview از صفحه Resume Management انتخاب شد؛ حساب واقعی Employer استفاده نشد.
- Confidence: high
- Claim: تغییر viewer از «خودم» به «کارفرما» controlهای add، edit و delete قابل مشاهده را حذف می‌کند و بخش‌های حرفه‌ای رزومه را قابل خواندن نگه می‌دارد. در این حساب preview کارفرما بخش‌های مخصوص Candidate شامل معرفی صوتی، رزومهٔ شخصی uploadشده و نتایج assessment را حذف کرد، اما بخش اطلاعات تماس را نشان داد.
- Remaining uncertainty: معلوم نیست همهٔ سطح‌های واقعی Employer دقیقاً همین representation را دارند یا plan، Application یا privacy visibility را تغییر می‌دهد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-005 — «درباره من» یک form دوزبانه تا مرز save باز می‌کند

- Type: observed
- Timestamp: 2026-08-07T17:15:53Z
- Scope: بخش «درباره من» در نمای self.
- Conditions: مقادیر موجود بدون تغییر ماندند و form بدون save بسته شد.
- Confidence: medium
- Claim: بخش «درباره من» dialog ویرایش با فیلدهای عنوان شغلی و شرح معرفی فارسی و انگلیسی، فیلد پروفایل LinkedIn و action «ذخیره تغییرات» باز می‌کند.
- Remaining uncertainty: required marker بومی دیده نشد و action ذخیره در state ازپیش‌پرشده enabled بود، اما validation مقدار خالی و ruleهای server-side آزموده نشدند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-006 — نتیجهٔ موجود ارزیابی AI از آغاز ارزیابی تازه جدا است

- Type: observed
- Timestamp: 2026-08-07T17:16:40Z
- Scope: banner دستیار AI در Resume Management Candidate.
- Conditions: حساب نتیجهٔ ارزیابی قبلی داشت؛ ارزیابی تازه شروع نشد.
- Confidence: high
- Claim: Resume Management actionهای جداگانه‌ای برای بازکردن آخرین نتیجهٔ موجود ارزیابی AI و آغاز ارزیابی تازه ارائه می‌کند. بازکردن نتیجهٔ موجود summary تاریخ‌دار ارزیابی را همراه action download گزارش نمایش می‌دهد.
- Remaining uncertainty: معیارهای ارزیابی، ruleهای entitlement، زمان تولید، failure stateها و محتوای گزارش آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-007 — download رزومه یک control مستقل در سطح صفحه است

- Type: observed
- Timestamp: 2026-08-07T17:15:00Z
- Scope: بخش بالایی Resume Management Candidate.
- Conditions: download عمداً آغاز نشد.
- Confidence: high
- Claim: صفحه کنار انتخاب viewer و قابلیت‌های مدیریت رزومه یک control مستقل «دانلود رزومه» نشان می‌دهد.
- Remaining uncertainty: formatهای در دسترس، language selection، generation behavior، permission و failure handling مشاهده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-008 — تکمیل کلی ۱۰۰٪ می‌تواند همراه بخش‌های اختیاری ۰٪ باشد

- Type: observed
- Timestamp: 2026-08-08T07:18:00Z
- Scope: همان رزومهٔ موجود در نمای self؛ Production.
- Conditions: بازبینی read-only، بدون تغییر داده.
- Confidence: high
- Claim: صفحه میزان تکمیل کلی ۱۰۰٪ را نمایش داد، در حالی که بخش‌های اختیاری «معرفی صوتی» و «بارگذاری رزومه شخصی» هرکدام ۰٪ بودند. بنابراین تکمیل کلیِ نمایش‌داده‌شده مستلزم تکمیل این دو بخش اختیاری نیست.
- Remaining uncertainty: وزن‌دهی همهٔ بخش‌ها و اینکه کدام بخش‌ها required هستند هنوز معلوم نیست.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

## باگ‌های مشکوک

- موردی ثبت نشده است. دشواری automation در profile popover ریسپانسیو برای اثبات باگ کاربرمحور کافی نیست.

## شکاف‌های پوشش

- stateهای رزومهٔ ناقص و خالی و قواعد دقیق محاسبهٔ تکمیل.
- validation امن هر بخش قابل ویرایش با دادهٔ disposable.
- رفتار save، cancel، confirmation حذف، error و recovery.
- visibility و privacy رزومه میان Candidate، Employer، Application و resume-bank.
- rendering و permission در حساب واقعی Employer.
- variantهای preview/download رزومهٔ تولیدشده و behavior زبان.
- constraintهای upload، validation فایل، replacement، deletion و download.
- جریان ارزیابی تازهٔ AI، entitlement، progress، failure و تولید گزارش.
- چند رزومه یا language variant، اگر پشتیبانی شود.
- تفاوت رزومهٔ جاری با representation پیوست‌شده به Application.
- پوشش موبایل، keyboard، screen reader و accessibility.

## پیشنهاد واکتروی بعدی

- از یک Candidate disposable با رزومهٔ ناقص برای آزمون required fieldها، محاسبهٔ تکمیل، save/cancel و confirmation حذف استفاده شود.
- یک واکتروی جداگانه و تأییدشده برای download/upload انجام شود تا formatهای تولیدشده، variantهای زبان، سقف فایل و error stateها پوشش یابند.
- خروجی employer preview سمت Candidate با همان رزومه در context واقعی Employer و دادهٔ تست تأییدشده مقایسه شود.
- یک واکتروی Application جدا تعیین کند Employer رزومهٔ زنده را می‌بیند یا snapshot مخصوص Application را.

## Product Areaهای مرتبط

- Primary: JobVision Candidate / Resume Management (candidate area)
- Secondary candidate areas requiring team confirmation: Application Submission و Application Tracking
- Shared concept for later reconciliation only: `shared.resume`

## پیشنهادهای Product Knowledge

- از این package draft برای تغییر canonical Product Knowledge استفاده نشود.
- پس از review Owner، claimهای پذیرفته‌شده ابتدا با Product Area مدیریت رزومهٔ Candidate و سپس با مفهوم shared Resume مقایسه شوند.
- تمایز حل‌نشده میان رزومهٔ جاری و قابل ویرایش با representation مربوط به Application حفظ شود.

## خلاصه handoff

این بخش فقط پس از review Owner تکمیل می‌شود.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: بخش «شکاف‌های پوشش» را ببینید.
- Suggested Product Knowledge scope: Candidate Resume Management؛ مفهوم shared Resume فقط برای معنا و رابطه‌های واقعاً بین‌محصولی.

یک package reviewed منبع تأییدشده برای reconciliation است، اما canonical Product Knowledge نیست و نباید بدون مقایسه با branch جاری `product-knowledge/main` مستقیماً در مستندات محصول کپی شود.
