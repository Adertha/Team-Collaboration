# Team Collaboration  
### Design and Development of a Licensed Publishing Program for Frontline Fitness  
**Resource Licensing System**

A **WordPress-based licensing platform** for Fitness Frontline that allows organisations to register interest, receive a priced invoice, pay securely via Stripe, and immediately access licensed digital resources and self-paced learning.

---

## Table of Contents
- Project Goals  
- What’s Included  
- System Workflow  
- Key Features  
- Architecture  
- Security & Quality Assurance  
- Tech Stack  
- Setup & Configuration  
- Repository Structure  
- Live Links  
- Stripe Integration  
- Admin Notes & Plugins  
- Roadmap / Future Enhancements  
- Contributors & Acknowledgements  
- License  
- Git Quick Start  

---

## Project Goals
- Provide organisations a safe, structured way to purchase and access digital resources (books and learning modules).  
- Automate registration, license code generation, invoicing, secure payment, and access control.  
- Reduce administrative effort, improve traceability, and support scalability.  

---

## What’s Included
- PHP backend for registration handling, CSRF/session security, Stripe Checkout, and admin invoice panel (in `functions.php`).  
- HTML templates for user journeys (registration, login, success, payment success, and downloads).  
- Documentation for setup, security measures, and future improvements.  

---

## System Workflow
1. Organisation submits the registration form — admin receives an email notification.  
2. Admin reviews the request and sets a price in the admin invoice dashboard.  
3. Invoice email is automatically sent with organisation name and license code.  
4. Organisation logs in using organisation name and license code.  
5. Stripe secure checkout is initiated for payment.  
6. On successful payment, access to digital resources and learning modules is granted.  

---

## Key Features
- Automated license code generation (e.g., MH0001, MH0002).  
- Admin dashboard to search organisations, set pricing, and send invoices.  
- Session-based organisation portal with login via organisation name and license code.  
- Stripe Checkout integration (PCI DSS compliant).  
- Immediate access to licensed resources after payment.  
- Email notifications to both admin and organisation.  

---

## Architecture
- **Frontend:** WordPress pages (Elementor), custom shortcodes, HTML views.  
- **Backend:** PHP (child theme `functions.php`), WordPress hooks/actions, `$wpdb` queries.  
- **Database:** WordPress MySQL table `{prefix}_license_registrations` stores all organisation data.  
- **Payments:** Stripe Checkout sessions; on success, `is_paid=1` is updated.  
- **Security:** PHP sessions (HttpOnly, strict mode), CSRF tokens on forms.  

---

## Security & Quality Assurance
- **Form protection:** CSRF tokens applied to all forms.  
- **Input sanitisation:** `sanitize_text_field`, `sanitize_email`, and `sanitize_textarea_field` used on all POST inputs.  
- **Session validation:** Access-controlled pages check for active `$_SESSION['lic_org_id']`.  
- **Transport security:** HTTPS enforced by Stripe and WordPress host.  
- **Data integrity:** All data stored securely in the WordPress database with controlled access.  
- **Testing:** Unit testing and UAT conducted with sponsor before deployment.  

---

## Tech Stack
- WordPress (Elementor and HTML)  
- PHP / MySQL  
- Stripe PHP SDK  
- Plugins: Elementor, Stripe, Happy Elementor Addons, Conditional Menus  

---

## Setup & Configuration

### 1. Add Code to Your WordPress Theme
- Add the PHP code from this repository into your WordPress **child theme** `functions.php` via Appearance → Theme File Editor.  
- Ensure the table `${wpdb->prefix}license_registrations` exists or is created automatically.  
- Create WordPress pages and insert the provided HTML or shortcodes where required.  

### 2. Stripe Payment Setup
- Test using **Stripe Test Mode**, then switch to **Live Mode**.  
- Find API keys: Stripe Dashboard → Developers → API Keys.  
- Add the live secret key in your `functions.php` file:

```php
define('STRIPE_SECRET_KEY', 'sk_live_****************');
define('STRIPE_SUCCESS_URL', home_url('/completed-payment/'));
define('STRIPE_CANCEL_URL', home_url('/org-dashboard/'));
```

### 3. Permalinks and HTTPS
- In WP Admin → Settings → Permalinks → set to **Post name**.  
- Ensure the site runs over HTTPS.  

---

## Repository Structure
```
License-Registration-System/
│
├─ theme_file/
│  └─ functions.php              # Core backend logic (registration, sessions, admin, Stripe)
│
└─ user/
   ├─ license-registration-form.html
   ├─ registration-success.html
   ├─ user-login.html
   ├─ program-resources.html
   ├─ download-access.html
   └─ payment-success.html
```

---

## Live Links
1. Home / Licensing Info — https://workhealthandfitnessrecord.com.au/licensing-page/  
2. Resource Display — https://workhealthandfitnessrecord.com.au/program-page/  
3. Registration Form — https://workhealthandfitnessrecord.com.au/542-2/  
4. Registration Success — https://workhealthandfitnessrecord.com.au/page-to-show-success-message-after-user-registration-and-link-it-to-whfr-page/  
5. Admin Invoice Dashboard — https://workhealthandfitnessrecord.com.au/admin-invoice-page/  
6. User Login — https://workhealthandfitnessrecord.com.au/user-login-registration/  
7. Organisation Dashboard — https://workhealthandfitnessrecord.com.au/org-dashboard/  
8. Payment Success — https://workhealthandfitnessrecord.com.au/completed-payment/  
9. Download Access — https://workhealthandfitnessrecord.com.au/program-copy/  

---

## Stripe Integration
- Use the **existing live Stripe account** provided by the sponsor.  
- Replace the test secret key with the live one.  
- Keep free downloads disabled until payment is confirmed.  
- All Stripe redirects occur over HTTPS, ensuring PCI DSS compliance.  

---

## Admin Notes & Plugins
- **Plugins:** Elementor, Stripe, Happy Elementor Addons, Conditional Menus.  
- **WP File Manager / cPanel:** Optional, helpful for uploads and quick edits.  
- **Backups:** Ensure hosting backups are active; consider exporting the database table for records.  

---

## Roadmap / Future Enhancements
- Restrict free downloads until payment completion.  
- Add license renewal or subscription features.  
- Develop a companion mobile app.  
- Implement AI-based resource recommendations.  
- Build analytics dashboard for admins (sales, license tracking, and engagement).  

---

## Contributors & Acknowledgements
- **Sponsor:** Miller Health Pty Ltd (John Miller)  
- **Team:** Capstone Student Team — WordPress, PHP, MySQL, Stripe Integration  
- **Mentor:** Fatema Afroz  
- Special thanks for feedback, support, and User Acceptance Testing.  

---

## License
© 2025 Team Lion — For academic and client demonstration purposes under university project guidelines.  

---

## Git Quick Start

### Initial setup
```bash
git init
git add .
git commit -m "Initial commit – License Resource System"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### If repository already has a README
```bash
git fetch origin
git pull --rebase origin main
git push -u origin main
```
