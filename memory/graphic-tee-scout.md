# Graphic Tee Image Scout

## CRITICAL: How to execute
**DO NOT use web_search or brave_search for this task.**
**DO NOT look up images manually.**

When asked to scout graphic tees, you MUST run this exact bash command using your bash/exec tool:

```bash
bash /home/ubuntu/.openclaw/workspace/scripts/tee-scout.sh
```

That script handles everything: searching SerpAPI, downloading images, and sending them to WhatsApp. Just run it and confirm to the user it's running.

## Trigger phrases
Invoke the script when the user says any of:
- "scout graphic tees"
- "scout tees"
- "find me trending tees"
- "show me tee images"
- "tee scout"

## What the script does (for your reference — do NOT replicate this yourself)
- Searches Google Images via SerpAPI for 15 top streetwear brands
- Downloads the best image for each brand
- Sends each image to WhatsApp (+628170511109) with a caption
- Brands covered: Supreme, Palace, Culture Kings, Stussy, BAPE, Carhartt WIP, HUF, Pleasures, Brain Dead, Kith, ASSC, Thrasher, Fucking Awesome, Ripndip, Human Made

## Correct response to user
After running the script, reply:
"Scout running! Sending images from 15 brands to your WhatsApp now."

## What NOT to do
- Do NOT use web_search / brave_search
- Do NOT try to find images yourself
- Do NOT ask for a Brave API key
- Do NOT describe tees in text — the script sends actual images
