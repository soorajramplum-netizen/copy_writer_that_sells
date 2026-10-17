# Right Copywriter
### Copy that sells. Built on behavioral science.

A copywriting tool engineered on **62 psychological principles** from Richard Shotton, Daniel Kahneman, Rory Sutherland, and System 1 Group research. Not a generic AI wrapper — a behavioral science constraint system.

---

## How It Works

The tool is architecturally different from a generic AI tool:

1. **Layer 1 — Bias Library (server-side, hardcoded)**: All 62 biases live in `api/generate.js` as the system prompt — baked into every single API call. The user never sees or controls this.

2. **Layer 2 — JSON Schema Enforcement**: The AI cannot return plain text. Every response must include `bias_name`, `explanation`, and `application`. No bias citation = invalid response.

3. **Layer 3 — Copy-Type Reasoning**: The prompt instructs the model to reason through which biases are most contextually relevant *before* writing — it writes a behavioral brief first, then executes it.

4. **Layer 4 — Model Fallback Chain**: Server tries 6 Gemini models in order. Users never see model switching.

5. **Layer 5 — Server-Only Engine**: The behavioral science brain lives exclusively in the serverless function — not in the browser.

---

## Bias Count by Source

| Source | Biases |
|--------|--------|
| Richard Shotton (Choice Factory + Illusion of Choice) | 42 |
| Daniel Kahneman (Thinking, Fast and Slow) | 34 concepts → 20 unique additions |
| Rory Sutherland (Alchemy) | 10 unique |
| System 1 Group (Profitable Growth) | 6 unique |
| **Total unique, deduplicated** | **~62** |

---

## Tabs

- **Copywriter** — 7 copy types (Headline, Tagline, Product Description, General Description, Social Caption, Email Subject, Email Copy). Copy type selected first, then contextual fields appear. 3 reference copy slots for brand tone.
- **Name Generator** — 8 names per run, each using a different naming principle. Each includes ≤50 char description + 3-4 word tagline. Existing portfolio names + guardrails optional.
- **Bias Audit** — Paste any copy. Get behavioral score /10, what's working, what's missing, and an improved rewrite.

Every output includes a bias badge with an `ⓘ` tooltip explaining: what the bias is + exactly how it was applied to this specific copy.

---

## Deployment (Vercel)

### 1. Clone and push to GitHub

```bash
git init
git add .
git commit -m "Initial commit — Right Copywriter"
git remote add origin https://github.com/YOUR_USERNAME/right-copywriter.git
git push -u origin main
```

### 2. Import to Vercel

- Go to [vercel.com](https://vercel.com) → New Project
- Import your GitHub repository
- Framework Preset: **Other**
- Root Directory: leave as `/`

### 3. Set Environment Variable

In Vercel → Project Settings → Environment Variables:

```
GEMINI_API_KEY = your_gemini_api_key_here
```

Add to: Production, Preview, and Development environments.

### 4. Deploy

Hit Deploy. Done.

---

## Local Development

```bash
npm install
npm run dev
# → Runs at http://localhost:3000
# → Uses .env file for GEMINI_API_KEY locally
```

Create a `.env` file (never commit this):
```
GEMINI_API_KEY=your_gemini_api_key_here
```

---

## Model Fallback Chain

The serverless function tries these models in order, silently falling back on any error:

1. `gemini-2.5-pro-preview-05-06` — Best reasoning, most thorough bias application
2. `gemini-2.5-pro` — Stable production model
3. `gemini-2.0-flash-001` — Fast, intelligent
4. `gemini-2.5-flash` — High throughput
5. `gemini-2.5-flash-lite-preview-06-17` — Ultra-fast backup
6. `gemini-1.5-pro` — Final safety net

The model used is returned in the API response (`d.model`) — useful for debugging.

---

## File Structure

```
right-copywriter/
├── public/
│   └── index.html          # Full frontend (mobile-first, light theme)
├── api/
│   └── generate.js         # Serverless function with behavioral science engine + Gemini fallback
├── vercel.json             # Vercel routing config
├── package.json
├── .gitignore
└── README.md
```

---

## Behavioral Sources

- **Richard Shotton** — *The Choice Factory* + *The Illusion of Choice*
- **Daniel Kahneman** — *Thinking, Fast and Slow*
- **Rory Sutherland** — *Alchemy*
- **System 1 Group** — *Profitable Growth Is Everyone's Business*
