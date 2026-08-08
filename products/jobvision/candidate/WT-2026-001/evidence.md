---
walkthrough_id: WT-2026-001
status: draft
product_group: jobvision
product: candidate
candidate_areas:
  - Job Search
recorded_at: 2026-08-06T13:11:12Z
source:
  type: browser-agent
  reference: Direct read-only Production walkthrough in Codex in-app Browser
reviewed_by: []
reviewed_at:
---

# Walkthrough Evidence Package

## Context

- Goal: Discover job opportunities from the home page and narrow results using search, location, job group, selected filters, and sorting.
- Actor: Jobseeker
- Role: Candidate
- Authentication state: Logged in, inferred only from authenticated navigation items and personalized search/recommendation surfaces visible in this session.
- Account, plan, or configuration: Unknown; no account identifiers or personal values were recorded.
- Permissions: Ordinary Candidate access observed; exact permission model unknown.
- Environment: Production
- Starting point: JobVision home page
- Permitted actions: Entering non-sensitive test search values, selecting and removing filters, sorting, navigation, and refresh.
- Forbidden actions: Applying to jobs, saving or clearing saved searches, editing profile/resume, purchasing, changing permissions, or performing irreversible actions.
- Stop conditions: Apply/payment/account-mutation surfaces, sensitive data, CAPTCHA, or any action affecting another user.

## Coverage

### Covered

- Home-page search entry point
- Keyword entry and results navigation
- City suggestion selection and application
- Job-group picker selection and application
- Results-page filter inventory
- Remote and employment-type filters
- Combining and individually removing filters
- Result sorting
- URL-backed persistence after refresh
- Empty-result state
- Logged-in saved/recent-search assistance visible on focus

### Narrated but not demonstrated

- None. This was a direct browser-agent walkthrough without recorder narration.

### Not covered

- Applying to a Job Post
- Saving a search or changing email/SMS alerts
- Clearing saved or recent searches
- Salary, publication-time, experience, seniority, benefits, industry, internship, disability-employment, or military-service filter details
- Pagination and returning from Job Details
- Mobile and responsive behavior
- Unauthenticated behavior or other Candidate account/plan variations
- Network failure, retry, or offline behavior

### Unclear or blocked

- Whether apparently unrelated results under the “newest” sort are intended broad-match behavior
- Whether the temporary stale browser-page title after client-side searching affects analytics, accessibility, or only browser chrome
- Exact authentication and permission requirements for personalized recommendations and saved-search alerts

## Evidence

### E-001 — Home page exposes a three-part job-search entry point

- Type: observed
- Timestamp: 2026-08-06T13:11:12Z
- Scope: Production home page; this logged-in Candidate session
- Conditions: Desktop/default browser viewport
- Confidence: high
- Claim: The home page lets the Candidate enter a job title or company, choose a job group, choose a city, and start the flow with “جستجو در مشاغل”.
- Remaining uncertainty: Required versus optional fields and unauthenticated behavior were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-002 — Keyword submission creates a keyword-scoped results page

- Type: observed
- Timestamp: 2026-08-06T13:11:48Z
- Scope: Keyword “طراح محصول”; Production
- Conditions: City text had been typed but no city suggestion had been selected
- Confidence: high
- Claim: Submitting “طراح محصول” navigated to a keyword URL, preserved the keyword in the search field, showed a keyword-specific heading, and defaulted sorting to “مرتبط‌ترین”.
- Remaining uncertainty: Keyword matching, stemming, synonyms, company-name matching, and ranking rules are unknown.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-003 — A typed city is applied only after selecting a city suggestion and submitting

- Type: observed
- Timestamp: 2026-08-06T13:11:36Z–2026-08-06T13:12:32Z
- Scope: City query “تهران” with keyword “طراح محصول”; Production
- Conditions: The first attempt typed “تهران” without selecting a suggestion; the second selected “تمامی شهرهای تهران”
- Confidence: high
- Claim: Typing city text alone did not scope the submitted search. After selecting the “تمامی شهرهای تهران” suggestion and submitting, the city appeared in the results URL and heading, and the visible result count changed from 740 to 526.
- Remaining uncertainty: Single-city versus province-wide options, multiple-city selection, and keyboard-only selection were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-004 — The results page exposes a broad filter set and sorting controls

- Type: observed
- Timestamp: 2026-08-06T13:11:48Z
- Scope: Keyword results page; Production; logged-in Candidate session
- Conditions: Keyword “طراح محصول”
- Confidence: high
- Claim: The results page exposed filters for publication time, remote work, employment type, internship, salary, experience, seniority, benefits, industry, disability employment, and military service, plus sorting by newest, relevance, or highest salary and a saved-search alert control.
- Remaining uncertainty: Most filter option sets and the saved-search behavior were not exercised.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-005 — Remote work is an immediately applied removable filter

- Type: observed
- Timestamp: 2026-08-06T13:12:45Z–2026-08-06T13:13:08Z
- Scope: Keyword “طراح محصول”, all cities of Tehran; Production
- Conditions: No other result filter selected
- Confidence: high
- Claim: Selecting “دورکاری” immediately added a remote segment to the URL, changed the heading to the remote-work result scope, reduced the visible count from 526 to 62, and showed one active-filter indicator. Removing it returned to the previous URL, heading, and count.
- Remaining uncertainty: Whether every returned Job Post actually supports remote work was not audited individually.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-006 — Employment type offers three mutually exclusive choices

