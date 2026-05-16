# Task Group: abc-homey / frontend UI for meter reading, bills, dashboard, and residential management
scope: Homey Next.js UI/API feature work around meter-reading and bill-page layout, residential-management forms, and dashboard charts.
applies_to: cwd=/Users/jj/Project/abc-homey; reuse_rule=reuse for `homey-next` and paired `homey-api` UI/API work in this checkout; verify current component library, page structure, and table/card layout before editing.

## Task 1: UI tweaks in `homey-next` for meter reading and bill pages, success

### rollout_summary_files

- rollout_summaries/2026-05-14T00-27-57-ACL7-homey_next_manage_bill_meter_reading_ui_tweaks.md (cwd=/Users/jj/Documents/New project 2, rollout_path=/Users/jj/.codex/sessions/2026/05/14/rollout-2026-05-14T07-27-57-019e23e2-0d41-7c11-9999-4fe6192e52a1.jsonl, updated_at=2026-05-15T07:40:37+00:00, thread_id=019e23e2-0d41-7c11-9999-4fe6192e52a1, localized UI changes validated with `npm run build`)

### keywords

- homey-next, manage-bill, recording-meter, formatThaiDateWithBuddhistYear, READING_SCHEDULE_LABELS.DATE_RANGE, dueDateLabel, badge under icon, flex-col items-center, border-b-2, current Thai date, buddhist year

## Task 2: Residential management create/edit/list feature update, success

### rollout_summary_files

- rollout_summaries/2026-03-30T16-37-30-LMPj-abc_homey_gcp_docker_cloud_run_artifact_registry.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/03/30/rollout-2026-03-30T23-37-30-019d3f9b-87bb-7f82-97f8-20ec2af44bb5.jsonl, updated_at=2026-04-01T07:29:32+00:00, thread_id=019d3f9b-87bb-7f82-97f8-20ec2af44bb5, frontend/API feature work validated)

### keywords

- residentials-management, required red asterisk, shadcn Sonner, top-right toast, UpdateResidentialPayload.status, editable residential status, default project sync, create-form email optional

## Task 3: Dashboard package bar chart and residential type pie chart, then Chart.js migration, success

### rollout_summary_files

- rollout_summaries/2026-03-30T16-37-30-LMPj-abc_homey_gcp_docker_cloud_run_artifact_registry.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/03/30/rollout-2026-03-30T23-37-30-019d3f9b-87bb-7f82-97f8-20ec2af44bb5.jsonl, updated_at=2026-04-01T07:29:32+00:00, thread_id=019d3f9b-87bb-7f82-97f8-20ec2af44bb5, Chart.js implementation passed lint/build)

### keywords

- dashboard, Chart.js, react-chartjs-2, Bar chart ประเภทของ package, Pie chart ประเภทของที่พักอาศัย, CategoryScale, ArcElement, font.weight, numeric 600

## User preferences

- when the user said "ในเมนู \"บันทึกค่ามิเตอร์\" และ \"ใบเสร็จ\" ให้เปลี่ยน \"ช่วงวัน\" นี้เป็นวันที่ เดือน ปี (พ.ศ.) ของปัจจุบัน" -> in these pages, prefer the current Thai Buddhist date display over the generic schedule-mode label. [Task 1]
- when the user said "ในเมนู \"บันทึกค่ามิเตอร์\" และ \"ใบเสร็จ\" ให้ย้าย badges มาอยู่ด้านใต้ตัวของ ico" -> default these schedule cards to `icon -> badge` vertical stacking instead of inline badge placement. [Task 1]
- when the user said "ในเมนู \"ใบเสร็จ\" ให้แบ่ง Layout ใหม่เฉพาะส่วนนี้โดยแบ่งเป็นแนวนอนให้ \"บิลทั้งหมดแสดงด้านบนและด้านล่างแสดง \"วันที่กำหนดชำระ\"" -> treat the left summary card in `manage-bill` as a two-row layout requirement, not a single mixed block. [Task 1]
- when the user said "ปรับ border เส้นแบ่งให้มีขนาดเท่ากันกับฝั่งของ ยอดเรียกเก็บ" -> preserve visual border-weight consistency across adjacent cards instead of treating divider thickness as incidental. [Task 1]
- when editing residential-management, the user explicitly asked for `Highlight * to red color for form fill important`, `Alert toast at position top right(success, error, warning)`, and `Can change the status of residential` -> treat these as required UX defaults for this screen. [Task 2]
- when the user gives a long create/edit/filter/table spec for residential-management -> expect complete form/table parity rather than minimal wiring. [Task 2]
- when the user links or asks for shadcn Sonner, default to the project's standard component ecosystem instead of a custom toast stack. [Task 2]
- when the user asks for `1. Bar chart ประเภทของ package, 2. Pie chart ประเภทของที่พักอาศัย` -> future dashboard work should include concrete chart visuals, not just text stats. [Task 3]
- when the user says `โดย Chart ให้เปลี่ยนไปใช้ Chartjs แทน` -> switch directly to Chart.js rather than keeping mixed custom chart code. [Task 3]

