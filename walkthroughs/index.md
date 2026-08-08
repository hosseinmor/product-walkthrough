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
| JobVision | Candidate | Resume Management (candidate area) | `partial` | — | پیش‌نویس WT-2026-003 نقطه‌های ورود حساب واردشده، state رزومهٔ تکمیل‌شده، employer preview، مرزهای validation امن و optionalبودن دو بخش با درصد صفر را پوشش می‌دهد. بعدی: stateهای ناقص، قواعد تکمیل، save/cancel/delete و مقایسهٔ تأییدشدهٔ سمت Employer. |
| JobVision | Candidate | Application Management (candidate area TBD) | `partial` | — | Draft WT-2026-006 covers the logged-in application list, visible statuses and filters, details, and read-only management controls. Next: withdrawal, resume-edit semantics, all status transitions, rejection feedback, My Priority, and accessibility coverage. |
| JobVision | Candidate | Job Details & Evaluation | `partial` | — | Draft WT-2026-005 covers the Saved Jobs empty state, one authorized save transition, and resulting one-item list. Next: removal, persistence, unavailable jobs, list navigation, and accessibility follow-up. |

## Walkthroughs

Use the next unused `WT-YYYY-NNN` value. Never renumber or reuse an ID.

Store each package under `products/<product-group>/<product>/WT-YYYY-NNN/evidence.md`; keep this registry centralized.

| ID | Product / area | Bounded scope and context | Status | Coverage | Package | Updated | Notes / next gap |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WT-2026-001 | JobVision Candidate / Job Search (candidate area) | کارجوی واردشده در Production از صفحه اصلی و `/jobs`؛ جستجو، فیلترهای visible و پیشرفته، مرتب‌سازی، صفحه‌بندی، ذخیره جستجو، history، ریسپانسیو و keyboard محدود. Apply به WT-2026-002 واگذار شده است. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-001/evidence.md) | 2026-08-08 | فیلترهای پیشرفته، pagination/history، URL shareable، saved search/alert، پاک‌کردن recent history و یک نمای موبایل پوشش داده شد. بعدی: B-003 و پاک‌سازی رکورد تستی «حسابرسی»، تحویل واقعی اعلان‌ها، unauthenticated، screen reader و network failure. چهار باگ مشکوک نیازمند بررسی Owner هستند. |
| WT-2026-002 | JobVision Candidate / Application Submission flow (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; navigate to an eligible job and inspect the application entry point, pre-submit steps, visible validations, and the final submission boundary. Excludes final submission to a real employer unless a pre-approved test posting is identified, resume/profile edits, messages, purchases, and irreversible actions. | `planned` | `not-assessed` | — | 2026-08-06 | Browser-agent safety boundary: stop before any action that sends an application or otherwise affects a real employer; record that path as blocked unless a safe test posting is explicitly approved. |
| WT-2026-003 | JobVision Candidate / Resume Management (candidate area) | کارجوی واردشده در Production از صفحه اصلی به Resume Management؛ بررسی نقطه‌های ورود، stateهای قابل مشاهدهٔ رزومه، preview و validationهای قابل دسترس بدون ذخیره. ذخیره/حذف داده رزومه، upload، Application، خرید، privacy و اقدام اثرگذار بر داده واقعی در این package انجام نشد. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-003/evidence.md) | 2026-08-08 | نقطه ورود، رزومهٔ تکمیل‌شده، employer preview، مرز validation امن و optionalبودن دو بخش ۰٪ پوشش داده شد. بعدی: حساب disposable با رزومه ناقص برای required field، تکمیل، save/cancel/delete و مقایسه با context تأییدشده Employer. |
| WT-2026-004 | JobVision Candidate / Recommended Jobs & Preferences (candidate area TBD) | کارجوی واردشده در Production از صفحه اصلی؛ بررسی سطح‌های recommended job، preference settings و entryهای visible، cueهای شخصی‌سازی، نتیجهٔ navigation و مرز validation امن. تغییر/ذخیره preference، profile/resume edit، Apply، upload/download، خرید، پیام و notification mutation انجام نشد. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-004/evidence.md) | 2026-08-08 | دو حالت recommendation، کارت‌ها، sort/pagination، summary ترجیحات، onboarding boundary و هم‌زمانی prompt inline با checkbox فعال notification پوشش داده شد. بعدی: حساب disposable برای editor پس از onboarding و semantics/persistence notification، سپس empty state، mobile و keyboard. مالکیت Product Area همچنان TBD است. |
| WT-2026-005 | JobVision Candidate / Job Details & Evaluation — Saved Jobs flow | کارجوی واردشده در Production از صفحه اصلی؛ بررسی entryهای Saved Jobs، ساختار و stateهای visible، نتیجه navigation و مرز save/remove. یک save action با اجازه صریح انجام شد؛ remove، Apply و اقدام‌های دیگر اجرا نشدند. | `draft` | `partial` | [evidence](products/jobvision/candidate/WT-2026-005/evidence.md) | 2026-08-08 | empty state، یک save transition، فهرست تک‌موردی و persistence پس از refresh پوشش داده شد. بعدی: remove، persistence بلندمدت، unavailable jobs، list-link navigation و keyboard/mobile. دو باگ مشکوک نیازمند review Owner هستند. |
| WT-2026-006 | JobVision Candidate / Application Management flow (candidate area TBD) | Logged-in jobseeker in Production, starting at the home page; inspect the entry point, application list, visible statuses and filters, application details, and available management controls. Excludes withdrawing or deleting an application, sending messages, resume/profile edits, purchases, and any action that may affect a real employer or another user. | `draft` | `partial` | [evidence](../products/jobvision/candidate/WT-2026-006/evidence.md) | 2026-08-07 | Next gap: use disposable candidate and employer test accounts to demonstrate withdrawal, resume editing, every status transition, rejection feedback, and My Priority end to end; then test keyboard and screen-reader behavior. Three suspected bugs require Owner review. Renumbered from the conflicting `WT-2026-003` allocation during the 2026-08-08 registry repair. |

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
