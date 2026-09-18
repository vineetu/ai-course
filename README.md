# AI course

Materials for a hands-on AI workshop aimed at finance teams with no software background.
Everything here is static HTML with no build step and no dependencies.

The workshop moves people from conversational AI use (open a chat window, talk through a
problem) to agentic workflows (give a goal plus files, get a finished artifact back). It is
built for an audience whose data lives in spreadsheets, purchased reports, and PDFs rather
than in a warehouse, so every exercise is file in, artifact out.

## What is in here

| Path | What it is |
|---|---|
| `survey/index.html` | Pre-workshop survey covering the tools people already use and their operating system, plus a question on MCP familiarity. Saves to a hosted JSON collection. |
| `survey/results.html` | Viewer for the survey responses, newest first. |
| `workflows/revenue-concentration.html` | Explainer: what revenue concentration analysis is, and how it looks as an agentic workflow. |
| `workflows/ma-evaluation.html` | Explainer for M&A valuation and the news sentiment layer that sits on top of it. |

Live copies:

- https://sites.simple-host.app/vineetu/ai-workshop-survey/
- https://sites.simple-host.app/vineetu/revenue-concentration/
- https://sites.simple-host.app/vineetu/ma-evaluation/

Each explainer page links to the other with a sibling-site path (`../ma-evaluation/`), which
resolves once each page is deployed as its own site. Opening them straight from disk leaves
those two links dead. Everything else on the pages still works.

## Run of show

Two hours is the complete unit. The third hour is the org-level payoff, not overflow.

| Time | Block |
|---|---|
| 0:00–0:15 | Framing. Chat versus agent, permission modes, planning until aligned, and voice input |
| 0:15–0:30 | One live demo of the full arc, files in to cited artifact out |
| 0:30–0:40 | Setup shakeout: everyone opens their tool and loads their own file |
| 0:40–1:40 | Lab: your file, your recurring question. Checkpoint at the halfway mark |
| 1:40–1:55 | Make it reusable: save the work as a re-runnable skill, then re-run it live |
| 1:55–2:00 | Close: what to do on Monday, office hours date |

The third hour opens with a ten minute break. Forty minutes then go to packaging the
analysis as a skill and publishing it as a page that refreshes on a cadence, and the last
ten minutes to share-outs from two or three volunteers.

At two hours each person leaves with a personal workflow. At three hours the team leaves
with shared artifacts, which is usually the reason the session was requested in the first
place.

## Points worth keeping

- **Cloud chat cannot reach local files.** A browser chat window and a cloud "work" mode
  have no access to what is on the laptop or behind the firewall. Agentic work needs a tool
  that runs locally, such as Codex, Claude Code, or Cursor.
- **Approve-per-step wastes the session.** Start attendees on the batch approval mode.
  Full access is for people who already know what they are approving and have guardrails.
- **Plan before executing.** Models are eager and fill gaps with assumptions. Iterate on the
  plan until it matches intent, and let the human decide when that point is reached. An
  agent claiming alignment is not evidence of alignment.
- **Voice input is a real unlock.** Dictating a paragraph of context beats typing a sentence
  of it, and context is what separates a useful run from a wasted one.
- **Security posture limits autonomy, not agency.** A supervised session where a person
  watches the work and approves the steps fits inside most corporate rules, and it is the
  right level for a first session anyway.

## Before the workshop

1. Send the survey about two weeks out. It establishes the tooling split, the Mac and
   Windows split, and who has used a terminal.
2. Send an install guide per operating system. Anyone with nothing installed needs at
   minimum a desktop AI app.
3. Set up MCP connections (Jira, Confluence, Slack, GitHub) ahead of the session rather
   than during it. Offer a short drop-in clinic for anyone stuck; OAuth and SSO prompts
   across eighteen laptops will eat a lab otherwise.
4. Ask each attendee to bring one file they work with regularly and one question they
   answer repeatedly. Keep a sanitized sample file ready for whoever forgets.
5. Seat people in pairs, so a broken setup means sharing a screen rather than dropping out.

## Deploying

The pages are plain static files and can be hosted anywhere. The live copies run on
simple-host, one site per page, uploaded as inline JSON:

```
POST /v1/sites/<sitename>/files
X-API-Key: <key>
{"files": {"index.html": "..."}}
```

The survey writes to a per-site JSON collection from the page itself, with no key in the
page. Responses are readable by anyone with the link, which is stated on the form.