## Reusable knowledge

- `formatThaiDateWithBuddhistYear(date)` already exists in both `recording-meter` and `manage-bill` pages and is the correct formatter for `d MMM BBBB` display in these UI slots. [Task 1]
- `READING_SCHEDULE_LABELS` still belongs in `homey-next/lib/meter-reading-window.ts`, but the small label line under the schedule card in these two pages is presentation-only and can render `formatThaiDateWithBuddhistYear(new Date())` directly without changing scheduling logic. [Task 1]
- The badge-under-icon adjustment was localized to the schedule card structure; a small `flex-col items-center` icon column can change the layout without touching the right-side copy block. [Task 1]
- `BillSummary` does not carry due-date info; `homey-next/app/(auth)/manage-bill/page.tsx` must derive `dueDateLabel` from `billsData.data` by sorting visible `bill.dueDate` values and showing one date or a Thai date range. [Task 1]
- The final two-row total-bills card uses `grid h-full min-h-36 grid-rows-2`, with the divider matched to the neighboring revenue card via `border-b-2 border-border/80`. [Task 1]
- `npm run build` in `homey-next` was the verification step after each localized UI pass. [Task 1]
- `UpdateResidentialPayload` includes `status`, `waterPrice`, `electricPrice`, `package`, and `months`; backend `ResidentialsService.updateResidential()` persists status and syncs default project utility/address/name fields. [Task 2]
- Residential create/edit dialogs use Sonner toasts and red required markers instead of inline alert banners. [Task 2]
- `homey-next/app/(auth)/dashboard/page.tsx` derives dashboard data from `residentialService`; providers see all residentials and customers see their own residential. [Task 3]
- Chart.js in this page requires explicit registration of `CategoryScale`, `LinearScale`, `BarElement`, `ArcElement`, `Tooltip`, and `Legend`, then `<Bar />` and `<Pie />` from `react-chartjs-2`. [Task 3]

## Failures and how to do differently

- The first pass on the Thai-date tweak preserved the old label source too long; the working fix was to remove that import from the two pages and render the current Thai date directly in the UI. [Task 1]
- The initial badge placement was still inline with the heading; the stable structure is a `flex-col items-center` icon column with badge underneath. [Task 1]
- Keep the due-date implementation minimal. A brief extra helper was added and removed; the durable version derives `dueDateLabel` directly from `bills`. [Task 1]
- The first toast implementation used a custom stack; the user corrected it to shadcn Sonner. Similar UI work should check the project component ecosystem when the user references official docs/components. [Task 2]
- The update flow initially omitted project utility updates; future residential edits should keep residential and default project data in sync. [Task 2]
- Chart.js `font.weight` caused a TypeScript issue when set as string `'600'`; numeric `600` worked. [Task 3]
- The custom CSS/SVG chart version was replaced entirely; once the user specifies a chart library, switch directly. [Task 3]

# Task Group: abc-homey / Prisma seed and deterministic seed data
scope: Seed-data fixes and rewrites for Homey API, especially `homey-api/prisma/seed.ts` alignment with schema/DTO constraints and real seed-backed app behavior.
applies_to: cwd=/Users/jj/Project/abc-homey/homey-api; reuse_rule=reuse for `prisma/seed.ts` and related `seed.md` tasks in this checkout; re-check current schema/DTOs and actual seeded states before editing because seed coverage and UI expectations can drift.

