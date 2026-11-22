# What you shipped

Read this file from `daily` when a space has GitHub links or a changelog page. It finds a change worth a post in the user's own work. Nothing has to be on this computer: the links say where to look.

## 1. Read what changed

Look only at the space's own `links`, since the newest SHIPPED idea in `get_recent_posts`, whether it was posted (`postedAt`) or is still waiting (`sentAt`); with none, the last 7 days. Never pick a change that a posted or waiting SHIPPED idea already covers.

**A public GitHub repo** (`kind: GITHUB_REPO`, not private): read its merged pull requests and releases on the web:
- `https://github.com/<owner>/<repo>/pulls?q=is%3Apr+is%3Amerged+sort%3Aupdated-desc` (titles and dates), then open the one or two that look best and read their description.
- `https://github.com/<owner>/<repo>/releases` for release notes.
- If you have the GitHub CLI (`gh`), `gh pr list --repo <owner>/<repo> --state merged --limit 20 --json number,title,mergedAt,body` gives the same faster.

**A private repo** (`private: true`): read it with your own GitHub access, the same way you read the user's code. In order, use what works:
1. The GitHub CLI if it is signed in: the `gh pr list` command above.
2. A GitHub connector or tool your app already has.
3. A copy of the repo on this computer: `git -C <folder> log --since="<date>" --merges --first-parent --pretty=format:"%h %ad %s%n    %b" --date=short -n 40`.
If none works, skip the repo and say once at the end why, in the words that fit:
- not signed in: "I could not read <repo>: sign in to GitHub in this app (for example `gh auth login`) and I will read it next time."
- signed in, but GitHub says the repo is not found: "I could not read <repo> with the GitHub account this app uses (<account>): check the link on the Space page, or give that account access."
Never ask the user for a GitHub key, and never paste one anywhere.

**A GitHub profile** (`kind: GITHUB_PROFILE`): look at the user's public repos with recent pushes (`https://github.com/<user>?tab=repositories&sort=updated`) and read the newest one or two like a public repo.

**A changelog or blog page** (a PAGE or WEBSITE link whose page lists changes): read the newest entries, with their dates.

Read only what you need. If a title alone does not say what the change does for people, read the pull request text, the release note or the README. Write only what those show; if the meaning is still a guess, pick another change. Never copy secrets, `.env` files, keys, customer data or internal links, and never put code in a post.

## 2. Pick one change

A good shipped post is about something a user can see or feel: a new feature, a clear speed-up, a fixed annoyance, a design change, a lesson learned the hard way. Skip chores (dependency bumps, formatting, tests only, refactors with no visible change) unless the lesson is interesting on its own.

Pick the one change people would care about most. If two are close, prefer the newer one. If nothing is worth a post, say so and give the slot to NEWS.

## 3. What you may say

- What changed, in the space's product words, and why it helps the people who use it.
- A short story or lesson if the pull requests or commits show it (for example "took three tries").
- Nothing private: for a private repo, no repo or owner names (say the product's name instead), no branch names, no file paths, no code, no customer names, no numbers you cannot see.
- "Why it helps" is your plain reading of the change for the people who use it. Keep it modest and true to what the change does; never claim results (more sign-ups, faster by 40%) that you cannot see.
- If the space has a product link, you may link it. Otherwise no link.

Set `kind` to SHIPPED, the `title` to the change in a few words, and `why` to one line, for example "a visible change people can try".
