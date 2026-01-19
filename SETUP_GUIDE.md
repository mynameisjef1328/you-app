# You App - Setup Guide

## Quick Start

Your app is ready to run! Here's how to enable payments and analytics.

## 1. Payment Integration (5 minutes)

### Stripe Payment Links (Recommended)

**Why Stripe?**
- Apple Pay & Google Pay included automatically
- Trusted by users worldwide
- 2.9% + 30¢ per transaction
- No monthly fees

**Setup Steps:**

1. Create a free Stripe account at https://stripe.com

2. Go to https://dashboard.stripe.com/payment-links

3. Click "Create payment link"

4. Configure your product:
   - Name: `You Plus`
   - Price: `$4.99 USD` (one-time payment)
   - Description: `Unlock all premium features in You app`

5. Under "After payment":
   - Success URL: `https://yourdomain.com?purchase=success`
   - This URL triggers the unlock automatically

6. Click "Create link" and copy the payment link
   - It looks like: `https://buy.stripe.com/xxxxx`

7. Open `index.html` and find line ~1486:
   ```javascript
   const STRIPE_PAYMENT_LINK = ""; // Paste your link here
   ```

8. Paste your link:
   ```javascript
   const STRIPE_PAYMENT_LINK = "https://buy.stripe.com/xxxxx";
   ```

9. Done! Users can now purchase with Apple Pay, Google Pay, or any credit card.

### Payment Methods Included:
- ✓ Apple Pay (iOS/Mac)
- ✓ Google Pay (Android/Chrome)
- ✓ All major credit cards
- ✓ International currencies (Stripe auto-converts)

## 2. Charity Donation Setup

Your app shows: "10% of every purchase supports mental health charities"

**How to fulfill this:**

### Option A: Manual Donations (Simple)
1. Track your revenue monthly
2. Donate 10% to charities like:
   - **NAMI** (National Alliance on Mental Illness) - https://nami.org
   - **Crisis Text Line** - https://crisistextline.org
   - **The Trevor Project** - https://thetrevorproject.org
3. Keep receipts for tax deductions

### Option B: Automatic via Stripe (Advanced)
1. Use Stripe Climate or create a custom workflow
2. Set up automatic percentage donations
3. Stripe handles it for you

**Suggested Charities:**
- **NAMI**: Grassroots mental health support
- **Crisis Text Line**: Free 24/7 text support
- **The Trevor Project**: LGBTQ+ youth crisis intervention
- **Mental Health America**: Prevention and early intervention

## 3. Analytics Setup (Optional)

Your app has analytics tracking built-in. Choose a service:

### Option A: Plausible (Recommended - Privacy-first)
1. Sign up at https://plausible.io ($9/month after trial)
2. Add this to `<head>` in index.html:
   ```html
   <script defer data-domain="yourdomain.com" src="https://plausible.io/js/script.js"></script>
   ```
3. Uncomment line 1098 in index.html:
   ```javascript
   if (window.plausible) plausible(eventName, { props: data });
   ```

### Option B: Google Analytics (Free)
1. Create account at https://analytics.google.com
2. Add GA4 tag to `<head>` in index.html
3. Uncomment line 1097:
   ```javascript
   if (window.gtag) gtag('event', eventName, data);
   ```

### Tracked Events:
- `tap_button` - User taps for affirmation
- `theme_select` - User changes background
- `breathing_toggle` - User toggles breathing animation
- `purchase_initiated` - User clicks "Get You Plus"
- `purchase_completed` - Successful purchase
- `share_click` - User shares an affirmation
- `plus_feature_attempted` - Free user tries premium feature

## 4. Deploy Your App

### Option A: GitHub Pages (Free)
1. Push your code to GitHub
2. Go to Settings → Pages
3. Select branch: `main`
4. Your app will be live at `username.github.io/you-app`

### Option B: Netlify (Free, better for PWA)
1. Connect your GitHub repo at https://netlify.com
2. Deploy automatically
3. Get custom domain support
4. Includes HTTPS automatically

### Option C: Vercel (Free, excellent performance)
1. Sign up at https://vercel.com
2. Import your GitHub repo
3. Automatic deployments on push
4. Built-in analytics

## 5. Testing Your Setup

1. **Test Payment Flow:**
   - Click "Get You Plus"
   - Complete checkout (use Stripe test card: 4242 4242 4242 4242)
   - Verify you're redirected with `?purchase=success`
   - Confirm "You Plus Active" badge appears

2. **Test PWA Installation:**
   - Visit your site on mobile
   - Look for "Add to Home Screen" prompt
   - Install and verify offline mode works

3. **Test Share Feature:**
   - Tap for an affirmation
   - Open menu → Share this moment
   - Verify native share dialog appears

## 6. Stripe Test Mode

Stripe starts in "Test mode" - perfect for development:

**Test Cards:**
- Success: `4242 4242 4242 4242`
- Decline: `4000 0000 0000 0002`
- Use any future expiry date and any CVC

**When ready for real payments:**
1. Complete Stripe account verification
2. Toggle "Test mode" off in Stripe Dashboard
3. Create a new payment link in live mode
4. Update `STRIPE_PAYMENT_LINK` with live link

## 7. Customization Tips

**Change Price:**
- Update line 678 in index.html: `<div class="plusPrice">$4.99</div>`
- Create new Stripe payment link with new price

**Change Charity Percentage:**
- Update line 865 in index.html
- Adjust your donation calculation accordingly

**Add More Themes:**
- Copy theme row in HTML (~line 609-618)
- Add theme to `THEMES` object in JavaScript (~line 1168)
- Define custom gradient colors

**Customize Affirmations:**
- Edit the `affirmations` array (~line 915)
- Add/remove/modify messages as you like

## Support

**Stripe Support:**
- Docs: https://stripe.com/docs/payments/payment-links
- Support: https://support.stripe.com

**Need Help?**
- All code is commented with clear instructions
- Search for "INTEGRATION POINT" in index.html for key areas
- Analytics tracking is automatic via `data-event` attributes

## Revenue Projection

At $4.99 per purchase:
- 100 users = $499 revenue, $449.10 after fees, $44.91 to charity
- 1,000 users = $4,990 revenue, $4,491 after fees, $449.10 to charity
- 10,000 users = $49,900 revenue, $44,910 after fees, $4,491 to charity

*(Assumes 2.9% + 30¢ Stripe fees)*

## What's Included

✅ PWA support (install as app)
✅ Offline mode via service worker
✅ Apple Pay & Google Pay ready
✅ Analytics tracking built-in
✅ Share functionality
✅ Keyboard shortcuts (spacebar to tap)
✅ Feature gating system
✅ Charity donation messaging
✅ Purchase state management
✅ Responsive design
✅ Accessibility (ARIA labels)
✅ SEO meta tags
✅ Social sharing cards

---

**You're ready to launch!** 🚀

Start in test mode, validate everything works, then flip to live mode and share with the world.
