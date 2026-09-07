# SmartSync — Reconciliation console for SAP ↔ Salesforce

*A portfolio case study by Elnaz, Business Systems Analyst*

[→ View the live demo](./index.html)

---

## The pain point

Any company running SAP (or another ERP) alongside Salesforce ends up maintaining the same facts — order totals, quantities, account details, statuses — in two systems that were never designed to fully agree with each other. Batch syncs run on a delay, reps override fields by hand, and integration jobs quietly fail on edge cases.

The result is a slow leak of trust in the data. Analysts find out about a mismatch when a customer disputes an invoice, or when month-end reporting doesn't tie out — by which point the error has already touched a quote, a shipment, or a forecast. The usual fix is a recurring manual audit: someone exports both systems to Excel and eyeballs the differences. It works, but it doesn't scale, it's error-prone, and it only catches problems after the fact.

## The solution

SmartSync is a lightweight reconciliation layer that sits between the two systems and does the audit continuously instead of manually:

- **Match** records across SAP and Salesforce by a shared key (order number, account ID).
- **Score** every discrepancy by business impact — a price mismatch on an open order outranks a stale timestamp on a closed one.
- **Surface** a short, ranked worklist instead of two spreadsheets, with the exact field-level diff and a suggested resolution for each item.
- **Trend** reconciliation health over time, so a spike in one discrepancy category (say, discount % mismatches after a pricing change) gets caught as a pattern, not seven separate tickets.

It's deliberately rules-based rather than a black-box model: for a finance-adjacent workflow, an analyst needs to see *why* something was flagged and trust the suggested fix enough to act on it. The "AI-assisted" part is the scoring and prioritization layer, not an opaque classifier — a decision made explicitly to keep the tool explainable to the people who have to act on its output.

## The market

This is built for the gap between two extremes:
- **Too small for an iPaaS platform** — tools like Boomi or MuleSoft solve this properly, but they need dedicated integration engineers to configure and maintain, which most mid-market manufacturers and distributors don't have on staff.
- **Too big for spreadsheets** — once you're past a few hundred records a week, manual cross-referencing stops being viable.

The target user is a BA, ops, or RevOps analyst at a mid-market manufacturer, distributor, or PE portfolio company running a dual ERP+CRM stack — someone who owns data quality but doesn't have engineering headcount to throw at it.

## How I got here

- **Discovery** — This came directly out of recurring pain seen during ERP/CRM integration and UAT work: the same categories of mismatch (price, quantity, missing sync, stale fields) kept resurfacing across cycles, always caught manually and always after the fact.
- **Framing** — I treated this as a BA problem first — a data-quality and process gap — rather than jumping straight to a dev solution. I shortlisted the discrepancy types worth building for using an impact-vs-effort pass, and deliberately scoped out anything that needed a trained model on day one.
- **Design tradeoff** — Rules + weighted scoring over machine learning, on purpose. There isn't enough labeled mismatch history on day one to train a reliable classifier, and explainability matters more than marginal accuracy for a tool that's recommending financial corrections.
- **Build** — Modeled realistic SAP/Salesforce export shapes, built the matching and scoring logic, and iterated on the console's layout with Claude — moving from a plain table to a ranked worklist with an inline diff view once it was clear analysts needed the "why," not just the "what."
- **Next steps** — Wire up real API pulls instead of static exports, make the scoring weights configurable per client, and start collecting labeled resolution outcomes so a proper anomaly-detection model becomes viable later.

---

*Tech: single-file React app (via CDN, no build step) so it deploys straight to GitHub Pages. See [`index.html`](./index.html).*
