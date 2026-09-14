# CorujãoCS 🦉

**CorujãoCS** is a single-file, offline-first web application built to help Brazilian e-commerce customer support agents (originally created for Amazon.com.br chat support) work faster and more consistently. It packages hundreds of ready-to-use response templates, internal knowledge-base articles, decision trees, and small productivity tools into one self-contained HTML file that runs entirely in the browser — no server, no build step, no external dependencies.

> ⚠️ **Disclaimer:** This is an unofficial, community-built productivity tool. It is **not** an official Amazon product. All content is written in Brazilian Portuguese (pt-BR) and reflects internal support workflows/policies used by customer service agents. It is intended purely as a personal/team reference and copy-paste assistant during live chat support.

---

## What it does

CorujãoCS is essentially a **searchable "cheat sheet" + macro library** for support agents, organized into several tabs (a left sidebar navigation):

| Tab | Purpose |
|---|---|
| 💬 **Chat** | A large, searchable library of pre-written chat response templates ("blurbs") for the most common support scenarios (order tracking, refunds, returns, coupons, payments, account security, subscriptions, seller issues, scams, etc.), each tagged by category/subcategory and source. |
| ✉️ **E-mails** | Similar template library formatted for email responses, including pre-filled subject lines. |
| 📖 **Guia** (Guide) | Longer-form knowledge-base articles explaining internal processes, policies, and step-by-step procedures (e.g., how refunds work per payment method, FBA vs. FBM responsibility, Guarantee A-to-Z rules, return deadlines). |
| 🔖 **Cupons & Ofertas** | Reference articles specifically about coupons, promotions, "missions," Programa e Poupe (Subscribe & Save), and other promotional mechanics. |
| 📋 **Anotações** | A glossary/reference of internal account "notes" or codes agents may see on a customer's account, with plain-language explanations and tips. |
| 🛠️ **Ferramentas** (Tools) | A set of interactive mini-tools (see below). |
| 🔬 **IA & Revisor** | Text-analysis helpers: paste a customer's message and get suggested matching templates, or paste a drafted reply for review/QA. |
| 📚 **Políticas** | A searchable database of internal policy documents. |
| 🎯 **DART & CDC** | Guided decision trees for escalation ("DART") scenarios and consumer-law ("CDC" — Código de Defesa do Consumidor) cases. |

### Key features

- **Fuzzy full-text search** across all templates and articles, including a lightweight Portuguese stemmer, typo-tolerant matching (Levenshtein-distance based), synonym handling, and TF-IDF–style relevance scoring — all implemented from scratch in vanilla JavaScript.
- **One-click copy** of any template to the clipboard, with automatic variable substitution: the agent can set their own name and the customer's name once, and every `[Nome]`, `[SEU NOME]`, `CLIENTE`, etc. placeholder in a template is automatically replaced before copying.
- **Variable detection modal**: templates containing placeholders like dates, order IDs, or values pop up a small form so the agent can fill them in before copying.
- **Favorites** and **"Most Used"** views, plus recent copy history, all persisted locally.
- **Multiple color themes/palettes** (light/dark and variants), remembered between sessions.
- **"Should I transfer?" decision tool** — a guided Q&A flow that tells the agent whether a case should be resolved directly or transferred to a specialized team/department.
- **DART template generator** — a form-based generator for ~20 official escalation templates (price matching, RMA, etc.), auto-formatted and ready to copy.
- **"Locked order" (Pedido Travado) troubleshooting simulator** — an interactive questionnaire that walks through a decision tree to diagnose why an order is stuck (payment declined, EDD not reached, out of stock, etc.) and suggests the correct next step.
- **Chat/message analyzer** — paste in a customer's message and the app scores it against the template library (and against the policy, DART, and CDC databases) to surface the most relevant responses/policies automatically.
- **Reply reviewer** — a lightweight QA helper for checking a drafted response before sending it.
- **Automatic update banner** — the app tracks its own version number and shows a small "updated to vX" toast the first time a user opens a newer version, reassuring them that their saved data (favorites, settings) was preserved.
- **Fully offline / local-first**: all user preferences (theme, agent name, favorites, usage stats, draft text, etc.) are stored in the browser's `localStorage`, with an automatic in-memory fallback if `localStorage` is unavailable (e.g., in restricted/sandboxed environments). No data is sent to any server.

---

## How it works (technical overview)

- **Single HTML file** (`CorujaoCS-VXX.html`): everything — markup, CSS, JavaScript, and *all data* (templates, guides, policy texts, decision trees) — lives inline in one file. This makes the tool completely portable: it can be opened directly from disk, hosted as a static file, or shared as an attachment, with zero installation and zero build tooling.
- **Vanilla JavaScript**, no frameworks or external libraries. The UI is a small hand-rolled SPA: a single `render()`/`renderContent()` function tree re-renders the relevant panel based on in-memory state (current section, search query, selected filters, etc.).
- **Client-side search engine**: custom tokenizer, Portuguese light-stemming rules, a synonym dictionary, fuzzy word matching (edit distance), and document-frequency/IDF-based scoring are all implemented inline to rank search results without any external search library.
- **State persistence** via `localStorage` (with graceful degradation to an in-memory store), covering theme, agent identity, favorites, usage counters, copy history, and in-progress text in the analyzer/reviewer tools.
- **No network calls, no analytics, no external assets** beyond system fonts — the app is designed to run safely inside locked-down corporate/BPO environments.

---

## Getting started

1. Download the HTML file.
2. Open it directly in any modern browser (double-click, or `File → Open`).
3. (Optional) Set your agent name and gender on first use so templates are automatically personalized.
4. Use the search bar (or `Ctrl+K`) to find a response, click **📋 Copiar**, and paste it into your support platform.

No installation, build step, backend, or internet connection is required.

---

## Content & language

All templates, guides, and policy text are written in **Brazilian Portuguese**, since the tool was built for a Brazil-based customer support operation. The content covers topics such as:

- Order tracking & delivery issues (OEMP), delayed/lost/returned shipments
- Returns & refunds across multiple payment methods (credit card, Pix, gift card, Geru, NuPay, Livelo points)
- Coupons, promotions, "missions," and Subscribe & Save
- Account security, phishing/scam alerts, and identity verification
- Subscriptions (Prime, Kindle Unlimited, Amazon Music, Audible, etc.)
- Marketplace/third-party seller responsibilities (FBA vs. FBM) and the A-to-Z Guarantee
- Escalation criteria and internal decision trees for complex or disputed cases

---

## License / Usage notes

No license file is currently included. Since the content is scenario- and policy-specific to a particular support operation, review and adapt it before reusing it in another context. Contributions that expand the template library, improve the search/analyzer logic, or add new tools are welcome — feel free to open a pull request or fork the project.
