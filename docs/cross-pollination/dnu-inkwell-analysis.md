# DNU ↔ Inkwell Cross-Pollination Analysis

**Date:** 2026-04-16  
**Purpose:** Map features between DentalNearYou and Inkwell/Mumega to identify mutual learning opportunities.

---

## Table 1: DNU Features → Inkwell (what Inkwell should learn)

| DNU Feature | Files | What It Does | Inkwell Equivalent | Action |
|---|---|---|---|---|
| **Legitimacy / Trust Score** | `components/expert/TrustScoreTooltip.tsx`, `ConsensusBar.tsx`, `migrations/027_trust_score_and_semantic_indexes.sql` | Expert consensus scoring on topic pages; visual bar showing agreement level | None | Add trust/consensus signal to Inkwell topic pages |
| **Expert Carousel + Story Viewer** | `components/expert/ExpertCarousel.tsx`, `ExpertStoryViewer.tsx`, `ExpertRing.tsx` | Instagram-style expert opinions on dental topics with video support | None | Add expert-opinion blocks to Inkwell content schema |
| **City × Service SEO matrix** | `app/[lang]/[city]/[service]/page.tsx`, `mumega-cms/ARCHITECTURE.md` | 15 cities × 15 services = 225+ geo-targeted pages, Haversine distance sort | Inkwell has topics pages but no geo matrix | Add city/location dimension to Inkwell content engine |
| **GHL Connector** | `ghl-connector/app.py` | OAuth app: patient lead → dentist's GHL CRM pipeline, retry queue, rate limiting | None | Build a generic CRM connector (GHL / HubSpot) as Inkwell plugin |
| **3-Layer Dashboard** | `app/dashboard/{patient,partner,admin}/` | Distinct UX layers: patient (appointments + copilot), partner (leads + analytics + Dandan AI), admin (revenue-ops + partner-ops + issues) | Inkwell has a single dashboard page | Implement role-based dashboard routing in Inkwell |
| **Partner Onboarding Wizard** | `app/dashboard/partner/onboarding/page.tsx` | Step-tracked onboarding: profile → license → verification → GHL connect → CMS publish | None | Add multi-step onboarding flow to Inkwell tenant setup |
| **Supabase as source of truth** | `migrations/` (36 files), `web/lib/supabaseServer.ts` | Relational schema for leads, appointments, partners, referrals, trust scores, CE credits | Inkwell uses Cloudflare D1 (simpler, no pgvector) | Inkwell should support Supabase adapter for data-heavy forks |
| **CE Credit System** | `migrations/022_ce_credit_system.sql`, `components/expert/CeCertificate.tsx` | Dentists earn continuing education credits; generates PDF certificates | None | Gamified credential system applicable to any professional vertical |
| **Mobile app layer** | `app/mobile/` (9 pages: book, chat, costs, find, health, insurance, settings) | Separate mobile-optimized routes with their own layout | None | Inkwell has no mobile-first routes |
| **Data Sovereignty Marketplace** | `migrations/025_data_sovereignty_marketplace.sql`, `components/expert/DataEarningsDashboard.tsx` | Patients opt-in to sell anonymized data; experts earn from content contributions | None | Radical feature — could be an Inkwell premium module |

---

## Table 2: Inkwell/Mumega Features → DNU (what DNU should get)

