---
walkthrough_id: WT-2026-006
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Application Management (candidate area TBD)
recorded_at: 2026-08-07
updated_at: 2026-08-08T07:55:00Z
source:
  type: browser-agent
  reference: واکتروی مستقیم و read-only محیط Production در https://jobvision.ir
reviewed_by: []
reviewed_at:
---

# بسته شواهد واکترو

## زمینه

- Goal: بررسی یافتن، مرور، فیلتر و مدیریت درخواست‌های قبلاً ارسال‌شدهٔ کارجوی واردشده.
- Actor: کارجو
- Role: Candidate واردشده؛ entitlement دقیق حساب نامشخص است.
- Authentication state: واردشده
- Account, plan, or configuration: حساب Production با درخواست‌های تاریخی؛ plan و permission ویژه بررسی نشد.
- Permissions: فقط دسترسی visible عادی Candidate مشاهده شد.
- Environment: Production
- Starting point: صفحه اصلی JobVision
- Safety constraints: read-only؛ انصراف، ویرایش رزومه ارسالی، rejection feedback، تغییر My Priority، پیام، profile/resume edit، خرید و اقدام اثرگذار انجام نشد.

## پوشش

### پوشش‌داده‌شده

- entry منوی حساب به درخواست‌های ارسال‌شده.
- status filterهای درخواست فعال و badgeهای اختصاصی حساب.
- empty state یک status بدون درخواست.
- sort درخواست‌های فعال، جزئیات بازشونده، گروه closed و pagination.
- مشاهدهٔ read-only controlهای edit و withdrawal.
- promptهای feedback درخواست ردشده و FAQ وضعیت‌ها.
- توضیح و quota قابل مشاهدهٔ My Priority بدون تغییر آن.

### روایت‌شده ولی نمایش‌داده‌نشده

- موردی وجود ندارد.

### پوشش‌داده‌نشده

- اجرای یا تأیید withdrawal.
- ویرایش resume متصل به درخواست.
- انتخاب/حذف My Priority یا تغییر introduction letter.
- submit feedback رد یا مصاحبه.
- بازکردن/Apply برای شغل مشابه.
- نمونه‌های initial evaluation، final evaluation یا withdrawn.
- empty-account، role/plan دیگر، mobile، keyboard و screen reader.

### نامشخص یا مسدود

- confirmation، برگشت‌پذیری و سرعت update withdrawal.
- snapshot یا live بودن resume ارسالی برای Employer.
- persistence و optional/required بودن rejection feedback.
- نمایش My Priority سمت Employer و variation quota بر حسب plan.
- اینکه All filter در همه contextها closedها را حذف می‌کند یا نه.

## شواهد

### E-001 — درخواست‌های ارسال‌شده از account menu قابل دسترسی‌اند
- Type: observed
- Timestamp: 2026-08-07 19:37:51–19:38:01 +03:30
- Confidence: high
- Claim: account menu Candidate entry «رزومه های ارسال شده» دارد که به `/my-applications` می‌رود و heading صفحه workspace درخواست‌های ارسال‌شده را مشخص می‌کند.
- Remaining uncertainty: layoutهای دیگر و unauthenticated آزموده نشد.

### E-002 — صفحه درخواست‌ها را با filterهای lifecycle تفکیک می‌کند
- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:38:44 +03:30
- Confidence: high
- Claim: filterهای همه، دریافت‌شده توسط کارفرما، ارزیابی اولیه، ارزیابی نهایی، ردشده، انصراف‌داده‌شده و آگهی‌های بسته وجود دارد؛ انتخاب filter فهرست را محدود و status را در URL ثبت می‌کند.
- Remaining uncertainty: status model server-side و stateهای وابسته به permission تأیید نشد.

### E-003 — summary درخواست، status و signal زمانی را نشان می‌دهد
- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:39:57 +03:30
- Confidence: high
- Claim: هر summary visible شغل، کارفرما، status فعلی و زمان نسبی ارسال را نشان می‌دهد و در صورت وجود، زمان مشاهدهٔ درخواست توسط کارفرما را نیز نشان می‌دهد.
- Remaining uncertainty: شرط حذف viewed timestamp مشخص نیست.

