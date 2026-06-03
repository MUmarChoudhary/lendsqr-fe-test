# Lendsqr Frontend Engineering Assessment

A pixel-perfect implementation of the Lendsqr Admin Console built with React, TypeScript, and SCSS.

---

## 🔗 Links

- **Live App:** `https://your-name-lendsqr-fe-test.vercel.app`
- **GitHub Repo:** `https://github.com/your-username/lendsqr-fe-test`
- **Documentation:** `https://your-doc-link.notion.site`

---

## 📸 Pages Built

| Page | Route | Description |
|---|---|---|
| Login | `/login` | Auth form with validation |
| Dashboard | `/dashboard` | Stat cards overview |
| Users | `/users` | 500-record paginated table with filters |
| User Details | `/users/:id` | Full profile with tabs, localStorage |

---

## 🛠 Tech Stack

| Tool | Reason |
|---|---|
| **React 18** | Component-based UI, fast rendering |
| **TypeScript** | Type safety, better DX, required by assessment |
| **SCSS** | Maintainable styles with variables and mixins, required by assessment |
| **React Router v6** | Client-side routing with nested layouts |
| **Vite** | Fast dev server and build tool |
| **Jest + Testing Library** | Unit testing with DOM assertions |
| **Axios** | HTTP client (ready for real API swap) |

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- npm v9+

### Installation

```bash
# Clone the repo
git clone https://github.com/your-username/lendsqr-fe-test.git
cd lendsqr-fe-test

# Install dependencies
npm install

# Start development server
npm run dev
```

The app runs at `http://localhost:5173`

### Build for Production

```bash
npm run build
npm run preview
```

### Run Tests

```bash
# Run all tests
npm test

# Run with coverage report
npm test -- --coverage

# Watch mode
npm run test:watch
```

---

## 📁 Project Structure

```
src/
├── types/          # TypeScript interfaces (User, UserDetail, etc.)
├── styles/         # Global SCSS variables, mixins, reset
├── services/       # Mock API + 500-user data generator
├── hooks/          # useUsers, useUserDetail custom hooks
├── utils/          # localStorage helpers, formatters
├── components/     # Reusable UI components
│   ├── Layout/     # AppLayout (sidebar + navbar wrapper)
│   ├── Sidebar/    # Navigation sidebar
│   ├── Navbar/     # Top navigation bar
│   ├── StatusBadge/# Active/Inactive/Pending/Blacklisted chips
│   ├── Pagination/ # Page number controls
│   ├── UserTable/  # Data table with filter + action menu
│   └── UserFilter/ # Column filter dropdown
└── pages/
    ├── Login/
    ├── Dashboard/
    ├── Users/
    └── UserDetails/
```

---

## 🎯 Key Implementation Decisions

### 1. Mock Data — Local Generator vs External API
I chose to generate 500 users locally in `src/services/mockData.ts` using a seeded pseudo-random function instead of hosting on mocky.io. This means:
- No network dependency — works 100% offline
- Consistent, reproducible data on every run
- Seeded random = same data every time, great for testing

### 2. Data Fetching — Simulated Delay
`src/services/api.ts` wraps the mock data in async functions with `setTimeout` delays (400–600ms). This simulates real network behaviour and lets skeleton loaders show correctly, without needing a real backend.

### 3. User Details — localStorage First
On the User Details page, data is read from `localStorage` first (set when the user clicks a row). If not found, it falls back to fetching by ID. This satisfies the assessment requirement and gives an instant load experience — no flicker.

### 4. SCSS Architecture
All SCSS variables (`$primary`, `$text-secondary`, breakpoints) and mixins (`@mixin flex-center`, `@mixin card`, `@mixin tablet`) are defined globally and auto-imported into every component via `vite.config.ts`. No component needs to manually import them.

### 5. Status Overrides via localStorage
When a user is Blacklisted or Activated via the 3-dot menu, the new status is saved to `localStorage` under a `userId → status` map. On next load, the hook merges these overrides into the API data so the change persists across page refreshes without a backend.

### 6. TypeScript Strictness
`tsconfig.json` uses `"strict": true` with `noUnusedLocals` and `noUnusedParameters`. All component props, API responses, and state are fully typed — no `any` types used anywhere.

---

## 🧪 Testing Strategy

Tests are written with **Jest** and **React Testing Library**.

Each test file covers both **positive** (happy path) and **negative** (error/edge) scenarios:

| File | Scenarios |
|---|---|
| `formatters.test.ts` | Valid dates, currencies, phones; empty/invalid inputs |
| `storage.test.ts` | Save/retrieve/clear user; corrupted JSON; multiple users |
| `StatusBadge.test.tsx` | All 4 statuses render with correct CSS classes |
| `Pagination.test.tsx` | Page change, disabled arrows, ellipsis, aria attributes |
| `Login.test.tsx` | Validation errors, toggle password, successful navigation |
| `Users.test.tsx` | Loading state, data render, API failure, empty state, filter |

---

## 📱 Responsive Design

| Breakpoint | Behaviour |
|---|---|
| `> 1024px` | Full layout — sidebar visible, 4-column stat grid |
| `768px – 1024px` | Sidebar hidden, hamburger menu, 2-column grid |
| `< 480px` | Single column layout, simplified navbar |

---

## ♿ Accessibility

- Semantic HTML throughout (`<nav>`, `<main>`, `<table>`, `<button>`)
- All interactive elements have `aria-label`
- `role="alert"` on form validation errors
- `aria-current="page"` on active pagination button
- `aria-selected` on active tab
- `role="tablist"` and `role="tab"` on the details tabs
- `role="menu"` and `role="menuitem"` on the 3-dot action menu
- Keyboard navigable

---

## 🚢 Deployment

Deployed to Vercel:

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Set custom URL
# Configure in Vercel dashboard to match:
# https://your-name-lendsqr-fe-test.vercel.app
```

---

## ✅ Assessment Checklist

- [x] React + TypeScript
- [x] SCSS for all styling
- [x] 4 pages — Login, Dashboard, Users, User Details
- [x] 500 mock user records
- [x] localStorage for User Details
- [x] Mobile responsive
- [x] Unit tests — positive and negative scenarios
- [x] Clean commit history
- [x] Deployed with correct URL format