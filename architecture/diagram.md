```
Azure Static Website Hosting Architecture (Cost-Optimized)

┌─────────────────────────────────────────────────────────────┐
│                    User Browser                             │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Azure Front Door / CDN                        │
│  (FREE: Global distribution, SSL, caching)                │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Azure Static Web Apps                          │
│  (FREE TIER: Up to 100GB bandwidth/month)                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Static Content:                                     │    │
│  │ - index.html (FREE)                                 │    │
│  │ - CSS, JS, images (FREE)                            │    │
│  │ - Contact form UI (fcf.form.htm) (FREE)            │    │
│  └─────────────────────────────────────────────────────┘    │
│  Features:                                                 │
│  - GitHub integration (FREE)                              │
│  - Staging environments (FREE)                            │
│  - Custom domains (FREE with limitations)                 │
└─────────────────────┬───────────────────────────────────────┘
                      │ (Form POST - Pay per execution)
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Azure App Service                             │
│  (CONSUMPTION PLAN: $0.20/million requests)               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Dynamic Processing:                                 │    │
│  │ - Form validation (fcf.config.php)                  │    │
│  │ - Email sending (PHPMailer)                         │    │
│  │ - Response handling                                 │    │
│  └─────────────────────────────────────────────────────┘    │
│  Runtime: PHP 8.x (Linux)                                │
│  Scaling: Auto-scale to zero (NO IDLE COSTS)            │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│              Email Service                                 │
│  (FREE: Gmail SMTP - 500 emails/day)                       │
│  (LOW COST: SendGrid free tier - 100 emails/day)          │
│  - HTML/Text templates                                     │
│  - Delivery confirmation                                   │
└─────────────────────────────────────────────────────────────┘

Cost Breakdown (Typical Personal Site):
• Static Web Apps: $0/month
• App Service (100 submissions): $0.02/month
• Email (Gmail): $0/month
• TOTAL: $0.02/month

Scaling Costs:
• 1,000 form submissions: ~$0.20/month
• 10,000 form submissions: ~$2/month
• 100,000+ submissions: Consider dedicated plan

Key Cost Benefits:
• Zero idle costs
• Pay only for actual usage
• Free tiers for most components
• Global CDN included
• No server management fees
```