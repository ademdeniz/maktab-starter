# CLAUDE.md – maktab website

A maktab teacher's own copy of the Maktab website (made from the starter of the Bosnian Islamic Community of Erie).
The teacher is usually not technical: one question at a time, plain words, show previews, never ask them to edit files.

## Rules
- Only ever commit and push to the teacher's OWN repository. Check `git remote -v` before every push; never push to,
  open a pull request on or change anything under `ademdeniz` (the Erie website and this starter).
- Never ask for or accept passwords, the Supabase secret key (`sb_secret_…`), a database password, a Gmail app password
  or card numbers. Only the Supabase Project URL and publishable key (`sb_publishable_…`) go into `supabase/config.json`.
- Children's privacy: no children's names, photos or contact details on any page; parents first name + last initial;
  weekly updates only say how many children came.
- Keep the credits (Abdo ef. Rekić – games; El-Kalem – Ilmihal books; Sahih International; Alafasy) – `credits/`.
- Qur'an quotes are Sahih International word for word (the tests check); never change religious content without asking.
- Run the tests (`.venv/bin/pytest tests`) before every publish; never publish with a failing test.

## How the site is built
- `site.json` – the mosque's name, short name, logo, website address, contact. After changing it (and the logo file):
  `python3 tools/build_site.py` rebuilds every page.
- `data/plan/plan.json` – the school year: start/end (the weekday of `start` is the class day), no-class days, groups and
  what each learns (tracks: ilmihal book 1–3, quran, sufara, tajwid), notes. Then `python3 tools/build_plan.py`.
- Lessons: `data/lessons/ilmihal-N/<book page>-<name>.json` → `python3 tools/build_lessons.py` (see README of the
  Erie site for the lesson format; book PDFs are needed to build new lessons and pictures).
- Weekly parent update: `data/updates/<date>.json` → `python3 tools/build_update.py <date>`. Sent updates are not rebuilt.
- Parent duty page: `data/duty/parents.json` → `python3 tools/build_duty.py`.
- Publishing = commit + push to `main`; GitHub Pages updates in 2–5 minutes (Ctrl/Cmd+Shift+R to see it).
