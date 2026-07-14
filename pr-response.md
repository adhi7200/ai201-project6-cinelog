# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** I renamed all instances of save_to_watchlist() to add_to_watchlist to mirror the add_to_collection naming convention and find-replace all instances to reflect that.
**How I verified:** This passed the default test suite.

## Comment 2 — Deduplication
**What I did:** I mirrored the duplication logic from collection_service.py to ensure duplicates are filtered out in the watchlist_service.py with an error raised for duplicates. Further Claude recommended me to add a DB-level UniqueConstraint on WatchlistEntry and an IntegrityError catch as a race-condition backstop that add_to_collection() itself doesn't have so I used AI to implement that.
**How I verified:** This passed the default test suite.

## Comment 3 — Missing test
**What I did:** I added a test_watchlist.py and realized I have to write similar tests for watchlist_service to check if the first 3 comments are fixed so I wrote those.
**How I verified:** I ran the updated test suite with add_watchlist tests for creating new entries, duplicates check, and nonexistent film check.

## Comment 4 — Default visibility
**My position:** The user's watchlist should remain public for the purposes of this app since users typically like to share watchlists with friends.
**Reasoning:** However, until there are endpoints established for other users viewing each others' watchlists, leaving it exposed as the app is being developed unnecessarily leaves the app vulnerable to security issues. Until there are secure viewpoints established for cross-user visibility. The default should be set to private.
**Tradeoff acknowledged:** While public may be best for this app's purpose, it should be noted that users may skip over warnings and save items to their list, thinking their list is default private and only viewable to themselves. This may backfire into a source of user frustration if not dealt with properly.

## Comment 5 — Sort order
**My position:** I agree with the comment advocating for a change to date added sorting order.
**Reasoning:** That seems like a more intuitive format for adding and removing from watchlist and watching shows based on what is more freshly on user's minds.
**Engagement with reviewer's point:** The reviewer's point mirrors how get_collection() already sorts (newest first by date_added), so this also brings the watchlist in line with the rest of the app's conventions instead of being the one view sorted differently (alphabetically by title). I changed get_watchlist() in watchlist_service.py to order by WatchlistEntry.date_added.desc(), matching add_to_collection()'s pattern.

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->