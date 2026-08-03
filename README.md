# ESL & Bilingual Department Portal

Live department portal for iLearn Schools' ESL & Bilingual Department — dashboard,
program timeline, identification/exit workflows, parent notice templates, weekly
PLC cohorts, PAC tracking, WIDA reference material, and curriculum links.

**Live site:** https://gcosgun-ai.github.io/esl-bilingual-portal/

## How data sharing works

All data-entry fields (campus counts, checklists, PLC rosters, notice tracking,
etc.) sync in real time for every visitor via Firebase Realtime Database. There
is no login — anyone with the link can view and edit, the same trust model as
a shared Google Sheet link.

## Firebase security rules

Apply `firebase-rules.json` in the Firebase console under
**Realtime Database → Rules → paste → Publish**. This restricts reads/writes to
the `store` path only (everything the app actually uses) and denies everything
else by default.

## Updating the site

This is a single static `index.html` file — no build step. Edit it and push to
`main`; GitHub Pages redeploys automatically within a minute or two.
