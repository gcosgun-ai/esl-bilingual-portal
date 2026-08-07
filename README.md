# ESL & Bilingual Department Portal

Live department portal for iLearn Schools' ESL & Bilingual Department — dashboard,
program timeline, identification/exit workflows, parent notice templates, weekly
PLC cohorts, PAC tracking, WIDA reference material, and curriculum links.

**Live site:** https://gcosgun-ai.github.io/esl-bilingual-portal/

## Access model

**Staff-only.** Nothing renders until the visitor signs in with a Google Workspace
account on an approved iLearn domain:

`ilearnschools.org` · `bergencharter.org` · `passaiccharter.org` ·
`patersoncharter.org` · `hudsoncharter.org` · `bronxcharter.org`

Two tiers:

- **View** — any approved domain. All sections, printable forms, and links.
- **Edit** — the Department Head (`gcosgun@ilearnschools.org`) only. Every data-entry
  field is disabled for everyone else.

Enforced in two places: the UI here, and the Firebase security rules server-side.
The rules are the real boundary — the database refuses reads from unapproved accounts
and writes from anyone but the Department Head, so editing the page in devtools
achieves nothing. Signing out also clears the local cache, so department data isn't
left behind in a shared browser.

## Firebase security rules

Apply `firebase-rules.json` in the Firebase console under
**Realtime Database → Rules → paste → Publish**. Reads require a verified Google account on an approved iLearn domain; writes require
the Department Head's account specifically. Everything outside `store` is denied.

Google sign-in must be enabled under **Authentication → Sign-in method**, and every
domain the portal is served from must be listed under **Authentication → Settings →
Authorized domains** (currently `gcosgun-ai.github.io`).

### Embedding

Google sign-in popups do not work reliably inside cross-origin iframes, so when the
portal is embedded (e.g. Google Sites) it detects this and offers an "Open the portal
to sign in" link that breaks out to a real tab. Embedding it in a restricted Google
Site does **not** restrict the portal — the sign-in gate above is what does.

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
