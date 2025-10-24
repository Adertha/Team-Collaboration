# Team Collaboration  
### Design and Development of a Licensed Publishing Program for Frontline Fitness  
**Resource Licensing System**

A **WordPress-based licensing platform** for Fitness Frontline that enables organisations to register interest, receive an invoice, make secure payments via Stripe, and gain immediate access to licensed digital resources and self-paced learning materials.

---

## Table of Contents
1. Project Goals  
2. System Workflow  
3. Key Features  
4. Architecture  
5. Security & Quality Assurance  
6. Repository Structure  
7. Setup & Configuration  
8. Stripe Integration  
9. Live Links  
10. License  
11. Git Quick Start  

---

## Project Goals
- Provide organisations with a safe, structured way to purchase and access licensed digital resources.  
- Automate the end-to-end process: registration, license code generation, invoicing, payment, and access.  
- Reduce manual effort for administrators, ensure transparency, and support scalability for future resource expansion.  

---

## System Workflow
1. **Organisation Registration:**  
   The organisation submits an online registration form expressing interest.  

2. **Admin Review & Pricing:**  
   Admin is notified via email, reviews the registration, and sets a license price using the invoice dashboard.  

3. **Invoice Generation:**  
   An automated invoice email is sent to the organisation containing the license code and payment link.  

4. **Organisation Login:**  
   The organisation logs in using its **name** and **license code**.  

5. **Stripe Payment:**  
   Payment is processed securely via Stripe Checkout.  

6. **Resource Access:**  
   Upon successful payment, the organisation gains instant access to licensed resources and learning modules.  

---

## Key Features
- Automated license code generation (e.g., MH0001, MH0002).  
- Admin dashboard for invoice management and payment tracking.  
- Secure organisation login using license code validation.  
- Stripe Checkout integration ensuring PCI DSS compliance.  
- Immediate access to licensed resources post-payment.  
- Email automation for both admin and organisation notifications.  

---

## Architecture
- **Frontend:** WordPress pages built with Elementor and custom HTML shortcodes.  
- **Backend:** PHP with WordPress hooks and actions for database operations and session handling.  
- **Database:** WordPress MySQL table for storing organisation data and payment status.  
- **Payment Gateway:** Stripe Checkout (session-based payment confirmation).  
- **Security Layers:** PHP sessions (HttpOnly, strict mode), CSRF token validation, HTTPS-enforced communication.  

---

## Security & Quality Assurance
- **Form Protection:** All forms use CSRF tokens to prevent cross-site request forgery.  
- **Data Sanitisation:** Inputs cleaned with `sanitize_text_field`, `sanitize_email`, and `sanitize_textarea_field`.  
- **Session Control:** Access-controlled pages verify active session variables (`$_SESSION['lic_org_id']`).  
- **Transport Security:** All data transmitted over HTTPS; payments handled by Stripe’s secure API.  
- **Testing:** User Acceptance Testing (UAT) completed with sponsor before deployment.  

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

## Setup and Configuration

### 1. Add Code to Your WordPress Theme
- Create WordPress pages and insert the provided HTML or shortcodes where required.  
- Copy the PHP code from this repository into your WordPress **child theme** `functions.php` via:  
  **Dashboard → Appearance → Theme File Editor → functions.php**

---

## Stripe Integration

### Step 1: Install Stripe PHP SDK  
- Download the official Stripe PHP SDK from GitHub:  
  🔗 [https://github.com/stripe/stripe-php](https://github.com/stripe/stripe-php)  
- Upload the SDK folder to your WordPress environment and include it in your theme or install it as a plugin.  

### Step 2: Configure Stripe in WordPress  
- Test using **Stripe Test Mode**, then switch to **Live Mode** once verified.  
- Find your API keys in **Stripe Dashboard → Developers → API Keys**.  
- Add your secret key and callback URLs in `functions.php`:  

```php
define('STRIPE_SECRET_KEY', 'sk_live_****************');
define('STRIPE_SUCCESS_URL', home_url('/completed-payment/'));
define('STRIPE_CANCEL_URL', home_url('/org-dashboard/'));
```

### Step 3: Enable Real-Time Payments  
- Use **live account keys** to make the payment system work in real-time.  
- Ensure all transactions are done through HTTPS.     
---

## Live Link
Resource License System: [https://workhealthandfitnessrecord.com.au/licensing-page/](https://workhealthandfitnessrecord.com.au/licensing-page/)

---

## License
© 2025 Team Lion — Developed for academic and client demonstration under university project guidelines.  

---

## Git Quick Start

### Initial Setup
```bash
git init
git add .
git commit -m "Initial commit – License Resource System"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### If Repository Already Has a README
```bash
git fetch origin
git pull --rebase origin main
git push -u origin main
```
