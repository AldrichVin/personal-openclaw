# Otsuka

Personal AI agent powered by [OpenClaw](https://docs.openclaw.ai), running 24/7 on EC2. Handles automated workflows, monitoring, and research — all controllable via WhatsApp.

## Active Workflows

### Job Hunter
Scans LinkedIn, Seek, and Indeed daily for Data Analyst roles in Melbourne. Generates tailored cover letters, sends them via WhatsApp for approval, and tracks all applications.

### TCC Coffee Monitor
Monitors social media mentions, competitor activity, and sentiment for TCC Coffee (B2B specialty coffee manufacturer in Jakarta). Weekly reports via WhatsApp.

### General Assistant
Research, web lookups, scheduling, and ad-hoc tasks — message Otsuka on WhatsApp anytime.

## Architecture

```
EC2 (Ubuntu) — OpenClaw Gateway
├── Otsuka Agent (Claude Sonnet 4.6)
├── WhatsApp Channel
├── Headless Chrome (browser automation)
├── SerpAPI (web search)
├── Memory System (persistent context)
└── Cron Scheduler (daily/weekly jobs)
```

## Tech Stack

OpenClaw · Claude Sonnet 4.6 · Google Chrome Headless · WhatsApp · SerpAPI · systemd · EC2
