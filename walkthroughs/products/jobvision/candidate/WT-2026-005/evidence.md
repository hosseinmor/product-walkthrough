---
walkthrough_id: WT-2026-005
status: draft
product_group: JobVision
product: Candidate
candidate_areas:
  - Job Details & Evaluation
recorded_at: 2026-08-08T05:26:45Z
updated_at: 2026-08-08T07:45:00Z
source:
  type: browser-audit
  reference: واکتروی Production روی jobvision.ir؛ بازبینی مستقیم در مرورگر داخلی و بدون نگه‌داری screenshot
reviewed_by: []
reviewed_at:
---

# بسته شواهد واکترو

## زمینه

- Goal: بررسی جریان Saved Jobs کارجوی واردشده از صفحه اصلی، شامل نقطه‌های ورود، stateهای قابل مشاهده، نتیجه navigation و مرزهای امن save/remove.
- Actor: کارجو
- Role: Candidate واردشده
- Authentication state: واردشده
- Account, plan, or configuration: حساب Production؛ Saved Jobs ابتدا خالی بود و سپس با اجازه صریح کاربر یک Job Post جاری ذخیره شد. پلن بررسی نشد.
- Permissions: دسترسی عادی Candidate؛ سطح دسترسی elevated آزموده نشد.
- Environment: Production، نمای دسکتاپ مرورگر داخلی
- Starting point: صفحه اصلی JobVision
- Permitted actions: مشاهده و با اجازهٔ صریح قبلی، ذخیرهٔ یک Job Post جاری. بازبینی این نوبت read-only بود.
- Forbidden actions: حذف saved job، Apply، تغییر profile/resume، upload/download، خرید، پیام و تغییر notification.

## پوشش

### پوشش‌داده‌شده

- entry Saved Jobs در account menu و جدایی آن از Saved Searches.
- navigation صفحه Saved Jobs و جایگاه آن در activity navigation Candidate.
- empty state و guidance آن.
- بررسی entryهای save با icon bookmark در card و detail.
- یک save action مجاز و transition کنترل.
- transition empty state به فهرست تک‌موردی.
- persistence همان مورد پس از refresh.
- accessibility signalهای visible کنترل save.

### روایت‌شده ولی نمایش‌داده‌نشده

- موردی وجود ندارد.

### پوشش‌داده‌نشده

- ordering، pagination، filter یا sort فراتر از فهرست تک‌موردی.
- navigation با فعال‌کردن link Job Post از Saved Jobs.
- remove saved Job Post.
- persistence پس از sign-out/sign-in، browser session یا device دیگر.
- save/remove تکراری.
- Job Post بسته، منقضی، حذف‌شده یا unavailable.
- خطای network/loading، retry یا recovery.
- unauthenticated و بازگشت پس از login.
- mobile، responsive، keyboard-only و assistive technology.
- variationهای account یا plan.

### نامشخص یا مسدود

- حساب در ابتدا هیچ Job Post ذخیره‌شده‌ای نداشت؛ فقط state تک‌موردی پس از save مجاز مشاهده شد.
- remove در این بسته اجرا نشد؛ اگرچه کاربر اکنون اختیار گسترده‌تر داده است، برای جلوگیری از حذف دادهٔ موجود به آزمون جداگانه و هدفمند واگذار می‌شود.
- پس از save toast یا status message قابل مشاهده‌ای دیده نشد.
- confirmation حذف، recovery و persistence بلندمدت نامشخص‌اند.
- فعال‌سازی link فهرست در browser automation این نوبت navigation ایجاد نکرد؛ به‌تنهایی برای ثبت defect کافی نیست.

## شواهد

### E-001 — Saved Jobs entry مستقل در account menu دارد

- Type: observed
- Timestamp: 2026-08-08T05:26:45Z
- Scope: Candidate واردشده در صفحه اصلی Production.
- Conditions: account menu باز شد؛ state حساب تغییر نکرد.
- Confidence: high
- Claim: account menu لینک «مشاغل نشان‌شده» را به `/saved-jobs` نمایش می‌دهد.
- Remaining uncertainty: entryهای دیگر و variation نقش/حساب آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Saved Jobs از Saved Searches جداست

- Type: observed
- Timestamp: 2026-08-08T05:26:45Z
- Scope: account menu Candidate واردشده.
- Conditions: menu از صفحه اصلی باز شد.
- Confidence: high
- Claim: account menu «مشاغل نشان‌شده» (`/saved-jobs`) و «جستجوهای ذخیره شده» (`/saved-searches`) را مقصدهای جداگانه نمایش می‌دهد.
- Remaining uncertainty: رابطه آن‌ها جز جدا بودن routeها آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-003 — Saved Jobs جزئی از activity navigation Candidate است

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: Candidate واردشده در `/saved-jobs`.
- Conditions: navigation از account menu صفحه اصلی آغاز شد.
- Confidence: high
- Claim: Saved Jobs کنار رزومه‌های ارسال‌شده، مشاغل پیشنهادی و شرکت‌های دنبال‌شده در navigation فعالیت Candidate قرار دارد و در route خودش visually selected است.
- Remaining uncertainty: navigation از مقصدهای دیگر اجرا نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-004 — empty state کاربرد مجموعه و نقطه save را توضیح می‌دهد

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: حساب واردشده بدون Job Post ذخیره‌شده.
- Conditions: `/saved-jobs` در Production کامل load شد.
- Confidence: high
- Claim: وقتی مجموعه خالی است، صفحه اعلام می‌کند مشاغل نشان‌شده در این بخش می‌آیند و Candidate را به استفاده از icon بالای Job Post برای ذخیره‌سازی راهنمایی می‌کند.
- Remaining uncertainty: CTA جداگانه در viewport یا configuration دیگر آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-005 — سطح‌های Job Post entry save مبتنی بر bookmark دارند