## Task 1: Make seed data coherent with real app behavior and resume the interrupted rewrite, partial/interrupted

### rollout_summary_files

- rollout_summaries/2026-05-13T22-23-18-l39B-abc_homey_seed_data_sync_interrupted.md (cwd=/Users/jj/Documents/New project 2, rollout_path=/Users/jj/.codex/sessions/2026/05/14/rollout-2026-05-14T05-23-18-019e236f-ed36-7b31-bda2-2832bcc6eb17.jsonl, updated_at=2026-05-14T00:27:40+00:00, thread_id=019e236f-ed36-7b31-bda2-2832bcc6eb17, inspection only; patch blocked by usage-limit rejection)

### keywords

- prisma seed, seed.ts, schema.prisma, real app behavior, mockup, inactive meter, seed-meter-e3, seed-meter-w6, seed-meter-apt-e3, seed-meter-hq-w-b03, MeterAssignment, MeterReading, imageUrl, current month, ACTIVE_BILLING_MONTH, update: {}, usage limit

## Task 2: Rewrite seed data to match schema constraints and cover all types, uncertain/interrupted

### rollout_summary_files

- rollout_summaries/2026-04-17T21-30-44-lG8V-prisma_seed_rewrite_schema_aligned_full_coverage.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/04/18/rollout-2026-04-18T04-30-44-019d9d5a-74a0-7062-aad6-ef59db9c9eb9.jsonl, updated_at=2026-04-18T20:42:08+00:00, thread_id=019d9d5a-74a0-7062-aad6-ef59db9c9eb9, inspection only; no final verified rewrite)

### keywords

- prisma seed, schema.prisma, seed.ts, seed.md, enum coverage, residentials, users, meter readings, bills, payments, DTO validation, upsert, ครบทุกประเภท, turn_aborted

## Task 3: Add organization sub-projects to seed data, success

### rollout_summary_files

- rollout_summaries/2026-04-18T21-51-06-IyY7-add_organization_projects_to_seed_data.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/04/19/rollout-2026-04-19T04-51-06-019da293-760b-75d0-af9a-b7d5723f8fc7.jsonl, updated_at=2026-04-18T23:07:26+00:00, thread_id=019da293-760b-75d0-af9a-b7d5723f8fc7, validated with `npm run build`)

### keywords

- prisma seed, organization residential, residential.projects, Homey HQ, seed.ts, seed.md, setting-residential, VILLAGE, APARTMENT, Not a git repository, npm run build

## User preferences

- when the user said "เขียน update file seed ให้ข้อมูลสอดคล้องกันหน่อยตอนนี้ฉันรู้สึกว่าข้อมูล mockup จัดไม่เป็นไปตามข้อมูลที่ควรจะแสดงเลย" -> favor real seed-backed app states over generic demo rows or stale mock-like data. [Task 1]
- when the user said "ลบออกทั้งหมดเลยเหลือแค่ที่ Mockup ที่ใช้งานจริงที่อยู่ในไฟล์ seed เท่านั้น" -> treat similar follow-ups as a request to remove fake/mock UI data and center the app on what `prisma/seed.ts` actually seeds. [Task 1]
- when the user said "จากบทสนทนานี้ให้ update file seed ต่อ ที่ยังค้างทำไม่เสร็จ" -> continue from the interrupted seed context instead of restarting analysis from scratch. [Task 1]
- when the user asked "เขียน File seed ใหม่โดยให้เขียนให้เข้ากับเงื่อนไขของแต่ละข้อมูลและสร้างข้อมูลให้ครบทุกประเภท" -> align seed data with each entity's actual constraints/validation, not just generic rows. [Task 2]
- when the user asks for "ครบทุกประเภท" -> proactively check enum/status coverage and relationship coverage across seeded entities. [Task 2]
- when the user said "ในส่วนของเมนู \"จัดการที่พักอาศัย\" ประเภทองค์กรไม่มีในส่วนของข้อมูลโครงการที่อยู่ภายในด้านในอยากให้เพิ่มเข้าไปหน่อยในไฟล์ seed" -> treat this as a seed-data fix request for organization residential projects, not a UI change request. [Task 3]
- when a request is narrowly scoped to "ในไฟล์ seed" -> default to minimal seed updates unless the user explicitly asks for app logic changes. [Task 3]

