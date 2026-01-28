# AI Growth Loop Vision

**Reference document for strategic decision-making**

## The Vision

Build a fully automated marketing system that learns and improves continuously:

```
┌─────────────────────────────────────────────────────────────┐
│                    AUTOMATED GROWTH LOOP                     │
└─────────────────────────────────────────────────────────────┘

1. DATA COLLECTION (Daily)
   BigQuery ← Meta Marketing API
   - Ad performance (impressions, clicks, CTR, CPC, conversions)
   - Best performing copy
   - Audience insights

2. ANALYSIS ENGINE
   Python/Node analyzes:
   - Top performing ads
   - Copy patterns that work
   - Image styles that convert
   
3. COPY GENERATION
   OpenAI/Claude generates:
   - New ad variants based on winning patterns
   - Multiple angles and hooks

4. IMAGE GENERATION
   DALL-E/Imagen creates:
   - New images in all required ratios
   - Based on winning visual styles

5. AD CREATION
   Meta Marketing API:
   - Creates ads automatically
   - Uses proper naming conventions

6. OPTIMIZATION
   - Pause underperforming ads
   - Increase budget on winners

7. REPORTING
   Daily summaries of:
   - What was created
   - What was paused
   - Performance metrics
```

## Guiding Principles

### 1. Data First
- Every action should be trackable
- All data flows to BigQuery
- Decisions should be data-driven, not gut-feeling

### 2. Automate Everything (Eventually)
- Manual today → Script tomorrow
- Build reusable components
- Document for future automation

### 3. Safety Mechanisms
- Confidence scoring before auto-publish
- Budget caps
- Human override always available
- Start with PAUSED status

### 4. Naming Conventions Matter
- Follow Meta Ads naming: `cid{XXX}_cam_{type}_[v01]`
- Consistent Creative Bases (CB001, CB002, etc.)
- UTM parameters for attribution

## ROI Projection

**Manual process:** 8 hours/month @ 500 kr/hour = 4000 kr
**Automated:** 1 hour/month + 56 kr tools = 556 kr

**Savings: 86% (3444 kr/month)**

Plus:
- 24/7 optimization
- Faster iteration (daily vs weekly)
- Consistent execution
- Data-driven decisions

## Current Status

Track progress in: `nastahem/docs/project-guides/shared/AUTOMATED_GROWTH_LOOP_DESIGN.md`

## When Working on Any Task

Ask yourself:
1. Does this support the growth loop vision?
2. Is the data being captured?
3. Can this be automated?
4. Are we following naming conventions?
5. Is this documented for future reference?
