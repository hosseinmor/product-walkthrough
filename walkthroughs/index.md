# Walkthrough Registry

This is the central index for walkthrough planning, package status, and product-area coverage. It helps select the next bounded scope, prevents duplicate IDs, and keeps known gaps visible.

The registry is operational metadata, not product evidence or canonical Product Knowledge. Do not copy claims from earlier packages into this file or use registry entries to complete a new extraction.

## Status model

- `planned` — the ID and bounded scope are reserved; extraction has not produced a package.
- `draft` — evidence has been extracted, but owner review is incomplete.
- `reviewed` — every evidence item has an owner decision and edited items have complete final claims.
- `handed-off` — the reviewed package has entered Product Knowledge reconciliation; record the proposal or pull request in notes.
- `cancelled` — the walkthrough stopped intentionally; keep the row so its ID is not reused.

Only `draft` and `reviewed` are evidence-package statuses. `planned`, `handed-off`, and `cancelled` describe the wider walkthrough lifecycle in this registry.

## Coverage model

- `not-assessed` — no extraction result exists yet.
- `partial` — the walkthrough covered meaningful behavior, but one or more paths, roles, states, or conditions in its bounded scope remain untested or unclear.
- `complete-for-scope` — the intended bounded scope was covered with no known gaps. This never means the whole product area is complete.

Coverage is an audit-planning assessment, not evidence confidence or owner approval. Record meaningful remaining gaps in the registry instead of inflating coverage.

## Product-area coverage

Use one row per product area. Base the summary only on registered walkthrough metadata and reviewed package coverage sections.

| Product group | Product | Product area | Coverage | Reviewed walkthroughs | Known gaps / next scope |
| --- | --- | --- | --- | --- | --- |
| JobVision | Candidate | Job Search (candidate area) | `partial` | — | پیش‌نویس WT-2026-001 اکنون جستجوی واردشده، مدل و اعمال نمونه‌ای فیلترهای پیشرفته، صفحه‌بندی و history، URL اشتراک‌پذیر، ذخیره جستجو و اعلان، پاک‌کردن history، نمای موبایل و بخشی از keyboard را پوشش می‌دهد؛ WT-2026-004 سطوح پیشنهاد شغل و مرزهای قابل مشاهده preferences را پوشش می‌دهد. بعدی: رفع حذف جستجوی ذخیره‌شده، تحویل واقعی اعلان‌ها، unauthenticated، screen reader و خطاهای شبکه. |
| JobVision | Candidate | Resume Management (candidate area) | `partial` | WT-2026-002 | WT-2026-003 رزومهٔ تکمیل‌شده و preview را پوشش می‌دهد؛ WT-2026-002 یک state ناقص کنترل‌شده، اثر تصمیم تحصیلات بر افت ۱۰۰٪ به ۶۵٪، recovery و بازگردانی را پوشش می‌دهد. بعدی: ماتریس کامل required/optional، save/delete، upload و مقایسهٔ تأییدشدهٔ Employer. |
| JobVision | Candidate | Application Management (candidate area TBD) | `partial` | WT-2026-002 | WT-2026-002 gate رزومه ناقص، close/retry، wizard چهارمرحله‌ای و مسیر جایگزین upload را تا مرز ارسال واقعی پوشش می‌دهد؛ WT-2026-006 فهرست و مدیریت read-only را پوشش می‌دهد. بعدی: آگهی تست برای ایجاد Application، confirmation، snapshot رزومه، withdrawal و transitionها. |
| JobVision | Candidate | Job Details & Evaluation | `partial` | WT-2026-002 | WT-2026-005 Saved Jobs را پوشش می‌دهد؛ WT-2026-002 شروع Apply از یک آگهی فعال و تحویل به gate Application را پوشش می‌دهد. بعدی: removal، unavailable jobs، share/report و مرزهای eligibility دیگر. |
| JobVision | Candidate | Company Discovery & Profile (candidate area TBD) | `partial` | — | WT-2026-007 فهرست، جستجوی نام، مرتب‌سازی و یک پروفایل عمومی شرکت در Production را پوشش می‌دهد. بعدی: اعمال/پاک‌کردن فیلترها، follow، rating/review، شرکت بدون داده و accessibility. |