## Reusable knowledge

- Related skill: skills/abc-homey-prisma-data/SKILL.md. [Task 1][Task 2][Task 3]
- `homey-api/prisma/seed.ts` is the main seed entrypoint; it uses deterministic IDs and many `upsert` patterns, so reseeding is repeatable but stale rows persist when `update: {}` is left empty. [Task 1][Task 2]
- Schema/DTO authority for valid seed data lives in `homey-api/prisma/schema.prisma` plus DTOs under `homey-api/src/core/**/dto`, including `CreateResidentialDto`, `CreateUserDto`, `CreateResidentDto`, and `CreateMeterReadingDto`. [Task 2]
- Important enum coverage handles in the seed are `ResidentialType`, `ResidentialStatus`, `Package`, `SubscriptionStatus`, `Role`, `UserStatus`, `MeterType`, `MeterStatus`, `BillStatus`, `PaymentStatus`, and `OtpUsed`. [Task 2]
- `prisma/schema.prisma` currently defines `AddressResidentStatus` as `ACTIVE | INACTIVE`; older seed summaries/comments can still mention `SUSPENDED`, so seed comments/docs need explicit cleanup when touching this area. [Task 1]
- Meter-reading demo data needs to align with real app behavior around active/inactive meters, `MeterAssignment`, `MeterReading`, and reading images; inactive meters such as `seed-meter-e3`, `seed-meter-w6`, `seed-meter-apt-e3`, and `seed-meter-hq-w-b03` were identified as contradictory seeded states. [Task 1]
- The current seed forces `imageUrl` onto all readings through `seededReadingsData.map((reading) => ({ ...reading, imageUrl: meterImageUrl(reading.meterId) }))`, which blocks a true "reading without image" state. [Task 1]
- The intended current-month target in the interrupted rewrite was May 2026 (`ACTIVE_BILLING_YEAR = 2026`, `ACTIVE_BILLING_MONTH = 5`) with three cases represented: reading with image, reading without image, and no reading at all. [Task 1]
- Organization residentials are expected to have at least 2 projects; the service enforces this and the setting page renders `residential.projects` for the organization section. [Task 3]
- `Homey HQ` is the organization residential seed; adding two projects there made the organization project section usable. [Task 3]
- The relevant UI check for organization projects was `homey-next/app/(auth)/setting-residential/page.tsx`, where organization mode renders "1.3 ข้อมูลโครงการ" from `residential.projects`. [Task 3]
- `npm run build` in `homey-api` is a useful quick compile check after seed edits. [Task 3]

## Failures and how to do differently

- `seed.md` initially overstated counts/statuses; treat it as documentation only and correct it after code changes. [Task 2][Task 3]
- The full seed rewrite rollout ended with `<turn_aborted>` and no verified execution. Future agents must verify the seed against schema/DTOs before claiming completeness. [Task 2]
- A large patch to `prisma/seed.ts` was rejected with a usage-limit/tool-review failure before any edit landed. Resume this work in small focused chunks instead of one large rewrite: first repair `update` blocks, then assignment cleanup, then current-month readings, then bill/payment cleanup. [Task 1]
- Do not assume intended seed fixes are already present after an interrupted rollout. If the previous run ended on `"You've hit your usage limit..."`, first confirm quota/tool access and then re-open the actual file state before continuing. [Task 1]
- `git status` / `git diff` failed from `/Users/jj/Project/abc-homey` with "Not a git repository"; use the actual repo root if git metadata is needed. [Task 3]
- A seed inconsistency was discovered: demo residential records labeled as village had been seeded as `APARTMENT`; they were corrected to `VILLAGE`. Future seed reviews should compare comments/names/types rather than trusting one surface. [Task 3]

