---
walkthrough_id: WT-2026-004
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Job Search
  - Recommended Jobs & Preferences (candidate area TBD)
recorded_at: 2026-08-07
updated_at: 2026-08-08T07:32:00Z
source:
  type: direct-browser-audit
  reference: واکتروی مستقیم Production در مرورگر داخلی Codex؛ مشاهدهٔ read-only و بازبینی مجدد در حساب واردشده
reviewed_by: []
reviewed_at:
---

# بسته شواهد واکترو

## زمینه

- Goal: ثبت تجربهٔ فعلی Candidate واردشده برای مشاغل پیشنهادی و مرز قابل مشاهدهٔ مدیریت ترجیحات.
- Actor: کارجو
- Role: Candidate
- Authentication state: واردشده
- Account, plan, or configuration: حساب Candidate موجود در Production؛ پلن و پیکربندی گسترده‌تر بررسی نشد.
- Permissions: مشاهدهٔ read-only؛ هیچ تغییر account، preference، notification، saved-job، resume یا application انجام نشد.
- Environment: Production، نمای دسکتاپ مرورگر داخلی Codex
- Starting point: صفحه اصلی JobVision و سپس `/recommended-jobs`
- Safety boundary: توقف پیش از ذخیره یا تغییر preference، تغییر notification، ذخیره شغل، Apply، upload/download، خرید، پیام یا هر اقدام پایدار و اثرگذار بر داده.

## پوشش

### پوشش‌داده‌شده

- نقطه‌های ورود صفحه اصلی برای recommended jobs و نشانه‌های شخصی‌سازی.
- صفحهٔ مستقل Recommended Jobs و دو حالت recommendation قابل مشاهده.
- اطلاعات کارت‌های شغلی، actionهای قابل مشاهده و pagination.
- sort در حالت مرتبط با علایق و pagination در حالت احتمال استخدام بالاتر.
- summary read-only preference و مرز entry ویرایش.
- controlها و پیام‌های notification بدون تغییر state.
- بازبینی read-only وضعیت فعلی summary و notification.

### روایت‌شده ولی نمایش‌داده‌نشده

- موردی وجود ندارد.

### پوشش‌داده‌نشده

- ذخیرهٔ تغییرات preference.
- dismiss یا تکمیل راهنمای onboarding ترجیحات.
- فعال/غیرفعال‌کردن notification، تحویل آن یا persistence.
- ذخیره یا حذف saved job.
- بازکردن Job Post در detail.
- Apply یا ارسال resume.
- رفتار recommendation در حساب، role، authentication state، plan یا empty-data state دیگر.
- mobile، responsive، keyboard-only و assistive technology.
- منطق ranking backend، inputهای مدل، cadence refresh و persistence recommendation.

### نامشخص یا مسدود

- رابطهٔ دقیق preferenceهای صریح، رفتار/عملکرد مشاهده‌شده و دو حالت recommendation.
- persistent یا session-only بودن onboarding guide.
- امکان رسیدن به editor بدون acknowledge guide.
- رابطهٔ control notification در settings و prompt inline فعال‌سازی.
- validation، cancellation و unsaved-change behavior در preference editor.

## شواهد

### E-001 — صفحه اصلی برای Candidate نقطه‌های ورود recommendation شخصی‌سازی‌شده دارد

