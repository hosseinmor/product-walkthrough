---
walkthrough_id: WT-2026-007
status: draft
product_group: jobvision
product: candidate
candidate_areas:
  - Company Discovery & Profile (candidate area TBD)
recorded_at: 2026-08-09
source:
  type: direct-browser-audit
  reference: Production browser audit; no screen recording
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: پیدا کردن شرکت‌ها و مشاهدهٔ صفحهٔ عمومی شرکت.
- Actor: کارجوی واردشده.
- Role: Candidate.
- Authentication state: logged in.
- Account, plan, or configuration: حساب موجود؛ جزئیات plan بررسی نشد.
- Permissions: فقط مشاهده و جستجو؛ هیچ follow، امتیازدهی، نظر، Apply یا تغییر داده انجام نشد.
- Environment: Production.
- Starting point: صفحهٔ اصلی `https://jobvision.ir/`.
- Browser / execution environment: Codex In-app Browser.

## Coverage

### Covered

- نقطهٔ ورود قابل‌مشاهده به «آشنایی با شرکت‌ها» از بخش کارجویان در footer صفحهٔ اصلی.
- فهرست شرکت‌ها، فیلترهای قابل‌مشاهده، تعداد نتیجه و مرتب‌سازی.
- جستجوی نام شرکت یا هولدینگ با عبارت «ماموت».
- صفحهٔ عمومی گروه ماموت و اطلاعات، امتیازها، تب‌های قابل‌مشاهده و آگهی‌های آن.

### Narrated but not demonstrated

- هیچ‌کدام.

### Not covered

- اعمال فیلترهای checkbox و «مشاهده بیشتر».
- صفحه‌بندی، empty/error/loading state پس از بارگیری.
- follow کردن، امتیازدهی، ثبت نظر یا تجربهٔ مصاحبه.
- Apply، مشاهدهٔ جزئیات آگهی، یا هر مسیر تغییر‌دهندهٔ داده.
- keyboard، screen reader، mobile و کاربران واردنشده.

### Unclear or blocked

- از DOM مشخص نیست چه کنترل یا containerی برای رفتن از کارت شرکت به پروفایل استفاده می‌شود؛ برای مشاهدهٔ پروفایل از URL عمومی همان نتیجه استفاده شد.
- معنای دقیق «داده کافی وجود ندارد» و قواعد نمایش رتبه/امتیاز بررسی نشد.

## Evidence

### E-001 — دایرکتوری شرکت‌ها از هوم در دسترس است و سطح‌های فیلتر قابل‌مشاهده دارد

- Type: observed
- Timestamp: Browser steps 1–2 (2026-08-09)
- Scope: Candidate واردشده، Production، شروع از هوم.
- Conditions: پس از بارگیری `/companies`، هیچ فیلتر checkboxی اعمال نشد.
- Confidence: high
- Claim: در footer بخش «کارجویان» صفحهٔ اصلی، لینک «آشنایی با شرکت‌ها» به `/companies` دیده می‌شود. صفحهٔ دایرکتوری، جستجوی «نام شرکت یا هولدینگ...» و فیلترهای قابل‌مشاهده برای حوزهٔ فعالیت، استان، اندازهٔ سازمان، موقعیت شغلی باز، مزایا و امکانات و امتیاز شرکت را نمایش می‌دهد؛ در مشاهده، مجموع 143169 شرکت اعلام شد.
- Remaining uncertainty: اثر هر فیلتر، ترکیب فیلترها، persistence و خطاها آزمایش نشد.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — جستجوی شرکت با Enter فهرست و URL را محدود می‌کند

- Type: observed
- Timestamp: Browser step 3 (2026-08-09)
- Scope: Candidate واردشده، Production، دایرکتوری شرکت‌ها.
- Conditions: عبارت «ماموت» در searchbox وارد و Enter فشرده شد؛ فیلتر دیگری اعمال نشد؛ مرتب‌سازی اولیه «بهترین امتیاز» بود.
- Confidence: high
- Claim: پس از اجرای جستجوی «ماموت»، URL شامل `keyword=ماموت` و `pageNumber=1` شد و صفحه 19 شرکت یافت‌شده را نمایش داد. نتیجه‌ها نام شرکت، تعداد موقعیت شغلی فعال و در صورت وجود، امتیاز یا عبارت «داده کافی وجود ندارد» را نشان می‌دهند.
- Remaining uncertainty: جستجوی partial، پاک‌کردن عبارت، debounce، تطبیق حروف و empty state بررسی نشد.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — تغییر مرتب‌سازی در URL منعکس می‌شود

