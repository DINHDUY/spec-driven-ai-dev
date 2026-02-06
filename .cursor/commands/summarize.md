---
description: Summarize each URL passed from extract and trigger email command
---

You will receive a list of URLs, one per line.

## TASK
For each URL:
  - Fetch and summarize the content
  - Collect all summaries into a single block

After summarizing all URLs, automatically trigger the email command by outputting:

    /email
    <FULL_SUMMARY_BLOCK>

Cursor will automatically run /email with the summary block as input.

## OUTPUT FORMAT
### Summaries
<summary for URL1>
<summary for URL2>
...

### Trigger Email
/email
<FULL_SUMMARY_BLOCK>

## RULES
- Do NOT wrap the /email line in code blocks
- Do NOT indent the command line
- Preserve the summaries exactly as generated
- Use web search or fetch tools to retrieve content from URLs
- Provide concise, factual summaries for each URL