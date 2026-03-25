# ElectroTrical — PCB Layout & Design Services

> Professional PCB Layout & Design Services website with a full-featured client dashboard, quote management system, project tracking, milestone workflow, and multi-role access control.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [File Structure](#file-structure)
3. [How to Open & Run](#how-to-open--run)
4. [Demo Accounts](#demo-accounts)
5. [Features Built](#features-built)
6. [User Roles & Permissions](#user-roles--permissions)
7. [Key Workflows](#key-workflows)
8. [Technical Architecture](#technical-architecture)
9. [Known Limitations](#known-limitations)
10. [Future Backend Integration](#future-backend-integration)
11. [Git Repository](#git-repository)
12. [Transferring to a New Laptop](#transferring-to-a-new-laptop)

---

## Project Overview

ElectroTrical is a complete client-facing website for a PCB layout and design services business. It includes:

- A **public landing page** (`index.html`) with service descriptions, a live quote calculator, portfolio, testimonials, and a contact section.
- A **full dashboard application** (`dashboard.html`) where customers can manage their projects, submit quote requests, track milestones, and communicate with the design team.
- An **admin dashboard** with KPI summary, quote approval, project management, user management, and role assignment.
- All data is stored in the **browser's localStorage** — no backend or server is required to run the site.

---

## File Structure

```
ElectroTrical/
│
├── index.html              ← Public landing page (homepage + quote calculator)
├── dashboard.html          ← Full dashboard application (all roles)
├── privacy.html            ← Privacy Policy page
├── terms.html              ← Terms of Service page
├── 404.html                ← Custom 404 error page
├── PCBcraft.html           ← Old/archived version (ignored by git)
│
├── Logo/                   ← Brand assets
│   ├── ElectroTrical_Logo.png
│   ├── ElectroTrical_Logo_1.png
│   ├── Transparent_logo_1.png
│   └── navbar_logo.png
│
├── favicon.svg             ← Favicon (SVG, modern browsers)
├── favicon.ico             ← Favicon (legacy browsers)
├── favicon.png             ← Favicon (PNG fallback)
├── favicon-192.png         ← PWA icon (192×192)
├── apple-touch-icon.png    ← iOS home screen icon
├── og-image.png            ← Open Graph / social share image
│
├── robots.txt              ← Search engine crawl rules
├── sitemap.xml             ← XML sitemap for SEO
│
├── PRE-LAUNCH-CHECKLIST.md ← Checklist of tasks before going live
├── README.md               ← This file
└── .gitignore              ← Git ignore rules
```

---

## How to Open & Run

This is a **pure static website** — no build step, no npm install, no server needed.

### Option 1 — Open directly in browser
Double-click `index.html` to open the homepage, or `dashboard.html` to open the dashboard directly.

### Option 2 — Use a local server (recommended)
To avoid any browser security restrictions with local files:

```bash
# Python (built into macOS/Linux, available on Windows)
python -m http.server 8080

# Then open: http://localhost:8080
```

Or use the **Live Server** extension in VS Code (right-click `index.html` → Open with Live Server).

### Option 3 — Deploy to Vercel / Netlify / GitHub Pages
Drag the entire folder into [vercel.com](https://vercel.com) or [netlify.com](https://netlify.com) — it deploys instantly as a static site.

---

## Demo Accounts

Four demo accounts are pre-seeded. Use these to test all roles:

| Role | Email | Password | Access |
|------|-------|----------|--------|
| **Super Admin** | admin@electrotrical.com | admin123 | Everything + delete projects + manage roles |
| **Admin** | manager@electrotrical.com | manager123 | All projects, quote approval, user management |
| **Designer** | designer@electrotrical.com | designer123 | View projects, upload milestone files |
| **Customer** | demo@customer.com | demo1234 | Own projects, submit quotes, track milestones |

> **Note:** Demo data resets if you clear your browser's localStorage. All state is stored under the key `electrotrical_data`.

---

## Features Built

### Public Landing Page (`index.html`)

- Full responsive dark-themed layout
- **Hero section** with animated tagline and CTA buttons
- **Services section** — PCB Layout Design and PCB Layout Modify
- **Quote Calculator** — live pricing with layer count, PCB type, board size, component sides, complexity, turnaround, special requirements, and delivery format selectors
- **File attachment on RFQ** — customers can attach design files (schematic, BOM, netlist, etc.) directly to the quote request before submitting
- **Role guard on submission** — admins and designers cannot submit quote requests; only customers can
- **Portfolio section** — showcase of completed PCB projects (IoT, satellite, power electronics)
- **Testimonials section**
- **Contact section**
- SEO optimizations — meta tags, Open Graph, Twitter Card, JSON-LD structured data, sitemap, robots.txt

---

### Dashboard Application (`dashboard.html`)

#### Authentication
- Sign In / Register forms with validation
- Session timeout after 30 minutes of inactivity
- Role-based routing on login (admin lands on Summary, customer lands on Quotes/Projects)
- Secure input sanitization throughout

#### Navigation
- Persistent top navbar with notification bell and user avatar
- **Tab system** per role:
  - Customer sees: Quotes · Projects · Account
  - Designer sees: Projects · Account
  - Admin sees: Summary · Quotes · Projects · Users · Account
  - Super Admin sees: Summary · Quotes · Projects · Users · Account (+ delete project button)

---

#### Summary Tab (Admin/Super Admin only)
- **KPI cards** — Total Revenue, Active Projects, Pending Quotes, Completed Projects
- **Project status breakdown** — Active / Review / Completed / Cancelled
- **Revenue ledger** — list of all paid projects with amounts
- **Global activity feed** — latest actions across all projects
- Empty state when no data exists

---

#### Quotes Tab

**Customer view:**
- List of all their submitted quote requests with status badges (Pending / Approved / Declined / Paid)
- Full spec breakdown per quote card (PCB type, layers, size, complexity, turnaround, special requirements, delivery formats)
- **Design file section** on each quote card:
  - Shows files attached at submission
  - **Add Files button** — customer can attach more files any time while quote is Pending or Approved
  - Files show name, size, and whether they were "uploaded with RFQ" or "added after submission"
  - Remove (×) button per file
  - File section becomes read-only once quote is Paid or Declined
- **"Proceed to Payment"** button on approved quotes — opens the checkout flow pre-filled with user info and approved price
- **"View Project"** button on paid quotes — jumps directly to the linked project

**Admin view:**
- All quote requests from all customers
- Customer info, full specs, and attached files visible
- **Review & Price modal** — set the final price, add notes, and Approve or Decline
- Attached files shown prominently in the modal before pricing
- Warning badge if customer attached no files: *"No design files — consider requesting files before finalising price"*
- Status badge updates in real time

---

#### Checkout Flow
- Pre-filled contact details from logged-in account
- Order summary panel (layer count, complexity, size, turnaround, special req., total)
- Payment form (card number, expiry, CVC, name on card) with formatted input
- **⚡ Demo Mode — Skip Payment button** — bypasses card form and creates the project instantly for demos
- Payment processing animation (2-second simulated Stripe delay)
- Order success screen with next steps

---

#### Projects Tab

**Customer view:**
- Project cards with status indicator, milestone progress, and layer/size info
- Click any project to open the full project detail view
- Empty state with guidance when no projects exist yet

**Admin/Designer view:**
- All projects from all customers
- Same project detail view with additional admin controls

**Project Detail view:**
- Project name, ID, status badge
- **Milestone Tracker Bar** — visual progress across 3 milestones (Component Placement → Nets Routing → Final Gerbers)
- **Cancel Project button** (admin only, on active projects) — opens cancellation modal with refund options
- **Delete Project button** (Super Admin only) — opens deletion confirmation requiring the project ID to be typed
- **Cancelled project banner** — shows cancellation reason and refund status (Full / Partial / None)
- **Project info panel** — customer name, order date, specs, quote amount
- **File uploads** — admins and designers can upload milestone files; customers can upload reference files
- **Milestone panels** — each milestone shows status, file list, and comments
  - Designer/Admin: Upload files, submit for review, approve or request changes
  - Customer: Approve milestone or leave comments
  - Sequential unlock: next milestone only activates after previous is approved
- **Activity log** — chronological log of all project events
  - Shows latest 5 entries by default
  - "Show more" / "Show less" toggle
  - Unified date format across all entries

---

#### Users Tab (Admin/Super Admin only)
- Stats overview — Total Users, Customers, Active, Designers, Admins
- Search bar (filter by name, email, company)
- User table with avatar, name, email, registration date, quote count, role badge, status badge
- **Suspend / Activate** user toggle (admin only, not on other admins)
- **Delete user** button (admin only, not on other admins)
- **Role selector dropdown** (Super Admin only) — change any non-super-admin user's role between Customer / Designer / Admin

---

#### Account Tab
- Edit profile (first name, last name, company, phone)
- Change password (with current password verification)
- Notification preferences
- Invoice history (linked projects with payment amounts)

---

#### Notifications System
- Bell icon in navbar with unread count badge
- Dropdown panel with notification list
- Types: new quote submitted, quote approved, quote declined, milestone update, payment confirmed, order confirmed, file update
- Mark all as read
- Custom dark scrollbar styled to match the site

---

#### Additional UX Details
- Custom dark scrollbars throughout (matches brand color scheme)
- Toast notifications for all actions (success / warning / error)
- Email preview modal — shows what notification emails look like (admin milestone approvals, customer updates)
- Browser back button support in project detail view
- Fully mobile-responsive layout (see Mobile section below)
- Input sanitization on all user-generated content
- **Invoice PDF export** — "Print / Save PDF" opens a clean standalone popup window with only the invoice (no dashboard chrome). Fallback `@media print` CSS also hides everything except the invoice if printing directly from the dashboard.

---

#### Notification Preferences (Account Tab)
- Toggle switches per notification category: Quote Updates, Project Status Changes, New Messages, File Uploads, Deadline Reminders, Browser Notifications
- Preferences saved per user in localStorage
- Browser Notifications category triggers native `Notification.requestPermission()` when enabled

---

#### Mobile Layout
Both `index.html` and `dashboard.html` are fully optimised for mobile:

**Homepage (`index.html`):**
- Fixed navbar uses `overflow-x: clip` (not `overflow: hidden`) so the mobile dropdown menu (position: fixed) is never clipped
- Mobile menu dropdown starts at exactly `top: 60px` to match the navbar height
- Hamburger toggle uses `flex-shrink: 0` to prevent it being pushed off-screen
- "Get a Quote" CTA hidden on mobile (accessible via hamburger menu)
- Process section stacks to single column at 768px
- Hero subtitle reduces to 16px on mobile
- Stats bar padding reduces at 768px and further at 480px
- Role guard overlay prevents admin/designer from submitting quotes

**Dashboard (`dashboard.html`):**
- Username text hidden on mobile to prevent navbar overflow
- Tighter nav padding and smaller logo on mobile
- Dashboard tabs scroll horizontally with a fade-right indicator
- Detail card padding properly scales down on smaller screens
- Milestone tracker, form rows, and action buttons all stack to single column

---

## User Roles & Permissions

| Feature | Customer | Designer | Admin | Super Admin |
|---------|----------|----------|-------|-------------|
| Submit quote request | ✅ | ❌ | ❌ | ❌ |
| View own quotes    | ✅ | ❌ | ✅ all | ✅ all |
| Approve / price quotes | ❌ | ❌ | ✅ | ✅ |
| View own projects  | ✅ | ❌ | ✅ all | ✅ all |
| View all projects  | ❌ | ✅ | ✅ | ✅ |
| Upload milestone files | ❌ | ✅ | ✅ | ✅ |
| Approve milestones | ✅ | ❌ | ✅ | ✅ |
| Cancel projects    | ❌ | ❌ | ✅ | ✅ |
| Delete projects    | ❌ | ❌ | ❌ | ✅ |
| View Summary/KPIs  | ❌ | ❌ | ✅ | ✅ |
| View Users tab     | ❌ | ❌ | ✅ | ✅ |
| Manage user roles  | ❌ | ❌ | ❌ | ✅ |
| Suspend/delete users | ❌ | ❌ | ✅ | ✅ |

---

## Key Workflows

### Customer Quote → Project Flow
1. Customer fills quote calculator on homepage (or from dashboard Quotes tab)
2. Optionally attaches design files (schematic, BOM, netlist, etc.)
3. Submits → redirected to dashboard, quote appears as **Pending**
4. Customer can add/remove files while quote is pending
5. Admin reviews specs + attached files → sets final price → **Approves** or **Declines**
6. Customer sees notification and **Approved** badge on their quote
7. Customer clicks **"Proceed to Payment"** → checkout opens pre-filled
8. Customer pays (or uses Demo Skip button) → **Project is created**
9. Attached RFQ files are transferred to the new project automatically
10. Activity log records: *"2 design files transferred from RFQ"*
11. Project enters **Active** status, milestones begin

### Milestone Approval Flow
1. Designer/Admin uploads files to a milestone and clicks **"Submit for Review"**
2. Customer receives notification
3. Customer opens project, reviews files, and either **Approves** or requests changes
4. If approved → milestone is marked complete, next milestone unlocks
5. Once all 3 milestones approved → project moves to **Completed**

### Project Cancellation Flow
1. Admin clicks **"Cancel Project"** on an active or in-review project
2. Cancellation modal asks for reason and refund type (Full / Partial / None)
3. Partial refund shows a calculated amount based on milestone completion %
4. Confirmation saves the cancellation reason, refund type, and amount
5. Project status changes to **Cancelled**
6. Cancelled banner appears in project detail showing reason and refund info

### Project Deletion (Super Admin only)
1. Super Admin opens any project
2. Clicks red **"Delete Project"** button
3. Confirmation overlay appears — must type the exact project ID (e.g. `PRJ-2026-001`) to enable the delete button
4. Project is permanently removed from all state
5. Any linked quote is unlinked

---

## Technical Architecture

### Stack
- **Pure HTML / CSS / Vanilla JavaScript** — zero dependencies, zero build tools
- **localStorage** for all data persistence (key: `electrotrical_data`)
- No backend, no database, no npm, no framework

### Data Model (localStorage)
```
{
  users: [...],           ← All registered users
  projects: [...],        ← All projects with milestones, files, activity
  quoteRequests: [...],   ← All quote requests with specs, files, pricing
  notifications: [...],   ← All user notifications
  currentUser: "user-id"  ← Currently logged-in user ID
}
```

### Key JavaScript Patterns
- `getState()` — reads and parses localStorage; runs data migrations on every load
- `saveState(updated)` — writes to localStorage AND syncs the global `state` variable to prevent stale state bugs
- `renderDashboard()`, `renderQuoteRequests()`, etc. — all call `state = getState()` on entry to ensure fresh data
- Role helpers: `isAdmin()`, `isDesigner()`, `isSuperAdmin()`, `canUploadMilestones()`
- `formatActivityDate()` — normalises both ISO and legacy date string formats
- `sanitizeInput()` — strips HTML from all user-generated content before rendering

### Migration System
`getState()` includes an idempotent migration block that runs on every page load. It patches missing fields on existing localStorage state without requiring a manual reset. This is how demo accounts, new flags (e.g. `superAdmin`), and schema changes are applied to returning users.

---

## Known Limitations

| Limitation | Detail |
|-----------|--------|
| **No real file storage** | Uploaded files store metadata only (name, size, type) — not actual content. Downloading files requires a backend. |
| **localStorage only** | All data lives in the browser. Clearing browser data resets everything. |
| **Single device** | Data does not sync across devices or browsers. |
| **No real payment** | Stripe integration is simulated. Use the "Skip Payment" demo button. |
| **No real email** | Email previews are UI-only. No emails are actually sent. |
| **No real auth** | Passwords are stored in plaintext in localStorage. Not suitable for production as-is. |
| **Popup blocker** | Invoice PDF export opens a new window. If the browser blocks popups, the `@media print` fallback still produces a clean invoice. |

---

## Future Backend Integration

When connecting a real backend (recommended: **Supabase**, **Firebase**, or a custom Node.js API), the following swaps are needed:

| Current (localStorage) | Replace with |
|----------------------|--------------|
| `getState()` / `saveState()` | API calls (GET/POST/PATCH) |
| User passwords in state | Supabase Auth / Firebase Auth |
| File metadata only | S3 / Supabase Storage / Cloudflare R2 |
| Simulated Stripe | Stripe.js real payment intent |
| UI-only emails | SendGrid / Resend / Postmark |
| localStorage notifications | WebSockets or Supabase Realtime |

> **Note:** The codebase was previously migrated to Supabase but reverted to localStorage for stability. The Supabase migration code exists in the git history (commit `d80f2f2`) as a reference.

---

## Git Repository

**Remote:** https://github.com/PROJECTAT-AE/electrotrical.git
**Branch:** `main`

### Pushing to GitHub (from your terminal)
```bash
cd "C:\Users\m-als\OneDrive\Desktop\ElectroTrical"
git push
```

### Full commit history summary

| Commit | Description |
|--------|-------------|
| `f5de2d3` | Initial release |
| `c5384bb` | Security improvements |
| `8b0f95f` | Quote review system with admin approval |
| `71e46e5` | Quote request persists through account creation |
| `47fe485` | Name & email validation on registration |
| `2330d95` | Admin users panel and form validation |
| `4bf7f16` | ElectroTrical logo across all pages |
| `4344fa2` | Portfolio updated with space/satellite PCB projects |
| `4dcc4df` | Full SEO — meta tags, Open Graph, structured data |
| `aca30e9` | Service type, PCB type, component sides, delivery formats |
| `947326e` | Quote-first workflow enforced |
| `bb65ad9` | Admin Summary tab with KPIs and revenue ledger |
| `f7d72a5` | Fix projectsList bleeding into other tabs |
| `1abd058` | Project cancellation with partial refund calculator |
| `e9ee04d` | Tab reorder: Summary → Quotes → Projects → Users → Account |
| `80a16f5` | Summary tab as admin default landing |
| `1549b85` | Fix admin landing on Projects instead of Summary |
| `bf4086a` | Custom dark branded scrollbars |
| `19816b6` | Fix cancelled banner message |
| `8849430` | Six UX improvements (notifications, mobile, back button, etc.) |
| `b117b44` | Three-tier role system: Customer / Designer / Admin / Super Admin |
| `8c78ecb` | Fix superAdmin flag migration |
| `a5ea6ae` | 4 demo accounts, clean seed data |
| `b9cdf3d` | Fix openProject crash (missing designer variable) |
| `62be3af` | Collapsible activity log (show 5, expand more) |
| `0d3cc7b` | Unified activity log date format |
| `498dcd8` | Fix quote approval reverting to pending (stale global state bug) |
| `6d0c8d0` | Demo skip payment button + checkout pre-fill fix |
| `dddfeb3` | Fix Skip Payment stuck (pendingQuote global not loaded) |
| `d5f64bd` | Fix Proceed to Payment crash (complexityLabel undefined) |
| `a637050` | Design file upload on RFQ — drag & drop, metadata stored |
| `c66b292` | Customers can add/remove files after RFQ submission |
| `0e756d6` | Styled number input spinner arrows (dark theme) |
| `8fecdc8` | Fix spacing in Design Files section |
| `dec09c8` | RFQ submission restricted to customers only |
| `3814cd4` | Fix RFQ role guard (wrong localStorage key) |
| `ddba5a4` | Super Admin can permanently delete projects |
| `e90da69` | Fix delete modal (dynamic overlay, not static element) |
| — | Replace projectat.ae@gmail.com with info@electrotrical.com across all files |
| — | Fix blank Quotes tab (duplicate function declaration causing infinite loop) |
| — | Filter paid quotes out of Quotes tab for all user roles |
| — | Auto-repair duplicate projects on dashboard load (bestById dedup + collision-safe IDs) |
| — | Projects sort newest-first |
| — | Role guard on homepage: admin/designer cannot submit quote requests |
| — | Fix hamburger menu clipped off-screen (overflow-x: clip on navbar) |
| — | Fix mobile menu not opening (top adjusted to 60px, matching navbar height) |
| — | Dashboard mobile: hide username, tighten navbar spacing |
| — | Notification preference toggles with per-user localStorage persistence |
| — | Toggle switch CSS for notification preferences |
| — | Expired badge added to quote status badge map |
| — | Fix addNotificationForUser signature (resolve string ID to user object) |
| — | Invoice PDF: popup window export (clean, no dashboard chrome) |
| — | Invoice PDF: @media print fallback hides dashboard, shows only invoice |
| — | Mobile audit: process grid single-column at 768px, hero subtitle smaller, stat padding at 768px |
| — | Dashboard mobile: detail card padding fixed (was backwards at 480px), tab scroll fade indicator |

---

## Transferring to a New Laptop

Everything you need to transfer:

1. **Copy the entire `ElectroTrical` folder** — that's it. No dependencies to install.

2. **Your browser data does NOT transfer automatically.** The demo accounts and any test data live in your current browser's localStorage. On the new laptop, the seed data will be recreated automatically on first load (the migration system in `getState()` handles this).

3. **To keep your current data** (projects, quotes, users you've created during testing):
   - Open your browser's DevTools (F12)
   - Go to Application → Local Storage → your site's URL
   - Copy the value of `electrotrical_data`
   - On the new laptop, paste it into the same location

4. **Git repository** — if you clone from GitHub on the new laptop, you get the latest code:
   ```bash
   git clone https://github.com/PROJECTAT-AE/electrotrical.git
   ```

5. **Push any uncommitted changes before transferring:**
   ```bash
   cd "C:\Users\m-als\OneDrive\Desktop\ElectroTrical"
   git push
   ```

---

*Built with Claude — Anthropic AI · March 2026 · Last updated: March 24, 2026*