| Inkwell Feature | What It Does | DNU Equivalent | Action |
|---|---|---|---|
| **Forkable config** | Single `inkwell.config.ts` drives theme, i18n, features flags, SEO org schema | DNU is monolithic — one codebase, one site | Extract DNU config into a single config file per instance (white-label dentist directory) |
| **Cloudflare edge delivery** | Astro 6 + Workers + KV + R2; content served from 300 PoPs globally | DNU runs on Next.js on Hetzner VPS; only Cloudflare for DNS | Move DNU static SEO pages (city/topic/dentist) to Cloudflare Pages |
| **Knowledge graph** | Wiki-links + graph view connecting content nodes | DNU `semantic_net_and_voting` migration exists but no UI | Wire the semantic net into a visible topic graph UI |
| **Command palette** | Client-side full-text search + keyboard-driven navigation (Pagefind) | DNU has no search on public pages | Add Pagefind or similar to DNU topic/city listing pages |
| **Tenant registry + multi-site publish** | `publisher-mcp` with `publisher_upsert_tenant`, `publisher_upsert_site`, `publisher_list_tenants` — multi-site from one Supabase | DNU publisher-mcp exists but is DNU-specific | Generalize DNU's publisher-mcp to match Inkwell's multi-tenant model |
| **MCP server (8 tools)** | Agent-operable via `POST /mcp`; standardized tool schema | DNU has 2 MCP servers (15 + 20 tools) but both are STDIO, not SSE/HTTP | Migrate DNU MCPs to Streamable HTTP transport so any agent can call them remotely |
| **Analytics flywheel (GSC + GA4)** | Daily cron pulls Search Console + GA4 data into D1; feeds content decisions | DNU has analytics page in partner dashboard but no automated ingestion | Add GSC/GA4 ingestion cron to DNU for topic and city page performance |
| **`llms.txt` generation** | Auto-generates AI-readable site manifest for LLM crawlers | None | Add `llms.txt` to DNU's sitemap suite (`/sitemap-cities.xml`, `/sitemap-dentists.xml`, etc.) |

---

## Table 3: Shared Infrastructure

| Component | DNU Version | Inkwell Version | Which Is Better | Recommendation |
|---|---|---|---|---|
| **SEO Schema** | 6 dedicated generators: `local-business`, `article`, `person`, `video`, `aggregate-rating`, `utils` — domain-specific (Dentist, MedicalWebPage, FAQPage) | 5 builder functions in `seo.ts`: Article, ScholarlyArticle, VideoObject, Product, Course — generic | DNU (more schema types, E-E-A-T focused) | Port DNU's `Person` + `LocalBusiness` + `AggregateRating` builders into Inkwell as optional plugins |
| **AI content assistant** | Dandan: Gemini-powered chat in partner dashboard — emails, video scripts, performance analysis | None in dashboard | DNU | Add Dandan-style AI copilot to Inkwell dashboard |
| **Multilingual** | `[lang]` route prefix, EN + FR today, 6 planned; content from Supabase | `i18n.languages` config array, single `en` default, RTL support built in | Inkwell (cleaner config-driven i18n) | DNU should adopt Inkwell's config-driven i18n rather than hard-coded FR strings |
| **Sitemap** | 5 specialized sitemaps: cities, dentists, services, topics + index | 1 generated sitemap.xml + RSS | DNU (granular) | Inkwell should support split sitemaps for large content sites |
| **Publisher / CMS pipeline** | `mumega-cms` + `publisher-mcp`: Supabase → Strapi → Cloudflare KV/R2; AI-generated content | `inkwell-publish` skill + `npm run publish` (file drop); Astro content collections | DNU (more powerful pipeline) | Extract DNU's publisher pipeline as a reusable Inkwell worker |

---

## Table 4: DNU Stats

| Metric | Count |
|---|---|
| TypeScript/TSX files (web/) | 5,520 |
| React components | 76 |
| Next.js pages (page.tsx) | ~55 |
| API routes (route.ts) | 35 |
| Dashboard pages | 21 (patient: 1, partner: 8, admin: 10, shared: 2) |
| Public SEO page types | city, city+service, dentist profile, topic, guide, cities list — 6 route patterns |
| Supabase migrations | 36 SQL files |
| Schema generators (web/lib/schema/) | 6 types |
| MCP tools (mcp-server) | 15 (dandan_*) |
| MCP tools (publisher-mcp) | 20 (publisher_*) |
| Mobile routes | 9 |
| CMS target pages (full build) | 15,000+ (2 languages × 15 cities × 15 services + topics) |