- Type: observed
- Timestamp: 2026-08-08T05:27:28Z–2026-08-08T05:29:02Z
- Scope: card صفحه اصلی و یک Job Post جاری در detail.
- Conditions: هیچ controlی در این بخش فعال نشد.
- Confidence: high
- Claim: cardها control bookmark با icon توخالی دارند و Job Post detail بررسی‌شده نیز control bookmark اصلی را نشان می‌دهد.
- Remaining uncertainty: remove، action تکراری، persistence و feedback contextهای دیگر آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-006 — کنترل‌های سراسری Job Search در Saved Jobs باقی می‌مانند

- Type: observed
- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:27:16Z
- Scope: Candidate واردشده در Saved Jobs خالی.
- Conditions: Production.
- Confidence: high
- Claim: صفحه Saved Jobs inputهای سراسری عنوان شغل/شرکت، گروه شغلی و شهر و action جستجو را بالای activity navigation نگه می‌دارد.
- Remaining uncertainty: submit جستجو و return behavior نسبت به Saved Jobs آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-007 — ذخیره Job Post جاری state bookmark را تغییر می‌دهد

- Type: observed
- Timestamp: 2026-08-08T05:34:36Z
- Scope: یک Job Post جاری در detail، حساب Candidate واردشده.
- Conditions: کاربر صریحاً ذخیره یک شغل را مجاز کرد؛ Apply یا اقدام دیگری انجام نشد.
- Confidence: high
- Claim: فعال‌سازی control ذخیره icon را از bookmark توخالی secondary به bookmark توپر primary تغییر داد.
- Remaining uncertainty: toast قابل مشاهده نبود؛ reload و persistence بین sessionها آن زمان آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-008 — Job Post تازه‌ذخیره‌شده در Saved Jobs ظاهر می‌شود

- Type: observed
- Timestamp: 2026-08-08T05:34:57Z
- Scope: همان حساب در `/saved-jobs`.
- Conditions: یک Job Post جاری همان لحظه ذخیره شده بود.
- Confidence: high
- Claim: پس از save، empty-state ناپدید شد و Saved Jobs یک link Job Post مطابق مورد ذخیره‌شده داشت؛ card آن bookmark توپر primary نشان داد.
- Remaining uncertainty: ordering، pagination، filter، بازکردن link، remove و persistence بلندمدت آزموده نشد.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

### E-009 — Job Post ذخیره‌شده پس از refresh باقی می‌ماند

- Type: observed
- Timestamp: 2026-08-08T07:42:00Z
- Scope: همان Candidate واردشده در `/saved-jobs`.
- Conditions: بازبینی read-only؛ صفحه پس از مشاهدهٔ فهرست تک‌موردی refresh شد.
- Confidence: high
- Claim: پس از refresh، همان card و link Job Post همچنان در Saved Jobs قابل مشاهده بود؛ بنابراین save دست‌کم در refresh همان session پایدار است.
- Remaining uncertainty: persistence در session، device یا login دیگر آزموده نشده است.

#### بررسی Owner

- Decision: pending
- Final claim:
- Owner note:

## باگ‌های مشکوک

### B-001 — متن empty state از heart نام می‌برد اما کنترل‌های visible bookmark هستند

- Timestamp: 2026-08-08T05:26:57Z–2026-08-08T05:29:02Z
- Scope: empty Saved Jobs و سطح‌های Job Post جاری.
- Observation: empty state کاربر را به کلیک icon قلب راهنمایی می‌کند، اما controlهای بررسی‌شده icon bookmark توخالی دارند.
- Why it may be a bug: متن راهنما و iconography قابل مشاهده هم‌خوان نیستند و تشخیص save action را سخت می‌کنند.
- Owner note: اصطلاح و icon مورد انتظار نیازمند تأیید است.

### B-002 — controlهای save نام accessibility ندارند

- Timestamp: 2026-08-08T05:27:28Z–2026-08-08T05:29:02Z
- Scope: card صفحه اصلی و Job Post detail بررسی‌شده.
- Observation: bookmark card button متن visible، `aria-label` یا `title` نداشت. bookmark اصلی detail icon داخل `div` clickable بدون role semantic، accessible name یا keyboard tabindex بود.
- Why it may be a bug: screen-reader و keyboard user ممکن است نتوانند action ذخیره را به‌طور قابل اتکا بشناسند یا اجرا کنند.
- Owner note: baseline مورد انتظار accessibility باید تأیید شود.

## شکاف‌های پوشش

- navigation فهرست با link Job Post
- remove state transition و persistence بلندمدت
- Job Post بسته، منقضی، حذف‌شده و unavailable
- feedback و recovery خطای save/remove
- unauthenticated و login return
- responsive، mobile، keyboard و assistive technology
- variationهای account و plan

## پیشنهاد واکتروی بعدی

- با حساب Production-safe یا staging و Job Post فعال/بسته، remove و recovery/persistence آزموده شود.
- flow با keyboard-only و viewport موبایل تکرار شود.

## خلاصه handoff

این بخش فقط پس از review Owner تکمیل می‌شود.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: شکاف‌های پوشش را ببینید.
- Suggested Product Knowledge scope: JobVision Candidate / Job Details & Evaluation.

یک package reviewed منبع تأییدشده برای reconciliation است، اما canonical Product Knowledge نیست و نباید بدون مقایسه با branch جاری `product-knowledge/main` مستقیماً در مستندات محصول کپی شود.
