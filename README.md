# The "100-Tab" Problem: In-Place Navigation (Concept POC)

An interactive concept exploring a calmer way to drill into records in a business or workflow application: **one tab, one place, no tab sprawl.**

> Personal concept. "Ledgerline" is a fictional product and all data is invented. Views are my own.

Inspired by my LinkedIn article, *The "100-Tab" Problem: Why Careless Navigation Breaks Customer Experience (And How to Fix It)*.

## The idea

You log in to complete a two-minute task: review a customer, check an order, adjust a setting.

- You click a row. New tab.
- You open the detail view. Another new tab.
- You open a linked document. A third new tab.

Before long the tab strip is an accordion, favicons shrink to specks, and the user's mental model fragments. This concept changes one thing: drill-down **updates the current tab in place** instead of spawning a new one.

## What the demo shows

A simulated browser window with a small fictional app (Customers, Orders, Settings).

- **Proposed** mode: rows and links update the current tab in place. Breadcrumbs keep the trail visible, the invoice opens in a slide-over drawer so the order stays in view, and the tab counter stays at 1.
- **Today** mode: every drill-down (row, link, document) opens a new tab. The tab strip fills up, the counter climbs, and a "Tab triage" button shows the clean-up users end up doing by hand.
- **Stale state**: in Today mode, open the same customer in two tabs and toggle its status in one. The other tab goes stale and shows an out-of-date warning.
- **Deep links**: the URL hash updates on every step in Proposed mode, so Back, Refresh and bookmarks work.
- **Unsaved work guard**: edit a field on Settings (or tick "Simulate unsaved work") and navigate in Proposed mode to see the leave-page confirmation a real build would need.
- A "Design considerations" panel with the points below.

## Run it

Open `index.html` in any modern browser. It is a single self-contained file with no build step, no dependencies, no images and no network calls. It also works on GitHub Pages.

Suggested walkthrough:

1. In **Today** mode, click Customers > Maple Grove Co. > an order > View invoice. Note the tab count.
2. Open the same customer again, toggle its status, and switch back to the older tab.
3. Click **Proposed** and repeat the same path. Note the single tab, the breadcrumbs and the drawer.
4. Use the simulated Back button to retrace your steps.

## Why it matters

| Impact | What happens |
|---|---|
| Context fragmentation | Users lose the trail of breadcrumbs and spend effort managing tabs instead of the task. |
| State disconnects | Each tab holds its own copy of the data. An update in one leaves the others stale unless cross-tab sync is built. |
| Execution friction | Repetitive tasks leave dozens of tabs behind, followed by manual clean-up at the end of the day. |

## Design considerations

| Area | Consideration |
|---|---|
| Replace and close | Closing a tab from client-side script is restricted: `window.close()` generally only works on windows opened by script. "Close the previous tab" is therefore best realised as single-window routing rather than literal tab closing. |
| In-place routing | Fits single-page-application routing (for example React Router, Vue Router or micro-frontends), with state in URL parameters or a client store. |
| Spatial continuity | Pair in-place rendering with breadcrumbs, drawers or modals so users know where they came from and how to step back. |
| Unsaved work | In-place navigation can discard edits. A leave-page or router guard is part of the design, not an afterthought. |
| Deep links | Each view needs a stable URL so browser navigation and bookmarks work. |
| Deliberate new tabs | Exports, print views, external links and side-by-side comparison are better as an explicit "open in new tab" action. Scope this change to routine drill-down. |

## Limitations of this POC

- It is a simulation of the interaction, not an integration with a real application.
- Tab counts are simulated. Memory use, load times and real-user effort are not measured.
- The simulated Back button is disabled in Today mode, and the real browser's Forward button is not modelled.
- Behaviour with real data, permissions and long-running pages is untested.

## Disclaimer

Ledgerline is a fictional product created for illustration of a UX concept only. Any resemblance to a real product is coincidental.