## Walkthroughs

Use the next unused `WT-YYYY-NNN` value. Never renumber or reuse an ID.

Store each package under `products/<product-group>/<product>/WT-YYYY-NNN/evidence.md`; keep this registry centralized.

| ID | Product / area | Bounded scope and context | Status | Coverage | Package | Updated | Notes / next gap |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WT-2026-001 | JobVision Candidate / Job Search (candidate area) | کارجوی واردشده در Production از صفحه اصلی و `/jobs`؛ جستجو، فیلترهای visible و پیشرفته، مرتب‌سازی، صفحه‌بندی، ذخیره جستجو، history، ریسپانسیو و keyboard محدود. Apply به WT-2026-002 واگذار شده است. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-001/evidence.md) | 2026-08-08 | فیلترهای پیشرفته، pagination/history، URL shareable، saved search/alert، پاک‌کردن recent history و یک نمای موبایل پوشش داده شد. بعدی: B-003 و پاک‌سازی رکورد تستی «حسابرسی»، تحویل واقعی اعلان‌ها، unauthenticated، screen reader و network failure. چهار باگ مشکوک نیازمند بررسی Owner هستند. |
| WT-2026-002 | JobVision Candidate / Application Submission flow (primary candidate area: Application Management; secondary: Resume Management and Job Details & Evaluation) | کارجوی واردشده در Production از صفحه اصلی؛ تست کنترل‌شدهٔ completeness با تغییرهای برگشت‌پذیر تحصیلات و زبان، شروع Apply روی آگهی فعال، gate رزومه ناقص، close/retry، wizard recovery و مسیر جایگزین upload. ارسال نهایی واقعی و upload انجام نشد و رزومه در پایان به وضعیت اولیه برگشت. | `reviewed` | `partial` | [evidence](products/jobvision/candidate/WT-2026-002/evidence.md) | 2026-08-09 | Owner همهٔ claimهای E-001 تا E-010 را پذیرفت؛ B-001 و B-002 همچنان suspected bug هستند. بعدی: آگهی تست مجاز برای ارسال نهایی، confirmation، snapshot رزومه و validation همهٔ معیارها. |
| WT-2026-003 | JobVision Candidate / Resume Management (candidate area) | کارجوی واردشده در Production از صفحه اصلی به Resume Management؛ بررسی نقطه‌های ورود، stateهای قابل مشاهدهٔ رزومه، preview و validationهای قابل دسترس بدون ذخیره. ذخیره/حذف داده رزومه، upload، Application، خرید، privacy و اقدام اثرگذار بر داده واقعی در این package انجام نشد. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-003/evidence.md) | 2026-08-08 | نقطه ورود، رزومهٔ تکمیل‌شده، employer preview، مرز validation امن و optionalبودن دو بخش ۰٪ پوشش داده شد. بعدی: حساب disposable با رزومه ناقص برای required field، تکمیل، save/cancel/delete و مقایسه با context تأییدشده Employer. |
| WT-2026-004 | JobVision Candidate / Recommended Jobs & Preferences (candidate area TBD) | کارجوی واردشده در Production از صفحه اصلی؛ بررسی سطح‌های recommended job، preference settings و entryهای visible، cueهای شخصی‌سازی، نتیجهٔ navigation و مرز validation امن. تغییر/ذخیره preference، profile/resume edit، Apply، upload/download، خرید، پیام و notification mutation انجام نشد. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-004/evidence.md) | 2026-08-08 | دو حالت recommendation، کارت‌ها، sort/pagination، summary ترجیحات، onboarding boundary و هم‌زمانی prompt inline با checkbox فعال notification پوشش داده شد. بعدی: حساب disposable برای editor پس از onboarding و semantics/persistence notification، سپس empty state، mobile و keyboard. مالکیت Product Area همچنان TBD است. |
| WT-2026-005 | JobVision Candidate / Job Details & Evaluation — Saved Jobs flow | کارجوی واردشده در Production از صفحه اصلی؛ بررسی entryهای Saved Jobs، ساختار و stateهای visible، نتیجه navigation و مرز save/remove. یک save action با اجازه صریح انجام شد؛ remove، Apply و اقدام‌های دیگر اجرا نشدند. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-005/evidence.md) | 2026-08-08 | empty state، یک save transition، فهرست تک‌موردی و persistence پس از refresh پوشش داده شد. بعدی: remove، persistence بلندمدت، unavailable jobs، list-link navigation و keyboard/mobile. دو باگ مشکوک نیازمند review Owner هستند. |
| WT-2026-006 | JobVision Candidate / Application Management flow (candidate area TBD) | کارجوی واردشده در Production از صفحه اصلی؛ بررسی entry، فهرست درخواست‌ها، status/filterهای visible، جزئیات و controlهای مدیریت. withdrawal، پیام، resume/profile edit، خرید و اقدام اثرگذار اجرا نشد. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-006/evidence.md) | 2026-08-08 | status/filter، sort، detail، FAQ، closed pagination و My Priority read-only پوشش داده شد. بعدی: حساب‌های تست برای withdrawal، resume editing، همه transitionها، feedback و My Priority؛ سپس keyboard/screen reader. سه باگ مشکوک نیازمند Owner review. |
| WT-2026-007 | JobVision Candidate / Company Discovery & Profile (candidate area TBD) | کارجوی واردشده در Production از صفحه اصلی؛ پیدا کردن شرکت‌ها، جستجوی شرکت یا هولدینگ، مرتب‌سازی و مشاهدهٔ یک صفحهٔ عمومی شرکت. فقط read-only؛ follow، rating/review، apply، پیام، ذخیره یا هر تغییر واقعی خارج از scope است. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-007/evidence.md) | 2026-08-09 | فهرست، جستجوی «ماموت»، مرتب‌سازی و پروفایل عمومی گروه ماموت ثبت شد. بعدی: فیلترها، follow، rating/review، دادهٔ ناکافی، accessibility و mobile. |