- Type: observed
- Timestamp: 2026-08-07T17:52:52.981Z
- Scope: Candidate واردشده در صفحه اصلی Production.
- Conditions: حساب Candidate دارای محتوای شخصی‌سازی‌شده.
- Confidence: high
- Claim: صفحه اصلی واردشده، entry اصلی مشاغل پیشنهادی و یک module شغلی شخصی‌سازی‌شده را نمایش می‌دهد. module نشانه‌هایی از علایق، احتمال استخدام، شیوهٔ کار، نزدیکی و رفتار/عملکرد مبتنی بر AI دارد.
- Remaining uncertainty: منطق ranking و معنای دقیق یا eligibility هر cue قابل مشاهده نبود.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Recommended Jobs دو حالت recommendation متمایز دارد

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z؛ 2026-08-07T17:53:37.639Z
- Scope: تجربهٔ Recommended Jobs برای Candidate واردشده.
- Conditions: ورود از navigation صفحه اصلی.
- Confidence: high
- Claim: تجربهٔ Recommended Jobs recommendationها را به حالت «مرتبط با علایق» و «با احتمال استخدام بالاتر» تفکیک می‌کند. هر حالت count فرصت خود و مبنای توضیحی متفاوتی برای فهرست دارد.
- Remaining uncertainty: ruleهای ورود، حذف یا ترتیب‌دادن فرصت‌ها در هر حالت قابل مشاهده نبود.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-003 — کارت‌های recommendation اطلاعات ارزیابی و actionهای اثرگذار بر حساب را نمایش می‌دهند

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z؛ 2026-08-07T17:53:37.639Z
- Scope: کارت‌های visible در هر دو حالت recommendation.
- Conditions: Candidate واردشده، Production.
- Confidence: high
- Claim: کارت‌ها context شغل و کارفرما مانند عنوان، سازمان، مکان و زمان انتشار و metadataهای شرطی مانند حقوق، شیوهٔ کار، فوریت، پاسخ‌گو بودن کارفرما یا بررسی فعال رزومه را نشان می‌دهند. هر کارت control ذخیره شغل و آغاز ارسال رزومه دارد.
- Remaining uncertainty: persistence ذخیره، action تکراری، eligibility Apply و flow مقصد اجرا نشدند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-004 — recommendationهای مرتبط با علایق سه حالت sort دارند

- Type: observed
- Timestamp: 2026-08-07T17:54:14.580Z–2026-08-07T17:54:28.215Z
- Scope: فهرست recommendation مرتبط با علایق.
- Conditions: Candidate واردشده، Production.
- Confidence: high
- Claim: این فهرست sortهای جدیدترین، مرتبط‌ترین و بیشترین حقوق را ارائه می‌کند. تغییر انتخاب query state صفحه را تغییر داد و در پایان selection پیش‌فرض مرتبط‌ترین بازگردانده شد.
- Remaining uncertainty: tie-breaking، شغل‌های بدون حقوق و persistence انتخاب میان sessionها آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-005 — نتایج recommendation صفحه‌بندی دارند

- Type: observed
- Timestamp: 2026-08-07T17:53:57.924Z
- Scope: فهرست recommendation احتمال استخدام بالاتر.
- Conditions: حساب بیش از یک صفحه نتیجه داشت.
- Confidence: high
- Claim: فهرست pagination شماره‌دار و control صفحه آخر دارد. انتخاب صفحه 2 URL را با query parameterهای page و sort تغییر می‌دهد و مجموعهٔ دیگری از کارت‌ها را بارگذاری می‌کند.
- Remaining uncertainty: behavior صفحه آخر، بازگردانی Back/Forward و pagination پس از تغییر داده آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-006 — summary ترجیحات، inputهای مؤثر بر recommendation را گروه‌بندی می‌کند

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z
- Scope: preference summary در صفحه Recommended Jobs.
- Conditions: preferenceهای موجود حساب دیده شدند اما مقدارهای شخصی عمداً در package ثبت نشده‌اند.
- Confidence: high
- Claim: صفحه summary read-only ترجیحات recommendation را در گروه‌های استان‌های مطلوب، حوزه‌های شغلی مطلوب، نوع همکاری مطلوب و تمایل دورکاری/حضوری همراه entry ویرایش نشان می‌دهد.
- Remaining uncertainty: required fieldها، limit انتخاب، dependency میان fieldها و اثر هر preference بر recommendation قابل مشاهده نبود.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-007 — ویرایش preference در این state حساب با onboarding زمینه‌ای آغاز می‌شود

