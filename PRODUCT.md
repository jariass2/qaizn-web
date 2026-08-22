# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Primary user: the owner or general manager of a Spanish PyME (roughly 10–200 employees), non-technical, evaluating whether AI is worth their time and money. They arrive skeptical and time-poor, usually already running an ERP and/or CRM, and are judging feasibility and payback rather than technology. The site is Spanish-language only.

## Product Purpose

qaizn is an AI consultancy that helps Spanish SMEs apply artificial intelligence to their existing operations — process automation, predictive analysis and dashboards, ERP/CRM optimization, and internal assistants for their teams. Success for the site is a booked diagnostic call: the visitor converts by scheduling a discovery/diagnostic session, not by downloading or self-serving.

## Positioning

The name fuses AI with *kaizen* — continuous improvement. The differentiator is not a product but a method: diagnóstico → proyecto piloto → escalado e integración → optimización continua, sized so a PyME sees measurable results in 4–6 weeks rather than committing to a multi-year transformation. AI is applied inside the systems the client already runs, not sold as a replacement platform.

## Operating Context

Clients are evaluated and served around their existing stack (ERP, CRM, administrative workflows, customer service channels). The four-stage engagement above is the factual shape of the work. Named problem set the product addresses: repetitive time-consuming tasks, unused data, high operating costs, and decisions made on intuition.

## Capabilities and Constraints

Delivered service lines: automatización inteligente, análisis predictivo y dashboards, optimización de procesos, asistentes inteligentes para equipos.

Technical constraints:
- The live site is `index.html`, plain hand-edited HTML with its CSS and JS inline. Edit it directly.
- `clasico.html` is the previous design, still deployed and documented in `DEPLOY.md` as the rollback path. It is the bundled build: its markup is a JSON-escaped HTML string inside a `<script type="__bundler/template">` tag, with assets inlined as base64/gzip and resolved to blob URLs at runtime. It cannot be regenerated from this repo and is not edited by hand.
- Earlier versions (`index_old.html`, `hero-neobrutalist-backup.html`, `qaizn2.html`) were deleted on 2026-08-22; they remain in git history.
- No build tooling, package manager, or framework is present in the repo.
- `index.html` hides its content behind `.reveal` (opacity 0) until JS adds `.visible`. A `<noscript>` override and a `prefers-reduced-motion` rule keep the page readable without JS or with motion disabled. The contact form still requires JS to submit.

Resolved: the live page moved to plain source files. The bundle survives only as `clasico.html`.

## Brand Commitments

- Name is lowercase **qaizn**, pronounced "kaizen". In the wordmark, **AI** is always uppercase and accented in color: q**AI**zn. Never "ai" lowercase.
- Logo: circular dotted ring (continuous-improvement cycle) with 7 interconnected neural nodes and a central ascending arrow. Assets: `qaizn-logo.svg`, `qaizn-logo-light.svg` (dark backgrounds), `qaizn-icon.svg` (favicon/social), plus PNG fallbacks.
- Logo usage rules are documented and binding in `LOGO-INFO.md`: no recoloring, rotation, added effects, or typeface substitution; minimum 120px width for the full lockup, 24px for the icon; clear space of at least 20px.
- Logo typeface is Fraunces (serif, weight 600). The live page uses Playfair Display for editorial headings and DM Sans for body text, loaded from Google Fonts.
- Voice is Spanish, direct and plain-language for a non-technical owner; results-framed rather than technology-framed.

## Evidence on Hand

Confirmed by the user as **real and verifiable client results** — usable as proof and not to be softened into hypotheticals. The three cases on the site are traced to delivered projects; client names are withheld and only sector is shown:
- Medical devices: monthly field-force reporting, 12h → 2h, five-week project.
- Nutraceuticals: nine chained agents covering formulation through label and regulatory verification, 0,25 $ per dossier.
- Multi-site hospitality: per-location P&L and balance sheet, one year in production.
- "4–6 semanas" to a first measurable result describes the engagement shape, not a client outcome.

The earlier headline metrics (250%, 150+, 96%) were removed from the live page. They survive only in `clasico.html` and are not to be reintroduced without a source.

Not on hand and must not be fabricated: named client attributions, testimonials with real people, pricing, logos of customers, press coverage, certifications. `og-image.png` exists and serves in production; it is used for both Open Graph and Twitter cards.

Supporting docs in repo: `SEO-GUIDE.md` (keyword targets and launch checklist), `LOGO-INFO.md`, `COLOR-PALETTES.md`, `PALETA-LIMA.md`, `BLOG-README.md`, one drafted blog post in `blog-posts/`.

## Product Principles

1. **Sell the outcome, not the technology.** A PyME owner buys recovered hours and lower cost, not models or architectures.
2. **Small, provable first step.** Every engagement narrative resolves to a diagnostic and a pilot with a 4–6 week horizon — never a transformation program.
3. **Work inside what they already run.** Value is expressed as improvement to the client's existing ERP, CRM, and processes.
4. **Kaizen is the throughline.** Continuous improvement is the product philosophy and the source of the name, symbol, and method — it should never read as decoration.
5. **Proof is real or absent.** Numbers and cases on the site are verified; nothing invented is ever added beside them.

## Accessibility & Inclusion

No formal standard was specified by the user. The page is readable without JavaScript and respects `prefers-reduced-motion`, but the contact form requires JS; the mailto fallback in the footer is the non-JS path to contact. Spanish is the only supported language.
