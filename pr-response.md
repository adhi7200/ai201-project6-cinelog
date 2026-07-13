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
**What I did:**
**How I verified:**

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->