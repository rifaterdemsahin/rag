# Timebox Estimation Formula & Timeline Template
 
Purpose
- Provide a repeatable formula for estimating time-to-release and a minimal checklist + calendar reminders.
 
Core formula
- TotalDays = DevDays + QA_Days + StoreReview_Days + ReleasePrep_Days + Buffer_Days + Contingency_Days
 
Where:
- DevDays = sum of developer effort (in days) for all scope items.
- QA_Days = manual + automated QA cycles (include regression runs).
- StoreReview_Days = App Store + Play Store review window (include remediation).
- ReleasePrep_Days = release notes, signing, assets, legal/privacy, marketing checklist.
- Buffer_Days = 10–30% of (DevDays + QA_Days) as schedule buffer.
- Contingency_Days = risk allowance (e.g., 3–7 days) for external blockers (signing, backend).
 
Guidelines / multipliers (recommended)
- QA_Days = ceil(0.5 * DevDays) + 2 (minimum)
- Buffer_Days = ceil(0.2 * (DevDays + QA_Days))
- Contingency_Days = 3 (low risk) → 7 (high risk)
 
Example (use values from current roadmap)
- DevDays = 9  (persistence 4 + perf 4 + polish 1)
- QA_Days = ceil(0.5*9)+2 = 7
- StoreReview_Days = 7 (Apple typical + Play overlap)
- ReleasePrep_Days = 3
- Buffer_Days = ceil(0.2*(9+7)) = ceil(3.2) = 4
- Contingency_Days = 4
 
TotalDays = 9 + 7 + 7 + 3 + 4 + 4 = 34 days (~5 weeks)
 
Minimal sprint plan (2-week sprint focus)
- Week 0 (Plan 1 day): lock scope & acceptance criteria
- Week 1: Dev (persistence + tests)
- Week 2: Dev (perf + fixes) + QA starts
- Week 3: QA wrap, polish, release prep
- Week 4: Submit to stores + monitor / remediate
 
Release checklist (must-haves before submission)
- Acceptance criteria passed for scoped items
- Passing CI + integration tests
- Crash reporting & analytics integrated
- Privacy/legal checklist + permissions documented
- App store assets + release notes prepared
- iOS signing / provisioning verified with intended team
 
How to use this template
1. Substitute DevDays with your team estimate.
2. Apply the multipliers above to compute QA/Buffer.
3. Pick a start date and use the timeline script to generate dated milestones and an .ics file you can import to your calendar.
 
Risks to consider (impact on contingency)
- iOS provisioning/signing issues
- Backend/API readiness
- Performance regressions on low-end devices
- Failing or flaky CI tests
- App Store rejections (privacy / permissions / crashes)
