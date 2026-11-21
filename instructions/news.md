# News

Read this file from `daily` or `write about <topic>`. It finds fresh, solid articles on the user's interests to write a post with their take.

## 1. Find candidates

For each interest (start with the ones not used in the last few posts or in `waiting`):
1. Search the web for news from the last 2 days. Good places: Google News search, Hacker News, the official blog of the tool or company, and well-known sites in that field. For Hacker News, `https://hn.algolia.com/api/v1/search?query=<topic>&tags=story&numericFilters=created_at_i%3E<unix time 2 days ago>` lists stories posted to HN in that time, most popular first (keep `%3E`: a plain `>` is refused).
2. Collect a few headlines with the article's own date and site. The date that counts is when the article was published, not when it was shared: open it to check, on the page itself (the date under the headline, or `datePublished` in the page source). Search results often show wrong dates and broken links, so never trust a date, number or link you have not seen on the page.

## 2. Pick

A good article for a post is:
- **fresh**: from the last 3 days;
- **solid**: an official announcement, a known publication or a clear first-hand write-up; not a rumour, a press release dressed as news, or an AI-written content farm;
- **useful to the user's audience**, and something the user can have a view on;
- **new to them**: not in `posted` (last 14 days) or `waiting`.

Prefer one strong article over two weak ones. If nothing qualifies for an interest, move on to the next interest. If no interest has a fresh article, you may use one up to 7 days old that is still being talked about; say how old it is in `why`. If there is still nothing, send fewer posts and say so at the end. Never lower the "solid" bar to fill a slot.

## 3. Read it in full

Open the article and read the whole text. Write only from what it says. If you cannot open it (paywall, blocked, too long), drop it and take the next one: never write from a headline or a search snippet alone.

Some fetch tools give only a summary of the page, and summaries can add or change facts. Before you use a number, date, name or quote, see it in the article's own words: ask the fetch tool for those exact sentences, or download the page (for example with `curl -sL <link>`) and read the paragraphs. If you cannot see the exact words, leave that fact out.

Note the exact link (`sourceUrl`), the site name (`sourceName`), and the one or two facts the post will use.

## 4. The take

The post needs a point of view, not a summary. Suggest one the user could hold, based on their goal, product and style: what it means for people like their readers, what they would try, or where they disagree. Put it in the text in their voice. The user can add their own line on Today ("Your take"), which goes on top, so do not start the text with a line that would clash with it.