### E-004 — filter خالی توضیح state مورد انتظار را می‌دهد
- Type: observed
- Timestamp: 2026-08-07 19:38:34 +03:30
- Confidence: high
- Claim: وقتی status filter نتیجه ندارد، متن توضیحی می‌گوید کدام transition کارفرما درخواست را به این بخش می‌آورد.
- Remaining uncertainty: متن empty state همه statusها دیده نشد.

### E-005 — درخواست‌های آگهی بسته جدا و صفحه‌بندی‌شده‌اند
- Type: observed
- Timestamp: 2026-08-07 19:38:44–19:38:54 +03:30
- Confidence: high
- Claim: درخواست‌های آگهی بسته filter اختصاصی و pagination دارند؛ رفتن به page دیگر parameter صفحه را در URL تغییر و cardهای تاریخی متفاوتی را load می‌کند.
- Remaining uncertainty: page size و page آخر کامل بررسی نشد.

### E-006 — درخواست‌های فعال بر مبنای تاریخ درخواست یا تصمیم status sort می‌شوند
- Type: observed
- Timestamp: 2026-08-07 19:40:08 +03:30
- Confidence: high
- Claim: فهرست فعال sort بر اساس تاریخ درخواست و تاریخ تصمیم status دارد؛ تغییر انتخاب order و `sortType` URL را تغییر می‌دهد.
- Remaining uncertainty: direction و tie-breaker نامشخص است.

### E-007 — جزئیات درخواست فعال اطلاعات مدیریت را نشان می‌دهد
- Type: observed
- Timestamp: 2026-08-07 19:39:30–19:39:49 +03:30
- Confidence: high
- Claim: expand یک درخواست فعال می‌تواند آخرین بازدید کارفرما از درخواست‌های آن شغل، introduction letter موجود و controlهای ویرایش resume ارسالی و withdrawal را نشان دهد.
- Remaining uncertainty: validation، confirmation، persistence و اثر downstream هیچ actionی آزموده نشد.

### E-008 — UI می‌گوید withdrawal فقط پیش از مشاهده رزومه مجاز است
- Type: observed
- Timestamp: 2026-08-07 19:40:31 +03:30
- Confidence: medium
- Claim: FAQ می‌گوید Candidate فقط تا زمانی که سازمان resume را ندیده باشد می‌تواند درخواست قبلی را withdraw کند.
- Remaining uncertainty: enforcement، race condition و exceptionها آزموده نشد.

### E-009 — درخواست ردشده feedback فرایند را می‌پرسد
- Type: observed
- Timestamp: 2026-08-07 19:39:57 +03:30
- Confidence: high
- Claim: expand درخواست ردشده، زمان مشاهده توسط کارفرما را نشان می‌دهد و از Candidate stage ردشدن و وقوع مصاحبه را می‌پرسد.
- Remaining uncertainty: trigger، optionality، persistence و کاربرد feedback مشخص نیست.

### E-010 — FAQ معنای statusهای اصلی را توضیح می‌دهد
- Type: observed
- Timestamp: 2026-08-07 19:40:17 +03:30
- Confidence: medium
- Claim: FAQ Received by employer، Initial evaluation، Final evaluation، Rejected و Closed را به‌عنوان stateهای employer-driven توضیح می‌دهد.
- Remaining uncertainty: FAQ Withdrawn را تعریف نمی‌کند.

### E-011 — جزئیات میان زمان مشاهده درخواست و activity کارفرما تمایز می‌گذارد
- Type: observed
- Timestamp: 2026-08-07 19:40:42 +03:30
- Confidence: medium
- Claim: صفحه میان زمان مشاهدهٔ درخواست Candidate توسط کارفرما و آخرین بازدید کارفرما از پنل درخواست‌های دریافتی همان شغل تمایز می‌گذارد.
- Remaining uncertainty: cadence refresh و دقت data source آزموده نشد.

