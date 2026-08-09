---
walkthrough_id: WT-2026-008
status: draft
product_group: Cando
product: salary
candidate_areas: [مدیریت تیم, بنچمارک حقوق, تحلیل سناریو, تنظیمات سازمان, مدیریت شناسنامه شغلی]
recorded_at: 2026-08-09
source:
  type: direct-product-audit
  reference: آدیت مستقیم مرورگر در Production؛ بدون screen recording
reviewed_by: []
reviewed_at:
---

# بستهٔ evidence Walkthrough

## Context

- هدف: آدیت مسیرهای قابل‌مشاهدهٔ محصول Salary و اقدام‌های کنترل‌شده روی دادهٔ تست.
- بازیگر: کاربر واردشدهٔ سازمان.
- نقش: نقش و permission دقیق شناسایی نشد.
- وضعیت ورود: واردشده.
- حساب یا پیکربندی: یک سازمان Production با تیم، شناسنامه‌های شغلی، دپارتمان‌ها و بیزینس‌لاین‌های موجود.
- مجوزها: کنترل‌های ایجاد، ویرایش و حذف در UI دیده شد؛ مدل دقیق مجوزها تست نشد.
- محیط: Production.
- نقطهٔ شروع: Home که به Team هدایت شد.

## Coverage

### پوشش‌داده‌شده

- فهرست و جست‌وجوی تیم، ایجاد همکار، جزئیات و ویرایش همکار و ثبت حقوق نهایی.
- جزئیات بنچمارک حقوق و ایجاد، ویرایش و حذف سناریو.
- گزارش‌های مدیریتی/تیم و trigger دریافت گزارش.
- ایجاد شناسنامهٔ شغلی و مشاهدهٔ جزئیات شناسنامهٔ تولیدشده.
- تنظیمات سازمان و guardهای ایجاد/ویرایش/حذف دپارتمان و بیزینس‌لاین.

### روایت‌شده اما نمایش‌داده‌نشده

- موردی ندارد.

### پوشش‌داده‌نشده

- mobile/responsive، حالت بدون ورود و نقش‌های دیگر، خطاهای شبکه، empty state و تغییر واقعی پروفایل سازمان یا مدل محاسباتی.

### نامشخص یا مسدود

- کلیک دریافت گزارش در این session خروجی دانلود یا تغییر UI قابل‌مشاهده نداشت.
- در حذف همکار، تأیید دوم مشاهده نشد و دستور حذف مستقیماً پیام موفقیت داد.

## Evidence

### E-001 — فهرست تیم فیلدهای مقایسهٔ جبران خدمات را نشان می‌دهد
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: صفحهٔ Team در سازمان Production واردشده.
- Conditions: رکوردهای همکار موجود.
- Confidence: high
- Claim: جدول Team فیلدهای سازمانی، حقوق ۱۴۰۴، بازهٔ حقوق پیشنهادی ۱۴۰۵ و حقوق نهایی ۱۴۰۵ را نمایش می‌دهد؛ جست‌وجو می‌تواند فهرست را با کد پرسنلی محدود کند.
- Remaining uncertainty: semantics جست‌وجو فراتر از query کد پرسنلی تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-002 — ایجاد همکار پیش از ذخیره، اطلاعات اجباری را validate می‌کند
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: dialog افزودن همکار.
- Conditions: فرم خالی در برابر رکورد تست کامل.
- Confidence: high
- Claim: فرم افزودن همکار اطلاعات هویتی، سازمانی و جبران خدمات را گروه‌بندی می‌کند؛ دکمهٔ ذخیره و محاسبه ابتدا غیرفعال بود و پس از تکمیل فیلدها و انتخاب‌های لازم فعال شد.
- Remaining uncertainty: ماتریس کامل required/optional استخراج نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-003 — ذخیرهٔ همکار محاسبهٔ بنچمارک را آغاز می‌کند
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: همکار تست کنترل‌شده در Production.
- Conditions: اتصال به شناسنامهٔ شغلی و ساختار سازمانی موجود.
- Confidence: high
- Claim: پس از ذخیره، ردیف Team ابتدا وضعیت «در حال محاسبه» و بعد بازهٔ حقوق پیشنهادی ۱۴۰۵ را نمایش داد.
- Remaining uncertainty: زمان‌بندی، retry و failure محاسبه تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-004 — جزئیات همکار، ورودی‌های بنچمارک در سطح مدل را نمایش می‌دهد
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: drawer جزئیات همکار تست.
- Conditions: نتیجهٔ بنچمارک موجود.
- Confidence: high
- Claim: جزئیات همکار حقوق پیشنهادی و نهایی، استراتژی پرداخت، پیچیدگی و بخش‌های هر مدل بنچمارک با وزن، منبع و مقادیر percentile/range را در صورت وجود نمایش می‌دهد؛ یک مدل پیام نبود دادهٔ کافی نشان داد.
- Remaining uncertainty: معنا و قواعد وزن مدل‌ها نیازمند review مالک است.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-005 — حقوق نهایی مستقل از بازهٔ پیشنهادی ثبت می‌شود
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: همکار تست کنترل‌شده.
- Conditions: مقدار تست داخل بازهٔ پیشنهادی ذخیره شد.
- Confidence: high
- Claim: UI جزئیات و Team امکان ثبت حقوق نهایی ۱۴۰۵ و نمایش درصد مقایسه با حقوق ۱۴۰۴ را فراهم می‌کنند.
- Remaining uncertainty: ویرایش یا حذف حقوق نهایی به‌طور کامل تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-006 — تحلیل سناریو ستون مقایسه‌ای پایدار ایجاد و باز‌محاسبه می‌کند
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: صفحهٔ تحلیل سناریو.
- Conditions: سناریوی تست با ضریب پیچیدگی ایجاد، ویرایش و حذف شد.
- Confidence: high
- Claim: سناریو می‌تواند ضریب پیچیدگی یا استراتژی پرداخت را فعال کند، ستون سناریو را ذخیره و محاسبه کند و دوباره برای ویرایش باز شود؛ ذخیرهٔ ویرایش نتیجه را باز‌محاسبه کرد.
- Remaining uncertainty: ترکیب چند filter و چند setting تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-007 — حذف سناریو تأیید می‌خواهد
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: سناریوی تست.
- Conditions: کنترل حذف در overflow سناریو.
- Confidence: high
- Claim: حذف سناریو warning تأیید نمایش می‌دهد که همهٔ اطلاعات سناریو پاک می‌شود؛ سناریوی تست پس از تأیید حذف شد.
- Remaining uncertainty: recovery پس از حذف تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-008 — ایجاد شناسنامهٔ شغلی به عنوان استاندارد resolve می‌شود
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: عناوین شغلی.
- Conditions: عنوان واقعی ارائه‌شده توسط کاربر و سطح ارشدیت انتخاب‌شده.
- Confidence: high
- Claim: ایجاد شناسنامهٔ شغلی عنوان، سطح ارشدیت و عنوان شغلی استاندارد می‌خواهد؛ پس از انتخاب عنوان استاندارد، محصول ایجاد را تأیید و یک شناسنامهٔ پیشنهادی با requirementها و محتوای قابل‌ویرایش فراهم کرد.
- Remaining uncertainty: قواعد پیشنهاد عنوان استاندارد و تولید شناسنامه مشخص نیست.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-009 — حذف ساختار متصل به همکار مسدود است
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: تنظیمات دپارتمان و بیزینس‌لاین.
- Conditions: رکورد انتخاب‌شده همکار تخصیص‌یافته داشت.
- Confidence: high
- Claim: تلاش برای حذف دپارتمان یا بیزینس‌لاین دارای همکار مسدود می‌شود و کاربر را به انتقال همکاران به واحد دیگر راهنمایی می‌کند.
- Remaining uncertainty: حذف ساختارهای خالی تست نشد.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

