# What you shipped

Read this file from `daily` when the profile has `shippedFrom`. It finds a change worth a post in the user's own code history. It only works in an AI app that can read folders on this computer.

## 1. Read the history

For each folder in `shippedFrom` (a path, or a project name you can find under the user's usual code folders; ask once if you cannot find it):
1. Check it is a git repository. Skip it quietly if not.
2. Read the history since the last SHIPPED post in `get_recent_posts` (or the last 7 days if none). Start with the merges on the main branch, because a merged pull request's title says what changed in words:
   `git -C <folder> log --since="<date>" --merges --first-parent --pretty=format:"%h %ad %s%n    %b" --date=short -n 40`
   The pull request title is usually the first line of the body (`%b`). If there are no merges, read the plain commits instead:
   `git -C <folder> log --since="<date>" --no-merges --pretty=format:"%h %ad %s" --date=short -n 60`
3. For the one or two changes that look best, look at the changed file names to understand them:
   `git -C <folder> show --stat --pretty=format:"%s" <hash>`
   For a merge, use `<hash>^1..<hash>` with `git log --stat --no-merges` to see its commits.
4. If the history does not say what the change does for people (commit messages that are only file names, for example), you may read the pull request text, a changelog, the README or a docs page in that folder, and the names of the screens that changed. Write only what those show; if the meaning is still a guess, pick another change.
5. Read only what you need. Never print or copy secrets, `.env` files, keys, customer data or internal links, and never put code in a post.

## 2. Pick one change

A good shipped post is about something a user can see or feel: a new feature, a clear speed-up, a fixed annoyance, a design change, a lesson learned the hard way. Skip chores (dependency bumps, formatting, tests only, refactors with no visible change) unless the lesson is interesting on its own.

Pick the one change people would care about most. If two are close, prefer the newer one. If nothing is worth a post, say so and give the slot to NEWS.

## 3. What you may say

- What changed, in the user's own product words, and why it helps the people who use it.
- A short story or lesson if the commit messages show it (for example "took three tries").
- Nothing private: no repo or owner names (say the product's name instead), no branch names, no file paths, no code, no customer names, no numbers you cannot see in the history.
- "Why it helps" is your plain reading of the change for the people who use it. Keep it modest and true to what the change does; never claim results (more sign-ups, faster by 40%) that the history does not show.
- If the product is public (`productUrl`), you may link it. Otherwise no link.

Set `kind` to SHIPPED, the `title` to the change in a few words, and `why` to one line, for example "a visible change people can try".