### E-012 — feedback رد کارفرما optional و ممکن است غایب باشد
- Type: observed
- Timestamp: 2026-08-07 19:41:09 +03:30
- Confidence: medium
- Claim: FAQ می‌گوید کارفرما می‌تواند reason یا feedback رد را ثبت کند، اما در نبود آن بخش جزئیات خالی می‌ماند.
- Remaining uncertainty: format، moderation، editability و notification آزموده نشد.

### E-013 — My Priority سهمیهٔ دوره‌ای محدود برای متمایزکردن درخواست است
- Type: observed
- Timestamp: 2026-08-07 19:38:01–19:40:08 +03:30
- Confidence: medium
- Claim: UI می‌گوید Candidate می‌تواند برخی درخواست‌های ارسال‌شده را My Priority کند تا resume برای کارفرما متمایز شود و introduction letter داشته باشد؛ سهمیهٔ پنج انتخاب در هر ۳۰ روز و remaining allowance/renewal زمان‌دار نمایش داده می‌شود.
- Remaining uncertainty: eligibility، presentation Employer، removal و quota enforcement آزموده نشد.

## باگ‌های مشکوک

### B-001 — terminology filter و application card متفاوت است
- Observation: filter «دریافت‌شده توسط کارفرما» بود اما card همان نتیجه status معادل «وضعیت تعیین نشده» نشان داد.
- Why it may be a bug: دو label ظاهراً به یک state اشاره دارند اما معنای متفاوتی می‌رسانند.
- Owner note:

### B-002 — FAQ status، Withdrawn را تعریف نمی‌کند
- Observation: Withdrawn filter دارد اما FAQ سایر statusهای اصلی را توضیح می‌دهد و آن را جا می‌اندازد.
- Why it may be a bug: help content نسبت به taxonomy visible ناقص است.
- Owner note:

### B-003 — چند control interactive role semantic استاندارد ندارند
- Observation: status filterها link بدون مقصد، expand card icon خام و edit/withdraw container clickable بودند.
- Why it may be a bug: keyboard operability و screen-reader clarity کاهش می‌یابد؛ آزمون accessibility مستقل لازم است.
- Owner note:

## شکاف‌های پوشش

- withdrawal امن با confirmation، cancel، update و reversibility.
- edit resume ارسالی و تشخیص snapshot در برابر live resume.
- نمونه cardهای initial/final/withdrawn.
- My Priority، validation نامه، removal، quota و visibility Employer.
- rejection feedback و persistence آن.
- empty account، mobile، keyboard و screen reader.
- تأیید terminology و FAQ با Product Owner.

## پیشنهاد واکتروی بعدی

- با Candidate disposable و posting تأییدشدهٔ Employer، withdrawal و edit resume بدون اثر بر کارفرمای واقعی آزموده شود.
- با accountهای زوج Candidate/Employer همهٔ transitionها، feedback، viewed timestamp و My Priority end-to-end ثبت شود.
- keyboard و screen-reader برای filterها، expand card و actionهای مدیریت جداگانه آزموده شود.

## Product Areaهای مرتبط

- Primary: JobVision Candidate / Application Management
- Secondary: Job Details & Evaluation، Resume Management و Premium Insights
- Shared concept: `shared.application`

## پیشنهادهای Product Knowledge

- این package draft برای تغییر canonical Product Knowledge مجاز نیست.
- پس از review Owner، ایجاد Product Area مستقل Application Management با outcome درک state و مدیریت امن درخواست‌های ارسال‌شده بررسی شود.
- تمایز current resume و Application-associated resume، transitionها، visibility Employer و ruleهای quota تا evidence زوج Candidate/Employer یا تصمیم Owner نامشخص بماند.

## خلاصه handoff

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: شکاف‌های پوشش و uncertainty هر شاهد.
- Suggested Product Knowledge scope: پس از review Owner و مقایسه با Product Knowledge جاری.

یک package reviewed منبع تأییدشده برای reconciliation است، اما canonical Product Knowledge نیست و نباید بدون مقایسه با `product-knowledge/main` مستقیماً در مستندات محصول کپی شود.
