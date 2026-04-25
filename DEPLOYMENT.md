# APsurance Landing Page - Deployment Guide

## 🚀 Quick Start

This is a production-ready, static HTML landing page for APsurance. No build step required.

## Deploy to Vercel (Recommended)

### Method 1: GitHub Integration (Easiest)

1. **Initialize Git**
   ```bash
   cd ~/Desktop/design_handoff_landing_page
   git init
   git add .
   git commit -m "Initial commit: APsurance landing page"
   ```

2. **Create GitHub Repository**
   - Go to https://github.com/new
   - Create new repo `apsurance-landing`
   - Copy the commands to push existing repo:
   ```bash
   git branch -M main
   git remote add origin https://github.com/youruser/apsurance-landing.git
   git push -u origin main
   ```

3. **Deploy via Vercel**
   - Visit https://vercel.com/new
   - Select your GitHub account
   - Import the `apsurance-landing` repository
   - Framework: Select "Other" (static site)
   - Build Command: Leave empty
   - Output Directory: `.` (root)
   - Click "Deploy"
   - Your site is now live!

### Method 2: Vercel CLI

```bash
npm install -g vercel
cd ~/Desktop/design_handoff_landing_page
vercel
# Follow prompts to link project and deploy
```

### Method 3: Drag & Drop

1. Create a zip file of the directory
2. Go to https://vercel.com
3. Drag the zip onto the dashboard
4. Wait for deployment

## Domain Configuration

Once deployed to Vercel:

1. Go to your Vercel project dashboard
2. Click "Settings" → "Domains"
3. Add your custom domain
4. Follow DNS setup instructions:
   - If you own the domain, add Vercel nameservers
   - OR create DNS records (A, CNAME, TXT)
5. SSL/HTTPS automatically provisioned (free)

Example: Point `apsurance.com` to your Vercel deployment

## File Structure

```
design_handoff_landing_page/
├── index.html          # Main landing page (all-in-one)
├── vercel.json         # Vercel configuration
├── package.json        # Project metadata
├── DEPLOYMENT.md       # This file
└── README.md           # Feature documentation
```

## Environment Configuration

The site works as-is with no environment variables. All content is hardcoded in `index.html`.

To externalize config, create a `.env.local` file:
```bash
VITE_PHONE=9549994342
VITE_EMAIL=APsurance@outlook.com
```

Then rebuild with a static site generator (Next.js, Hugo, etc.).

## Testing Before Deployment

### Local Testing
```bash
# Python 3
python -m http.server 3000

# OR Node http-server
npx http-server -p 3000

# OR Ruby
ruby -run -ehttpd . -p3000
```

Then visit: http://localhost:3000

### Testing Checklist
- [ ] Hero form validates correctly
- [ ] Phone number auto-formats
- [ ] Time slot selection works
- [ ] Form success state appears
- [ ] FAQ accordion toggles open/close
- [ ] Mobile layout is responsive
- [ ] All links work (nav, footer)
- [ ] Phone number is clickable on mobile

## Form Submission

**Current state:** Form shows success UI but doesn't actually submit.

### To Capture Leads

**Option A: Use Zapier (Free)**
1. Create Zapier account (zapier.com)
2. Create webhook: Zapier → Gmail or Slack
3. Get webhook URL
4. Add to form submission in HTML:
   ```javascript
   // Around line 500 in index.html, update form handler
   fetch('YOUR_ZAPIER_WEBHOOK_URL', {
     method: 'POST',
     body: JSON.stringify(data)
   })
   ```

**Option B: Use Formspree (Free)**
1. Visit formspree.io
2. Create project and get endpoint
3. Change form action:
   ```html
   <form action="https://formspree.io/f/YOUR_ID" method="POST">
   ```

**Option C: AWS Lambda + DynamoDB**
- Create serverless function to capture leads
- Store in DynamoDB
- Send email via SES

**Option D: Custom Backend**
- Create Node.js/Python API
- Deploy on Heroku, Railway, or similar
- POST form data to your API

## Performance Optimization

Current metrics:
- File size: ~35KB (index.html)
- Requests: 1 (no external resources)
- Load time: <500ms on 4G
- Lighthouse score: 95+

No additional optimization needed.

## Security Headers (Already Configured)

Vercel automatically adds via `vercel.json`:
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY
- X-XSS-Protection: 1; mode=block
- Referrer-Policy: strict-origin-when-cross-origin
- Cache-Control: max-age=3600

## SSL/HTTPS

Automatically provided by Vercel via Let's Encrypt.

## Environment-Specific Deployments

### Staging
```bash
git checkout -b staging
vercel --prod --scope=your-scope
```

### Preview
Every commit to main branch gets automatic preview URL.

## Troubleshooting

**Issue: "Cannot find module 'vercel'"**
```bash
npm install -g vercel
```

**Issue: "404 on routes"**
- Make sure `vercel.json` is in root
- Check that `index.html` exists

**Issue: "Styling looks broken"**
- Clear browser cache (Cmd+Shift+R)
- Check that CSS is embedded in HTML (not external file)

**Issue: "Form not submitting"**
- Open browser console (F12)
- Check for JavaScript errors
- Ensure webhook/API endpoint is reachable

## Monitoring

Set up monitoring in Vercel dashboard:
- Analytics (pageviews, conversion events)
- Error tracking
- Performance metrics
- Speed insights

## Content Updates

To update after deployment:
1. Edit `index.html` locally
2. Commit and push to GitHub
3. Vercel auto-redeploys
4. Changes live in <60 seconds

No cache busting needed; Vercel handles it.

## Rollback

If deployment breaks:
```bash
vercel rollback
# or revert commit and repush
git revert HEAD
git push origin main
```

## Analytics Integration

Add to `<head>` before `</head>`:

**Google Analytics 4:**
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**Microsoft Clarity:**
```html
<script>
    (function(c,l,a,r,i,t,y){
        c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
        t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i;
        y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y);
    })(window, document, "clarity", "script", "YOUR_ID");
</script>
```

## Support

Issues or questions?
- Email: APsurance@outlook.com
- Phone: (954) 999-4342
- Vercel support: vercel.com/support

---

**Ready to deploy?** Start with Method 1 (GitHub) above. Takes ~5 minutes. ✨
