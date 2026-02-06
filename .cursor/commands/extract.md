---
description: Extract links from a named section and trigger summarization
---

The user will provide:
  Section: <SECTION NAME>

## TASK
1. Locate the section whose header matches the provided section name (case-insensitive)
2. Extract all <a href="..."> links inside that section
3. Output them as a clean list
4. Then automatically trigger the next command by outputting:

     /summarize
     <URL1>
     <URL2>
     <URL3>

Cursor will automatically run /summarize with the URLs as input.

## OUTPUT FORMAT
### Extracted Links from "<SECTION>"
<one URL per line>

### Trigger Summaries
/summarize
<URL1>
<URL2>
<URL3>

## RULES
- Do NOT wrap commands in code blocks
- Do NOT indent the /summarize line
- If no section found, output:
    No section found matching: <SECTION>
- If no links found, output:
    No links found in section: <SECTION>