---
description: Extract links from a specified section and automatically invoke /summarize for each URL and then send the email
---

The user will provide a section name in the format:
  Section: <SECTION NAME>

## TASK 1 — Extract links from the specified section
- Invoke the /extract command with provided <SECTION>

Command invocation format:
  /extract <SECTION>

## TASK 2 — Generate summaries for extracted URLs
After extracting the URLs, invoke the /summarize command with all extracted URLs.

Command invocation format:
  /summarize <URL1> <URL2> <URL3> ...

// TASK 3 — Send the email
// (Disabled: This section is currently inactive and should not be executed.)

//After generate the <SUMMARY>, invoke the /email command with generated <SUMMARY>.

//Command invocation format:
//  /email <SUMMARY> ...

## RULES
- Execute each task in sequence