| WT-2026-008 | Cando Salary Benchmark / Product-wide audit (areas TBD) | کاربر لاگین‌شده در Production از Home؛ مسیرهای Team، Benchmark، Scenario، Job Profile و Settings با کنترل‌شدهٔ test data بررسی شد. | `draft` | `partial` | [evidence](products/cando/salary-benchmark/WT-2026-008/evidence.md) | 2026-08-09 | پوشش اصلی UI و رفتارهای ایجاد/ویرایش/حذف محدود؛ بعدی: role/error/empty/mobile و model/profile change کنترل‌شده. |

## Update rules

Before a walkthrough:

1. Read this registry from the current `main` branch.
2. Check related coverage and known gaps without reading prior evidence claims.
3. Select a bounded scope, allocate the next unused ID, and add a `planned` row with `not-assessed` coverage.

After extraction:

1. Set the row to `draft`.
2. Set coverage to `partial` or `complete-for-scope` from the new package's Coverage and Coverage gaps sections.
3. Link the package when it is stored in this repository; otherwise write `workspace only`.
4. Add the most useful remaining gap or follow-up scope.

After owner review or handoff:

1. Set the row to `reviewed` only when the package meets all review completion criteria.
2. Set it to `handed-off` only after reconciliation starts, and link the proposal or pull request in notes.
3. Recalculate the product-area summary without treating one walkthrough as proof of the whole area.
4. Commit registry updates with the related walkthrough or handoff change whenever practical.
