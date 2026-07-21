# Working conventions for this repo — Drishti 2.0 Designs

Read this before touching files here. This file exists so any Claude
Cowork / Claude Code session in this repo behaves consistently, no matter
who's driving.

## What this repo is

Iterations of Drishti 2.0 HTML designs. `main` is the reviewed, approved
state. It does not move except through a merged, reviewed Pull Request —
including for the repo owner (@abhiramrajilan).

## Folder structure

    designs/<project-or-screen>/...

Organize by what's being designed (e.g. `designs/dashboard/`,
`designs/onboarding/`), not by who's designing it. Authorship already
lives in git history and branch names.

Starting a brand-new flow/project: there's no separate step to "create a
folder" — git has no concept of an empty folder. Just add your first
file at `designs/<new-flow-name>/whatever.html` on your branch, commit,
and push. The folder exists the moment the file does. Pick a clear,
lowercase-hyphenated name; if it might overlap with someone else's area,
a quick heads-up before you start avoids duplicate structure — that's a
courtesy, not something the tooling enforces.

## Iterations within a flow

Designs iterate as **separate, versioned HTML files that all live side by
side** in the flow folder — this is deliberate, so anyone can open any two
versions in a browser and compare renders without a git checkout.

Convention:

    designs/<flow>/<flow>-v<N>.html      # e.g. scrutiny-review-v10.html
    designs/<flow>/CHANGELOG.md           # what changed, which is current

- **Highest version number = the current design.** No `latest.html`, no
  moving files into archives — you just save the next `-v<N>.html`.
- Each flow folder has a **`CHANGELOG.md`** listing every version with a
  one-line "what changed". Update it in the same commit as a new version.
- Version numbers may skip (a `v5` gap is fine) — note intentional skips in
  the CHANGELOG so they don't read as a lost file.
- Keep each iteration self-contained (embed assets) so a single `.html`
  opens correctly on its own.

### Large demo files

Self-contained "demo master" HTMLs can be 10–12 MB (embedded assets). A few
are fine in plain git. If a flow starts accumulating *many* large-file
iterations, raise it — we'll move those to Git LFS rather than let the repo
balloon. Small iteration files (tens to a few hundred KB) never need this.

## Branch naming

    <github-username>/<short-description>

Example: `abhiram/dashboard-nav-redesign`. Always branch off the latest
`main`. Never commit directly to `main`.

## The "push to GitHub" convention

When someone says "push to GitHub" (or "push to git"/"push to get" —
treat the same), do this:

1. `git add` the files they've been working on.
2. `git commit` with a short, specific, present-tense message describing
   the actual change. Each commit is a logged design iteration.
3. `git push origin <their-branch>` (create the branch first if new,
   based on their GitHub username).

Never push to `main`. Never open a PR automatically — only when asked
explicitly ("open a PR", "send this for review").

## Requesting review / merging

- Trusted team members (repo collaborators): push your branch, then
  `gh pr create --base main --head <your-branch>`. @abhiramrajilan
  reviews and merges — see CODEOWNERS, which auto-requests that review.
- Community / open-source contributors: fork this repo, branch on your
  fork, push there, open a PR from your fork into this repo's `main`.
  No collaborator access needed.

`main` is protected: PRs require review and approval before merging.

## Commit message convention

Short, specific, imperative. Good: "Rework settings screen empty state
for v2 nav". Bad: "updates", "wip", "fixes".
