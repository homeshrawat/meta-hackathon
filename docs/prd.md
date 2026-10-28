# PRD: Lost Wins — a self-building record of your wins from Gmail and Slack

Problem definition: [Lost wins: why people can't recall their own impact at review time](https://claude.ai/artifact/RbPp6so5kJhHUGU7QKdj6i)

Status: draft, 2026-10-29. Built for the Meta Global AI Developer Hackathon (due 2026-11-04).

## Glossary

| Term | Meaning |
|---|---|
| **Win** | One objective the person moved forward, backed by evidence. Many messages about the same objective collapse into one win. |
| **Win type** | What kind of win it is: Shipped, Praise received, Helped or unblocked, Decision driven, Ambiguity cleared, Customer impact. A win can carry several. |
| **Citation** | A pointer from a win back to a source message (Slack message or email) that supports it. |
| **Evidence label** | How the win is backed: **Praised by name** (someone else credited the person explicitly) or **Inferred from your messages** (the agent read the person's role from the conversation). |
| **Story** | A named, ordered chain of wins where each builds on earlier ones (e.g. "Pricing overhaul, Mar–Nov"). |
| **Review state** | Per win: Unreviewed, Ticked (kept), or Crossed (rejected). |
| **Timeline** | The person's wins ordered by when each objective happened. |
| **Source** | A connected place the agent reads: Gmail or Slack. |
| **Wins engine** | The part that turns a person's messages into wins and stories. |

## Problem Statement

People whose work happens in conversation (product managers, salespeople, and similar roles) do a year of real work but reach their review remembering only the last few weeks. Their wins are spread across Slack threads, DMs, private channels and email: a thread where they merged two teams' efforts, an email chain where they saved a customer, a "thanks, this saved us" from another team. Praise from others, the most convincing evidence, is the most scattered. A manual brag document fails because the habit doesn't last. At review time they face a blank page, keyword search returns noise, and the self-review leads with whatever happened recently. Existing tools read code and tickets, depend on manual logging, or read Slack only. None reads across email and Slack to give the person a complete, cited record they own.

## Solution

The person connects Gmail and Slack. That is the only setup. An agent then reads the last 12 months of their email and every Slack DM, public channel and private channel they can see, and builds a timeline of their wins on its own.

Each win is one objective, deduplicated across channels, with all its citations grouped underneath. It includes team wins and implicit wins, not only explicit callouts, and says plainly whether it was praised by name or inferred. Wins that build on earlier wins are linked into stories. The person ticks the wins they want to keep and crosses the ones that are wrong. After the first run, the agent keeps picking up new wins quietly, so the next review never starts from a blank page.

There is no export in v1. Instead, the person connects their AI assistant (such as Claude) over MCP. The assistant sees only ticked wins and their stories, and can write a self-review, a promotion case or 1:1 notes from them.

The record belongs to the person: their employer and manager can't see it, only ticked wins ever leave it, and they can delete everything at any time.

## User Stories

### Connecting and first run

1. As a product manager, I want to connect my Gmail account in one step, so that the agent can read my email without any further setup.
2. As a product manager, I want to connect my Slack workspace in one step, so that the agent can read my conversations without any further setup.
3. As a salesperson, I want connecting my accounts to be the only thing I have to do, so that I get value without configuring channels, labels or keywords.
4. As a user, I want the agent to start working as soon as I connect a source, so that I don't have to trigger anything.
5. As a user, I want the agent to look back over the last 12 months by default, so that a full review period is covered.
6. As a user, I want to see that the agent is working and roughly how far it has got, so that I know to wait instead of assuming it's broken.
7. As a user, I want wins to appear on my timeline as they are found, so that I'm not staring at an empty screen until the whole year is processed.
8. As a user, I want to connect one source first and add the other later, so that I can start with whichever account I have to hand.
9. As a user, I want wins from a newly connected source to merge into my existing timeline, so that I don't get duplicates when I add Slack after Gmail.

### What the agent reads

10. As a user, I want the agent to read my Slack DMs, so that praise and help given one-to-one is captured.
11. As a user, I want the agent to read my private Slack channels, so that work done in small team channels is captured.
12. As a user, I want the agent to read the public Slack channels I'm in, so that help I gave in places like a #product-help channel is captured.
13. As a user, I want the agent to read my sent and received email, so that escalations, customer threads and forwarded praise are captured.
14. As a user, I want newsletters, notifications and other automated mail to be ignored, so that my timeline isn't polluted with noise.
15. As a user, I want praise that was sent to my manager and forwarded to me to be found, so that thanks that didn't come to me directly still counts.

### What counts as a win

16. As a product manager, I want things I shipped to show up as wins, so that my launches and deliverables are on record.
17. As a user, I want praise I received to show up as wins, so that what others said about my work is on record.
18. As a user, I want the times I helped or unblocked someone to show up as wins, so that glue work isn't forgotten.
19. As a product manager, I want decisions I drove to show up as wins, so that alignment work that left no artifact is on record.
20. As a product manager, I want ambiguities I cleared to show up as wins, so that the times I turned a confused thread into a clear plan are on record.
21. As a salesperson, I want customer impact to show up as wins, so that saves, renewals and relationship work count, not only closed deals.
22. As a user, I want team wins I was part of to show up, so that shared launches count even when nobody singled me out.
23. As a user, I want implicit wins to show up, so that work I clearly drove counts even when no one said "thanks".
24. As a user, I want each win to say what I did specifically, so that a team win still describes my part.
25. As a user, I want a win to carry more than one win type when it fits, so that a shipped launch that was also praised shows both.

### The win card

26. As a user, I want each win to have a short, clear title, so that I can scan my year quickly.
27. As a user, I want each win to say in one line what I did, so that I remember my role.
28. As a user, I want each win to say in one line what the impact was, so that the outcome sits next to the activity.
29. As a user, I want each win to show its date span, so that I know when it happened and how long it took.
30. As a user, I want each win to list its citations, so that I can prove it.
31. As a user, I want each citation to open the original Slack message or email, so that I can check the context myself.
32. As a user, I want each citation to show who said it, when, and a short quote, so that I can judge it without opening every link.
33. As a user, I want each win labelled "Praised by name" or "Inferred from your messages", so that I know how strong the evidence is before I keep it.

### Deduplication and stories

34. As a user, I want a Slack thread and an email chain about the same objective to become one win, so that my timeline isn't cluttered with repeats.
35. As a user, I want all citations for one objective grouped under that one win, so that the evidence is in one place.
36. As a product manager, I want wins that build on earlier wins to be linked into a story, so that I can show I owned something end to end.
37. As a user, I want each story to have a name and a date span, so that I can talk about it as one arc.
38. As a user, I want to see a story's wins in order, so that I can follow how the work developed.
39. As a user, I want each win in a story to stay its own card, so that the individual moments aren't lost in the arc.

### Reviewing wins

40. As a user, I want to tick a win, so that it goes on my record.
41. As a user, I want to cross a win, so that wrong or unimportant finds are kept out of my record.
42. As a user, I want to change my mind and untick or uncross a win, so that a mistaken click isn't permanent.
43. As a user, I want to see which wins I haven't reviewed yet, so that I can work through them.
44. As a user, I want the timeline ordered by when each objective happened, so that my year reads in order.
45. As a user, I want wins I've ticked or crossed to keep their title, text and review state when new messages arrive, so that my reviewed record is stable.
46. As a user, I want a late thank-you about a win I've already reviewed to be added to that win as a new citation, so that the same objective never splits into two cards.

### Ongoing pickup

47. As a user, I want the agent to keep picking up new wins after the first run, so that my timeline is already full at my next review.
48. As a user, I want ongoing pickup to happen quietly without notifications, so that the product doesn't nag me.
49. As a user, I want new wins that continue an existing objective to join its story, so that the arc keeps growing on its own.

### Using wins with an AI assistant

50. As a user, I want to connect Claude (or another MCP-capable assistant) to my record, so that it can write review documents from my wins.
51. As a user, I want the assistant to see only my ticked wins, so that nothing I rejected or haven't reviewed leaves my record.
52. As a user, I want the assistant to see my stories as well as individual wins, so that it can write "led pricing from research to launch".
53. As a user, I want the assistant to receive each win's citations, so that what it writes is backed by evidence.
54. As a user, I want the assistant to filter my wins by date range and win type, so that I can ask for "praise I got in the second half of the year".
55. As a user, I want the assistant to fetch the details of one win or one story, so that it can quote the evidence precisely.

### Privacy and ownership

56. As a user, I want my record to be visible only to me, so that my employer and manager can't see it.
57. As a user, I want only ticked wins to ever leave my record, so that I control what is shared.
58. As a user, I want to delete everything (wins, stories, citations and stored messages) at any time, so that I can walk away cleanly.
59. As a user, I want to disconnect a source at any time, so that the agent stops reading it.
60. As a user, I want the privacy promise stated plainly in the product, so that I trust it with my DMs and private channels.

### Demo

61. As a hackathon judge, I want to see a full year of a realistic person's wins without connecting my own accounts, so that I can judge the product in a few minutes.
62. As a hackathon judge, I want to see a forgotten win surface with the thank-you message cited right there, so that the value is obvious at a glance.

## Implementation Decisions

### Constraints

- Only Meta models, through the Meta Model API (Muse Spark for all language work). No other model providers.
- Open source, as the hackathon requires.
- The demo runs on an open-source synthetic enterprise dataset where the same people appear in both Slack and email. Candidates: OrgForge (MIT, with a fixed event log as ground truth), EnterpriseRAG-Bench (Slack, Gmail and more), HERB (Slack, no email). Licence and content still to be verified before committing to one.

### Modules

1. **Source connectors.** One each for Gmail, Slack, and dataset import. Each one only converts its source into the common message shape and keeps a per-source sync position for ongoing pickup. No win logic lives here.
2. **Person identity.** Maps one person to their identities across sources (email addresses, Slack user ID, display names), so the engine can tell when a message is from, to, or about them. For the demo, it selects a dataset persona.
3. **Wins engine (seam 1).** The core. Takes the person's identity, a batch of messages, and the current record, and returns the updated record. Internally it filters noise, finds win signals, groups them by objective, attributes the person's role, assigns win types and the evidence label, writes the card text, and links stories. Its internal steps are free to change; its contract is the seam.
4. **Record store.** Holds wins, stories, citations, review states, the messages they cite, and sync positions. Supports delete-everything.
5. **Sync runner.** Runs the 12-month backfill on first connect, then picks up new messages continuously and feeds them to the wins engine in batches.
6. **Timeline app.** A web app. Shows connect screens, progress, the timeline, win cards, story views, and tick/cross.
7. **MCP server (seam 2).** Exposes the person's ticked wins and their stories to an AI assistant. Read-only.

### Common message shape

Every connector produces messages with: a stable ID, source (Gmail or Slack), conversation (email thread or Slack channel/DM and thread), author, recipients or participants, timestamp, text, and a permalink back to the original. Nothing downstream depends on which source a message came from.

### Record shape

- **Win:** ID, title, what you did (one line), impact (one line), win types (one or more of the six), date span, citations, evidence label, optional story, review state.
- **Citation:** the cited message's ID, source, author, timestamp, short quote, permalink.
- **Story:** ID, name, date span, ordered list of its wins.
- **Evidence label rule:** a win is "Praised by name" if at least one citation is someone else crediting the person explicitly; otherwise "Inferred from your messages".

### Wins engine rules

- Every citation must point to a message the engine was actually given. No invented evidence.
- Messages about the same objective, across sources and threads, produce one win.
- Team wins are included. Each card describes the person's own part.
- Implicit wins are included and labelled "Inferred from your messages".
- Wins that build on earlier wins join the same story. Each stays its own card.
- Late evidence about an existing objective attaches to that objective's win as a new citation, whether the win is reviewed or not. The same objective never becomes two cards.
- Ticked and crossed wins keep their title, text and review state. Late evidence only adds citations, and can upgrade the evidence label to "Praised by name" when it's explicit praise. Unreviewed wins may have their text updated as new evidence arrives.
- Work that builds on an objective, rather than more evidence about it, becomes a new win in the same story.
- Automated mail and notifications are filtered out before any language work.

### MCP contract

- List ticked wins, filterable by date range, win type and story.
- Get one ticked win with its citations.
- List stories and get one story with its ticked wins in order.
- Crossed and unreviewed wins are never returned by any tool, including inside stories.

## Testing Decisions

- **What a good test is:** it checks behaviour through one of the two seams, giving inputs and checking outputs. It never reaches into the engine's internal steps, so those can be reworked freely.
- **Seam 1, the wins engine.** Given a person and a set of messages (and optionally an existing record), check the record that comes back:
  - every citation refers to an input message
  - duplicate discussion across Slack and email yields one win
  - follow-on work joins the right story
  - team wins and implicit wins appear, with the correct evidence label
  - a second batch of messages adds or extends wins and stories, and leaves the title, text and review state of ticked and crossed wins unchanged
  - late evidence about an already-reviewed win is added to that win as a citation, not as a new card
  - automated mail produces no wins
- **Seam 2, the MCP server.** Given a record with ticked, crossed and unreviewed wins, every tool returns only ticked wins, including when listing a story that contains crossed or unreviewed ones.
- **Two kinds of test:**
  - **Fixed-output tests** replace the Meta model with a stand-in that returns predictable answers. These run fast and check the rules above.
  - **Quality checks** run the real Meta model on OrgForge data, whose event log is ground truth. They measure how many real wins are found (recall) and how many finds are real (precision), plus the share of found wins older than 90 days, which comes from the problem statement's success measures.
- **Connectors** get light tests with sample Gmail, Slack and dataset payloads, checking only that they produce the common message shape.
- **Prior art:** none. The repo is empty, so these tests set the pattern.

## Out of Scope

- Documents (written or reviewed), GitHub, and other sources beyond Gmail and Slack.
- Google Calendar, including spotting 1:1s and preparing for them.
- Any export: PDF, document or brag-doc file. The MCP connection replaces it in v1.
- Misses, hard moments and growth areas. v1 records wins only.
- Edit actions beyond tick and cross (editing wording, merging or splitting wins, renaming stories). Planned, not yet defined.
- A manager view, or any view for anyone other than the person.
- A phone notetaker or meeting capture.
- Notifications and weekly digests.

## Further Notes

- **Dataset choice deferred:** the candidate datasets haven't been opened yet. Check licence, how realistic the email is, and whether one persona has enough wins over a year before choosing.
- **Success measures** (from the problem statement): share of a year's wins a person can recall and back with evidence; share of evidence from before the last 90 days; hours spent preparing a self-review.
- **Access to real work accounts:** IT teams often block personal apps from connecting to work email and Slack. Accepted for the hackathon; the demo uses dataset data.
