# RoundReady — Product Write-up

**The problem.** During Indian campus placement season, a TPO fits forty companies into eight weeks. Students track drives across WhatsApp, notice boards, portals and spreadsheets, but still cannot answer four questions: Am I eligible? Does this clash? Does placement policy allow me to sit for it? And what does accepting an offer close?

**Why not an existing tracker.** Huntr, Teal and Notion serve self-directed job hunting. Campus placement is different: the calendar is imposed, eligibility is a hard filter, rounds collide, and accepting an offer can silently close other opportunities. General trackers do not model these constraints.

**What I built.** RoundReady is a decision engine with a list attached. Students enter their CGPA, backlogs and branch once. The board explains eligibility, identifies policy-blocked or undecidable drives, ranks available opportunities and flags scheduling conflicts. Drives are shared across a college and graduating batch, while student profiles and applications remain private.

**The decision I am proudest of.** Nothing derived is stored: no `isEligible` column, clash flag or cached score. Verdicts are recomputed from current profiles, drives and applications, preventing stale eligibility badges. The offer simulator compares the board against a hypothetical accepted offer, showing which companies would close without touching real data.

**The detail that matters.** Clash detection uses half-open intervals: a 10:00–11:00 test does not conflict with one starting at 11:00. This prevents false alarms for back-to-back rounds.

**Two roles, one asymmetry.** CDC officers publish drives and configure higher-offer multipliers; students manage their own placement journey. The distinction matters because eligibility criteria and policy affect an entire batch. Students can inspect the multipliers behind a verdict rather than receiving an unexplained cutoff.

Building exposed a subtle defect: the board's headline policy figure was calculated separately from its verdicts, ignoring batch-specific multipliers. A student with a 1.75× policy could see a 1.5× headline above drives blocked at the higher threshold. I fixed this by deriving the headline from the board that produced the verdicts.

**Where I stopped.** I left out notice scraping and notifications to prioritise the decision engine. The suite reports 427 tests, 99% statement coverage and 95% branch coverage, including checks that demo data matches its claims.