# CLAUDE.md — Mutual Fund Dashboard (Mentorship Project)

## What this is
A cloud-hosted Mutual Fund Performance Dashboard. The app is the vehicle; the
real deliverable is **Ben's understanding**. Ben is a rising junior CS student
with some Python, AWS, and Linux experience. New to him: Git workflow,
Terraform, Lambda+DynamoDB, GitHub Actions, and pairing with an AI in VS Code.

## The one rule
**If Ben can't explain it, it doesn't merge.** Optimize for his understanding,
not for shipping fast.

## How Claude should behave
- Explain the concept and *why* before writing code.
- Pair-mode, split work:
  - **Claude scaffolds:** Terraform boilerplate, project structure, CI skeleton,
    test harness, tricky IAM.
  - **Ben writes:** DynamoDB schema, read-Lambda query/sort/filter/search logic,
    frontend fetch+render, his own tests.
  - **Always Ben:** every Git op, every PR description, an explanation before merge.
- Small, reviewable commits: branch → PR → Ben explains → merge.
- Teach Ben to read generated code critically and catch mistakes.
- Slide the knob per task: harder pieces → Claude leads + Ben reviews.

## Architecture
Live free API → **Ingestion Lambda** (scheduled) → **DynamoDB**
→ **Read Lambda** (Function URL) → **S3 static site** (HTML/CSS/JS) → public URL.
Terraform provisions everything; GitHub Actions deploys it. CloudWatch for logs.

Key decision: the read path serves from DynamoDB and never touches the external
API live — keeps the demo fast and always-up.

## Stack
Python · AWS Lambda + Function URL · DynamoDB · S3 static hosting · Terraform ·
GitHub Actions · CloudWatch · VS Code + Claude.

## Data source
Live free API (candidates: yfinance/Yahoo, Financial Modeling Prep, Twelve Data).
Ben spikes 2–3 in Week 3 and picks based on real fund coverage.

## Four-week plan
- **Week 1** — Repo + Git workflow to muscle memory; README + architecture sketch.
- **Week 2** — Terraform: DynamoDB, S3, IAM, stub Lambdas + Function URL.
- **Week 3** — API spike & pick → ingestion Lambda → schema → read logic + tests → frontend.
- **Week 4** — CI/CD, CloudWatch, secrets, docs, diagram, screenshots, polish.

## Definition of done
Résumé-ready public repo: README, architecture diagram, screenshots, live demo
link, meaningful commit history, PRs, and a working CI/CD pipeline.

## Cost
Stay near-free. S3 + Lambda + DynamoDB only. Add CloudFront/API Gateway only if
justified with a reason Ben can explain.
