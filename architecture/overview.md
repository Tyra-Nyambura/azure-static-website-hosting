# Azure Budget Static Site Architecture

## Overview

This repository implements a cost-optimized static website hosting solution on Azure, with minimal serverless contact form processing. The architecture prioritizes free/low-cost services while maintaining functionality and scalability.

## Cost Optimization Strategy

### Primary Cost Drivers Addressed
- **Static Content**: Use free tier of Azure Static Web Apps
- **Dynamic Processing**: Minimal compute time for form submissions only
- **Email**: Leverage free SMTP quotas or low-cost providers
- **Scaling**: Pay-per-use model with no idle costs

### Estimated Monthly Costs (Low Traffic)
- **Azure Static Web Apps**: $0 (free tier up to 100GB bandwidth)
- **Azure App Service**: $0-10 (consumption plan, billed per execution)
- **Email Service**: $0 (Gmail SMTP free tier) - $5 (SendGrid free tier)
- **Total**: $0-15/month for typical personal/business sites

## High-Level Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   User Browser  │────│ Azure CDN/Static │────│ Azure Static    │
│                 │    │ Web Apps (Free)  │    │ Web Apps        │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │
         │ (Form Submission - Pay per use)
         ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Contact Form  │────│ Azure App Service│────│ Consumption     │
│   (HTML/JS)     │    │ (Consumption Plan)│    │ Plan (PHP)     │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                       │
                                                       ▼
                                               ┌─────────────────┐
                                               │   Free Email    │
                                               │   Service       │
                                               └─────────────────┘
```

## Components

### 1. Azure Static Web Apps (Free Tier)
- **Cost**: Free up to 100GB bandwidth/month
- **Purpose**: Hosts static website content
- **Features**:
  - Global CDN (included)
  - Automatic SSL certificates (free)
  - GitHub integration (free)
  - Staging environments (free)
- **Scaling**: Handles millions of requests without cost increase

### 2. Azure App Service (Consumption Plan)
- **Cost**: $0.20 per million requests + execution time
- **Purpose**: Processes contact form submissions
- **Runtime**: PHP on Linux containers
- **Features**:
  - Pay only when forms are submitted
  - Auto-scaling to zero
  - No idle costs
- **Typical Cost**: <$1/month for 100 form submissions

### 3. Email Infrastructure (Free/Low-Cost)
- **Options**:
  - **Free**: Gmail SMTP (500 emails/day)
  - **Low-Cost**: SendGrid free tier (100 emails/day)
  - **Paid**: $1-5/month for higher volumes
- **PHPMailer**: Open-source, no additional cost

## Data Flow

1. **Page Load** (Free):
   - Static content served via global CDN
   - No compute costs

2. **Form Submission** (Minimal Cost):
   - Brief execution on consumption plan
   - Email sent via free SMTP
   - Response returned

## Cost Optimization Features

### Static Web Apps Benefits
- No server management costs
- Free SSL and custom domains (with limitations)
- Built-in CDN reduces bandwidth costs

### Consumption Plan Benefits
- Zero cost when no forms submitted
- Sub-second billing
- Automatic scaling

### Email Cost Controls
- Client-side validation reduces invalid submissions
- Rate limiting prevents abuse
- Template reuse minimizes processing

## Scaling Considerations

### Low Traffic (<1000 visits/month)
- Total cost: $0-5/month
- Use free tiers exclusively

### Medium Traffic (1000-10000 visits/month)
- Static Web Apps: Still free
- App Service: $1-10/month
- Email: May need paid tier ($5-20/month)

### High Traffic (>10000 visits/month)
- Consider premium Static Web Apps ($9/month)
- App Service dedicated plan for consistent performance

## Alternative Cost-Optimized Architectures

### Option A: Fully Static (Zero Cost)
- Use services like Formspree or Netlify Forms
- No PHP required
- Limited customization

### Option B: Azure Functions (Lower Cost)
- Custom handler for PHP
- Potentially cheaper than App Service for sporadic use
- More complex setup

### Option C: Single App Service
- Host everything on one service
- Simpler but higher baseline cost
- Better for consistent traffic

## Monitoring Costs

- **Application Insights**: Free tier available
- **Azure Monitor**: Basic metrics free
- **Email Delivery Tracking**: Built into PHPMailer logs

This architecture provides enterprise-grade functionality at personal website costs, scaling from $0 to hundreds of dollars based on traffic patterns.