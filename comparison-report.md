# Documentation Comparison Report

**Generated:** 2026-01-31
**Source PR:** #9 - fix: increase max-turns and optimize Claude prompt
**Author:** rasheed-fabrichq

## Summary

This report compares the current source code (`source-repo/src/app.js`) with the existing documentation (`docs-repo/docs/*.md`) to identify discrepancies.

## Changes Required

### Items to UPDATE (Changed Values)

#### authentication.md

| Item | Current in Docs | Actual in Code | Line Reference |
|------|----------------|----------------|----------------|
| Token expiry duration | 24h | 48h | authentication.md:33, 43, 56 |
| Max login attempts | 5 | 10 | authentication.md:45 |
| Min password length | 8 characters | 10 characters | authentication.md:47 |

#### billing.md

| Item | Current in Docs | Actual in Code | Line Reference |
|------|----------------|----------------|----------------|
| Starter tier price | $29/month | $39/month | billing.md:13 |
| Pro tier price | $99/month | $129/month | billing.md:14 |

#### index.md

| Item | Current in Docs | Actual in Code | Line Reference |
|------|----------------|----------------|----------------|
| JWT expiry duration | 24-hour | 48-hour | index.md:28 |

### Items to ADD (New Features Not Documented)

#### authentication.md

1. **Google OAuth Authentication**
   - New endpoint: `POST /api/v2/auth/oauth/google`
   - Accepts `googleToken` in request body
   - Returns JWT token with `provider: 'google'` field
   - Code reference: app.js:78-101

#### billing.md

2. **Additional Payment Methods**
   - Code supports: `credit_card`, `bank_transfer`, `paypal`, `stripe`
   - Docs only mention: Credit Card and Bank Transfer
   - Missing in docs: PayPal, Stripe
   - Code reference: app.js:134

3. **Payment Methods API Endpoint**
   - New endpoint: `GET /api/v2/billing/payment-methods`
   - Returns list of available payment methods
   - Code reference: app.js:181-183

#### index.md

4. **Health Check Endpoint**
   - New endpoint: `GET /api/v2/health`
   - Returns API status, version, and timestamp
   - Code reference: app.js:188-194

### Items to DELETE (Removed Features Still in Docs)

#### authentication.md

1. **Password Reset Feature**
   - Documented at authentication.md:58-73
   - Endpoint `POST /api/v2/auth/reset-password` does NOT exist in code
   - Error code 429 (RATE_LIMITED) also not implemented in code
   - Should be removed from documentation

## Changes by File

### authentication.md
- **UPDATE:** JWT token expiry from "24h" to "48h" (3 occurrences)
- **UPDATE:** Max login attempts from "5" to "10"
- **UPDATE:** Min password length from "8 characters" to "10 characters"
- **ADD:** Google OAuth authentication section
- **DELETE:** Password reset section (feature not implemented)
- **DELETE:** Error code 429 RATE_LIMITED (not in code)

### billing.md
- **UPDATE:** Starter tier price from "$29/month" to "$39/month"
- **UPDATE:** Pro tier price from "$99/month" to "$129/month"
- **ADD:** PayPal payment method
- **ADD:** Stripe payment method
- **ADD:** Payment methods API endpoint documentation

### index.md
- **UPDATE:** JWT expiry duration from "24-hour" to "48-hour"
- **UPDATE:** Version history to include PR #9 changes
- **ADD:** Health check endpoint to key features
- **DELETE:** Password reset from key features list (feature not implemented)

## Summary Statistics

- **Total Updates Required:** 6 value changes
- **Total Additions Required:** 4 new features
- **Total Deletions Required:** 2 removed features
- **Files Affected:** 3 (authentication.md, billing.md, index.md)

## Priority

All changes are documentation-only updates to align with the actual codebase. No breaking changes for existing API consumers, but clarifications prevent confusion about:
- Token expiry expectations (24h vs 48h)
- Security limits (login attempts, password length)
- Available payment options
- Non-existent password reset feature