# Task Group: abc-homey / legacy PostgreSQL to Prisma migration, cleanup, and billing history
scope: Historical staged ETL from legacy `watermanagement` dump into Prisma target, later cleanup of that migration scaffolding, current Prisma migration continuity, Bill/Payment snapshot schema, and target DB reset guidance.
applies_to: cwd=/Users/jj/Project/abc-homey/homey-api; reuse_rule=reuse for Homey migration, cleanup, billing-history, and Prisma-migration tasks only after checking whether the current checkout still has legacy tooling; current repo state after 2026-04-29 is argon2-only and does not include `scripts/migration/`.

## Task 1: Remove legacy DB migration tooling from the API, success

### rollout_summary_files

- rollout_summaries/2026-04-21T16-54-21-PDQ5-homey_api_remove_legacy_migration_tooling.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/21/rollout-2026-04-21T23-54-21-019db0f6-dc63-7ab2-8ff5-fdbbdceb0d41.jsonl, updated_at=2026-04-29T13:40:28+00:00, thread_id=019db0f6-dc63-7ab2-8ff5-fdbbdceb0d41, cleanup verified with `npx prisma generate` and `npm run build`)

### keywords

- scripts/migration, .env.migration.example, .env.migration.local, prisma/legacy-migration-assessment, migration:restore, migration:import, bcryptjs, argon2-only, legacyBillId, legacyPaymentId, 20260429180500_remove_legacy_migration_fields

## Task 2: Keep the app's normal Prisma migration flow working after cleanup, success

### rollout_summary_files

- rollout_summaries/2026-04-21T16-54-21-PDQ5-homey_api_remove_legacy_migration_tooling.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/21/rollout-2026-04-21T23-54-21-019db0f6-dc63-7ab2-8ff5-fdbbdceb0d41.jsonl, updated_at=2026-04-29T13:40:28+00:00, thread_id=019db0f6-dc63-7ab2-8ff5-fdbbdceb0d41, normal Prisma migration flow preserved)

### keywords

- prisma generate, npm run build, normal Prisma migration flow, package-lock.json, EPERM, repo cleanup, targeted diffs, unrelated repo noise

## Task 3: Assess legacy dump and build migration scaffold, success

### rollout_summary_files

- rollout_summaries/2026-04-06T16-50-54-b4bm-homey_legacy_to_prisma_migration_billing_history_and_reset.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/06/rollout-2026-04-06T23-50-54-019d63b4-5189-7f61-8f35-cdae2525f218.jsonl, updated_at=2026-04-11T20:19:54+00:00, thread_id=019d63b4-5189-7f61-8f35-cdae2525f218, historical scaffold and docs added before later cleanup)

### keywords

- pg_restore, PGDMP, watermanagement, dump-data/test-homey_prod_db-202604060446.sql, staging DB, ETL, DIRECT_URL, .env.migration.example, restore-legacy.sh, import.ts, validate.ts

## Task 4: Make legacy bcrypt users work after migration, success

### rollout_summary_files

- rollout_summaries/2026-04-06T16-50-54-b4bm-homey_legacy_to_prisma_migration_billing_history_and_reset.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/06/rollout-2026-04-06T23-50-54-019d63b4-5189-7f61-8f35-cdae2525f218.jsonl, updated_at=2026-04-11T20:19:54+00:00, thread_id=019d63b4-5189-7f61-8f35-cdae2525f218, historical bcrypt/argon2 compatibility before later removal)

### keywords

- bcryptjs, argon2, UtilitiesService.comparePassword, AuthService.validateUser, legacy bcrypt, rehash to argon2, `$2[aby]`, `$argon2`, bcryptViaService

## Task 5: Add Bill/Payment schema and switch bills endpoint to snapshot data, success

### rollout_summary_files

- rollout_summaries/2026-04-06T16-50-54-b4bm-homey_legacy_to_prisma_migration_billing_history_and_reset.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/06/rollout-2026-04-06T23-50-54-019d63b4-5189-7f61-8f35-cdae2525f218.jsonl, updated_at=2026-04-11T20:19:54+00:00, thread_id=019d63b4-5189-7f61-8f35-cdae2525f218, `npx tsc --noEmit` passed)

