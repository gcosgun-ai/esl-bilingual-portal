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
