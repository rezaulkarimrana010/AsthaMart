# AsthaMart — ecommerce starter

Premium responsive Bangladesh-focused storefront + admin dashboard.

## Preview locally
1. Install Node.js 20+ (https://nodejs.org).
2. Extract the ZIP and open this folder in Terminal/CMD.
3. Run:
   ```bash
   npm install
   npm run dev
   ```
4. Visit the localhost URL Vite displays.

## Demo admin (preview-only)
Go to the footer **Admin** button.
- Email: `admin@asthamart.com`
- Password: `AsthaDemo#2026`

This demo login and data are stored in the browser. This is **not secure for a live business**. It is for previewing the interface only. Do not use this password for real accounts or expose customer data.

## Included
- Responsive premium store UI, category filters, search, product cards/details, cart, checkout
- Demo orders, admin dashboard, add/delete products, inventory overview, order status updates
- Customer email magic-link and Google login integration scaffold
- Payment selection UI (COD, bKash, Nagad, Rocket, SSLCommerz/card)
- Supabase schema starter included at `supabase/schema.sql`

## Supabase setup for production
1. Create a Supabase project at https://supabase.com (free tier availability/limits may change).
2. In Project Settings → API, copy Project URL and anon/public key.
3. Create `.env` from `.env.example`, fill `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
4. Run `supabase/schema.sql` in Supabase SQL Editor.
5. Configure Authentication providers (Google OAuth) and email OTP/magic links. Phone login requires enabling phone provider and configuring an SMS provider; SMS may cost money.
6. Create your admin user using Supabase Auth. In SQL Editor, set that user's role:
   ```sql
   update public.profiles set role='admin' where id='YOUR_AUTH_USER_UUID';
   ```
7. For a real production app, integrate Supabase-backed catalog, cart, order reads, secure server-side admin routes and payment gateway callback verification. This starter currently uses browser localStorage for product/cart/order management; the order insert Supabase hook is included, but full remote sync and admin role enforcement need backend wiring before real use.

## Free deployment (Vercel)
1. Create a GitHub account, new repository and upload/extract these files.
2. Sign in to https://vercel.com and import that GitHub repository.
3. Framework preset: Vite. Build command `npm run build`, output directory `dist`.
4. Add environment variables from `.env` in Vercel project settings.
5. Deploy. Vercel provides a free `*.vercel.app` URL subject to its plan terms. Custom domains may require purchase.

## Payment gateways
Payment methods are display/selection only in this starter. For live bKash/Nagad/Rocket or SSLCommerz, apply for merchant credentials and implement their official API checkout + server-side validation/webhooks. Never collect/store card data yourself.

## Security checklist before launch
- Replace demo admin; disable preview admin credential
- Enable Supabase Auth; admin-only database policies and server-side authorization
- Do not expose service-role keys in frontend
- Server-side validate product prices, inventory and totals
- Payment callback verification; never trust browser checkout status
- Privacy policy, terms, return policy and delivery policy
- HTTPS, rate limiting, backups, audit logs