### E-010 — trigger دریافت گزارش تیم خروجی قابل‌مشاهده نداشت
- Type: observed
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: صفحهٔ گزارش تیم.
- Conditions: session واردشده در Production؛ کنترل دانلود دو بار کلیک شد.
- Confidence: medium
- Claim: کلیک کنترل دریافت گزارش تیم در این جلسهٔ آدیت، دانلود مرورگر، tab جدید یا تغییر visible UI ایجاد نکرد.
- Remaining uncertainty: ممکن است به browser/session وابسته باشد و rule محصول محسوب نمی‌شود.

#### Owner review
- Decision: pending
- Final claim:
- Owner note:

## باگ‌های مشکوک

### B-001 — کنترل دریافت گزارش خروجی قابل‌مشاهده نداشت
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: کنترل دریافت گزارش تیم.
- Observation: دو تلاش دانلود، tab جدید یا feedback قابل‌مشاهده‌ای نداشت.
- Why it may be a bug: کنترل برچسب‌دار دریافت گزارش خروجی قابل‌مشاهده نداشت.
- Owner note:

### B-002 — حذف همکار در flow مشاهده‌شده تأیید دوم نداشت
- Timestamp: جلسهٔ آدیت مستقیم، 2026-08-09
- Scope: حذف همکار تست کنترل‌شده.
- Observation: انتخاب حذف همکار پیام موفقیت داد، بدون آنکه dialog تأیید مشاهده شود.
- Why it may be a bug: ممکن است اقدام مخرب guard کافی نداشته باشد؛ قبل از تصمیم باید reproduce شود.
- Owner note:

## شکاف‌های پوشش

- نقش/مجوز، بدون ورود، error، empty و mobile/responsive.
- ذخیرهٔ تغییر واقعی پروفایل سازمان یا وزن مدل انجام نشد.
- همکار تست حذف شد؛ شناسنامهٔ شغلی واقعی ایجادشده با درخواست کاربر باقی است.

## recording پیشنهادی بعدی

- با سازمان disposable، error handling، permission، ساختار خالی و تغییر کنترل‌شدهٔ مدل محاسباتی تست شود.
- رفتار دریافت گزارش در مرورگر استاندارد کاربر validate شود.

## خلاصهٔ handoff

این بخش فقط پس از owner review تکمیل می‌شود.

- Package status: draft
- Accepted evidence IDs:
- Edited evidence IDs:
- Rejected evidence IDs:
- Remaining unknowns: شکاف‌های پوشش را ببینید.
- Suggested Product Knowledge scope: Cando Salary — مدیریت تیم، محاسبهٔ بنچمارک، تحلیل سناریو، شناسنامه‌های شغلی و تنظیمات سازمان.
