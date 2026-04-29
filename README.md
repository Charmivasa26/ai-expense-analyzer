---

## 🤖 AI Agents

| Agent | What it does |
|-------|-------------|
| 📥 **Expense Agent** | Auto-categorizes transactions by vendor keyword into Food, Travel, Software, etc. |
| 🔍 **Anomaly Agent** | Flags transactions exceeding μ + 2σ per category as statistically unusual |
| 🔮 **Forecast Agent** | Predicts next-month spend using rolling averages with best/worst case bands |
| 🧠 **CFO Agent** | Generates on-demand executive summary, risk flags, and cost-reduction recommendations |

---

## 📊 Pages Overview

### Dashboard
Real-time KPI cards (total spent, budget remaining, transaction count, active alerts), spending by category bar chart, category breakdown doughnut chart, recent transactions list, and per-category budget usage bars.

### AI Agents
Live agent status panel with execution log, on-demand **CFO Report Generator** (produces executive summary + risk flags + recommendations), and **What-If Scenario Planner** (simulate reducing any category by any percentage).

### Insights
AI-generated insight chips, category spending breakdown, per-category next-month predictions with trend direction, total forecast with best/worst case range and confidence bar, and 30-day daily spending trend chart.

### Alerts
Smart alerts for budget overruns (≥100%), budget warnings (≥80%), and anomalous transactions — each with an AI-suggested action. Plus a budget configuration panel with daily/monthly/yearly input toggle.

### Add Expense
Form to log new transactions (amount, date, vendor, category, notes). Expense Agent processes each entry immediately. Full transaction table with delete support and anomaly badges.

---

## 🎨 Categories

Categories are defined in the `CAT` object in the `<script>` block:

```javascript
const CAT = {
  Food:      { emoji: '🍕', color: '#f97316' },
  Travel:    { emoji: '✈️', color: '#3b82f6' },
  Software:  { emoji: '💻', color: '#8b5cf6' },
  Office:    { emoji: '🖨️', color: '#10b981' },
  Bills:     { emoji: '⚡', color: '#ef4444' },
  Marketing: { emoji: '📣', color: '#ec4899' },
  Other:     { emoji: '📦', color: '#6b7280' },
};
```

To add a category: add an entry to `CAT`, add a matching `<option>` in the Add Expense form's `<select>`, and add a default budget entry in `DEMO_BUDGETS`.

---

## 💰 Default Budget

The default monthly budget cap is set to ₹1,50,000:

```javascript
let TOTAL_BUDGET = parseInt(localStorage.getItem('cfoos_total_budget') || '150000');
```

Change `'150000'` to your preferred default (in rupees). Users can also update it live from the Alerts tab.

---

## 💾 Data Persistence

All data is saved to `localStorage` under three keys:

| Key | Contents |
|-----|----------|
| `cfoos_exp` | Array of all expense transactions |
| `cfoos_bud` | Per-category budget limits (monthly) |
| `cfoos_total_budget` | Total monthly budget cap |

Data survives page refreshes but is browser-local only. To fully reset:

```javascript
localStorage.removeItem('cfoos_exp');
localStorage.removeItem('cfoos_bud');
localStorage.removeItem('cfoos_total_budget');
```

Or via DevTools → Application → Local Storage → delete the keys above.

---

## 📦 Dependencies

| Dependency | Purpose |
|------------|---------|
| `chart.js 4.4.0` | Bar, doughnut, and line charts (loaded via CDN) |
| `localStorage API` | All data persistence — no backend needed |
| Vanilla JS | All UI logic — no framework |

Chart.js is loaded from `cdn.jsdelivr.net`. No other external dependencies.

---

## 🌐 Hosting

Drop the single HTML file onto any static host — no build or server config needed:

```bash
# GitHub Pages
gh-pages -d .

# Netlify CLI
netlify deploy --dir=.

# Vercel
vercel --prod
```

---

## 🔧 Troubleshooting

### Charts not rendering
Chart.js loads from `cdn.jsdelivr.net`. Open over a local dev server if needed:
```bash
npx serve .
# or
python3 -m http.server 8080
```

### Data not persisting
Ensure you're not in a private/incognito window — `localStorage` is disabled in incognito mode in most browsers.

### Want to reset completely
Open DevTools (`F12`) → Application tab → Local Storage → delete `cfoos_exp`, `cfoos_bud`, and `cfoos_total_budget`, then reload.

---

## 📄 License

MIT — free to use, fork, and modify.
