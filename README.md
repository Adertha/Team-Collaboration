# Team-Collaboration
Design and Development of a Licensed Publishing Program for Frontline fitness

Work Health & Fitness Resource Licensing System

A WordPress-based licensing platform for Miller Health / Fitness Frontline that lets organisations register interest, receive a priced invoice, pay securely via Stripe, and immediately access licensed digital resources and self-paced learning.

Demo video: to be added
Live site: see Links section below.

Table of Contents

⦁	Project Goals
⦁	What’s Included
⦁	System Workflow
⦁	Key Features
⦁	Architecture
⦁	Security & Quality Assurance
⦁	Tech Stack
⦁	Setup & Configuration
⦁	Repository Structure
⦁	Links (Live Pages)
⦁	Stripe (use existing live account)
⦁	Admin Notes & Plugins
⦁	Roadmap / Future Enhancements
⦁	Contributors & Acknowledgements
⦁	License

Project Goals

⦁	Provide organisations a safe, structured way to purchase and access digital resources (books + learning modules).
⦁	Automate registration, license code generation, invoicing, secure payment, and access control.
⦁	Reduce admin effort, improve traceability, and support scalability.

What’s Included

⦁	PHP code for registration handling, CSRF/session security, Stripe Checkout, and admin invoice panel (in functions.php).
⦁	HTML views for user journeys (registration, login, success, payment success, download access).
⦁	Documentation for setup, security measures, and future improvements.

System Workflow

⦁	Organisation submits interest form → admin notified by email.
⦁	Admin reviews & sets price in the invoice admin page.
⦁	Invoice email sent automatically with org name + license code.
⦁	Org logs in (organisation name + license code).
⦁	Stripe secure checkout for payment.
⦁	On success → access to downloadable resources and self-paced learning.

Key Features

⦁	Automated license codes (e.g., MH0001, MH0002).
⦁	Admin dashboard to search orgs, set price, and send invoices (persisting amount & state).
⦁	Session-based org portal (login using org name + license code).
⦁	Stripe Checkout (HTTPS, PCI DSS compliant processor).
⦁	Immediate access to resources after successful payment.
⦁	Email notifications to both admin and organisation.

Architecture

⦁	Frontend: WordPress pages (Elementor), custom shortcodes, HTML views.
⦁	Backend: PHP (child-theme functions.php), WordPress hooks/actions, $wpdb queries.
⦁	Data: All org records are stored in WordPress MySQL ({prefix}_license_registrations).
⦁	Payments: Stripe Checkout Sessions; success webhook/return marks is_paid=1.
⦁	Sessions & CSRF: PHP sessions with HttpOnly & strict mode; CSRF token on forms.

Security & Quality Assurance

⦁	Form protection: CSRF tokens on login/checkout forms.
⦁	Input sanitisation: sanitize_text_field, sanitize_email, sanitize_textarea_field on all POST fields.
⦁	Session validation: gated pages check $_SESSION['lic_org_id'].
⦁	Transport security: HTTPS enforced by Stripe Checkout and WordPress host.
⦁	Data integrity: All data/resources stored in the WordPress database with controlled access.
⦁	QA: Unit checks on modules, end-to-end user flows, and UAT with sponsor before deployment.

Tech Stack

⦁	WordPress (Elementor + custom PHP in child theme)
⦁	PHP, MySQL (via $wpdb)
⦁	Stripe PHP SDK
⦁	Plugins used: Elementor, Stripe, Happy Elementor Addons, Conditional Menus

Setup & Configuration
1) Add code to your WordPress theme

Place the PHP from this repo into your child theme functions.php.

Create / verify the table: ${wpdb->prefix}license_registrations is created/updated by the code.

Create WordPress pages and add the included shortcodes/HTML where applicable.

2) Environment / constants

Set these in functions.php (already stubbed in the code):

define('STRIPE_SECRET_KEY', 'sk_live_****************'); // John’s live key
define('STRIPE_SUCCESS_URL', home_url('/completed-payment/'));
define('STRIPE_CANCEL_URL',  home_url('/org-dashboard/'));

3) Stripe (existing live account)

Log in to John’s Stripe Dashboard → Developers → API Keys.

Copy the Live secret key and paste into STRIPE_SECRET_KEY.

(Optional) Add a webhook endpoint in Stripe (Events: checkout.session.completed) pointing to your success handler if you enable webhooks.

Test with Stripe test mode first, then switch to live keys.

4) Permalinks & HTTPS

In WP Admin → Settings → Permalinks → set to “Post name”.

Ensure the site runs on HTTPS.

5) Email deliverability

Configure a transactional email sender (e.g., host SMTP, WP Mail) so invoice emails reach inbox.

Repository Structure
.
├─ theme_file/
│  └─ functions.php               # Core backend logic (registration, CSRF, sessions, admin invoice, Stripe)
└─ user/
   ├─ license registration form.html
   ├─ license registration form success page.html
   ├─ user login authentication.html
   ├─ program resources.html
   ├─ program resouces download.html
   └─ payment successful.html


You can rename folders without spaces (e.g., theme_file, user) for cleaner Git and Windows compatibility.

Links (Live Pages)

1.	Home / Licensing info: https://workhealthandfitnessrecord.com.au/licensing-page/
2.	Display resources: https://workhealthandfitnessrecord.com.au/program-page/
3.	Registration form: https://workhealthandfitnessrecord.com.au/542-2/
4.	Registration success: https://workhealthandfitnessrecord.com.au/page-to-show-success-message-after-user-registration-and-link-it-to-whfr-page/
5.	Admin invoice dashboard: https://workhealthandfitnessrecord.com.au/admin-invoice-page/
6.	User login: https://workhealthandfitnessrecord.com.au/user-login-registration/
7.	Org dashboard: https://workhealthandfitnessrecord.com.au/org-dashboard/
8.	Payment success: https://workhealthandfitnessrecord.com.au/completed-payment/
9.	Downloads access: https://workhealthandfitnessrecord.com.au/program-copy/
10.	Access to some pages is restricted by session and/or admin capabilities.

Stripe (use existing live account)

Replace the secret key with John’s live secret key.
Keep free downloads disabled before payment to protect IP and reduce revenue leakage.
All Stripe redirections occur over HTTPS; PCI DSS is handled by Stripe checkout.

Admin Notes & Plugins

Plugins: Elementor, Stripe, Happy Elementor Addons, Conditional Menus.
WP File Manager / CPanel: Not required for runtime, but useful for uploads and quick edits.
Backups: Ensure hosting backups are on; consider exporting DB table for records.

Roadmap / Future Enhancements

Remove free download before payment (enforce license compliance & IP protection).
License renewal / subscriptions.
Mobile app companion to broaden reach and improve engagement.
AI-based recommendations for tailored resource bundles.
Admin analytics dashboard (license sales, payment status, usage).

Contributors & Acknowledgements

Sponsor: Miller Health Pty Ltd (John Miller)
Team: Capstone Student Team — WordPress, PHP, MySQL, Stripe integration
Thanks to mentors for feedback and UAT support.


Git Quick Start
# first time
git init
git add .
git commit -m "Initial commit – License Resource System"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main


If you created the repo with a README, do:

git fetch origin
git pull --rebase origin main
git push -u origin main
