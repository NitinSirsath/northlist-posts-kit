# Daily

Read this file for `daily`. It writes today's post ideas and sends them to Today. It takes a few minutes. If it runs as a scheduled task with nobody watching, never stop to ask: skip what needs an answer and say so at the end.

## 1. Read the app

1. Call `get_profile` and `get_recent_posts`.
2. If the profile has no interests, no product and no `shippedFrom`, it is not set up: run `instructions/setup.md` first (or, with nobody watching, stop and say "Run setup first").
3. How many are still wanted today: `postsPerDay` minus the SHIPPED, OWN and NEWS ideas in `sentInLast20Hours`. If that is 0, say that today's ideas are already on Today and stop, unless the user asked for more.
4. Channels: write X texts only if `useX`, LinkedIn texts only if `useLinkedIn`. `connectedChannels` does not matter here: the user can connect later.

## 2. Plan the mix

Pick the posts by the goal. With 3 posts a day:

| Goal | Post 1 | Post 2 | Post 3 |
| --- | --- | --- | --- |
| PROMOTE | SHIPPED (or OWN about the product) | NEWS with a take | NEWS or SHIPPED, whichever has better material |
| NETWORK | NEWS with a take | SHIPPED or OWN | NEWS |
| JOB | SHIPPED (show a skill) | NEWS in their field | SHIPPED or NEWS |

With fewer posts, take them from the left. With more, add NEWS and SHIPPED in turn.

The product (PROMOTE only) goes in about 1 in 3 posts. A SHIPPED post always counts as one. Count the posts that went out in the last week and the ideas in `waiting`: if more than a third of them name the product, write today's posts without it. With 3 posts a day that means one product post a day; with little history, just keep to one in today's set.

Do not repeat a topic or article from the last 14 days of `posted` or from `waiting`.

## 3. Gather the material

1. **Shipped**: if `shippedFrom` has folders and you can read local folders, follow `instructions/shipped.md`. If nothing is worth a post, use that slot for NEWS.
2. **News**: follow `instructions/news.md` for as many NEWS slots as you have (find one or two spare in case one fails).

## 4. Write

Follow `instructions/writing.md` for each idea. For each one fill:
- `kind`, `title` (a short headline the user sees, not the post's first line), `why` (one line: why post this today);
- NEWS: `sourceUrl` and `sourceName`;
- `x` and/or `linkedin` texts.

Before sending, check each text yourself: lengths, no made-up facts, the source link in news posts, no private details.

The shape `submit_drafts` takes (the tool also describes it):
```json
{ "ideas": [
  { "kind": "NEWS", "title": "Next.js: 51 advisories this year", "why": "Official post from yesterday; useful to React developers",
    "sourceUrl": "https://nextjs.org/blog/...", "sourceName": "Next.js Blog",
    "x": "…", "linkedin": "…" },
  { "kind": "SHIPPED", "title": "Gmail page is now a short summary", "why": "A visible change people can try",
    "x": "…", "linkedin": "…" }
] }
```

## 5. Send

Call `submit_drafts` once with all ideas (at most 15). If it answers `invalid_input`, fix only the named fields and send those ideas again once.

## 6. Tell the user

Two lines: "Sent to Today: 1 shipped, 2 news." plus anything you skipped and why (for example "No news on Gmail tips from the last two days"). End with "Open Today in NorthList Posts to post them."
