# RBC Lighthouse

**A lighthouse does not chase ships and it does not report on them. It stands where it is, it is visible from everywhere, and it shows you the rocks before you hit them.**

RBC Lighthouse is a centralised hub for early talent, built into the RBC HR portal that co-ops and new grads already use. It captures their voice continuously, surfaces what the program needs to fix, and flags the students at risk of leaving while there is still time to do something about it.

Built for the Tech@RBC Women's Advisory Program hackathon, November 2026.

**Live demo:** https://chhayaprdn.github.io/RBC-Hackathon/

---

## The problem

RBC already asks early talent how it is going. There are onboarding programs, mentorship for co-ops and new grads, workshops, RBC Connect, midterm and endterm surveys, and attendance numbers for everything.

The gap is not the asking. It is **when** the asking happens and **how honest** the answer is.

- Feedback arrives on RBC's calendar, not the student's. A co-op has a bad three weeks in June and says so in the August endterm survey, after they have already accepted something else.
- Surveys are not anonymous, so the answers are biased.
- The signals that matter are scattered across RBC Connect, Webex, the HR portal and performance conversations, with no single place to see them.
- Problems usually surface in a performance conversation, which is far too late.

## Where it lives

**Lighthouse is not another application to adopt.** It is a tile inside the RBC HR portal, under Early Talent, behind the same single sign-on. No second login, no second place to look, and nothing for a student to discover and then forget about.

That matters for three reasons:

- **The data is already there.** Role, team, term dates and access requests are read from the portal record on day one, so nothing is typed twice and the onboarding checklist can tick itself.
- **Adoption is not a campaign.** Students already open the portal for pay, benefits and time off. Lighthouse is where they already are, not somewhere new they have to be sold on.
- **Mentors need nothing at all.** Every mentor interaction happens by email, so a director with one mentee never logs into anything.

Practically, "integrated into the HR portal" means single sign-on, a tile surfaced in the portal, and reading and writing through the portal's APIs. It does not mean custom code inside a vendor platform.

Everything else a student needs is linked from the one place: RBC Connect for events, Webex for mentor meetings, TIA for policy and IT questions, and the team's own tooling and runbooks. That is the hub.

## What we built

Two views on the same data.

### The harbour (student)

You arrive on a ship and come ashore into a harbour where every building is something you need. Nothing is sequenced and nothing is locked behind anything else, because real onboarding is not linear. You need Mentor Hall in week 2 and in week 14, and you need the Resource Library the moment something breaks.

| Building | What it does |
|---|---|
| **Welcome Centre** (the ship) | Your intake profile, your team, your pod, and why you were matched with your mentor |
| **Onboarding Checklist** | 12 items in three groups. Six tick themselves from the HR portal, GitHub and Slack |
| **Mentor Hall** | Your mentor and buddy, your goals, your meeting history, and the overdue meeting |
| **Check-in Station** | The main feature. Three separate things a student can send, below |
| **Connect Plaza** | Events from RBC Connect, with the points you earn for attending |
| **TIA Tower** | Opens RBC's existing assistant. We route to it, we do not rebuild it |
| **Resource Library** | Every tool and link in one list, including what RBC Connect and Webex are for |
| **Wrapped Arena** | Your month at RBC as a highlight reel, shareable with your mentor |

Buildings you never open are themselves a signal. The Resource Library reads "Not opened yet" for a reason.

### The Check-in Station, three types

1. **Weekly check-in.** Opens Friday 09:00, closes Monday 17:00, with a live countdown. Three taps, about 20 seconds. Miss the window and the streak resets, which is what makes the streak mean something.
2. **General feedback.** Any time, as often as you like, does not affect the streak. Pick a category and optionally **send it anonymously**.
3. **Support request.** Pick a category and an urgency, and the request comes back with a **named owner and a response time**, not a ticket number. If nobody replies, Lighthouse chases and then escalates.

### The Program tab (Early Talent manager)

- **Cohort KPIs:** health, check-in completion, flags actioned within 5 days, path visibility
- **Engagement signals** with cohort medians, and a **See who** button on every row that names the students outside the median and lets you email each one's mentor, or all of them at once
- **Flags**, each with evidence, a named owner, an action and a due date. The low-activity flag lists the affected students inline with a per-student ping to their own mentor
- **Mentor pool** with an approval queue for volunteers
- **Themes** grouped from feedback and repeated questions, each with a proposed fix and a status
- **Events** from RBC Connect, scored on a follow-up rating sent two weeks later rather than on attendance
- **Cohort settings**, including an on/off switch for onboarding points

## What is actually new here

1. **Signal over survey.** Most of the risk indicators need nobody to fill anything in. They come from systems the cohort already uses: RBC Connect attendance, Webex and calendar gaps, checklist stalls, repeated questions. Zero added burden, and it works on the students who have stopped answering surveys, which is exactly the at-risk group.

2. **Comments group at three.** A comment reaches a manager only once three or more people in the cohort say something similar. Below that it goes to the program team with the name removed. This is a mechanism, not a promise, and it is a direct answer to "our surveys are biased because they are not anonymous."

3. **Mentors never log in.** After a Webex meeting, Lighthouse emails the mentor the transcript summary. They reply to that email to confirm or correct it, and the summary plus any new goals land in the student's Mentor Hall. The student takes no notes. The mentor adopts no new tool. Low-engagement alerts and meeting requests work the same way.

4. **Wrapped is what the mentor sees.** Every tool like this gives managers problems. Lighthouse also gives them something good to say in a 1:1, built from work the student actually did. Achievements and engagement are shared. Check-in answers never are.

## Privacy

- Metadata only. Counts, dates and attendance. No message content and no meeting recordings.
- Students can open everything Lighthouse holds about them.
- Comments group at three before any manager sees them.
- Lighthouse data is walled off from the rest of the HR portal and is not used in performance reviews or return-offer decisions. This is written into the pilot terms.

## Integrations

All read-only except for calendar invites and outbound email. No new vendor and no new licence.

| System | Used for |
|---|---|
| HR portal | **Host.** Single sign-on, intake profile, access requests, auto-ticked checklist items |
| RBC Connect | Event listings, registration, attendance, points |
| Webex | Mentor meetings, transcript summaries |
| Outlook | Meeting gaps, booking |
| TIA | Linked out to for HR, policy and IT questions |
| Corporate GitHub / Helios | Optional, first merge and delivery signals |
| Email | Every mentor interaction |

## Implementation

Phased so that phase 1 ships without waiting on any approvals.

- **Phase 1:** the harbour, the three check-in types, the resource library and the mentor emails, surfaced as a portal tile behind existing SSO. No new data flows, therefore no privacy review blocking it.
- **Phase 2:** RBC Connect and Webex.
- **Phase 3:** GitHub, Jira and the rest of the passive signals.

**Pilot:** one cohort in one business unit, 8 to 12 weeks, one small squad. Measured on feedback latency, flags actioned within 5 days, path visibility and regretted attrition against last year's cohort.

The long pole is privacy and access approval, not engineering.

## Running it

It is one self-contained HTML file with no build step and no dependencies.

```bash
git clone https://github.com/chhayaprdn/RBC-Hackathon.git
cd RBC-Hackathon
open index.html
```

Or serve it:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## A note on the data

**This is a hackathon prototype, not an RBC system.** Every student, mentor, number, event and flag in it is invented for the demo. No real RBC data, no real people, and no connection to any RBC system. The integrations listed above describe what a real build would connect to, not what this prototype does.

## Team 10

Tech@RBC Women's Advisory Program hackathon, November 2026.