### keywords

- BillStatus, PaymentStatus, Bill, Payment, bill snapshots, BillsService.findAllForBillingMonth, confirmPayment, prisma.bill.findMany, migration.sql, imageUrl, paymentDate

## Task 6: Import billing history into `homey_new_target`, validate, then truncate target data, success

### rollout_summary_files

- rollout_summaries/2026-04-06T16-50-54-b4bm-homey_legacy_to_prisma_migration_billing_history_and_reset.md (cwd=/Users/jj/Project/abc-homey/homey-api, rollout_path=/Users/jj/.codex/sessions/2026/04/06/rollout-2026-04-06T23-50-54-019d63b4-5189-7f61-8f35-cdae2525f218.jsonl, updated_at=2026-04-11T20:19:54+00:00, thread_id=019d63b4-5189-7f61-8f35-cdae2525f218, imported 3865 bills before later wipe)

### keywords

- homey_new_target, DOTENV_CONFIG_PATH=.env.migration.local, prisma migrate deploy, import-billing-history.ts, validate-billing-history.ts, meterReadingId unique constraint, reading_id, bills = 3865, payments = 0, TRUNCATE, _prisma_migrations

## User preferences

- when the user said "ในฝั่งของ API ในส่วนที่เกี่ยวข้องกับ database migration จาก database อันเก่ามาอันใหม่ให้ลบทิ้งไปก่อน" -> treat cleanup as targeting only legacy migration scaffolding and leave the app's normal Prisma migrations working. [Task 1][Task 2]
- when the user asks in Thai to migrate old SQL into the new Prisma schema "without losing data" -> prefer concrete repo-specific migration guidance, not generic advice. [Task 3]
- when the user said "ถ้าเขียนออกมาเป็นไทยได้จะดีมากๆ" -> prefer Thai writeups for this migration work. [Task 3]
- when the user asked "แล้วโค้ดต้องใช้อะไรและวิธีการเขียน เขียนยังไง" and later asked to write files with backups -> translate the plan into actual repo artifacts and code, not only chat guidance. [Task 3]
- the user's goal was to preserve data and usability, which includes migrated accounts being able to authenticate after import. [Task 4]
- when the user said bill history is important and asked to do the schema/service parts first -> prioritize Bill/Payment schema and backend behavior before broader follow-up tasks. [Task 5]
- when the user said images stay on the old bucket for now and duplicate emails can be nulled -> do not move file blobs or over-solve duplicate email handling during this migration phase. [Task 5]
- when the user asked to clear everything from `homey_new_target` before checking again -> preserve schema/migration history but empty application data tables. [Task 6]

## Reusable knowledge

- Related skill: skills/abc-homey-prisma-data/SKILL.md. [Task 1][Task 2][Task 3][Task 4][Task 5][Task 6]
- Current repo state after the cleanup: legacy migration tooling under `scripts/migration/`, `.env.migration*`, and `prisma/legacy-migration-assessment*.md` was removed; `package.json` no longer carries `migration:*` scripts. [Task 1]
- Current auth state after the cleanup: `UtilitiesService.comparePassword()` is argon2-only and `AuthService.validateUser()` no longer rehashes bcrypt. If legacy imports are revived later, bcrypt compatibility would need to be reintroduced intentionally. [Task 1][Task 4]
- Current schema cleanup state: `Bill` and `Payment` no longer include `legacyBillId` / `legacyPaymentId`; `prisma/migrations/20260429180500_remove_legacy_migration_fields/migration.sql` drops those columns through a normal Prisma migration. [Task 1][Task 2]
- After removing legacy tooling, the stable way to keep schema/client alignment was a normal Prisma migration plus `npx prisma generate`, followed by `npm run build`. [Task 2]
- Historical migration context, only if this capability needs to be rebuilt: the dump `dump-data/test-homey_prod_db-202604060446.sql` is a PostgreSQL custom dump (`PGDMP`) from schema `watermanagement`; the prior successful path used `pg_restore -l`, `pg_restore -s`, isolated staging restore, then ETL. [Task 3]
- Historical scaffold names, only for recovery/rebuild work: the removed migration workspace had `scripts/migration/common.ts`, `helpers.ts`, `import.ts`, `validate.ts`, `restore-legacy.sh`, and `.env.migration.example`. [Task 1][Task 3]
- `Bill` snapshot fields include `waterUsage`, `previousValue`, `currentValue`, `unitPrice`, `baseAmount`, `additionalFeesAmount`, `otherCharges`, `totalAmount`, `dueDate`, `status`, `paymentDate`, `paymentMethod`, and `receivedByName`. [Task 5]
- `Payment` stores `amount`, `paidAt`, `method`, `referenceNo`, `status`, `slipUrl`, `remark`, and `receivedById`. [Task 5]
- `BillsService.findAllForBillingMonth()` is snapshot-driven through `prisma.bill.findMany(...)`; frontend history should not rely on live recomputation from `meter_readings`. [Task 5]
- Historical billing import validation matched source and target counts exactly: `bills = 3865`, `payments = 0`, and all bills linked to readings before the later target wipe. [Task 6]
- After the user-requested wipe, `homey_new_target` had schema/migration history applied up to `20260410093000_add_bill_and_payment_models`, but app data tables were empty. [Task 6]

