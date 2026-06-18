# CodeCrunch Labs — Team Playbook

How we use the **Project board**, **Issues**, and **Milestones** on GitHub.

---

## TL;DR — the three tools, one sentence each

- **Issue** = one unit of work (a bug, a feature, a chore). If we're going to do it, it's an Issue.
- **Milestone** = one **sprint** (a 2-week chunk of time) or a **release**. It answers *"when."*
- **Project board** = the single live view of all work across every repo. It answers *"what's the status."*

> Rule of thumb: **Issues are the work, Milestones are the calendar, the Project is the dashboard.**

---

## Why we're changing a few things

Quick audit of where we are today (June 2026):

- There is **no Project board** anywhere yet (org, user, or repo). We're creating one.
- **Milestones are being used as per-person buckets** ("Jaed Backlog", "Santiago Backlog"). We're switching milestones to mean **sprints**, and tracking *who* via **assignees** instead.
- We're only using GitHub's **default labels**. We're adding a small, shared scheme (priority / size / type / product).
- Some issues in codecrunchworldwide are actually **image uploads**, not tasks. Those stay out of the board (see "Issues" below).

---

## 1) The Team Project (board)

We run **one org-level Project** called **"CodeCrunch Labs — Delivery"** that pulls Issues and PRs from all product repos. One place to see everything.

### How to create it (Scrum Master, one-time)
1. Go to `github.com/orgs/CODECRUNCHLABS` → **Projects** → **New project** → start from **Board**.
2. Name it **CodeCrunch Labs — Delivery**.
3. Add the repos: open the Project → `…` menu → **Settings** → **Manage access**, and in each repo (`PSJDoughDrop`, `codecrunchworldwide-development`, `pablosdelivery`) you can also use **Add item** to link issues.

### The board columns (Status field)
We use a simple flow. Every item lives in exactly one column:

| Status | Meaning |
|---|---|
| **Backlog** | Captured, not yet planned into a sprint |
| **Ready** | Meets *Definition of Ready* — scoped, estimated, pickable |
| **In Progress** | Someone is actively working it (must have an assignee) |
| **In Review** | PR open, waiting on review |
| **Done** | Merged / shipped, meets *Definition of Done* |

### Custom fields to add (Project → Settings → + Field)
- **Product** — single-select: `PSJ DoughDrop`, `HackU Worldwide`, `Pablos`. (Lets us filter one product out of the shared board.)
- **Priority** — single-select: `P0 urgent`, `P1 high`, `P2 normal`, `P3 low`.
- **Size** — single-select: `S`, `M`, `L` (or story points `1/2/3/5/8` if we prefer).
- **Sprint** — use the built-in **Iteration** field set to **2-week** iterations. This is how the board knows which sprint an item is in.

### Views to save (tabs at the top of the Project)
- **Board** grouped by *Status* — the daily working view.
- **This sprint** — a Board filtered to the current Iteration.
- **By product** — a Table grouped by *Product* (for per-product standups).
- **Roadmap** — timeline view by Milestone/Iteration for planning ahead.

### Automate it (Project → Workflows)
Turn on the built-ins so we don't move cards by hand:
- Item **added** → set Status **Backlog**.
- Issue/PR **closed** → set Status **Done**.
- PR **opened/ready for review** → set Status **In Review**.

---

## 2) Issues

**An Issue = one piece of work we intend to do.** If it's not worth an Issue, it's not on the board.

### Writing a good Issue
**Title:** short and specific — `fix: certificate page returns "no record" on codecrunchglobal.com`, not `bug`.

**Body template** (we'll add these as Issue Templates in `.github/ISSUE_TEMPLATE/`):

```
## What
One or two sentences on the problem or feature.

## Why
The user/business reason.

## Acceptance criteria
- [ ] Specific, checkable outcome 1
- [ ] Specific, checkable outcome 2

## Notes / links
Screenshots, repro steps, related issues (#123), docs.
```

### Every Issue that goes on the board gets:
- **Assignee** — exactly one owner (more is fine, but one is accountable).
- **Labels** — `type:` + `priority:` (+ `product:` if the repo holds more than one).
- **Project** — add it to *CodeCrunch Labs — Delivery* (set Product, Priority, Size, Sprint there).
- **Milestone** — the sprint it's committed to (only once it's `Ready`/`In Progress`).

