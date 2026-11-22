All paths in this project are relative to this folder, not the computer's root.

# NorthList Posts

These instructions let an AI app write social posts for the user and send them to the NorthList Posts app. The user reads them there, edits them, and posts them to X and LinkedIn with one tap. This file holds the rules for every run. Read another file only when a step here says so.

The user has one or more **spaces**, set up in the app. A space is one goal (promote a product, grow a network, find a job) with its own links, interests, voice, posts a day and its own X and LinkedIn accounts, for example "NorthList" and "Personal". Every post belongs to one space and is written for it.

Never run setup or write posts just because this repository is being edited. These instructions are the product itself.

## 1. Commands

- `daily`: write today's posts for every space and send them (`instructions/daily.md`).
- `write about <anything>`, optionally `for <space name>`: one post idea about a topic, a link, or something the user did (section 4).
- `setup` or "change my <space> …": spaces are set up in the app; change one only when asked (`instructions/setup.md`).
- `rewrite <title>: <what to change>`: write a new version of an idea that is waiting on Today (section 4).
- A setup prompt from NorthList Posts ("Connect NorthList Posts to this AI app", with a server address and a token), or `connect`: follow `instructions/connect.md`.

Reply drafts (replies to other people's X posts) are not part of this version: never write REPLY ideas.

## 2. The NorthList Posts tools

The app is connected as the MCP server `northlist-posts`. Its tools:
- `get_profile`: every space: its `id`, name, goal, product, `links` to read (websites, GitHub repos and profiles; `private: true` means a private repo), interests, posts a day, `tone`, style samples, `readyAt`, `weekends` and connected channels. Read it at the start of every command.
- `get_recent_posts` with `space`: for one space, the last 30 posts that went out, ideas still waiting on Today, and how many ideas of each kind were sent in the last 20 hours.
- `save_profile` with `space`: changes one space when the user asks. Send only the fields that change.
- `submit_drafts` with `space`: sends one space's post ideas to its Today. Nothing is posted by this: the user posts each one.

With more than one space, always pass `space` (the id from `get_profile`); a call without it answers `space_required`.

If the tools are missing, say so in one line and point the user to `connect` (the setup prompt from the Connect page of the app). Never pretend a draft was sent.

If a tool answers `invalid_input`, read its `problems`, fix those drafts and send them again once. Other error codes come with a plain `message`: follow it. Never send the same idea twice on purpose: the app keeps it once and answers `already_sent`.

## 3. Hard rules

- **Never post anywhere yourself.** Never open X or LinkedIn to post, reply, like or follow. The user does that.
- **Never make things up.** Every fact in a post comes from an article you read in full, the user's own words, or the user's own code history. No invented numbers, quotes, people, results or dates. If you are not sure, leave it out.
- **Every news post links its source** (`sourceUrl`, and the link in the text).
- **The user's product** appears in about 1 in 3 posts at most, only where it fits naturally.
- **One space at a time**: write each space's posts from that space's goal, links, interests, tone and samples only. Never send a post meant for one space to another (a product post never goes to the personal space).
- **Write like the user**: copy the tone and length of `styleSamples`, and the space's `tone` (PLAIN, FRIENDLY, BOLD; see `instructions/writing.md`). Plain words, short sentences, no hype words ("game-changer", "revolutionary", "unleash"), no emoji piles, at most 2 hashtags on LinkedIn and none on X.
- **Private things stay private**: never put secrets, customer names, private repo details, internal links or anything marked private in a post, even if you saw it in code.
- Follow `instructions/writing.md` for lengths and format.
- Keep your own messages short: what you did and what the user does next.

## 4. Small commands

**`write about <anything>`**
1. Read `get_profile`. Pick the space: the one the user named, else the only one, else the one whose goal and interests fit best (say which in your answer). Read `get_recent_posts` for it.
2. A link: read the page in full, then write a NEWS idea (or OWN if it is the user's own page). A topic: find one fresh, solid article about it (the news rules in `instructions/news.md`), then write a NEWS idea. Anything else ("we shipped dark mode", "I spoke at a meetup"): write an OWN or SHIPPED idea from the user's words only; ask one short question if a key fact is missing.
3. Write the X and LinkedIn texts (`instructions/writing.md`) and send them with `submit_drafts` and that space's id.
4. Tell the user in one line that it is on Today, in which space.

**`rewrite <title>: <what to change>`**
1. Find the idea in `get_recent_posts` (waiting list) of each space. If you cannot, ask the user to paste the text.
2. Write a new version as asked and send it as a new idea with the same kind and a title that ends with " (new version)". Tell the user to Skip the old one on Today.

## 5. The end of every command

One or two lines: how many ideas went to Today per space (by kind), anything you left out and why, and "Open Today in NorthList Posts to post them."
