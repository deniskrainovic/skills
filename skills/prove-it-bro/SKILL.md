---
name: prove-it-bro
description: Produce undeniable proof that something works - screenshots, videos, raw outputs, logs - bundled in one plain HTML page, with a ledger of everything odd found on the way.
disable-model-invocation: true
---

Show me that it works. Undeniable proof: anything a skeptic could replay and check, not a description of what you believe. Screenshots, videos, raw command transcripts, test logs, database rows, diffs. Dazzle me, but with evidence, never with decoration.

The subject is whatever the conversation is about: a feature, a fix, a migration, a claim someone made. If it is unclear, ask once, then proceed.

## Steps

1. **List the claims.** Write down every behaviour the subject promises, one line each, numbered. Include the negative cases: what must be refused, must fail, must stay unchanged. Done when a reader could tick each line without reading anything else.
   Where claims depend on two dimensions (who times what, input times state, environment times action), lay them out as a **matrix**: every cell is a claim with its own verdict, and no cell stays empty, "not applicable" included. The matrix goes into the index as a table, one row per dimension value, verdict colour per cell.

2. **Sketch the expectation per claim.** Before capturing anything, draw how it is supposed to go: a sequence, a before/after diff, a state flow, whichever is smallest (the show-me skill's forms). The expectation goes into the index above the evidence, so the reader compares "should" with "did".

3. **Pick the witness per claim.** The strongest evidence available, in this order: video of the real thing, screenshot set, raw command transcript with its output, test run log, data excerpt, diff. Real environment (rig, staging, disposable copy), never production unless told. One claim may need several witnesses; a witness that proves nothing is dead weight.

4. **Capture raw, and keep the ledger.** One numbered folder per claim. Commands exactly as run, output unedited, timestamps left in. Every script or harness you wrote goes into `harness/` so the run can be repeated. Videos through Playwright `recordVideo` or a screen recording; screenshots at a real viewport size. Reset what you changed in the environment afterwards and say so.
   The ledger is two lists you append to the moment something catches your eye, then you continue with the run instead of fixing it: **Findings** (failures, errors, side effects, unexpected outcomes, plain wrong things) and **UX/UI notes** (anything that looks or behaves badly for a user). Each entry: claim number, what happened, where the evidence is. A finding that breaks a claim turns that claim's verdict red; it never hides in the list.

5. **Run every gate** the project defines (tests, type checks, linters, builds) on the final tree and keep the full logs as witnesses of their own.

6. **Record provenance.** Exact commit, branch, dirty-file count, what was pushed or not. Then the honest block: what was NOT proven and why (an environment limit, a path covered only by tests). Missing evidence stated plainly beats evidence implied.

7. **Build the index.** One self-contained `index.html` next to the folders, plain by default: system font, one column, thin borders, green or red verdict per claim. Per claim: the claim, the expectation sketch, how it was checked (the command or step), the observed result, the verdict, images embedded by relative path, videos linked, raw output in `<pre>`, long logs behind `<details>`. **Mark the decisive line** in every big block (`<mark>` on the one line that proves or breaks the claim; a frame or arrow on the spot in a screenshot) and leave the rest plain, so the reader finds the point in two seconds. Structure beyond that (a table, a matrix, a diagram, two columns) is allowed exactly when it makes the evidence clearer, never prettier. Then two closing sections: the Findings ledger and the UX/UI notes, both complete even when empty ("none"). Opens from disk, readable at phone width. Start from [`index-template.html`](index-template.html).

8. **Hand it over.** Open the index locally or send the file; attach the key images and videos where the work is tracked (the issue, the PR); reply with the index path on the first line, one line per claim with its verdict, then the two ledgers. Local only; never publish to a cloud artifact.

Done when every claim has an expectation, a witness and a verdict, every unproven claim is listed as unproven, both ledgers are in the index, and the index opens from disk with no broken image or link.
