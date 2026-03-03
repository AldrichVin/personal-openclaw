# Otsuka — Personal AI Agent on AWS EC2

A 24/7 personal AI assistant running on AWS EC2 using the OpenClaw framework, powered by Claude Sonnet 4.6. Otsuka handles job applications, brand monitoring, research tasks, and automated workflows through WhatsApp integration.

## Features

- **Multi-Skill Architecture**: Job tracking with tailored cover letter generation, TCC Coffee brand sentiment analysis, graphic tee market scouting
- **WhatsApp Integration**: Chat interface for controlling automation and receiving alerts
- **Browser Automation**: Headless Chrome for web scraping and data collection
- **Cron Scheduling**: Automated daily/weekly tasks with persistent memory
- **Persistent Memory**: JSON-based storage with session continuity
- **Subagent Delegation**: Opus/Sonnet for complex multi-step tasks

## Tech Stack

- **Framework**: OpenClaw (Node.js-based AI agent framework)
- **Model**: Claude Sonnet 4.6
- **Hosting**: AWS EC2 (t3.micro)
- **Integrations**: WhatsApp API, SerpAPI (web search), Chrome Automation
- **Storage**: JSON files, local filesystem
- **Task Scheduling**: Cron, systemd timers

## How It Works

1. **Listen**: Otsuka listens on WhatsApp for incoming messages
2. **Parse**: Analyzes intent (job application, monitoring request, research query)
3. **Execute**: Spawns subagents or runs tasks based on request type
4. **Report**: Returns results via WhatsApp with formatted output
5. **Persist**: Logs learnings and decisions to memory files for continuity

### Example Workflows

**Job Application Pipeline**
```
User: "I'm applying for this role at [company]"
→ Parse job posting
→ Generate tailored cover letter (Sonnet subagent)
→ Save to tracker
→ Send via WhatsApp + email
```

**Brand Monitoring**
```
Cron: Daily 9 AM
→ Scrape TCC Coffee social media + news
→ Sentiment analysis
→ Alert if significant change detected
```

## Project Structure

```
├── skills/
│  ├── job-application/
│  │  └── SKILL.md (cover letter generation)
│  ├── graphic-tee-scout/
│  │  └── SKILL.md (streetwear market intel)
│  └── ...
├── data/
│  ├── job-tracker.json
│  ├── profile.json
│  └── cover-letters/
├── memory/
│  ├── YYYY-MM-DD.md (daily logs)
│  └── MEMORY.md (long-term learnings)
├── SOUL.md (personality + values)
├── USER.md (owner context)
└── openclaw.json (gateway config)
```

## Key Learnings

- **Persistence matters**: JSON-based memory survives session restarts
- **Skill modularity**: Breaking tasks into reusable skills scales well
- **Subagent delegation**: Opus for planning, Sonnet for execution
- **WhatsApp as CLI**: Natural interface beats traditional chat UIs
- **AWS EC2 viability**: t3.micro is sufficient for 24/7 agent duty

## Deployment

Runs on AWS EC2 with systemd service auto-restart on failure.

```bash
# Check status
systemctl status openclaw

# View logs
journalctl -u openclaw -f
```

## Future Enhancements

- [ ] Gmail API integration (OAuth 2.0)
- [ ] Google Calendar sync
- [ ] Slack/Discord integration
- [ ] Network CRM (relationship tracking)
- [ ] Skill marketplace integration
- [ ] Multi-agent orchestration

---

**Author**: Aldrich Vincent  
**Status**: Active (2026-present)  
**Location**: AWS EC2 (t3.micro, Ubuntu 22.04)
