# Muse weekly capture: spec

What Muse does each week to turn parent-group posts into solution records. This is step 1 of [How it works](../README.md#how-it-works). The content rules are in [CONTRIBUTING.md](../CONTRIBUTING.md); this spec does not relax any of them.

## Goal

Each week, find the problems families raised in the parent groups and what other families say worked, with the product and where to buy it. Turn them into clean, anonymised records. Send the maintainer one summary to review. Nothing is published until the maintainer approves it.

## Schedule and window

- **Runs weekly**, Monday at 06:00 Eastern.
- **New posts:** posts created in the previous 7 days (Monday 00:00 to Sunday 23:59 Eastern).
- **Late comments:** re-read the comments on posts from the 14 days before that. Most solutions arrive as comments, often days after the post. Add only comments not seen before.
- **First pass for a new group:** the last 60 days, done once. Weekly runs pick up from there. The first group's pass is done and is migrated as described in [Migrating the first pass](#migrating-the-first-pass).
- **Volume cap:** if a run hits a cap, split the window into single days and run them one after another. If a day still hits the cap, log the date range that was missed. Never skip it silently.

## Sources

- The maintainer gives Muse the list of groups. The list is kept outside this repo, because the groups are private.
- Muse reads with the maintainer's own access. It only reads. It never posts, comments, reacts, sends messages or joins groups.
- Before a group's first run, its admins have agreed to the group being used this way. The maintainer confirms this when adding the group.

## What to read

- Every text post in the window, and all its comments and replies.
- **Photo-only posts:** read any text in the image (product labels, screenshots of listings, packaging). Do not save the image. If there is no readable text, count the post as "not assessed".
- **Skip:** admin announcements, fundraisers, memorials, and posts that only ask for prayers or support with no problem to solve.

## Where output goes

One Google Sheet in the maintainer's private Drive folder, with three tabs:

| Tab | What it holds |
|---|---|
| Records | One row per record (schema below). Each run appends new rows; it never deletes rows. |
| Weekly summary | One section per run (format below). Newest first. |
| Run log | One row per group per run: window, posts scanned, text posts, photo-only posts, not assessed, records created, caps hit, errors. |

Raw post text and post links stay in this Sheet only. They are never committed to this repo (see `captures/` in [.gitignore](../.gitignore)).

## Record schema

**One row per problem, solution and product.** If a comment names three products, that is three rows sharing a `thread_id`. If the solution is not a product (a care practice, or "call the manufacturer"), leave the product fields empty and set `solution_type`.

| Field | What goes in it |
|---|---|
| `record_id` | Unique ID, for example `G1-2026W47-001` (group code, ISO week, number). |
| `thread_id` | The same for every record from one post. |
| `group` | Short group code, such as `G1`. The names behind the codes are kept with the group list. |
| `post_url` | Link to the post. **Private: never published.** |
| `post_date` | Date of the post (YYYY-MM-DD). |
| `solution_date` | Date of the comment that gave the solution. |
| `captured_at` | When Muse captured it. |
| `need` | A need from [docs/keywords.md](keywords.md), for example `G-tube`. If none fits, write `new: ` and a short name. |
| `devices_conditions` | Tags, separated by `;`, such as `g-tube; blended diet; SBS`. |
| `age_band` | `NICU`, `0-12 months`, `1-3 years`, `4-12 years`, `13+` or `unknown`. Never an exact age. |
| `country` | `CA`, `US`, `other` or `unknown`. Only if the post or comment says so. Do not guess. |
| `problem` | The problem in general terms, one sentence. No names, hospitals, exact ages or detailed medical history. |
| `solution` | What the family did and why it helped them, written as their experience. See [Safety rules](#safety-rules). |
| `solution_type` | `product`, `practice`, `where to buy`, or `process` (for example, how to get a replacement from a manufacturer). |
| `product_name` | One product, as specific as was shared, for example `Mic-Key low-profile button`. |
| `brand` | Brand, if known. |
| `product_link` | The link as shared, if any. Do not add links yourself. |
| `search_terms` | 1 to 3 words a parent could search a shop with, for example `tubie pads`. |
| `reports_worked` | How many different people said it worked for them. |
| `reports_not_worked` | How many said it did not work, or caused a problem. |
| `safety_flags` | Any that apply, separated by `;` (list below). Empty if none. |
| `status` | `new`, `needs review`, `approved`, `rejected` or `merged`. Muse only ever sets `new`, `needs review` or `merged`. |
| `merged_into` | If `merged`, the `record_id` it was merged into. |
| `notes` | Anything the reviewer should know. |

"Didn't work for us" is worth recording too, in `reports_not_worked`. A product five families tried and two returned is more useful than one that only has praise.

## Merging duplicates

- Same product and same need, in the same or another group: keep the record with the clearest solution, add up the counts, set the others to `merged` with `merged_into`.
- Same product, different needs: separate records. A CPAP hose cover for line bundling and for warmth are two records.
- Spelling variants of a product (`MicKey`, `Mic-Key`, `mickey button`) are merged under one name.

## Safety rules

The hard limits from [CONTRIBUTING.md](../CONTRIBUTING.md#peer-experience-labelled) apply to the `problem` and `solution` fields. The raw post stays as it was; the record is what gets cleaned.

| Flag | When | What Muse does |
|---|---|---|
| `dose` | An amount of a medicine, supplement, herb or tincture, or a feed volume or rate (for example "5 ml senna", "1/2 teaspoon a day", "10 ml more per feed"). | Remove the amount from `solution`. Set `needs review`. |
| `medicine` | A medicine, supplement or herbal remedy is the solution (senna, magnesium citrate, tinctures, mupirocin). | Keep the name, no amount. Set `needs review`. |
| `treatment change` | Stopping, swapping or changing a prescribed treatment, formula or device. | Set `needs review`. Never word it as advice. |
| `health claim` | A claim of what something does to the body ("repairs the gut lining", "heals leaky gut"). | Rewrite as the family's experience ("they felt it helped her digestion"). |
| `diagnosis` | A commenter suggests what condition the child has. | Leave the diagnosis out. Set `needs review`. |
| `urgent` | Symptoms that need the care team now (breathing trouble, a dislodged tube, signs of infection, blood, fever with a line). | Set `needs review`. The published version points to the care team first. |
| `homemade` | Making a medical or nutrition product at home (eggshell calcium, nasal rinse). | Set `needs review`. |

Any record with a flag gets status `needs review`. Muse never sets `approved`.

The "check with your dietitian" or "check with your child's doctor" wording is added later, when a record is published, based on the family's country. Muse does not write it into the record.

## Privacy

- No names of children, parents or commenters. No hospitals, doctors' names, cities or photos.
- Replace exact ages with `age_band`. Leave out details that could identify a family when combined (for example, a rare condition plus age plus city).
- `post_url` and raw text never leave the private Sheet.

## Weekly summary

One section per run in the Weekly summary tab, short enough to read in five minutes:

1. **Run health:** posts scanned per group, photo-only and not assessed, caps hit, errors, date ranges missed.
2. **Numbers:** new records, merged, needing review, by group.
3. **Top needs this week:** the 5 needs with the most new records, with one line on what's changing (for example, "reports of G-tube button leaks are up sharply").
4. **New products:** products not seen in earlier weeks.
5. **Needs review:** every flagged record, with the flag and a one-line reason, so the maintainer can approve or reject from the list.
6. **Keyword suggestions:** new `need` names and `search_terms` that are not in [docs/keywords.md](keywords.md) yet.

Muse sends a short message to the maintainer when the summary is ready, with a link to it.

## Quality checks before the summary

- Every row has the required fields: `record_id`, `thread_id`, `group`, `post_url`, `post_date`, `need`, `problem`, `solution`, `solution_type`, `status`.
- No row has more than one product in `product_name`.
- Scan `problem` and `solution` for names, amounts with units (ml, mg, oz, tsp, drops) and the words "dose" and "dosage". Any match must be flagged or fixed.
- Spot-check 10 random records against their posts and note the result in the Run log.

## Migrating the first pass

The first group's 60-day table (141 rows, six columns) is moved into this schema before the first weekly run:

- Split rows that name several products into one row per product.
- Fill `need`, `devices_conditions`, `age_band`, `country`, `solution_type` and the report counts from the posts.
- Apply the safety rules. The first pass has at least 12 rows with amounts in `solution` (senna in ml, eggshell powder per day, tincture drops, feed volumes and rates) and some health claims ("repair the gut lining").
- Re-read the posts from the last 14 days of that window for comments added since.

## Not in scope

- Posting, commenting, reacting or messaging in any group.
- Saving photos or member profiles.
- Checking whether a product is sold on Shopify. That happens in the coverage test, after review.
- Anything about commission or affiliate links. They never affect what is captured or shown.

## Open questions

- Which day and time suit the maintainer's review. Monday morning is the default.
- Whether a product photo with no text should be described in words (for example, "a quilted pad around the button") so it can still become a record.
