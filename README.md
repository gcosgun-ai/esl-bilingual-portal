# ESL & Bilingual Department Portal

Live department portal for iLearn Schools' ESL & Bilingual Department — dashboard,
program timeline, identification/exit workflows, parent notice templates, weekly
PLC cohorts, PAC tracking, WIDA reference material, and curriculum links.

**Live site:** https://gcosgun-ai.github.io/esl-bilingual-portal/

## Access model

The portal is **view-only for everyone** by default. Any visitor with the link can
browse all sections, print the forms, and follow the external links, but cannot
change any data.

Editing is restricted to the Department Head (`gcosgun@ilearnschools.org`) via
Google sign-in. Signing in unlocks every data-entry field; those values then sync
in real time to everyone viewing the site, powered by Firebase Realtime Database.

The lock is enforced in two places: the UI disables fields client-side (for clarity),
and the Firebase security rules reject unauthorized writes server-side (the actual
security boundary — removing the disabled attribute in devtools achieves nothing).

## Firebase security rules

Apply `firebase-rules.json` in the Firebase console under
**Realtime Database → Rules → paste → Publish**. These rules allow the whole world
to *read* the `store` path, but permit *writes* only from the Department Head's
authenticated Google account. Everything outside `store` is denied by default.

Google sign-in must also be enabled under **Authentication → Sign-in method**, with
`gcosgun-ai.github.io` listed under **Authentication → Settings → Authorized domains**.

## Updating the site

This is a single static `index.html` file — no build step. Edit it and push to
`main`; GitHub Pages redeploys automatically within a minute or two.

## Sections

**New Jersey (default):** Dashboard, Program Timeline, Identification, Service & Instruction,
Exit & Reclassification, Former ML Monitoring, Parent Notices, Weekly PLC, PAC, WIDA ELD
Standards, Curriculum Files.

**Lesson Plans & Journals:** the three department templates (ESL Pull-Out Lesson Plan,
Teacher Push-In Journal, Aide Push-In Journal) as downloadable `.xlsx` files in `templates/`,
plus printable blank forms and the weekly Google Drive submission process.

**New York — Bronx:** ENL Program & Regulations (CR Part 154), NY Timeline 2026–27, and
NY Resources. Shown in purple throughout so NJ and NY requirements are never confused.

### New York sources

The NY section was built from four documents, all verified claim-by-claim against source text:

- NYC DOE *Policy and Reference Guide for MLs/ELLs*, August 2025 (SY 2025–26)
- NYSED *Final Dates for the 2026–27 Elementary- and Intermediate-level Testing*, June 2026
- NYSED *Model Policy and Compliance Procedures: NY Educ. Law § 3201-b*, effective May 27, 2026
- NYSED *Blueprint for ELL/MLL Success* (OBEWL)

Resource links come from the CTE Technical Assistance Center of New York (nyctecenter.org).

### Known caveats for the NY section

1. **2026–27 is a WIDA transition year.** The final NYSESLAT was Spring 2026. WIDA ACCESS is
   the annual assessment this year (Feb 1 – Apr 9, 2027); NYSITELL remains the identification
   test until the WIDA Screener replaces it in Fall 2027. The NYC guide predates this and says
   "NYSESLAT" throughout.
2. **Exit cut scores are unconfirmed.** The three exit pathways in the app are the NYSESLAT-era
   criteria. Confirm the WIDA ACCESS exit determination with OBEWL before exiting any student.
3. **Charter vs. NYC DOE.** Bronx ASCS is a NY charter school, so NYC DOE systems (ATS, STARS,
   iPlan, LAP, ELPC/BNDC screens, Aspira Consent Decree) do not apply. CR Part 154 itself does.
   The app states this split explicitly.
4. **Student deadlines are school-day counts.** Dates shown assume enrollment on the first day
   (Aug 31, 2026) and were computed against the Bronx ASCS 2026–2027 calendar, validated by
   reproducing that calendar's month totals and quarter boundaries. For later enrollees, count
   from their own enrollment date.