- Type: observed
- Timestamp: 2026-08-07T17:53:07.639Z–2026-08-07T17:53:08.404Z
- Scope: entry ویرایش preference در Recommended Jobs.
- Conditions: حساب واردشده؛ onboarding state پیش‌تر تثبیت نشده بود.
- Confidence: medium
- Claim: فعال‌سازی entry ویرایش ابتدا guidance زمینه‌ای نمایش می‌دهد که توضیح می‌دهد preferenceها برای پیشنهاد شغل شخصی‌سازی‌شده استفاده می‌شوند و action acknowledge دارد، نه اینکه editor را بی‌درنگ باز کند.
- Remaining uncertainty: guide acknowledge نشد؛ editor، cancellation path و save validation آزموده نشدند.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-008 — controlهای notification کنار recommendation و preference قرار دارند

- Type: observed
- Timestamp: 2026-08-07T17:52:56.145Z
- Scope: فهرست Recommended Jobs و منطقه summary preference.
- Conditions: Candidate واردشده، Production.
- Confidence: high
- Claim: صفحه پیام‌های notification را در دو محل نشان می‌دهد: prompt inline برای دریافت فرصت‌های مطلوب از email یا SMS و control settings برای دریافت email و SMS مشاغل پیشنهادی.
- Remaining uncertainty: رابطهٔ دو control، granularity کانال، delivery state، consent و persistence آزموده یا ثبت نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-009 — prompt inline و notification settings هم‌زمان در state فعال قابل مشاهده‌اند

- Type: observed
- Timestamp: 2026-08-08T07:30:00Z
- Scope: فهرست «مرتبط با علایق» و preference settings؛ Production.
- Conditions: بازبینی read-only؛ هیچ control notification تغییر نکرد.
- Confidence: high
- Claim: در بازبینی، checkbox settings با برچسب «دریافت ایمیل و پیامک فرصت‌های شغلی پیشنهادی» checked بود و در همان صفحه prompt inline «فعال سازی اطلاع‌رسانی شغلی» نیز دیده می‌شد.
- Remaining uncertainty: prompt inline ممکن است مسیر یا سطح notification متفاوتی داشته باشد؛ بدون تعامل نمی‌توان آن را ناسازگاری یا defect دانست.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

## باگ‌های مشکوک

- موردی ثبت نشده است. رابطهٔ onboarding و controlهای notification تا روشن‌شدن semantics با Owner یا آزمون کنترل‌شده، defect تلقی نمی‌شود.

## شکاف‌های پوشش

- fieldهای preference editor، validation، cancel و نتیجه save به حساب disposable یا تغییر state کنترل‌شده نیاز دارد.
- activation/deactivation و delivery notification به حساب تست و channelهای ازپیش‌تأییدشده نیاز دارد.
- saved-job و Apply به walkthroughهای bounded جدا نیاز دارند.
- empty state، refresh، توضیح ranking و variationهای account/plan آزموده نشده‌اند.
- mobile، keyboard و accessibility آزموده نشده‌اند.

## پیشنهاد واکتروی بعدی

- با حساب disposable یا test-safe، onboarding guide acknowledge شود، editor کامل بررسی و validation/cancellation آزموده شود و update recommendation بدون افشای مقدارهای شخصی سنجیده شود.
- opt-in/out notification و رفتار channelها با contact pointهای test و ازپیش‌تأییدشده جداگانه آزموده شود.
- پس از فهم جریان desktop editor، variantهای mobile و keyboard-only ثبت شوند.

## خلاصه handoff

این بخش فقط پس از review Owner تکمیل می‌شود.

- Package status: draft
- Accepted evidence IDs: none
- Edited evidence IDs: none
- Rejected evidence IDs: none
- Remaining unknowns: behavior و semantics preference edit، notification، ranking، persistence، empty state، variationهای account/plan و accessibility.
- Suggested Product Knowledge scope: Candidate Job Search و یک Product Area احتمالی Recommended Jobs & Preferences، مشروط به تأیید Product Owner.

یک package reviewed منبع تأییدشده برای reconciliation است، اما canonical Product Knowledge نیست و نباید بدون مقایسه با branch جاری `product-knowledge/main` مستقیماً در مستندات محصول کپی شود.