- Type: observed
- Timestamp: 2026-08-06T13:13:46Z–2026-08-06T13:14:34Z
- Scope: Keyword “طراح محصول”, all cities of Tehran; Production
- Conditions: Employment-type filter expanded
- Confidence: high
- Claim: The employment-type filter displayed radio choices for full-time, part-time, and contract/project work. Selecting part-time immediately added a part-time segment to the URL, changed the heading, reduced the visible count to 41, and showed one active-filter indicator.
- Remaining uncertainty: Switching directly between the three options was not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-007 — Remote and part-time filters can be combined and removed independently

- Type: observed
- Timestamp: 2026-08-06T13:14:47Z–2026-08-06T13:15:52Z
- Scope: Keyword “طراح محصول”, all cities of Tehran; Production
- Conditions: Part-time was selected before remote
- Confidence: high
- Claim: Adding remote work to part-time produced a combined URL segment, a heading describing both conditions, a visible count of 25, and an active-filter count of two. Removing remote preserved part-time; using the × control on the part-time chip removed the remaining filter.
- Remaining uncertainty: Other filter combinations and any maximum-selection rules were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-008 — Sorting is URL-backed and persists after refresh

- Type: observed
- Timestamp: 2026-08-06T13:13:23Z and 2026-08-06T13:17:27Z
- Scope: Keyword results; Production
- Conditions: Sorting changed from relevance to newest
- Confidence: high
- Claim: Choosing “جدیدترین‌” changed the sort query parameter from 1 to 0. After refreshing a keyword results URL, the keyword and newest-sort selection were restored from the URL.
- Remaining uncertainty: Highest-salary sorting, stability between refreshes, and pagination interactions were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-009 — City and job-group edits are staged until search submission

- Type: observed
- Timestamp: 2026-08-06T13:16:56Z–2026-08-06T13:17:07Z and 2026-08-06T13:18:53Z–2026-08-06T13:19:25Z
- Scope: Results-page search controls; Production
- Conditions: Existing keyword results
- Confidence: high
- Claim: Clearing the selected city or selecting/clearing a job group changed the corresponding control first, while the current URL and results remained unchanged until “جستجو در مشاغل” was submitted.
- Remaining uncertainty: Whether this staged behavior is consistent for keyword edits and keyboard submission was not fully verified.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-010 — The job-group picker is searchable and applies a category URL

- Type: observed
- Timestamp: 2026-08-06T13:18:44Z–2026-08-06T13:19:04Z
- Scope: Results-page job-group control; Production
- Conditions: Existing no-result keyword
- Confidence: high
- Claim: Opening the job-group control showed a search field and a long option list. Selecting “طراحی رابط و تجربه کاربری (UI/UX)” and submitting added the UI/UX category to the results URL.
- Remaining uncertainty: Multi-select behavior, option ordering, and zero-match filtering inside the picker were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-011 — A no-result search provides recovery guidance

- Type: observed
- Timestamp: 2026-08-06T13:17:45Z
- Scope: Deliberately unmatched keyword; Production
- Conditions: Keyword “xyzqwalkthrough1405”
- Confidence: high
- Claim: When no Job Posts matched, the page stated that no opportunity was found and suggested checking spelling, trying other keywords, or removing filters.
- Remaining uncertainty: The behavior for a temporary server error or partial-result state was not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

### E-012 — Focusing keyword search exposes saved and recent search assistance

- Type: observed
- Timestamp: 2026-08-06T13:18:08Z
- Scope: Results page; this logged-in Candidate session
- Conditions: Keyword input focused
- Confidence: medium
- Claim: Focusing the keyword field exposed saved searches with an edit entry point, recent searches, and a “پاک کردن همه” control.
- Remaining uncertainty: Persistence duration, maximum history size, deduplication, ownership, and clear-all confirmation behavior were not tested.

#### Owner review

- Decision: pending
- Final claim:
- Owner note:

## Suspected bugs

### B-001 — Client-side search temporarily retained the previous document title

- Timestamp: 2026-08-06T13:17:45Z–2026-08-06T13:17:59Z
- Scope: Navigation from “طراح محصول” results to an unmatched keyword
- Observation: The URL and visible content changed to the unmatched keyword and empty state, but the browser title still referenced “طراح محصول”. Refreshing corrected the title to the new keyword.
- Why it may be a bug: Browser title, visible result state, and URL were temporarily inconsistent after client-side navigation.
- Owner note:

### B-002 — Newest sorting surfaced apparently unrelated titles above matching titles

- Timestamp: 2026-08-06T13:13:23Z–2026-08-06T13:13:31Z
- Scope: Keyword “طراح محصول”, all cities of Tehran, sort “جدیدترین‌”
- Observation: The first visible results included “Senior Android Developer”, “دستیار اجرایی”, “Senior Front-End Developer”, and “برنامه نویس فول استک - آقا”, despite the active keyword being “طراح محصول”.
- Why it may be a bug: The top results did not visibly match the submitted keyword. This may instead be intended broad matching, hidden description/company matching, or a ranking trade-off and requires owner confirmation.
- Owner note:

## Coverage gaps

- Exercise each untested filter and document its option model, combination rules, counts, URL state, and removal behavior.
- Test pagination, back/forward navigation, shareable filtered URLs, and return from Job Details.
- Test saving a search and alert-channel behavior with an approved disposable account.
- Test mobile/responsive and keyboard/screen-reader behavior.
- Compare authenticated and unauthenticated flows.
- Validate suspected bugs with logs or a second account/session.

## Recommended follow-up recording

- A focused recording of advanced filters and saved-search alerts using a disposable Production-safe account, followed by a separate mobile/keyboard walkthrough.

## Handoff summary

Not completed. The package is a draft and every evidence item still requires an Owner decision.
