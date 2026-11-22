# NorthList Posts kit

Instructions that let your AI app write social posts for you and send them to [NorthList Posts](https://posts.northlist.site). You read them there, edit them, and post them to X and LinkedIn with one tap. Nothing is posted without you.

Your AI does the work with its own web search and your own AI plan. The app only shows the drafts and posts the ones you pick.

## What it writes

Each day, for each of your **spaces** (one goal each, for example "NorthList" for your product and "Personal" for you, each with its own accounts), in the mix its goal asks for:
- **What you shipped**: from the GitHub repos and changelog links you added to the space (merged pull requests and release notes, never secrets or code). Private repos are read with your AI app's own GitHub access.
- **News with your take**: fresh articles on the space's interests, read in full, always with the source link.

A product is mentioned in about 1 in 3 posts at most, only where it fits.

## Works in

Antigravity (recommended), Claude Code (also the Code tab of the Claude desktop app) and Codex.

## Start

1. Sign up in NorthList Posts. The first-run steps set up your first space (goal, links, interests, voice, accounts, rhythm) and end with the steps below.
2. Get this folder: download it from GitHub (Code › Download ZIP) or clone it, and open it in your AI app.
3. Paste the setup prompt from NorthList Posts (first-run step "Connect your AI", or the Connect page). It connects itself; the app ticks "Connected".
4. Each morning, type `daily` (or let your AI app run it on a schedule). The drafts show up on **Today**, per space.

Other commands: `write about <anything> [for <space>]`, `rewrite <title>: <what to change>`, `setup`, `connect`.

## Privacy

- This folder never stores personal data or your token. The token lives only in your AI app's own settings.
- Your AI reads only the links in your spaces, and never puts private details in a post.
- The app gets only what your AI sends: the drafts (and a space change, when you ask your AI for one).
