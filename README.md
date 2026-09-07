# SmartSync

AI-assisted anomaly detection for SAP ↔ Salesforce data reconciliation. A portfolio case study project.

**[Live demo](#)** · **[Full case study](./CASE_STUDY.md)**

![status](https://img.shields.io/badge/status-demo-4FD1C5) ![type](https://img.shields.io/badge/type-portfolio_project-16202C)

## What this is

A reconciliation console that compares mock SAP and Salesforce records, flags discrepancies (price mismatches, quantity differences, missing syncs, stale fields), ranks them by severity, and shows the exact field-level diff with a suggested fix — instead of two spreadsheets and a manual cross-check.

## Running it

No build step, no install. It's a single static HTML file using React via CDN.

- **Locally:** open `index.html` directly in a browser, or run a tiny local server:
  ```bash
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```
- **On GitHub Pages:** push this repo to GitHub, then in **Settings → Pages**, set the source to the `main` branch, root folder. Your live URL will be `https://<your-username>.github.io/smartsync/`.

## Structure

```
smartsync/
├── index.html       # the app (React, no build step)
├── CASE_STUDY.md     # pain point / solution / market / how I got here
└── README.md
```

## Why no build tooling

This is meant to be cloned and deployed in minutes, by anyone, with zero setup — so it uses React + Babel Standalone from a CDN instead of Vite/webpack. That's a deliberate tradeoff for a demo project: instant deploy over build-time optimization.
