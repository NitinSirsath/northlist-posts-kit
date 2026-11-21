# Setup

Read this file for `setup`, or right after connecting when the setup prompt asks for it. The answers go to the app with `save_profile`; nothing is saved in this folder.

## 1. Start from what is there

Call `get_profile`. If fields are already filled, show them in a few short lines and ask only about what is empty or what the user wants to change. Never ask again for what is already there.

## 2. The questions

Ask them in this order, a few at a time, in plain words. Offer a sensible default for each, so the user can just say "yes".

1. **Goal**: promote your product, grow your network, or find a job? (`goal`: PROMOTE, NETWORK, JOB)
2. **Your product** (skip if the goal is not PROMOTE and the user has none): its name, its link, and one line on what it does. (`productName`, `productUrl`, `productLine`)
3. **Interests**: up to 8 topics to find news about, for example "React", "AI coding tools", "Job search". (`interests`)
4. **What you ship**: which project folders or repos on this computer should be read for "what I shipped" posts? Names or paths, up to 8. Say that only the code history is read (commit messages and changed file names), never secrets, and that private details never go into a post. They can say none. (`shippedFrom`)
5. **How much each day**: posts a day (default 3). (`postsPerDay`)
6. **Channels**: X, LinkedIn, or both (default both). (`useX`, `useLinkedIn`)
7. **Your style**: paste 2 or 3 posts you wrote before and liked. If they have none, offer to skip; drafts will then use plain, short sentences. (`styleSamples`)

Check what you can: a product link must start with `https://` or `http://`; folders in `shippedFrom` should exist on this computer (say so if one does not, and ask). Keep each answer short.

## 3. Save and confirm

1. Call `save_profile` with the fields from this conversation only.
2. If it answers `invalid_input`, fix the named fields with the user and save again.
3. Tell the user in two or three lines: what was saved, that it can be changed on the Profile page of the app, and to type `daily` to get today's posts. Ask once whether to run `daily` now.
