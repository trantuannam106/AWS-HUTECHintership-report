---
title: "Week 10 Worklog"
date: 2026-06-22
weight: 10
chapter: false
pre: "  1.10.  "
---

### Week 10 Objectives:

In the InboxIQ team assignment, I am in charge of three areas often considered "secondary" but which determine the final product quality: documentation (the Hugo report the whole team will submit), testing (the first and most demanding user of every feature), and cost monitoring (ensuring the entire project stays within the Free Tier). This week, while the others built the system, I built what runs parallel to the system: a place to store every decision, every lesson, every number — so that come submission day, no one has to sit and try to remember "what did we do back then".

* Initialize the Hugo report repo with a workshop theme, a bilingual chapter structure, and image naming conventions.
* Draw the official 5-layer architecture diagram on draw.io based on the sketch from the team meeting, numbering each processing flow.
* Establish a recording process: all design decisions and incidents of team members are recorded during the week, preventing a backlog at the end of the term.
* Test the first backend part: Producer → SQS → Worker flow with dummy messages.
* Set up a routine for cost monitoring: Billing Dashboard, Free Tier estimation for each service finalized in the architecture.

---

### Tasks to be implemented this week:

Dưới đây là bảng đã được sửa lại lỗi ngắt dòng (bỏ các thẻ `<br>` thừa gây vỡ bảng) và viết đầy đủ tên các ngày trong tuần:

| Day | Task Category | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Team meeting to finalize architecture; take on documentation/testing/cost areas. <br> - Record meeting minutes: assignments, boundaries of responsibilities, "communication contracts" between parts (message format, endpoints) — the original document for any future debates. | 22/06/2026 | 22/06/2026 | Internal team |
| Tuesday | - Initialize Hugo repo with workshop theme: `content/` structure by chapters, bilingual support (`.vi.md`/`.en.md`), `static/images/` directory per convention. <br> - Test run `hugo server`, confirm correct rendering of shortcodes (`notice`, `children`). | 23/06/2026 | 23/06/2026 | [https://gohugo.io/documentation/](https://gohugo.io/documentation/) |
| Wednesday | - Draw the official architecture diagram on draw.io from the backend member's sketch: 5 layers, 14 numbered processing flows, legend categorizing stroke types (main flow, retry, optional, observability). <br> - Gather team feedback, revise 2 rounds before finalizing. | 24/06/2026 | 24/06/2026 | [https://app.diagrams.net](https://app.diagrams.net) |
| Thursday | - Outline the report chapters: introduction, architecture, deployment steps (placeholders for each area), testing, costs. <br> - Agree on conventions with the team: every technical incident must have "symptom → cause → solution → lesson" so I can rewrite it into documentation. | 25/06/2026 | 25/06/2026 | Internal team |
| Friday | - Create a Free Tier estimation table for each service in the architecture: Lambda (1 million requests/month), DynamoDB (25GB on-demand), SQS (1 million requests), API Gateway, Secrets Manager (charged per secret + calls). <br> - Identify "cost hotspots" to monitor in advance: OpenAI API calls (outside AWS), Secrets Manager API calls. | 26/06/2026 | 26/06/2026 | [https://aws.amazon.com/free/](https://aws.amazon.com/free/) |
| Saturday | - Conduct first backend testing with the backend member: send dummy messages to SQS, confirm the Worker receives and writes results to DynamoDB with the correct structure. <br> - Write the first test case as a manual checklist (not yet automated): steps, input data, expected results. | 27/06/2026 | 27/06/2026 | Project internal |
| Sunday | - Check Billing Dashboard at the end of the first week: confirm zero costs (all services within Free Tier). <br> - Write the weekly summary report and update documentation from the notes of the other 3 members. | 28/06/2026 | 28/06/2026 | InboxIQ project internal |
---

### Achieved Results for Week 10:

#### 1. Hugo Repo — the foundation of the final submitted product

The product the team submits is not code but a **process report** — so the Hugo repo is indeed the "main product" of the area I am in charge of. The structure was built properly from the start: chapters by `weight`, bilingual via `.vi.md`/`.en.md` suffixes, illustration images following the `/images/<chapter>/<section>/` directory convention so that later, whoever inserts images will do so consistently. The lesson learned right in the first week: setting up conventions early is much cheaper than cleaning up late — a messy documentation repo in the final week is a nightmare on par with messy code.

#### 2. Architecture Diagram — from sketch to "common language"

The paper sketch from the team meeting was converted into the official draw.io diagram: 5 layers (User, Auth, API, Compute, Async Workflow, Storage, Observability), 14 numbered processing flows, and a legend categorizing stroke types — solid line for main flow, red dashed line for retry, orange dashed line for optional, gray line for observability. The details seem formal but have a real effect: when the backend member explains the whoami flow or the Flutter member asks about the path of push results, the whole team points to the same number on the same diagram instead of describing it verbally in different ways.

One principle was finalized when drawing: the diagram only contains what belongs to the **application's runtime flow** — resources serving deployment (like the S3 bucket containing SAM artifacts) are not drawn, even though they physically exist in the account. The boundary between "application architecture" and "infrastructure tooling" is clearly noted to avoid revisiting the debate later.

#### 3. "Record in the week" convention — fighting against human memory

Lesson from previous academic projects: by the final week, no one can remember why we chose option A over B in the first week. The convention agreed upon by the whole team: every incident or design decision must be recorded using a 4-part framework (symptom → cause → solution → lesson) right in the week it occurs, even if just a few rough lines — I am responsible for editing them into complete documentation. This is why the troubleshooting sections in the final report have a high level of detail: they were written when the event was still fresh, not recalled from memory.

#### 4. Cost discipline from day one

The Free Tier estimation table was completed even before the system had real traffic, with two "hotspots" marked for special monitoring: OpenAI costs (outside AWS, with a separate dashboard) and Secrets Manager (charged per API call — which is exactly why the backend member caches secrets at the global scope). Checked Billing at the end of the week: costs are zero as expected. The routine of "checking Billing every Sunday" was established this week.

---

### Week 10 Results Evaluation:

* The documentation infrastructure (bilingual Hugo, image conventions, chapter outlines) is ready to receive content from all members.
* The official architecture diagram was approved by the whole team, becoming a common language during technical discussions.
* The 4-part incident recording convention was agreed upon — the most important investment for the quality of the final report.
* The backend flow with dummy messages was successfully tested; cost monitoring discipline became a routine.

---

### Difficulties Encountered:

* The Hugo workshop theme has many shortcodes and implicit conventions (`pre` structure, `weight`, children) that had to be figured out through examples because the official documentation is thin.
* Drawing a diagram for an unfinished system requires continuous updates as the design changes — one must accept that the diagram is a "living" document, not drawn once and done.
* Persuading members to record incidents during the week is not easy when everyone is caught up in their main tasks — I have to proactively "interview" each person at the end of the week instead of waiting for them to write it themselves.

---

### Solutions and Best Practices Derived:

* With documentation themes/frameworks that have thin docs, read the theme's source and sample sites directly instead of just looking for official documentation.
* Accept versioning for architecture diagrams: save each finalized version by milestone and date — this both reflects the design evolution process (a nice detail for the report) and avoids arguments about "which diagram is the newest".
* Proactively gather information from members on a fixed schedule (weekends) instead of waiting — the documentation role is proactive, not passively receiving submissions.

---

### Directions for Next Week:

* Test the OAuth flow and the complete pipeline with real emails once the security member finishes — playing the "first user" of the most important feature.
* Start writing the first in-depth documentation section: Gmail OAuth integration, based on the security member's incident notes.
* Closely monitor OpenAI costs as the system begins making real API calls.