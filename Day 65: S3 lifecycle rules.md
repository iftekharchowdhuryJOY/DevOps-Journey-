# Day 65: S3 Lifecycle Rules

## The Core Concept

S3 Lifecycle rules are automated policies that decide how long data lives, where it lives, and when it dies.

---

## First: The Mental Model (Burn This In)

Every object in S3 goes through a life:

```
Born → Used → Rarely used → Archived → Deleted
```

Lifecycle rules move objects along that path **automatically**.

> Humans forget. Policies don't.

---

## What Lifecycle Rules Can Do (Capabilities)

Lifecycle rules can:

### 1. Transition Objects
- Standard → IA
- IA → Glacier
- Glacier → Deep Archive

### 2. Expire Objects
- Permanent deletion after N days

### 3. Handle Versions
- Delete old versions
- Keep only last N versions

### 4. Clean Up Failed Multipart Uploads
- Silent cost killer if ignored

---

## Storage Classes (Why Lifecycle Exists)

Let's speak plainly.

| Class | Cost | Speed | Purpose |
|-------|------|-------|---------|
| Standard | $$ | Fast | Active data |
| IA | $ | Fast (retrieval fee) | Rarely accessed |
| Glacier | $ | Slow (minutes–hours) | Archive |
| Deep Archive | ¢ | Very slow (12–48h) | Legal cold storage |

**Lifecycle rules move data down this ladder.**

---

## Real-Life Example #1 — Startup SaaS (The Most Common Case)

### Scenario
A startup runs:
- A web app
- User uploads images and documents
- Growth is fast, money is not

### Data Reality
- **New files** → accessed often
- **30–90 days later** → almost never accessed
- **1 year later** → basically dead

### Lifecycle Strategy
```
Day 0     → S3 Standard
Day 30    → S3 IA
Day 180   → Glacier
Day 365   → Delete
```

### Why This Works
- App stays fast
- Costs drop silently
- No engineer touches it again

**This alone can cut S3 bills by 60–80%.**

---

## Real-Life Example #2 — Logs (Enterprises Love This)

### Scenario
- ALB logs
- CloudTrail logs
- Application logs

### Reality
- 99% never read
- Kept for audits
- Accessed only during incidents

### Lifecycle Strategy
```
Day 0    → Standard
Day 7    → IA
Day 30   → Glacier
Day 365  → Delete (or Deep Archive if regulated)
```

### Why Companies Do This
- Compliance satisfied
- Auditors happy
- Storage bill sane

---

## Real-Life Example #3 — Versioned Buckets (Critical)

**This is where beginners bleed money.**

### Problem
- Versioning enabled
- Old versions accumulate
- Deleted objects still cost money

### Lifecycle Fix
- Keep last 3 versions
- Delete older versions after 30 days

> Without this rule, versioning is a financial leak.

---

## How GOOD Companies Think About Lifecycle

This is important.

### Startups
- Aggressive deletion
- Short retention
- Optimize for survival

### Scale-ups
- Tiered storage
- Cost dashboards
- Product-aware rules

### Enterprises
- Compliance-driven
- Separate rules per data type
- Legal holds override lifecycle

**Lifecycle rules are designed with legal + finance + engineering together.**

---

## Lifecycle Filters (How Rules Stay Sane)

Rules don't have to apply to everything.

They can target:
- **Prefixes** (`logs/`, `uploads/`)
- **Tags** (`env=prod`, `type=backup`)
- **Object size**

### Example Thinking
*"Only move logs, not user uploads."*

**This is how grown-ups avoid accidents.**

---

## What Lifecycle Rules Do NOT Do (Important)

Let's kill myths.

- ❌ Not real-time
- ❌ Not guaranteed to run at exact midnight
- ❌ Not reversible
- ❌ Not a backup
- ❌ Not an access control mechanism

**They are eventually consistent cleanup machines.**

---

## Common Mistakes (I've Seen These in Real Companies)

### Mistake #1: No Lifecycle at All

**Result:**
- S3 bill explodes quietly
- Finance asks questions
- Engineers scramble

### Mistake #2: Archiving Too Early

**Result:**
- App reads from Glacier
- Latency spikes
- Incident at 2am

### Mistake #3: Forgetting Multipart Uploads

**Result:**
- Thousands of orphaned parts
- Invisible cost
- Nobody knows why

### Mistake #4: Lifecycle + Replication Confusion

**Result:**
- Objects deleted in source
- Deleted in destination
- DR compromised

---

## Lifecycle + Business Mindset (This Is Key)

Lifecycle rules encode business intent.

You're answering:
- How long is data valuable?
- When does risk > value?
- When does storage cost > usefulness?

**That's architecture. Not configuration.**

---

## Final Mentor Truth

If you:
- Enable versioning
- Don't define lifecycle
- And store logs

You're not "secure" or "safe". **You're just postponing pain.**

### Lifecycle Rules Are:
- Quiet
- Boring
- Extremely powerful

**They don't make headlines. They make budgets survivable.**
