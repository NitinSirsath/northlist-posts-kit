# Setup

Spaces are set up in the NorthList Posts app: the first-run steps make the first one, and the Space page changes any of them (links, accounts, goal, interests, voice, rhythm). There are no setup questions here.

Read this file for `setup`, or when the user asks in chat to change a space ("add React to my interests", "make Personal 1 post a day").

1. Call `get_profile` and show the spaces in a few short lines: name, goal, posts a day, interests.
2. For `setup` alone: say that the app's Space page is the place to change them, and stop.
3. For a change the user asked for: call `save_profile` with that space's `space` id and only the fields that change (`goal`, `productName`, `productUrl`, `productLine`, `interests`, `postsPerDay`, `tone`, `styleSamples`, `useX`, `useLinkedIn`). Links and accounts are changed in the app only: say so if asked.
4. If it answers `invalid_input`, fix the named fields with the user and save again. Then say in one line what changed; the app shows that you changed it.