### Labels (shared across all repos)
| Group | Labels |
|---|---|
| **type** | `type:bug` · `type:feature` · `type:chore` · `type:docs` |
| **priority** | `priority:P0` · `priority:P1` · `priority:P2` · `priority:P3` |
| **size** | `size:S` · `size:M` · `size:L` |
| **status helpers** | `blocked` · `needs-info` · `good first issue` |

### Linking work
- In a PR description write `Closes #42` so merging the PR auto-closes the Issue and moves the card to **Done**.
- Use **sub-issues** (the "Create sub-issue" button) to break a big Issue into a checklist of smaller ones.
- Branch naming: `type/short-slug` → `fix/cert-referer-allowlist`, `feat/cart-checkout`.

### Not every Issue is a task
In codecrunchworldwide we've used Issues to **host images** (`panelimage01`, `pic-bryan`). That's fine as a trick, but those are **not work** — label them `asset` (or keep them out of the Project) so they never show up on the board or in sprint counts.

---

## 3) Milestones

**A Milestone = a sprint or a release.** Not a person, not a backlog.

### Our convention
- One Milestone per **sprint**, named by date so it sorts: **`Sprint 01 — Jun 23 to Jul 4`**.
- Give it a **due date** = the last day of the sprint. GitHub then shows a live **% complete** bar as issues close.
- Optionally, named **release** milestones for big targets: `PSJ DoughDrop — MVP`, `Pablos — Sprint 0`.

### How we use them
- During **sprint planning** we drag `Ready` issues into the upcoming sprint Milestone (and the Project's Iteration field).
- An Issue **with no Milestone** = not committed to any sprint yet (it lives in Backlog).
- At sprint end, anything unfinished is explicitly **moved to the next Milestone** or **back to Backlog** — never left silently.

### Migrating today's milestones
The current `Jaed Backlog` / `Santiago Backlog` milestones get retired. Their issues:
1. Get an **assignee** (the person it was "named" after).
2. Move to a real **Sprint** milestone (or Backlog if not yet planned).

---

## 4) The weekly rhythm (Scrum on GitHub)

Sprints are **2 weeks**. The org promise is **a demo every Friday** — so we review weekly and close the sprint every other Friday.

| Ceremony | When | Where it happens |
|---|---|---|
| **Backlog refinement** | Mid-sprint, ~30 min | Groom `Backlog` → add detail, labels, size; promote to `Ready` |
| **Sprint planning** | Start of sprint | Pull `Ready` items into the new **Sprint Milestone** + Iteration; assign owners |
| **Daily check-in** | Async, daily | Update card **Status** + drop a line in the Discord channel; flag `blocked` |
| **Sprint review / demo** | **Friday** | Show working software; move shipped items to **Done** |
| **Retro** | End of sprint | What went well / what to change → 1-2 action items as Issues |

**Definition of Ready** (before an Issue can be pulled into a sprint): has a clear title, acceptance criteria, a size, and no unanswered blocking question.

**Definition of Done** (before an Issue is closed): acceptance criteria checked, PR merged to `main`, no broken links/build, and (where relevant) deployed and verified.

---

## 5) Quick-start checklist (Scrum Master)

- [ ] Create org Project **CodeCrunch Labs — Delivery** (Board) and add the 3 repos.
- [ ] Add fields: Product, Priority, Size, Sprint (Iteration, 2-week).
- [ ] Turn on the auto-workflows (added→Backlog, closed→Done, PR→In Review).
- [ ] Create the shared **labels** in each repo.
- [ ] Retire `Jaed Backlog` / `Santiago Backlog`; create **`Sprint 01 — <dates>`** with a due date.
- [ ] Add Issue Templates to each repo's `.github/ISSUE_TEMPLATE/`.
- [ ] Move existing open issues onto the board with assignee + labels.
- [ ] Run the first **sprint planning**; book the recurring **Friday demo**.

---

## 6) One-line cheat sheet for the team

> Find your work on the **board** → it's an **Issue** with your name on it → it belongs to a **Milestone (this sprint)** → move your card **In Progress → In Review → Done** as you go, and open a PR that says **`Closes #yourissue`**.
