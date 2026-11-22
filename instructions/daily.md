# Daily

Read this file for `daily`. It writes today's post ideas for every space and sends each space's ideas to its Today. It takes a few minutes. If it runs as a scheduled task with nobody watching, never stop to ask: skip what needs an answer and say so at the end.

## 1. Read the app

1. Call `get_profile`. If it has no spaces, say "Set up your first space in NorthList Posts" and stop.
2. Then do sections 2 to 5 for **each space in turn**, as if it were the only one. Never mix their material, voice or accounts.
3. Skip a space for today when its `postsPerDay` is 0, or when it has no interests and no links (nothing to read): say "<space>: add interests or links on the Space page" at the end. In a **scheduled** run (nobody typed `daily`), also skip a space with `weekends: false` on the user's Saturday and Sunday. When the user types `daily` themselves, write for it on any day.
4. For the space: call `get_recent_posts` with `space`. How many are still wanted today: `postsPerDay` minus the SHIPPED, OWN and NEWS ideas in `sentInLast20Hours`. If that is 0, today's ideas for this space are already on Today: go to the next space.
5. Write both an X text and a LinkedIn text. `channels` (the connected accounts) does not matter here: the user can connect later.

## 2. Plan the mix

Pick the space's posts by its goal. With 3 posts a day:

| Goal | Post 1 | Post 2 | Post 3 |
| --- | --- | --- | --- |
| PROMOTE | SHIPPED (or OWN about the product) | NEWS with a take | NEWS or SHIPPED, whichever has better material |
| NETWORK | NEWS with a take | SHIPPED or OWN | NEWS |
| JOB | SHIPPED (show a skill) | NEWS in their field | SHIPPED or NEWS |

With fewer posts, take them from the left. With more, add NEWS and SHIPPED in turn. When some of today's ideas were already sent (`sentInLast20Hours`), cross those kinds off the row from the left and fill only what is left: for example PROMOTE with 1 SHIPPED already sent and 2 a day leaves one NEWS.

The space's product (PROMOTE only) goes in about 1 in 3 posts. A SHIPPED post always counts as one. Count the posts that went out in the last week and the ideas in `waiting`: if more than a third of them name the product, write today's posts without it. With 3 posts a day that means one product post a day; with little history, just keep to one in today's set.

Do not repeat a topic or article from the last 14 days of `posted` or from `waiting`.

## 3. Gather the material

1. **Shipped**: only when a SHIPPED slot is left today and the space has GitHub links (or a changelog page): follow `instructions/shipped.md`. If nothing is worth a post, use that slot for NEWS.
2. **News**: follow `instructions/news.md` with this space's interests, for as many NEWS slots as you have (find one or two spare in case one fails).

## 4. Write

Follow `instructions/writing.md` for each idea. For each one fill:
- `kind`, `title` (a short headline the user sees, not the post's first line), `why` (one line: why post this today);
- NEWS: `sourceUrl` and `sourceName`;
- `x` and/or `linkedin` texts.

Before sending, check each text yourself: lengths, no made-up facts, the source link in news posts, no private details.

The shape `submit_drafts` takes (the tool also describes it):
```json
{ "space": "<the space id from get_profile>",
  "ideas": [
  { "kind": "NEWS", "title": "Next.js: 51 advisories this year", "why": "Official post from yesterday; useful to React developers",
    "sourceUrl": "https://nextjs.org/blog/...", "sourceName": "Next.js Blog",
    "x": "…", "linkedin": "…" },
  { "kind": "SHIPPED", "title": "Gmail page is now a short summary", "why": "A visible change people can try",
    "x": "…", "linkedin": "…" }
] }
```

## 5. Send

Call `submit_drafts` once per space with that space's id and all its ideas (at most 15). If it answers `invalid_input`, fix only the named fields and send those ideas again once.

## 6. Tell the user

One line per space: "NorthList: 1 shipped, 2 news. Personal: 1 news." plus anything you skipped and why (for example "No news on Gmail tips from the last two days"). End with "Open Today in NorthList Posts to post them."
