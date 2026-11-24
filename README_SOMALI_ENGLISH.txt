TAMAL PLATFORM — MVP SOURCE PACKAGE

WHAT THIS BUILDS
- Customer registration/login using email + password.
- 4-digit PIN gate each time the dashboard is opened after login.
- Customer order submission inside the website (no WhatsApp order submission).
- Customer can view their own order history and status.
- Admin/staff dashboard: view orders, update status, maintain exchange rates and fees, view users.
- Only the initial owner/admin can grant or revoke staff role. Staff can operate orders/rates but cannot grant roles.
- Supabase Row Level Security protects customer records and order access.

IMPORTANT SECURITY / SCOPE
- A 4-digit PIN alone is not strong account authentication. This implementation uses email+password authentication plus a PIN gate. The PIN is hashed in the database and throttled after failed attempts.
- Do not share the Supabase service_role key. Only use the anon/public key in the website.
- The site collects order requests; it does NOT automatically receive money, send crypto/mobile money, or execute exchanges. Admin manually verifies payment and fulfils each order.
- The starter does not include SMS/email OTP, identity verification, payment gateway integration, live market feeds, automated wallet custody, automatic rate-based customer quotes, or dispute handling.
- Customer recipient numbers/wallet addresses are personal data; publish a privacy notice and restrict staff access appropriately before public launch.
- Review local laws, licensing, AML/KYC and sanctions obligations before operating exchange/payment services.

SETUP
1. Create a Supabase project.
2. Open SQL Editor and run supabase/schema.sql.
3. Sign up once in the website using your owner email.
4. The owner account used for this project is tamalexchange@gmail.com. Your earlier SQL result showed the role as maamule (the browser's Somali translation of admin). To verify using the actual database values, run:
   select email, role, role = 'admin' as is_admin from public.profiles where lower(email)=lower('tamalexchange@gmail.com');
   Expected role is admin and is_admin is true. If it is not, run:
   update public.profiles set role='admin' where lower(email)=lower('tamalexchange@gmail.com');
5. Open index.html locally for a quick test or deploy it to a static host (HTTPS required).
6. The supplied index.html is preconfigured with your Supabase Project URL and Publishable key. Never enter service_role or secret keys. The publishable key is intended for browser use.
7. Create a separate account for each staff member. As admin, open Users & Staff, enter their email and choose Staff. They must sign up first.
8. Test with a second customer account and confirm it cannot see other customers' orders.

DEPLOYMENT
Upload index.html to a static host that supports HTTPS (for example Netlify, Cloudflare Pages, or Vercel). Add your domain after deployment. The site uses Supabase JS from a CDN.

OWNER ACCESS
Keep your owner email account private. You can delegate staff access from the Admin panel; staff cannot promote themselves or other users. If you lose owner access, use Supabase account recovery and project controls.

RATE ENTRY
Admin > Qiimaha & khidmadaha. Enter a direction, e.g. USDT -> EVC Plus, the rate (how many EVC units for 1 USDT), and fee percentage. The initial MVP records rates for display/management but does not automatically quote or settle customer orders yet. The order page tells customers that final amount/fees are confirmed by TAMAL before funds are sent.


CURRENT CONNECTION STATUS (23 Nov 2026)
- Supabase SQL schema has been run successfully by the owner; the six database object checks returned OK.
- Owner/admin role was displayed as 'maamule' in the translated dashboard. In the database the expected role value is 'admin'.
- Project URL and publishable key are embedded in index.html.
- This ZIP is not a public live website yet. It must be uploaded to an HTTPS static host (or opened locally for testing). No hosting account or domain has been connected from this chat.


EMAIL CONFIRMATION REDIRECT FIX (23 Nov 2026)
- Signup now passes the currently opened website address as emailRedirectTo.
- When deployed on a public HTTPS domain, confirmation should return to that domain (not localhost), provided the same URL is allowed in Supabase Authentication > URL Configuration > Redirect URLs.
- Set Supabase Site URL to the final public HTTPS website URL after deployment.
- If you open the file locally, the redirect will still be localhost; this cannot be fully fixed until the site has a public hosting URL.
