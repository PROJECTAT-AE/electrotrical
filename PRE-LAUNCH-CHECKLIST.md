# ElectroTrical — Pre-Launch Checklist

> Work through this before pointing your domain live. Items marked **MUST** are blockers. Items marked **SHOULD** are strongly recommended. Items marked **NICE** can come after launch.

---

## 1. Domain & Hosting

- [ ] **MUST** — Purchase `electrotrical.com` domain (e.g. via Vercel)
- [ ] **MUST** — Connect domain to GitHub Pages or Vercel deployment
- [ ] **MUST** — Confirm HTTPS is active (green padlock in browser)
- [ ] **MUST** — Confirm `www.electrotrical.com` redirects to `electrotrical.com` (or vice versa)
- [ ] **SHOULD** — Set up a custom email address (e.g. `info@electrotrical.com`) via Zoho Mail, Google Workspace, or Resend

---

## 2. Content — Replace Placeholders

- [ ] **MUST** — Update `info@electrotrical.com` in the contact section to your real email
- [ ] **MUST** — Update `info@electrotrical.com` in the footer email notification previews (dashboard.html)
- [ ] **MUST** — Verify the stats bar numbers are accurate (Boards Delivered: 2,400+, Rush Turnaround: <24h, Max Layers: 16, DRC Pass Rate: 99%)
- [ ] **MUST** — Update social media icons in footer with real profile URLs (LinkedIn, Twitter/X, GitHub, YouTube) — or remove icons you don't use
- [ ] **SHOULD** — Replace portfolio SVG placeholders with real PCB screenshots/renders when available
- [ ] **SHOULD** — Add your real business location or country to the contact section

---

## 3. EmailJS — Contact Form & Notifications

- [ ] **MUST** — Create an account at [emailjs.com](https://emailjs.com)
- [ ] **MUST** — Create an Email Service (connect your Gmail or business email)
- [ ] **MUST** — Create two email templates:
  - `contact_form` — for messages submitted via the contact form on index.html
  - `quote_notification` — for new quote requests submitted via dashboard.html
- [ ] **MUST** — Replace the `// TODO: Wire EmailJS` comment in `index.html → handleContact()` with real credentials
- [ ] **MUST** — Add your EmailJS Public Key, Service ID, and Template IDs to dashboard.html
- [ ] **SHOULD** — Test both forms end-to-end and confirm you receive emails

---

## 4. Dashboard — Admin Setup

- [ ] **MUST** — Change the default admin password from `admin123` to something strong
- [ ] **MUST** — Change the admin email from `admin@electrotrical.com` to your real email
- [ ] **SHOULD** — Remove or disable the "Admin Demo" and "Customer Demo" quick-login buttons before going public
- [ ] **SHOULD** — Test the full customer quote → admin approve → project creation flow end-to-end

---

## 5. SEO & Analytics

- [ ] **MUST** — Submit `sitemap.xml` to [Google Search Console](https://search.google.com/search-console) after domain is live
- [ ] **MUST** — Verify your site in Google Search Console
- [ ] **SHOULD** — Set up [Bing Webmaster Tools](https://www.bing.com/webmasters)
- [ ] **SHOULD** — Add Google Analytics or a privacy-friendly alternative (Plausible, Fathom) to track visitors
- [ ] **NICE** — Add a FAQ section to index.html for better Google "People Also Ask" visibility

---

## 6. Cross-Browser & Device Testing

- [ ] **MUST** — Test on Chrome (desktop)
- [ ] **MUST** — Test on Safari (desktop + iPhone)
- [ ] **MUST** — Test on Firefox (desktop)
- [ ] **MUST** — Test on a real mobile phone (not just DevTools)
- [ ] **SHOULD** — Test on Android Chrome
- [ ] **SHOULD** — Check all sections render correctly at 320px, 768px, 1024px, 1440px widths

---

## 7. Functional Testing

- [ ] **MUST** — Quote calculator updates price in real time for all dropdowns
- [ ] **MUST** — "Submit Quote Request" flows correctly into the dashboard quotes tab
- [ ] **MUST** — Login and registration work correctly
- [ ] **MUST** — Admin view shows all customers and quotes
- [ ] **MUST** — Customer view only shows their own quotes and projects
- [ ] **MUST** — Sign Out works and returns to login screen
- [ ] **MUST** — Contact form shows success message and saves submission
- [ ] **MUST** — Cookie consent banner appears on first visit and remembers choice
- [ ] **SHOULD** — All smooth-scroll nav links (#services, #why, #process, etc.) scroll correctly
- [ ] **SHOULD** — Mobile hamburger menu opens and closes correctly
- [ ] **SHOULD** — Navbar hides/shows correctly on scroll

---

## 8. Performance

- [ ] **SHOULD** — Run a [Google PageSpeed Insights](https://pagespeed.web.dev) audit after going live — target 90+ on mobile
- [ ] **SHOULD** — Run a [GTmetrix](https://gtmetrix.com) test to check load time
- [ ] **NICE** — Convert logo/image files to WebP format for faster loading
- [ ] **NICE** — Consider a CDN (Cloudflare free tier) for global speed improvement

---

## 9. Legal & Trust

- [ ] **MUST** — Review `privacy.html` — update company name, jurisdiction, and contact email with real details
- [ ] **MUST** — Review `terms.html` — update company name, jurisdiction, and contact email with real details
- [ ] **SHOULD** — Add your business registration / trade licence number if applicable
- [ ] **NICE** — Add trust badges (SSL, secure payment) to the checkout section

---

## 10. Final Checks Before Going Live

- [ ] Confirm no placeholder text visible anywhere on the public site (`lorem ipsum`, `555`, `TODO`, `demo@`, etc.)
- [ ] Confirm all internal links work (privacy, terms, dashboard)
- [ ] Confirm `robots.txt` is accessible at `electrotrical.com/robots.txt`
- [ ] Confirm `sitemap.xml` is accessible at `electrotrical.com/sitemap.xml`
- [ ] Confirm favicon shows correctly in browser tab
- [ ] Share your link on WhatsApp and verify the og:image preview looks correct
- [ ] Do a final `git push` and confirm the live site matches what you see locally

---

*Last updated: March 2026*