## Failures and how to do differently

- Do not assume the April 2026 legacy-migration scaffold still exists in the repo; check the current checkout first. After 2026-04-29, any legacy import work would require recreating the tooling intentionally. [Task 1][Task 3]
- `npm install --package-lock-only --ignore-scripts` hit `EPERM` on `package-lock.json` during cleanup; permission-sensitive npm rewrites in this environment may need a different execution context. [Task 1][Task 2]
- Cleanup happened in a repo with many unrelated modified/untracked files; use targeted diffs instead of assuming the full worktree belongs to the task. [Task 1][Task 2]
- Do not treat the dump as plain SQL; use `pg_restore` into staging first. [Task 3]
- Do not import directly from dump into target DB; staging restore + ETL + validation was the stable path. [Task 3]
- Unknown hash formats should fail closed by returning `false`, not throwing in the login flow. This matters only if bcrypt compatibility is reintroduced again. [Task 4]
- The first billing import failed because a naive one-to-one `meterReadingId` mapping did not fit legacy data; legacy bills can repeat for the same `meter_id + billing_month`. [Task 5][Task 6]
- The failed billing import left 84 partial rows; the safe recovery was to truncate `public.bills` and `public.payments`, remap using legacy `reading_id` with grouped ordering, and rerun. [Task 6]
- When target DB should be "empty", truncate application tables with `RESTART IDENTITY CASCADE` while leaving `_prisma_migrations` intact instead of dropping/recreating schema. [Task 6]

# Task Group: abc-homey / GCP Docker, Cloud Run, Artifact Registry deployment
scope: Frontend/backend containerization and GCP deployment packaging for Homey, including Cloud Run, Artifact Registry, Cloud SQL, env-driven CORS/cookies, and image reference explanations.
applies_to: cwd=/Users/jj/Project/abc-homey; reuse_rule=reuse for Homey deployment packaging and explanation tasks; verify current project IDs, registry repos, service names, and env values before issuing commands.

## Task 1: Frontend Docker + Cloud Run + Artifact Registry deployment packaging, success

### rollout_summary_files

- rollout_summaries/2026-03-30T16-37-30-LMPj-abc_homey_gcp_docker_cloud_run_artifact_registry.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/03/30/rollout-2026-03-30T23-37-30-019d3f9b-87bb-7f82-97f8-20ec2af44bb5.jsonl, updated_at=2026-04-01T07:29:32+00:00, thread_id=019d3f9b-87bb-7f82-97f8-20ec2af44bb5, frontend Docker/Cloud Run files added)

### keywords

- homey-next, Dockerfile, output standalone, NEXT_PUBLIC_API_URL, build arg, Cloud Run, Artifact Registry, cloudbuild.yaml, port 8080, Next.js Turbopack sandbox

## Task 2: Backend Docker + Cloud Run + Cloud SQL deployment packaging, success

### rollout_summary_files

