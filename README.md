# GPBL site prototype (private, not deployed)

A phone-first redesign of gamepigeonbattleleague.com that replaces the embedded Google Sheets with a native schedule, result reporting, standings and bracket. Plain HTML/CSS/JS, no build step.

**All rosters, schedules, results, belt holders and trophy counts are SAMPLE data.** Real names come from the public site; "Sample Player N" are placeholders. Results save only in this browser (localStorage).

## Run
    cd gpbl && python3 -m http.server 8000   # open http://localhost:8000
    node test.js                              # logic tests

## Files
- index.html, styles.css, app.js: the site (hash routes: #/, #/match, #/schedule, #/standings, #/bracket, #/rules, #/belts, #/trophies, #/records, #/archive, #/fit, #/merch, #/about, #/join, #/proposal, #/more)
- core.js: schedule (week windows, round robin), standings (3/1/0, win% with draw = 0.5, head-to-head, best-of-3 flag, streaks), bracket seeding. Shared by browser and node tests.
- data.js: league config and sample data. test.js: node tests.
- manifest.json, icon.svg, icon-180/192/512.png: Home Screen install.

## Demo notes
- The demo clock is fixed at Nov 9 2026 12:00 PM ET (mid-season) so countdowns and results make sense.
- "Executive mode" is a demo toggle with no login.
- The Join form sends and stores nothing.

## Deploying for real (needs exec approval)
1. Static hosting: GitHub Pages, Netlify or Cloudflare Pages.
2. Shared data and logins: a small backend such as Supabase (Postgres + auth). Tables: players, leagues, seasons, matches, results(status: pending/confirmed/disputed/resolved), roles(exec/arbiter).
3. Row-level security so players can only report or confirm their own matches; execs can override.
4. Discord webhook or bot: post confirmed results and deadline reminders (send/start and finish).
5. Import rosters, all-time stats, records and archives from the current sheets once; then retire the public workbook (including the ADMIN tabs).