- Type: observed
- Timestamp: Browser step 5 (2026-08-09)
- Scope: Candidate واردشده، Production، نتایج جستجوی «ماموت».
- Conditions: در combobox مرتب‌سازی، «بزرگ‌ترین سازمان» انتخاب شد.
- Confidence: high
- Claim: دایرکتوری یک combobox با گزینه‌های «بهترین امتیاز» و «بزرگ‌ترین سازمان» دارد. انتخاب «بزرگ‌ترین سازمان» در UI به‌عنوان selected نمایش داده شد و URL از `orderBy=0` به `orderBy=1` تغییر کرد.
- Remaining uncertainty: معنای business دقیق orderByها، ترتیب کامل تمام نتایج و persistence پس از refresh بررسی نشد.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — پروفایل عمومی شرکت، اطلاعات ارزیابی و کنترل‌های follow/rating را نمایش می‌دهد

- Type: observed
- Timestamp: Browser step 4 (2026-08-09)
- Scope: Candidate واردشده، Production، صفحهٔ عمومی گروه ماموت.
- Conditions: صفحهٔ `/companies/9432/استخدام-گروه-ماموت` مشاهده شد؛ هیچ کنترل اثرگذار انتخاب نشد.
- Confidence: high
- Claim: پروفایل عمومی مشاهده‌شده برای گروه ماموت نام، امتیاز 4.8، اندازهٔ «بیش از 5000 نفر»، معرفی کوتاه، دکمه‌های «دنبال کنید» و «امتیاز به شرکت»، و بخش‌های فرصت‌های شغلی، درباره شرکت، تجربه مصاحبه، سازمان از نگاه آمار، مراحل استخدام و معرفی اعضای سازمان را نشان می‌دهد. همچنین صنعت، وب‌سایت، شاخص‌های امتیاز سازمان/رضایت کارمندان/تجربه مصاحبه/پاسخگویی به رزومه‌ها و محتوای معرفی سازمان قابل‌مشاهده بود.
- Remaining uncertainty: رفتار و permission کنترل follow/rating، قواعد نمایش هر بخش و تفاوت شرکت‌های دارای دادهٔ ناکافی آزمایش نشد.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — صفحهٔ شرکت، آگهی‌های فعال همان شرکت را فهرست می‌کند

- Type: observed
- Timestamp: Browser step 4 (2026-08-09)
- Scope: Candidate واردشده، Production، صفحهٔ عمومی گروه ماموت.
- Conditions: در همان پروفایل عمومی؛ هیچ آگهی باز یا Apply نشد.
- Confidence: high
- Claim: پروفایل مشاهده‌شده، «فرصت‌های شغلی (52)» و heading «آگهی‌های استخدام گروه ماموت» را نمایش می‌دهد و کارت‌های قابل‌کلیک آگهی را با عنوان، نام شرکت، موقعیت مکانی، زمان انتشار و در برخی موارد signalهای «کارفرمای پاسخگو»، «در حال بررسی رزومه‌ها»، «فوری» یا بازهٔ حقوق نشان می‌دهد.
- Remaining uncertainty: دلیل تفاوت شمار 52 با تعداد linkهای قابل‌مشاهده در viewport، صفحه‌بندی و navigation هر آگهی بررسی نشد.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

- هیچ‌کدام در scope مشاهده‌شده ثبت نشد.

## Coverage gaps

- اعمال و ترکیب فیلترها، reset و shareable URL.
- رفتار کارت/نقطهٔ ورود مستقیم به پروفایل از نتایج.
- follow، rating، review و تجربهٔ مصاحبه با حساب یا دادهٔ تست.
- شرکت بدون امتیاز یا بدون آگهی، empty/error/loading، unauthenticated، accessibility و mobile.

## Recommended follow-up recording

- یک اجرای کنترل‌شده با حساب تست برای follow/unfollow، flow امتیازدهی یا تجربهٔ مصاحبه و اعمال/پاک‌کردن ترکیبی فیلترها؛ بدون ارسال نهایی نظر یا تغییر غیرقابل‌بازگشت.

## Handoff summary

Complete this section only after owner review.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: رفتارهای mutation و ruleهای فیلتر، رتبه و امتیاز.
- Suggested Product Knowledge scope: یک Product Area پیشنهادی «Company Discovery & Profile» در JobVision Candidate؛ ownership نهایی با تیم محصول.