- rollout_summaries/2026-03-30T16-37-30-LMPj-abc_homey_gcp_docker_cloud_run_artifact_registry.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/03/30/rollout-2026-03-30T23-37-30-019d3f9b-87bb-7f82-97f8-20ec2af44bb5.jsonl, updated_at=2026-04-01T07:29:32+00:00, thread_id=019d3f9b-87bb-7f82-97f8-20ec2af44bb5, backend Docker/Cloud Run/Cloud SQL files added)

### keywords

- homey-api, Cloud SQL, DB_SOCKET_PATH, --add-cloudsql-instances, runtime-config.ts, env-driven CORS, COOKIE_SAME_SITE, COOKIE_SECURE, Prisma generate, DIRECT_URL placeholder, openssl, trust proxy

## Task 3: Docker image reference/path semantics and command validation, success

### rollout_summary_files

- rollout_summaries/2026-03-30T16-37-30-LMPj-abc_homey_gcp_docker_cloud_run_artifact_registry.md (cwd=/Users/jj/Project/abc-homey, rollout_path=/Users/jj/.codex/sessions/2026/03/30/rollout-2026-03-30T23-37-30-019d3f9b-87bb-7f82-97f8-20ec2af44bb5.jsonl, updated_at=2026-04-01T07:29:32+00:00, thread_id=019d3f9b-87bb-7f82-97f8-20ec2af44bb5, image reference explanation accepted)

### keywords

- docker push, docker build --platform linux/amd64, REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY/IMAGE:TAG, asia-southeast1-docker.pkg.dev, abc-homey, homey-old, test-for-dev, homey-api-new

## User preferences

- when the user asks to build frontend/backend as Docker images for GCP using Artifact Registry, Cloud Run, and Cloud SQL -> provide deploy-ready configs and concrete commands, not just conceptual advice. [Task 1][Task 2]
- when the user answered `ใช่` to continue backend deployment setup -> proceed to the obvious next infrastructure step without asking again. [Task 2]
- when the user asks what each part of the image string means after `docker push` -> decompose registry/project/repository/image/tag precisely. [Task 3]
- when the user asks whether an alternate image ref shape is valid -> answer syntax validity directly and distinguish build-time local tagging from push-time repo existence/auth failures. [Task 3]

## Reusable knowledge

- `homey-next` uses `output: 'standalone'`; its Dockerfile runs on port `8080`. [Task 1]
- `NEXT_PUBLIC_API_URL` is build-time for the client bundle, so it must be passed as a Docker build arg and the frontend image must be rebuilt if the backend URL changes. [Task 1]
- `homey-api/src/shared/runtime-config.ts` centralizes CORS origins, cookie settings, and DB connection construction. [Task 2]
- `PrismaService` can build the DB connection string from `DIRECT_URL` or split env vars such as `DB_SOCKET_PATH`/`DB_HOST`, `DB_NAME`, `DB_USER`, and `DB_PASSWORD`. [Task 2]
- Cloud Run + Cloud SQL pattern here is Unix socket path plus `--add-cloudsql-instances`; the frontend should never connect to Cloud SQL directly. [Task 2]
- Cookie auth across separate Cloud Run services needs CORS allowlisting plus `COOKIE_SAME_SITE=none` and `COOKIE_SECURE=true` in production. [Task 2]
- Artifact Registry image reference format used here is `REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY/IMAGE_NAME:TAG`. `docker build -t` only tags locally; `docker push` requires the Artifact Registry repo to exist and auth to be configured. [Task 3]

## Failures and how to do differently

- Next.js build hit a sandbox/Turbopack limitation once; rerunning outside the sandbox succeeded. Treat similar failures as possibly environment-specific before rewriting code. [Task 1]
- `prisma generate` initially failed in Docker because Prisma config required DB env; adding a placeholder `DIRECT_URL` build arg fixed image build. [Task 2]
- Prisma warned about OpenSSL in the container; installing `openssl`/`ca-certificates` in the base image removed the warning. [Task 2]
- The first `main.ts` change used a non-existent `app.set` method; setting `trust proxy` through the underlying Express instance resolved it. [Task 2]
