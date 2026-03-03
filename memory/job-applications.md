# Job Tracker & Cover Letter Skill

## Data Files
- **Tracker:** `~/.openclaw/workspace/data/job-tracker.json`
- **Profile:** `~/.openclaw/workspace/data/profile.json`
- **Resume PDF:** `~/resume.pdf`
- **Cover letters saved to:** `~/.openclaw/workspace/data/cover-letters/`

---

## PRIMARY COMMAND: "I'm applying for [job posting]"

**Trigger phrases:** "I'm applying for", "Im applying for", "applying for this job", "apply for this", or any message that contains a job posting/description with intent to apply.

**This is the main workflow. It does THREE things automatically:**

### Step 1: Duplicate Check
1. Read `job-tracker.json`
2. Extract company name and role from the job posting
3. Fuzzy match against existing entries (case-insensitive, partial match)
4. **If duplicate found:** STOP. Warn user: "You already applied to [Company] - [Role] on [Date] (ID #X). Status: [Status]. Want to continue anyway?"
5. **If no duplicate:** proceed to Step 2

### Step 2: Generate Tailored Cover Letter
1. Read `profile.json` for full resume data
2. Parse job requirements from the posting — extract:
   - Company name
   - Role title
   - Top 3-5 required skills
   - Company mission/values (if visible)
   - Industry/domain
   - Salary (if listed)
3. Use `projectSelectionRules` from profile.json to pick 2-3 most relevant projects
4. **Delegate to Sonnet subagent** for writing (this is long-form writing)
5. Write a 5-paragraph tailored cover letter following the template below
6. Save to `~/.openclaw/workspace/data/cover-letters/[Company]_[Role]_CoverLetter.txt`
7. Send the full cover letter text via WhatsApp

### Step 3: Auto-Track the Application
1. Read `job-tracker.json`
2. Add new entry with:
   - Next auto-incremented ID
   - Company name and role extracted from posting
   - `dateApplied`: today's date (YYYY-MM-DD)
   - `status`: "Applied"
   - `salary`: from posting if listed, otherwise null
   - `coverLetterFile`: the filename from Step 2
   - `notes`: brief note on which projects/skills were emphasized
3. Write updated JSON back
4. Confirm at the end of the WhatsApp message:
```
---
✅ Tracked as #[ID] | [Company] - [Role] | Applied [Date]
Cover letter saved to: [filename]
```

---

## Cover Letter Template

**Paragraph 1 — Hook + Credentials (2-3 sentences):**
- Reference specific company mission or recent project
- Mention CS degree from Monash University (3.81 GPA)
- Express enthusiasm for the specific role

**Paragraph 2 — Technical Fit (3-4 sentences):**
- Lead with their #1 required skill
- Connect to a specific project with concrete outcomes (use the `copyPaste` field from profile.json)
- Show breadth with 2-3 more matching skills
- Match their specific tech stack
- When referencing projects that have URLs, include the URL inline

**Paragraph 3 — Experience + Business Impact (3-4 sentences):**
- Highlight Veve Clothing internship (1 year, Operations & Sales)
- Emphasize business impact (workflow automation, improved reporting accuracy)
- Connect past experience to their domain
- Use phrase: "translate complex data insights into actionable business recommendations"

**Paragraph 4 — Enthusiasm + Culture Fit (2-3 sentences):**
- Reference specific aspect of the company
- Connect collaboration experience (Student Council, cross-functional teams)
- Show communication skills for technical-to-non-technical translation

**Paragraph 5 — Closing (2 sentences):**
- Melbourne-based, full Australian working rights
- Eager to discuss, professional sign-off with "Sincerely, Aldrich Vincent"

**Footer — ALWAYS include after sign-off:**
```
Portfolio: https://personal-project-eight-gamma.vercel.app/
LinkedIn: https://www.linkedin.com/in/aldrich-vincent-4463b2355/
GitHub: https://github.com/AldrichVin
```

## Cover Letter Rules
- **DO NOT** use generic phrases: "hard worker", "team player", "passionate about data"
- **DO** use specific project outcomes and measurable achievements
- **DO** show value brought, not desire to learn
- **DO** match the company's industry with relevant project emphasis
- **DO** include project URLs where available (Australia Weather viz, DataPraktis, Portfolio)
- **ALWAYS** include portfolio, LinkedIn, GitHub links at the end
- **ALWAYS** mention Melbourne-based + full working rights in closing
- Keep total length under 400 words
- Professional but confident tone — not sycophantic

---

## OTHER COMMANDS

### "status" or "tracker" or "applications"
1. Read `job-tracker.json`
2. Group applications by status
3. Format as clean WhatsApp summary:
```
📋 Job Tracker (X total)

✅ Applied (N):
#1 Company - Role (Date)
...

🎤 Interview (N):
...

❌ Rejected (N):
...

🎉 Offer (N):
...
```

### "update [id] [status]"
1. Find application by ID in `job-tracker.json`
2. Update status to: Applied, Interview, Rejected, or Offer
3. Confirm: "Updated #[ID] [Company] - [Role] → [Status]"

### "have I applied to [company]?" or "did I apply to [company]?"
1. Fuzzy search company name in `job-tracker.json`
2. If found: "Yes — #[ID] [Company] - [Role], status: [Status], applied: [Date]"
3. If not found: "No applications found for [Company]."

### "delete [id]"
1. Remove application by ID from `job-tracker.json`
2. Confirm: "Deleted #[ID] [Company] - [Role]"

### "track [company] [role]"
Manual tracking without cover letter:
1. Check for duplicates
2. If new: add entry with status "Applied", current date
3. Confirm: "Tracked: [Company] - [Role] (ID #X)"

---

## Duplicate Detection Rules
- Normalize company names: lowercase, strip "Pty Ltd", "Ltd", "Group", "Inc", "Corporation"
- Match if company name contains 80%+ of the search term
- Same company but different role is NOT a duplicate
- If duplicate found on primary command, STOP and ask before proceeding
